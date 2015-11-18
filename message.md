# Messages

### GET /notifications

说明

	【用户】 取得自己的提醒汇总统计

输入参数说明：	
	
	无

输入样例：

	GET /notifications HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb

输出样例：

	[
		{
			"type": "subscriptions_messages",
			"num": "6"
		},
		{
			"type": "dataitem_comments",
			"num": "20+"
		},
		{
			"type": "comment_replies",
			"num": "2"
		},
		{
			"type": "private_messages",
			"num": "6"
		},
		{
			"type": "website_broadcasts",
			"num": "1"
		}
	]


### POST /message/private

说明

	【用户】对另当前用户发一条私信

输入参数说明：	
	
	token: 一个隐藏的防止重复发表的token
	receiver: 消息接受者
	content: 消息内容（最多200字）

输入样例：

	POST /message/private HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb
	
	{
		"token": "a1a2a3a4a5a6a7a8",
		"receiver": "zhang3@aaa.com",
		"content": "bla bla ..."
	}

输出样例：

	{
		"messageid" : "1234567"
	}

### GET /messages/private/receiveds?beforetime={beforetime}

说明

	【用户】返回当前用户接受到的私信列表

输入参数说明：
	
	beforetime: 最晚时间, 毫秒数

输入样例：

	GET /messages/private/receiveds?beforetime=78191821212 HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb

输出样例：

	[
		{
			"sender": "zhang3@aaa.com",
			"createtime": "2015-11-10T15:04:05Z08:00",
			"content": "bla bla ..."
		},
		{
			"sender": "li4@aaa.com",
			"createtime": "2015-11-10T15:04:09Z08:00",
			"content": "bla bla ..."
		},
		{
			"sender": "li4@bbb.com",
			"createtime": "2015-11-10T15:06:09Z08:00",
			"content": "bla bla ..."
		}
	]

### GET /messages/private/sents?beforetime={beforetime}

说明

	【用户】返回当前用户发出的私信列表

输入参数说明：
	
	beforetime: 最晚时间, 毫秒数

输入样例：

	GET /messages/private/sents?beforetime=78191821212 HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb

输出样例：

	[
		{
			"receiver": "zhang3@aaa.com",
			"createtime": "2015-11-10T15:04:05Z08:00",
			"content": "bla bla ..."
		},
		{
			"receiver": "li4@aaa.com",
			"createtime": "2015-11-10T15:04:09Z08:00",
			"content": "bla bla ..."
		},
		{
			"receiver": "li4@bbb.com",
			"createtime": "2015-11-10T15:06:09Z08:00",
			"content": "bla bla ..."
		}
	]

### GET /messages/private?peeruser={peeruser}&beforetime={beforetime}

说明

	【用户】返回当前用户和另一个用户之间的私信列表

输入参数说明：

	peeruser: 另一个用户
	beforetime: 最晚时间, 毫秒数

输入样例：

	GET /messages/private?peeruser=li4@bbb.com&beforetime=78191821212 HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb

输出样例：

	[
		{
			"type": "received",
			"createtime": "2015-11-10T15:04:05Z08:00",
			"content": "bla bla ..."
		},
		{
			"type": "sent",
			"createtime": "2015-11-10T15:04:09Z08:00",
			"content": "bla bla ..."
		},
		{
			"type": "received",
			"createtime": "2015-11-10T15:06:09Z08:00",
			"content": "bla bla ..."
		}
	]

### POST /message/broadcast

说明

	【管理员】给全体用户发送一条广播

输入参数说明：	
	
	token: 一个隐藏的防止重复发表的token
	content: 消息内容（最多200字）

输入样例：

	POST /message/broadcast HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb
	
	{
		"token": "a1a2a3a4a5a6a7a8",
		"content": "bla bla ..."
	}

输出样例：

	{
		"messageid" : "1234567"
	}

### DELETE /message/broadcast?messageid={messageid}

说明

	【管理员】删除一条广播

输入参数说明：	
	
	messageid: 广播id

输入样例：

	DELETE /message/broadcast?messageid=1233456 HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb

输出样例：

	空


