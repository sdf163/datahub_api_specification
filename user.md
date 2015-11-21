# API 列表
	

- [GET] /users/:loginname 查询用户

- [POST] /users/:loginname 创建用户

- [PUT] /users/:loginname 修改用户

- [DELETE] /users/:loginname 删除用户

- [PUT] /users/:loginname/status 激活用户

- [PUT] /users/:loginname/pwd 修改密码

- [GET] /users/:loginname/repository 获取repo配额信息

- [POST] /users/:loginname/repository 创建repo配额信息

- [PUT] /users/:loginname/repository/quota 修改repo配额

- [POST] /users/:loginname/repository/use 修改repo的使用量

- [GET] /users/:loginname/deposit 获取托管配额信息

- [POST] /users/:loginname/deposit 新建托管配额

- [PUT] /users/:loginname/deposit/quota 修改用户的托管配额

- [GET] /users/:loginname/pullnum 获取用户下载量配额信息

- [POST] /users/:loginname/pullnum/ 创建用户下载量配额

- [PUT] /users/:loginname/pullnum/quota 修改用户下载量配额

- [PUT] /users/:loginname/pullnum/use 修改用户的已下载量

	
----------

##指令：GET /users/:loginname 查询用户(71)
	说明
		【任意】 返回一个用户的详细情况，如果是自己，可以获得更详细的情况，如何是其他人，获得基本情况
	输入参数说明：
		无
	Example Request：
		GET /users/foo HTTP/1.1 
		Accept: text/json;charset=UTF-8
		Authorization: token
		USER:admin

	返回数据说明：
		code:状态码，如果成功返回0，如果失败返回-1，对应msg记录出错信息
		msg:操作信息，用来记录失败信息
		usertype：用户类型(1：普通用户，2：管理员用户)
		nickname：昵称 
		username:真实名称
		comments：描述信息
		quata:已经使用的量【仅限查询本人】(暂时不提供)
	返回数据示例
		{"data":{"comment":"abc","nickName":"foo","userName":"FOO","userType":1},"code":0,"msg":"ok"}
	

##指令：POST /users/:loginname 创建用户(72)
	说明：
		创建一个用户
	输入参数说明：
		passwd：MD5以后的密码
	Example Request：
		POST /users/foo?passwd=abc
	
	返回数据说明：
		code:状态码，如果成功返回0，如果失败返回-1，对应msg记录出错信息
		msg:操作信息，用来记录失败信息
	返回数据示例
		{"code":0,"msg":"ok"}

##指令：PUT /users/:loginname/status 激活用户(73)
	说明：
		激活用户
	输入参数说明：
		无
	返回数据说明
		code:状态码，如果成功返回0，如果失败返回-1，对应msg记录出错信息
		msg:操作信息，用来记录失败信息
	返回数据示例
		{"code":0,"msg":"ok"}

##指令：PUT /users/:loginname/pwd 修改密码(74)
	说明：
		修改用户密码
	输入参数说明：
		oldpwd：修改前密码（md5）
		passwd：修改后密码（md5）
	Example Request：
		PUT /users/aaa@126.com/pwd HTTP/1.1 
		Content-Type: text/json;charset=UTF-8
		Authorization: token
 
		{"passwd":"aaaaaa","oldpwd":"1234"}
	返回数据说明
		code:状态码，如果成功返回0，如果失败返回-1，对应msg记录出错信息
		msg:操作信息，用来记录失败信息
	返回数据示例
		{"code":0,"msg":"ok"}


