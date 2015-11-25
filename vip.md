# API 列表
- GET /vip/:loginname 查看用户会员相关信息

- POST /vip/:loginname 添加用户会员相关信息

- PUT /vip/:loginname 修改用户会员相关信息

##指令：GET /vip/:loginname 查询用户会员信息
	说明：
		查看用户会员的相关信息
	输入参数说明：
		无
	Example Request：
		GET /users/foo HTTP/1.1 
		Accept: text/json;charset=UTF-8
		Authorization: token
		USER:foo
	返回数据说明：
		userType:会员级别
		repoPub:共有repo资源量
		repoPri:私有repo资源量
		pullNum:免费数据Pull量
		buyWay:pull付费方式 (1:预付费，2后付费)
		deposit：托管配额
		annualFee:年费
	返回数据示例：
		{
			"userType":1,
			"repoPub":0,
			"repoPri":0,
			"pullNum":500,
			"buyWay":1,
			"deposit":0M,
			"annualFee":0
		}
#指令：POST /vip/:loginname 新增会员信息
	说明：
		新增用户的会员信息
	输入参数说明：
		userType：会员级别
	Example Request：
		GET /users/foo HTTP/1.1 
		Accept: text/json;charset=UTF-8
		Authorization: token
		USER:foo
		{
			"userType":"3"
		}
	返回数据说明：
		code:状态码
		msg:操作信息，用来记录失败信息
	返回数据示例：
		{"code":0,"msg":"ok"}
#指令：PUT /vip/:loginname 修改会员信息
	说明：
		修改用户的会员信息
	输入参数说明：
		userType：会员级别
	Example Request：
		GET /users/foo HTTP/1.1 
		Accept: text/json;charset=UTF-8
		Authorization: token
		USER:foo
		{
			"userType":"3"
		}
	返回数据说明：
		code:状态码
		msg:操作信息，用来记录失败信息
	返回数据示例：
		{"code":0,"msg":"ok"}
