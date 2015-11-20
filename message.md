# Messages

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

	[
		{
			"type": "subs_message",
			"num": 6
		},
		{
			"type": "dataitem_comment",
			"num": 20
		},
		{
			"type": "comment_reply",
			"num": 2
		},
		{
			"type": "private_message",
			"num": 6
		},
		{
			"type": "admin_broadcast",
			"num": 1
		}
	]

### POST /notifications

说明

	【微服务模块】 创建一条用户提醒

输入参数说明：	
	
	type: 消息类型
	receiver: 消息接收者 (可选，如未提供，表示全部符合type的接受用户)
	data: 消息内容
	extra: 额外信息，具体取决于type (比如subs_message需要reponame和itemname信息)

输入样例：

	POST /notifications HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb
	
	{
		"type": "admin_broadcast",
		"data": "bla bla ..."
	}

输出样例：

	空

### GET /notifications?type={type}&sender={sender}&status={status}&beforetime={beforetime}

说明

	【用户】返回当前用户接受到的消息列表

输入参数说明：
	
	type: （不可选）消息类型
	sender: 消息发送者
	status: (可选，默认为未读) 已读未读
	beforetime: （可选，默认为now）最晚时间, 毫秒数

输入样例：

	GET /notifications?type=admin_broadcast&status=0 HTTP/1.1 
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

