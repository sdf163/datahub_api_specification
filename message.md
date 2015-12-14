# Messages

### POST /notifications

说明

	【用户】 创建一条用户提醒。
	此接口主要作为一个public API给客户端使用，目前只有一个用处：用户从客户端申请某个dataitem的白名单。
	内部接口需使用下面的kafka API通信。

输入参数说明：	
	
	type: 消息类型，必选
	data: （不同type有各自不同的data）

输入样例：

	POST /notifications HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb
	
	{
		"type": "apply_whitelist",
		"data": {
			"repname": "repo001",
			"itemname": "item123"
		}
	}

输出样例：

	空

### GET /notification_stat

说明

	【用户】 取得自己的提醒汇总统计

输入参数说明：	
	
	无

输入样例：

	GET /notification_stat HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb

输出样例：

	{
		"subs_message": 6,
		"dataitem_comment": 20,
		"comment_reply": 2,
		"private_message": 6,
		"admin_broadcast": 1
	}

### DELETE /notification_stat

说明

	【用户】清除自己的提醒汇总统计

输入参数说明：	
	
	无

输入样例：

	DELETE /notification_stat HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb

输出样例：

	空

### GET /notifications?type={type}&sender={sender}&status={status}&beforetime={beforetime}

说明

	【用户】返回当前用户接受到的消息列表

输入参数说明：
	
	type: （可选）消息类型
	sender: (可选) 消息发送者
	beforetime: （可选，默认为now）最晚时间, 毫秒数

输入样例：

	GET /notifications?type=private_message HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb

输出样例：

	[
		{
			"sender": "zhang3@aaa.com",
			"status": 0,
			"createtime": "2015-11-10T15:04:05Z08:00",
			"content": "bla bla ..."
		},
		{
			"sender": "li4@aaa.com",
			"status": 1,
			"createtime": "2015-11-10T15:04:09Z08:00",
			"content": "bla bla ..."
		},
		{
			"sender": "li4@bbb.com",
			"status": 0,
			"createtime": "2015-11-10T15:06:09Z08:00",
			"content": "bla bla ..."
		}
	]

# Messages Lib

## 初始化(golang)

```go
	import (
		"github.com/asiainfoLDP/datahub_messages/mq"
	)

	var (
		theMQ mq.MessageQueue
	)
	
	func initMQ() {
		kafkas := fmt.Sprintf("%s:%s", os.Getenv("KAFKA_HOST"), os.Getenv("KAFKA_PORT"))
		log.Infof("kafkas = %s", kafkas)
		theMQ, err := mq.NewMQ([]string{kafkas}) // ex. {"192.168.1.1:9092", "192.168.1.2:9092"}
		if err != nil {
			log.Infof("initMQ error: %s", err.Error())
			return
		}
		
		// if this service will call other service with http format, call this line.
		// "datahub_messages_caller" is just an example topic. 
		// You should use a unique topic name for your service module.
		theMQ.EnableApiCalling("datahub_messages_caller")
		
		// if this service will be called by other services with http format, call this line.
		// "datahub_messages_handler" is just an example topic. 
		// You should use a unique topic name for your service module.
		theMQ.EnableApiHandling(Port, "datahub_messages_handler", mq.Offset_Marked) // or Offset_Newest, Offset_Oldest
	}
```

## 消息发送

目前消息支持http和自定义格式。每种格式都支持同步和异步发送。但是同步的意义对于http和自定义格式有所不同。对于http发送，同步意味着发送者将得到一个消息接受者的回应。对于自定义格式，同步仅仅意味着发送者得到了消息队列服务器的回应(成功或不成功)。

在以下示例中，[]byte("")表示messsage key，在多数情况下，它可以被忽略。
	
### 自定义格式同步发送
	
```go
	partition, offset, err := theMQ.SendSyncMessage("a_topic_for_others_to_read", []byte(""), []byte("hello world")
```

### 自定义格式异步发送
	
```go
	err := theMQ.SendAsyncMessage("a_topic_for_others_to_read", []byte(""), []byte("hello world")
```

### http同步发送

```go
	// here localhost is just a placeholder, whatever it is.
	request, err := http.NewRequest("GET", "http://localhost/subscription_stat/a/b", nil)
	if err != nil {
		log.Debugf("create request error: %s", err.Error())
		return
	}
	
	response, err := theMQ.SyncApiRequest("datahub_subscription_handler", []byte(""), request)
	if err != nil {
		log.Debugf("response error: %s", err.Error())
		return
	}
	
	log.Debugf("response.Status = %s", response.Status)
	
	// ...
```

### http异步发送

