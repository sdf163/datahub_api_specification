# API 列表
	

- [GET] /users/:loginname 查询用户

- [POST] /users/:loginname 创建用户

- [PUT] /users/:loginname 修改用户

- [DELETE] /users/:loginname 删除用户

- [PUT] /users/:loginname/status 激活用户

- [PUT] /users/:loginname/pwd 修改密码

- [GET] /quota/:loginname/repository 获取repo配额信息

- [POST] /quota/:loginname/repository 创建repo配额信息

- [PUT] /quota/:loginname/repository 修改repo配额

- [POST] /quota/:loginname/repository/use 修改repo的使用量

- [GET] /quota/:loginname/deposit 获取托管配额信息

- [POST] /quota/:loginname/deposit 新建托管配额

- [PUT] /quota/:loginname/deposit 修改用户的托管配额

- [GET] /quota/:loginname/pullnum 获取用户下载量配额信息

- [POST] /quota/:loginname/pullnum/ 创建用户下载量配额

- [PUT] /quota/:loginname/pullnum 修改用户下载量配额

- [PUT] /quota/:loginname/pullnum/use 修改用户的已下载量

- [GET] /vip/:loginname 查询会员信息

- [PUT] /vip/:loginname 修改会员信息

	
----------

##指令：GET /users/:loginname 查询用户(81)
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
		code:状态码
		msg:操作信息，用来记录失败信息
		usertype：用户类型(1：普通用户，2：管理员用户)
		nickname：昵称 
		username:真实名称
		comments：描述信息
		quata:已经使用的量【仅限查询本人】(暂时不提供)
	返回数据示例
		{"data":{"comment":"abc","nickName":"foo","userName":"FOO","userType":1},"code":0,"msg":"ok"}
	

##指令：POST /users/:loginname 创建用户(82)
	说明：
		创建一个用户
	输入参数说明：
		passwd：MD5以后的密码
	Example Request：
		POST /users/foo?passwd=abc
	
	返回数据说明：
		code:状态码
		msg:操作信息，用来记录失败信息
	返回数据示例
		{"code":0,"msg":"ok"}

##指令：PUT /users/:loginname/active 激活用户(83)
	说明：
		【管理员】激活用户
	输入参数说明：
		无
	返回数据说明
		code:状态码
		msg:操作信息，用来记录失败信息
	返回数据示例
		{"code":0,"msg":"ok"}

##指令：PUT /users/:loginname/pwd 修改密码(84)
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
		code:状态码
		msg:操作信息，用来记录失败信息
	返回数据示例
		{"code":0,"msg":"ok"}