##指令：PUT /users/:loginname 修改用户(75)
	【管理员角色】 说明 ：
		修改一个用户
	【管理员角色】输入参数说明：
		PUT /users/aaa@126.com HTTP/1.1 
		Content-Type: text/json;charset=UTF-8
		Authorization: token

		usertype：用户类型(只有管理员有权限修改)
		userstatus:用户状态（除了激活状态，其他状态需要有管理员权限）
		nickname：昵称
		username：真实名称
		comments：描述信息
		passwd：密码

	【管理员角色】Example Request：
		PUT /users/foo HTTP/1.1 
		Content-Type: text/json;charset=UTF-8
		Authorization: token
		USER:admin
 
		{
			"usertype":"2",
			"userstatus":"3",
			"nickname":"foo",
			"username":"FOO",
			"comments":"测试用户",
			"passwd":".........."
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
		Content-Type: text/json;charset=UTF-8
		Authorization: token
 	
		{
			"nickname":"foo",
			"comments":"测试用户"
		}
	返回数据说明
		code:状态码，如果成功返回0，如果失败返回-1，对应msg记录出错信息
		msg:操作信息，用来记录失败信息
	返回数据示例
		{"code":0,"msg":"ok"}

##指令：DELETE /users/:loginname 删除用户(76)
	说明：
		【管理员角色】删除一个用户
		注：本操作不是真的删除一条数据，是将用户状态改成 注销状态（user_status:7）
	输入参数说明：
	
		无 
	Example Request：
		DELETE /users/foo HTTP/1.1 
		Content-Type: text/json;charset=UTF-8
		Authorization: token
		USER:admin
                  
	返回数据说明
		code:状态码，如果成功返回0，如果失败返回-1，对应msg记录出错信息
		msg:操作信息，用来记录失败信息
	返回数据示例
		{"code":0,"msg":"ok"}
##指令：GET /users/:loginname/repository 获取用户的repo配额（77）
	说明：
		获取用户的配额信息
	输入参数说明：
		无
	Example Request：
		GET /users/foo/repository HTTP/1.1 
		Content-Type: multipart/form-data

	返回数据说明
		code:状态码，如果成功返回0，如果失败返回-1，对应msg记录出错信息
		msg:操作信息，用来记录失败信息
		quotaPublic:public的repo的配额
		usePublic：Public的repo的使用量
		quotaPrivate:Private的repo的配额
		usePrivate：Private的repo的使用量
	返回数据示例
		{"code":0,"msg":"ok",
			data:{
				"quotaPublic":10,"usePublic":5,
				"quotaPrivate":15,"usePrivate":10
				}
		}
##指令：POST /users/:loginname/repository/ 增加用户的repo配额（78）
	说明：
		【管理员角色】添加用户的repo配额信息
	输入参数说明：
		private:私有repo配额数量
		public:共有repo配额数量

	Example Request：
		POST /users/foo/repository HTTP/1.1 
		Content-Type: text/json;charset=UTF-8
		User:admin
		{
			"private":"20",
			"public":"50"
		}	
	返回数据说明
		code:状态码，如果成功返回0，如果失败返回-1，对应msg记录出错信息
		msg:操作信息，用来记录失败信息
	返回数据示例
		{"code":0,"msg":"ok"}
##指令：PUT /users/:loginname/repository/quota 修改用户的repo配额（79）
	说明：
		【管理员角色】修改用户的repo的配额
	输入参数说明：
		private:私有repo配额数量
		public:共有repo配额数量
	Example Request：
		PUT /users/foo/repository/quota HTTP/1.1 
		Content-Type: text/json;charset=UTF-8
		User:admin
		{
			"private":"30",
			"public":"60"
		}
	返回数据说明
		code:状态码，如果成功返回0，如果失败返回-1，对应msg记录出错信息
		msg:操作信息，用来记录失败信息
	返回数据示例
		{"code":0,"msg":"ok"}
##指令：POST /users/:loginname/repository/use 修改用户的repo使用量（7a）
	说明：
		修改用户的repo的使用量
	输入参数说明：
		private:私有repo配额数量 增量（如果增加1个为1，如果减少1个为-1）
		public:共有repo配额数量 增量（同上）
	Example Request：
		POST /users/foo/repository/use HTTP/1.1 
		Content-Type: text/json;charset=UTF-8
		{
			"private":"1",
			"public":"1"
		}
	返回数据说明
		code:状态码，如果成功返回0，如果失败返回-1，对应msg记录出错信息
		msg:操作信息，用来记录失败信息
	返回数据示例
		{"code":0,"msg":"ok"}


##指令：GET /users/:loginname/deposit 获取用户的托管信息（7b）
	说明：
		获取用户的托管的配额信息
	输入参数说明：
		无
	Example Request：
		GET /users/foo/deposit HTTP/1.1 
		Content-Type: text/json;charset=UTF-8

	返回数据说明
		code:状态码，如果成功返回0，如果失败返回-1，对应msg记录出错信息
		msg:操作信息，用来记录失败信息
		quota:托管的配额
		use：托管使用量
	返回数据示例
		{"code":0,"msg":"ok",
			data:{
				"quota":"10M","use":"5M"
				}
		}
##指令：POST /users/:loginname/deposit/ 增加用户的托管配额（7c）
	说明：
		【管理员角色】添加用户的托管配额信息 
	输入参数说明：
		quota:配额空间

	Example Request：
		POST /users/foo/deposit HTTP/1.1 
		Content-Type: text/json;charset=UTF-8
		User:admin

		{
			"quota":"200M",
		}	
	返回数据说明
		code:状态码，如果成功返回0，如果失败返回-1，对应msg记录出错信息
		msg:操作信息，用来记录失败信息
	返回数据示例
		{"code":0,"msg":"ok"}
##指令：PUT /users/:loginname/deposit/quota 修改用户的托管配额（7d）
	说明：
		【管理员角色】修改用户的托管的配额 
	输入参数说明：
		quota:托管配额空间大小
	Example Request：
		PUT /users/foo/deposit/quota HTTP/1.1 
		Content-Type: text/json;charset=UTF-8
		User:admin
		{
			"quta":"300M",
		}
	返回数据说明
		code:状态码，如果成功返回0，如果失败返回-1，对应msg记录出错信息
		msg:操作信息，用来记录失败信息
	返回数据示例
		{"code":0,"msg":"ok"}


##指令：GET /users/:loginname/pullnum 获取用户的下载量信息（7f）
	说明：
		获取用户的下载量信息
	输入参数说明：
		无
	Example Request：
		GET /users/foo/pullnum HTTP/1.1 
		Content-Type: text/json;charset=UTF-8

	返回数据说明
		code:状态码，如果成功返回0，如果失败返回-1，对应msg记录出错信息
		msg:操作信息，用来记录失败信息
		quota:pull量的配额
		use：实际pull量
	返回数据示例
		{"code":0,"msg":"ok",
			data:{
				"quota":"10000","use":"100"
				}
		}
##指令：POST /users/:loginname/pullnum/ 增加用户的下载量配额信息（7g）
	说明：
		【管理员角色】添加用户的托管配额信息 
	输入参数说明：
		quota:配额空间

	Example Request：
		POST /users/foo/pullnum HTTP/1.1 
		Content-Type:text/json;charset=UTF-8
		User:admin

		{
			"quota":"20000",
		}	
	返回数据说明
		code:状态码，如果成功返回0，如果失败返回-1，对应msg记录出错信息
		msg:操作信息，用来记录失败信息
	返回数据示例
		{"code":0,"msg":"ok"}
##指令：PUT /users/:loginname/pullnum/use 修改用户的已下载量（7h）

	说明：
 	   修改用户的已下载量
	输入参数说明：
   	 use:已使用数量
	Example Request：
    	PUT /users/foo/pullnum/use HTTP/1.1 
   		Content-Type:text/json;charset=UTF-8
  	  	{
       	 "use":"100"
   		 }
	返回数据说明
 	   code:状态码，如果成功返回0，如果失败返回-1，对应msg记录出错信息
 	   msg:操作信息，用来记录失败信息
	返回数据示例
   		{"code":0,"msg":"ok"}

##指令：PUT /users/:loginname/pullnum/quota 修改用户的下载量配额（7i）
	说明：
		【管理员角色】修改用户的下载量的配额 
	输入参数说明：
		quota:下载量配额
	Example Request：
		PUT /users/foo/pullnum/quota HTTP/1.1 
		Content-Type: text/json;charset=UTF-8
		User:admin
		{
			"quta":"300000",
		}
	返回数据说明
		code:状态码，如果成功返回0，如果失败返回-1，对应msg记录出错信息
		msg:操作信息，用来记录失败信息
	返回数据示例
		{"code":0,"msg":"ok"}