```go
	// here localhost is just a placeholder, whatever it is.
	request, err := http.NewRequest("GET", "http://localhost/subscription_stat/a/b", nil)
	if err != nil {
		log.Debugf("create request error: %s", err.Error())
		return
	}

	err = theMQ.AsyncApiRequest("datahub_subscription_handler", []byte(""), request)
	if err != nil {
		log.Debugf("AsyncApiRequest: %s", err.Error())
		return
	}
```

## 消息接收

欲接收消息，需实现如下mq.MassageListener接口

```go
	type MassageListener interface {
		// return whether or not the offset will be marked in server
		OnMessage(key, value []byte, topic string, partition int32, offset int64) bool
		
		// return whether or not to stop listenning 
		OnError(error) bool
	}
```

Example:
	
```go
	type MyMesssageListener struct {
		name string
	}
	
	func newMyMesssageListener(name string) *MyMesssageListener {
		return &MyMesssageListener{name: name}
	}
	
	func (listener *MyMesssageListener) OnMessage(key, value []byte, topic string, partition int32, offset int64) bool {
		log.Debugf("%s received: (%d) message: %s", listener.name, offset, string(value))
		return true // to save offset on server
	}
	
	func (listener *MyMesssageListener) OnError(err error) bool {
		log.Debugf("api response listener error: %s", err.Error())
		return false // will not stop listenning
	}
```
	
然后注册此MassageListener

```go
	myListener := newMyMesssageListener("test")
	
	// 0 is the partition id
	err := theMQ.SetMessageListener("the_topic_i_will_read", 0, mq.Offset_Marked, myListener)
	if err != nil {
		// ...
	}
```

# json消息格式 (目前在使用)

json消息格式被视为自定义格式。json将被转化为bytes进行传输。

## topic: to_notifications.json

### 发送一条网站广播

	{
		"type": "site_broadcast",
		"receiver": "zhang3@example.com",
		"sender": "",
		"time": "2015-11-10T15:06:09Z08:00",
		"data": "bla bla ..."
	}

### 发送一条私信

	{
		"type": "private_message",
		"receiver": "zhang3@example.com",
		"sender": "li4@example.com",
		"time": "2015-11-10T15:06:09Z08:00",
		"data": "bla bla ..."
	}

### dataitem events

	{
		"type": "item_events",
		"receiver": "zhang3@example.com",
		"sender": "",
		"time": "2015-11-10T15:06:09Z08:00",
		"data": {
			"event": "tag_deleted",
			"repname": "repo1",
			"itemname": "item2",
			"tag": "tag3"
		}
	}

	{
		"type": "item_news",
		"receiver": "zhang3@example.com",
		"sender": "",
		"time": "2015-11-10T15:06:09Z08:00",
		"data": {
			"event": "item_deleted",
			"repname": "repo1",
			"itemname": "item2"
		}
	}

### 订购事件

	{
		"type": "sub_event",
		"receiver": "zhang3@example.com",
		"sender": "",
		"time": "2015-11-10T15:06:09Z08:00",
		"data": {
			"subscriptionid": 1234567,
			"phase": "freezed"
		}
	}

## topic: to_subscriptions.json

### 增加tag

	{
		"type": "0x00020000",
		"repname": "repo001",
		"itemname": "item002",
		"tag": "tag003",
		"time": "2015-11-10T15:06:09Z08:00"
	}

### 删除tag

	{
		"type": "0x00020001",
		"repname": "repo001",
		"itemname": "item002",
		"tag": "tag003",
		"time": "2015-11-10T15:06:09Z08:00"
	}

### 删除dataitem

	{
		"type": "0x00020002",
		"repname": "repo001",
		"itemname": "item002",
		"time": "2015-11-10T15:06:09Z08:00"
	}

### 删除repository

	{
		"type": "0x00020003",
		"repname": "repo001",
		"time": "2015-11-10T15:06:09Z08:00"
	}

# 纯自定义消息格式（草稿，未应用）

	所有消息格式：
		version(int32): 4字节
		type(int32): 4字节
		[具体消息内容]
	
	当前version必须为0
	
	在消息内容中string的格式：
		length(int16): 2字节
		[string内容]
	
	在消息内容中bytes的格式：
		length(int32): 4字节
		[bytes内容]

## topic: to_notifications

### 新建一条用户提醒消息

	type: 0x00010000
	receiver(string): 接收者
	data(bytes): json格式的具体notification内容

## topic: to_subscriptions

### 增加tag

	type: 0x00020000
	repname(string): 
	itemname(string): 
	tag(string): tag
	time(string): 增加时间

### 删除tag

	type: 0x00020001
	repname(string): 
	itemname(string): 
	tag(string): 
	time(string): 删除时间

### 删除dataitem

	type: 0x00020002
	repname(string): 
	itemname(string): 者
	time(string): 删除时间

### 删除repository

	type: 0x00020003
	repname(string): 
	itemname(string): 
	time(string): 删除时间