##指令：PUT /users/:loginname 修改用户(85)
	【管理员角色】 说明 ：
		修改一个用户
	【管理员角色】输入参数说明：
		PUT /users/aaa@126.com HTTP/1.1 
		Content-Type: text/json;charset=UTF-8
		Authorization: token

		userstatus:用户状态（除了激活状态，其他状态需要有管理员权限）
		nickname：昵称
		username：真实名称
		comments：描述信息
		passwd：密码(MD5)

	【管理员角色】Example Request：
		PUT /users/foo HTTP/1.1 
		Content-Type: text/json;charset=UTF-8
		Authorization: token
		USER:admin
 
		{
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
		code:状态码
		msg:操作信息，用来记录失败信息
	返回数据示例
		{"code":0,"msg":"ok"}

##指令：DELETE /users/:loginname 删除用户(86)
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
		code:状态码
		msg:操作信息，用来记录失败信息
	返回数据示例
		{"code":0,"msg":"ok"}
##指令：GET /quota/:loginname/repository 获取用户的repo配额（87）
	说明：
		获取用户的配额信息
	输入参数说明：
		无
	Example Request：
		GET /quota/foo/repository HTTP/1.1 
		Content-Type: multipart/form-data
		
	返回数据说明
		code:状态码
		msg:操作信息，用来记录失败信息
		quotaPublic:public的repo的配额
		usePublic：Public的repo的使用量
		quotaPrivate:Private的repo的配额
		usePrivate：Private的repo的使用量
	返回数据示例
		{"code":0,"msg":"ok",
			data:{
				"quotaPublic":"10","usePublic":"5",
				"quotaPrivate":"15","usePrivate":"10"
				}
		}
##指令：POST /quota/:loginname/repository 增加用户的repo配额（88）
	说明：
		【管理员角色】添加用户的repo配额信息
	输入参数说明：
		private:私有repo配额数量
		public:共有repo配额数量

	Example Request：
		POST /quota/foo/repository HTTP/1.1 
		Content-Type: text/json;charset=UTF-8
		User:admin
		{
			"private":"20",
			"public":"50"
		}	
	返回数据说明
		code:状态码
		msg:操作信息，用来记录失败信息
	返回数据示例
		{"code":0,"msg":"ok"}
##指令：PUT /quota/:loginname/repository 修改用户的repo配额（89）
	说明：
		【管理员角色】修改用户的repo的配额
	输入参数说明：
		private:私有repo配额数量
		public:共有repo配额数量
		注：输入参数可单独使用
	Example Request：
		PUT /quota/foo/repository HTTP/1.1 
		Content-Type: text/json;charset=UTF-8
		User:admin
		{
			"private":"30",
			"public":"60"
		}
	返回数据说明
		code:状态码
		msg:操作信息，用来记录失败信息
	返回数据示例
		{"code":0,"msg":"ok"}
##指令：POST /quota/:loginname/repository/use 修改用户的repo使用量（8a）
	说明：
		修改用户的repo的使用量
		注：只允许本人或者管理员修改
	输入参数说明：
		private:私有repo配额数量 增量（如果增加1个为1，如果减少1个为-1）
		public:共有repo配额数量 增量（同上）
		注：输入参数可单独使用
	Example Request：
		POST /quota/foo/repository/use HTTP/1.1 
		Content-Type: text/json;charset=UTF-8
		USER:foo
		{
			"private":"1",
			"public":"1"
		}
	返回数据说明
		code:状态码
		msg:操作信息，用来记录失败信息
	返回数据示例
		{"code":0,"msg":"ok"}


##指令：GET /quota/:loginname/deposit 获取用户的托管信息（8b）
	说明：
		获取用户的托管的配额信息
	输入参数说明：
		无
	Example Request：
		GET /quota/foo/deposit HTTP/1.1 
		Content-Type: text/json;charset=UTF-8

	返回数据说明
		code:状态码
		msg:操作信息，用来记录失败信息
		quota:托管的配额
		use：托管使用量
	返回数据示例
		{"code":0,"msg":"ok",
			data:{
				"quota":"10M","use":"5M"
				}
		}
##指令：POST /quota/:loginname/deposit 增加用户的托管配额（8c）
	说明：
		【管理员角色】添加用户的托管配额信息 
	输入参数说明：
		quota:配额空间
		unit:单位

	Example Request：
		POST /quota/foo/deposit HTTP/1.1 
		Content-Type: text/json;charset=UTF-8
		User:admin

		{
			"quota":"200",
			"unit":"M"
		}	
	返回数据说明
		code:状态码
		msg:操作信息，用来记录失败信息
	返回数据示例
		{"code":0,"msg":"ok"}
##指令：PUT /quota/:loginname/deposit 修改用户的托管配额（8d）
	说明：
		【管理员角色】修改用户的托管的配额 
	输入参数说明：
		quota:托管配额空间大小
	Example Request：
		PUT /quota/foo/deposit HTTP/1.1 
		Content-Type: text/json;charset=UTF-8
		User:admin
		{
			"quota":"300",
		}
	返回数据说明
		code:状态码
		msg:操作信息，用来记录失败信息
	返回数据示例
		{"code":0,"msg":"ok"}


##指令：GET /quota/:loginname/pullnum 获取用户的下载量信息（8f）
	说明：
		获取用户的下载量信息
	输入参数说明：
		无
	Example Request：
		GET /quota/foo/pullnum HTTP/1.1 
		Content-Type: text/json;charset=UTF-8

	返回数据说明
		code:状态码
		msg:操作信息，用来记录失败信息
		quota:pull量的配额
		use：实际pull量
	返回数据示例
		{"code":0,"msg":"ok",
			data:{
				"quota":"10000","use":"100"
				}
		}
##指令：POST /quota/:loginname/pullnum 增加用户的下载量配额信息（8g）
	说明：
		【管理员角色】添加用户的托管配额信息 
	输入参数说明：
		quota:配额空间

	Example Request：
		POST /quota/foo/pullnum HTTP/1.1 
		Content-Type:text/json;charset=UTF-8
		User:admin

		{
			"quota":"20000",
		}	
	返回数据说明
		code:状态码
		msg:操作信息，用来记录失败信息
	返回数据示例
		{"code":0,"msg":"ok"}
##指令：POST /quota/:loginname/pullnum/use 修改用户的已下载量（8h）

	说明：
 	   修改用户的已下载量
	输入参数说明：
   	 	use:下载数增量
	Example Request：
    	PUT /quota/foo/pullnum/use HTTP/1.1 
   		Content-Type:text/json;charset=UTF-8
  	  	{
       	 "use":"10"
   		 }
	返回数据说明
 	   code:状态码，(0：成功；7000:未知错误；7005：未登录；7006：权限不够)
 	   msg:操作信息，用来记录失败信息
	返回数据示例
   		{"code":0,"msg":"ok"}

##指令：PUT /quota/:loginname/pullnum 修改用户的下载量配额（8i）
	说明：
		【管理员角色】修改用户的下载量的配额 
	输入参数说明：
		quota:下载量配额
	Example Request：
		PUT /quota/foo/pullnum HTTP/1.1 
		Content-Type: text/json;charset=UTF-8
		User:admin
		{
			"quota":"300000",
		}
	返回数据说明
		code:状态码
		msg:操作信息，用来记录失败信息
	返回数据示例
		{"code":0,"msg":"ok"}
##指令：GET /vip/:loginname 查询用户会员信息（8j）
	说明：
		【任意】查看用户会员的相关信息
	输入参数说明：
		无
	Example Request：
		GET /vip/foo HTTP/1.1 
		Accept: text/json;charset=UTF-8
		Authorization: token
		USER:foo
	返回数据说明：
		userType:会员级别
		repoPub:共有repo资源量
		repoPri:私有repo资源量
		pullNum:免费数据Pull量
		payWay:pull付费方式 (1:预付费，2后付费)
		deposit：托管配额
		annualFee:年费
	返回数据示例：

		{"data":	{
			"deposit":"0M",
			"fee":0,
			"payWay":0,
			"pullNum":100,
			"repoPri":10,
			"repoPub":20,
			"userType":0
			},
		"code":0,"msg":"ok"
		}


#指令：PUT /vip/:loginname 修改会员信息(8k)
	说明：
		【管理员】修改用户的会员信息
	输入参数说明：
		userType：会员级别
	Example Request：
		PUT /vip/foo HTTP/1.1 
		Accept: text/json;charset=UTF-8
		Authorization: token
		USER:admin
		{
			"userType":"3"
		}
	返回数据说明：
		code:状态码
		msg:操作信息，用来记录失败信息
	返回数据示例：
		{"code":0,"msg":"ok"}
