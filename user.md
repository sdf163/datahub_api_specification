# API 列表
	

- [GET] /users/:loginname 查询用户

- [POST] /users/:loginname 创建用户

- [PUT] /users/:loginname 修改用户

- [DELETE] /users/:loginname 删除用户

- PUT /users/:loginname/status 激活用户

- PUT /users/:loginname/pwd 修改密码

	
----------

##指令：GET /users/:loginname 查询用户(71)
说明
	【任意】 返回一个用户的详细情况，如果是自己，可以获得更详细的情况，如何是其他人，获得基本情况
输入参数说明：
	无
Example Request：
	GET /users/foo HTTP/1.1 
	Accept: application/json
	Authorization: token
返回数据说明：
	usertype：用户类型
	nickname：昵称 
	username:真实名称
	comments：描述信息
	quata:已经使用的量【仅限查询本人】
返回数据示例
	{"nickname":"liuxy10","username":"真实名称","comments":"描述","userType":1}

##指令：POST /users/:loginname 创建用户(72)
说明：
	创建一个用户
输入参数说明：
	passwd：MD5以后的密码
Example Request：
	POST /users/liuxueying@126.com HTTP/1.1
	Content-Type: multipart/form-data;boundary=------FormBoundary1511af7b6f7
	Content-Length: 119

	------FormBoundary1511af7b6f7
	Content-Disposition: form-data; name="passwd"
	1234
返回数据说明：
	无，若有出错在msg中说明出错原因
返回数据示例
	待补充

##指令：PUT /users/:loginname/status 激活用户(73)
说明：
	激活用户
输入参数说明：
	无
返回数据示例
	无，若有出错在msg中说明出错原因

##指令：PUT /users/:loginname/pwd 修改密码(74)
说明：
	修改用户密码
输入参数说明：
	oldpwd：修改前密码（md5）
	passwd：修改后密码（md5）
返回数据示例
	无，若有出错在msg中说明出错原因
Example Request：
	PUT /users/aaa@126.com/pwd HTTP/1.1 
	Content-Type: multipart/form-data
	Authorization: token
 
	{"passwd":"aaaaaa","oldpwd":"1234"}

##指令：PUT /users/:loginname 修改用户(75)
【管理员角色】 说明 ：
	修改一个用户
【管理员角色】输入参数说明：
	usertype：用户类型(只有管理员有权限修改)
	userstatus:用户状态（除了激活状态，其他状态需要有管理员权限）
	nickname：昵称
	username：真实名称
	comments：描述信息
	passwd：密码

【管理员角色】Example Request：
	PUT /users/foo HTTP/1.1 
	Content-Type: multipart/form-data
	Authorization: token
 
	{
		"usertype"="2",
		"userstatus"="3"，
		"nickname"="foo",
		"username"="FOO",
		"comments"="测试用户",
		"passwd"=“..........”
	}

【普通用户】 说明 ：
	修改一个用户
【普通用户】输入参数说明：

	{
		nickname：昵称
		comments：描述信息
	}

【普通用户】Example Request：
	PUT /users/foo HTTP/1.1 
	Content-Type: multipart/form-data
	Authorization: token
 
	{
		"nickname"="foo",
		"comments"="测试用户",
	}

##指令：DELETE /users/:loginname 删除用户(76)
说明：
	【管理员角色】删除一个用户
输入参数说明：
	无                     
返回数据说明：
	无，若有出错在msg中说明出错原因
返回数据示例
待补充


