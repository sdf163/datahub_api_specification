# API 列表
	

- [GET] /users/:username 查询用户

- [POST] /users/:username 创建用户

- [PUT] /users/:username 修改用户

- [DELETE] /users/:username 删除用户

- [GET] /users/auth 用户验证，目前仅支持basic验证方式

	
----------

## 指令：GET /users/:username 查询用户

说明
	【任意】 返回一个用户的详细情况，如果是自己，可以获得更详细的情况，如何是其他人，获得基本情况

输入参数说明：
	
	无

Example Request：

	GET /users/foo HTTP/1.1 
	Accept: application/json
	Authorization: Basic akmklmasadalkm==

返回数据说明：

	usertype：用户类型
	nickname：昵称
	comments：描述信息
	quata:已经使用的量【仅限查询本人】

返回数据示例
        
	待补充

## 指令：POST /users/:username 创建用户
	
说明：
	
	【管理员角色】创建一个用户

输入参数说明：

	usertype：用户类型
	nickname：昵称
	comments：描述信息
	passwd：MD5以后的密码
	
Example Request：

	POST /users/foo HTTP/1.1 
	Accept: application/json
	Authorization: Basic akmklmasadalkm==
	
	{
		usertype=2,
		nickname="foo",
                comments="测试用户",
                passwd=“..........”
	}

返回数据说明：

	无，若有出错在msg中说明出错原因

返回数据示例
        
	待补充


## 指令：PUT /users/:username 修改用户
	
说明：
	
	【管理员角色】修改一个用户

输入参数说明：

	usertype：用户类型
	nickname：昵称
	comments：描述信息
	passwd：MD5以后的密码
	
Example Request：

	PUT /users/foo HTTP/1.1 
	Accept: application/json
	Authorization: Basic akmklmasadalkm==
	
	{
		usertype=2,
		nickname="foo",
                comments="测试用户",
                passwd=“..........”
	}

返回数据说明：

	无，若有出错在msg中说明出错原因

返回数据示例
        
	待补充

## 指令：DELETE /users/:username 删除用户
	
说明：
	
	【管理员角色】删除一个用户

输入参数说明：

	无						
	
Example Request：

	DELETE /users/foo HTTP/1.1 
	Accept: application/json
	Authorization: Basic akmklmasadalkm==
	
	
返回数据说明：

	无，若有出错在msg中说明出错原因

返回数据示例
        
	待补充

## 指令：GET /users/auth 用户验证，目前仅支持basic验证方式
	
说明：
	
	【任意】认证一个用户是否有效

输入参数说明：

	无						
	
Example Request：

	GET /users/auth HTTP/1.1 
	Accept: application/json
	Authorization: Basic akmklmasadalkm==
	
	
返回数据说明：

	Token

返回数据示例
        
	待补充
