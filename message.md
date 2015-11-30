# Messages

### POST /messages

说明

	【内部API】 创建一条用户提醒

输入参数说明：	
	
	type: 消息类型
	receiver: 消息接收者 (可选，如未提供，表示全部符合type的接受用户)
	data: 消息内容, json格式，不同消息类型元素不同。此service不关心其元素。
	
	注意：此API是一个内部API，不通过网关暴露给外部。它接收的auth是username而不是加密后的token。

输入样例：

	POST /messages HTTP/1.1 
	Accept: application/json
	User: zhang3@example.com
	
	{
		"type": "admin_broadcast",
		"data": "bla bla ..."
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
