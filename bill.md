# API 列表
- GET /bill/:loginname 查看用户账单信息

- PUT /bill/:loginname 修改用户账单信息

##指令：GET /bill/:loginname 查看用户账单信息
	说明：
		【自己，管理员】查看用户会员的相关信息
	输入参数说明：
		无
	Example Request：
		GET /bill/foo HTTP/1.1 
		Accept: text/json;charset=UTF-8
		Authorization: token
		USER:foo
	返回数据说明：
		balance:余额
		type:交易类型，1：充值；2：消费
		op_time:交易时间
		consumption_item:消费Item
		trade_amount:消费金额

	返回数据示例：

		{"data":	[{
			"balance":"1000",
			"type":2,
			"op_time":"2015-09-01 10:20:10",
			"trade_item":"re_it",
			"trade_amount":"100",
			},{
			"balance":"1100",
			"type":1,
			"op_time":"2015-09-02 10:20:10",
			"trade_item":"",
			"trade_amount":"100",
			}],
		"code":0,"msg":"ok"
		}


#指令：PUT /bill/:loginname 修改账单
	说明：
		【管理员,自己】修改用户的会员信息
	输入参数说明：
		type:交易类型，1：充值；2：消费
		op_time:交易时间
		consumption_item:消费Item
		trade_amount:消费金额
	Example Request：
		PUT /bill/foo HTTP/1.1 
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
