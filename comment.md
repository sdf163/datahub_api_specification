# Comments

### (B0) POST /comment/:repname/:itemname

说明

	【用户】对一个dataitem发表一个评论 (欲评论，先订阅)

输入参数说明：
	
	token: 一个隐藏的防止重复发表的token。此token由前端生成，最好是一个uuid，可用这个库: https://github.com/broofa/node-uuid
	replyto: 被回复的评论id (0表示未回复任何评论, 只有dataitem creator可以回复)
	content: 评论内容（最多200字）

输入样例：

	POST /comment/repo1/item123 HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb
	
	{
		"token": "a1a2a3a4a5a6a7a8",
		"replyto": 0,
		"content": "bla bla ..."
	}

输出样例：


	"commnetid" : "1234567"

### (B1) PUT /comment/:repname/:itemname

说明

	【用户】修改自己对一个dataitem的评论

输入参数说明：
	
	commnetid: 将被修改的评论id
	content: 更新后的内容

输入样例：

	PUT /comment/repo1/item123 HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb
	
	{
		"commnetid": "123456",
		"content": "bla bla ..."
	}

输出样例：

	(空)

### (B2) DELETE /comment/:repname/:itemname?commentid={commentid}

说明

	【用户】删除自己对一个dataitem的评论

输入参数说明：
	
	无

输入样例：

	DELETE /comment/repo1/item123?commentid=1234567 HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb

输出样例：

	(空)

### (B3) GET /comments/:repname/:itemname?beforetime={beforetime}

说明

	【任何】返回一个dataitem上的评论列表

输入参数说明：
	
	beforetime: （可选，默认为当前时间）最晚时间, 格式：2015-11-23T09:02:52Z（可以使用上次返回的评论列表中的最后一个评论的createtime）

输入样例：

	GET /comments/repo1/item123?beforetime=2015-11-23T09:02:52Z HTTP/1.1 
	Accept: application/json

输出样例：

	[
		{
			"commentid": "1234567"
			"username": "zhang3@aaa.com",
			"createtime": "2015-11-10T15:04:05Z08:00",
			"content": "bla bla ...",
			"replyto": {
				"commentid": "1234569",
				"username": "li4@bbb.com",
				"content": "cool data! ..."
			}
		},
		{
			"commentid": "1234568"
			"username": "li4@aaa.com",
			"createtime": "2015-11-10T15:04:09Z08:00",
			"content": "bla bla ...",
			"replyto": null
		},
		{
			"commentid": "1234569"
			"username": "li4@bbb.com",
			"createtime": "2015-11-10T15:06:09Z08:00",
			"content": "bla bla ...",
			"replyto": null
		}
	]

### (B4) GET /comment_stat/:repname/:itemname

说明

	【任何】返回一个dataitem上的评论数

输入参数说明：
	
	无

输入样例：

	GET /comment_stat/repo1/item123 HTTP/1.1 
	Accept: application/json

输出样例：

	numcomments: 33