### GET /messages/broadcast?beforetime={beforetime}

说明

	【用户】返回系统广播消息列表

输入参数说明：
	
	beforetime: 最晚时间, 毫秒数

输入样例：

	GET /messages/broadcast?beforetime=78191821212 HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb

输出样例：

	[
		{
			"createtime": "2015-11-10T15:04:05Z08:00",
			"content": "bla bla ..."
		},
		{
			"createtime": "2015-11-10T15:04:09Z08:00",
			"content": "bla bla ..."
		},
		{
			"createtime": "2015-11-10T15:06:09Z08:00",
			"content": "bla bla ..."
		}
	]

### POST /message/broadcast/:repname/:itemname

说明

	【提供者】给自己的一个dataitem的所有订阅者发送一条广播

输入参数说明：	
	
	token: 一个隐藏的防止重复发表的token
	content: 消息内容（最多200字）

输入样例：

	POST /message/broadcast/repo1/item123 HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb
	
	{
		"token": "a1a2a3a4a5a6a7a8",
		"content": "bla bla ..."
	}

输出样例：

	{
		"messageid" : "1234567"
	}

### DELETE /message/broadcast/:repname/:itemname?messageid={messageid}

说明

	【提供者】删除自己的一个dataitem的上的一条广播

输入参数说明：	
	
	messageid: 将被删除的广播的id

输入样例：

	DElETE /message/broadcast/repo1/item123?messageid=1223345 HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb

输出样例：

	空

### GET /messages/subscriptions?beforetime={beforetime}

说明

	【用户】返回自己订阅上的广播消息列表

输入参数说明：
	
	beforetime: 最晚时间, 毫秒数

输入样例：

	GET /messages/subscriptions?beforetime=78191821212 HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb

输出样例：

	[
		{
			"repname": "repo1231",
			"itemname": "item9883",
			"time": "2015-11-10T15:04:05Z08:00",
			"content": "bla bla ..."
		},
		{
			"repname": "repo1231",
			"itemname": "item9883",
			"time": "2015-11-10T15:04:09Z08:00",
			"content": "bla bla ..."
		},
		{
			"repname": "repo1231",
			"itemname": "item9883",
			"ctime": "2015-11-10T15:06:09Z08:00",
			"content": "bla bla ..."
		}
	]

### GET /messages/dataitem_comments?beforetime={beforetime}

说明

	【提供者】返回自己dataitems上的评论

输入参数说明：
	
	beforetime: 最晚时间, 毫秒数

输入样例：

	GET /messages/dataitem_comments?beforetime=78191821212 HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb

输出样例：

	[
		{
			"repname": "repo1231",
			"itemname": "item9883",
			"username": "zhang3",
			"time": "2015-11-10T15:04:05Z08:00",
			"content": "bla bla ..."
		},
		{
			"repname": "repo1231",
			"itemname": "item9883",
			"username": "li4",
			"time": "2015-11-10T15:04:09Z08:00",
			"content": "bla bla ..."
		},
		{
			"repname": "repo1231",
			"itemname": "item9883",
			"username": "John",
			"ctime": "2015-11-10T15:06:09Z08:00",
			"content": "bla bla ..."
		}
	]

### GET /messages/comment_replies?beforetime={beforetime}

说明

	【用户】返回自己评论上的回复

输入参数说明：
	
	beforetime: 最晚时间, 毫秒数

输入样例：

	GET /messages/comment_replies?beforetime=78191821212 HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb

输出样例：

	[
		{
			"repname": "repo1231",
			"itemname": "item9883",
			"replier": "zhang3",
			"time": "2015-11-10T15:04:05Z08:00",
			"content": "bla bla ..."
		},
		{
			"repname": "repo1231",
			"itemname": "item9883",
			"replier": "li4",
			"time": "2015-11-10T15:04:09Z08:00",
			"content": "bla bla ..."
		},
		{
			"repname": "repo1231",
			"itemname": "item9883",
			"replier": "John",
			"time": "2015-11-10T15:06:09Z08:00",
			"content": "bla bla ..."
		}
	]

