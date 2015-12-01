# API 列表
- GET /bill/:loginname/info 查看用户账户信息

- GET /bill/:loginname/detail 查看用户账单明细

- PUT /bill/:loginname/recharge 充值

- PUT /bill/:loginname/trade 购买交易

- PUT /bill/:loginname/cancel 取消交易

- PUT /bill/:loginname/status 退款审核

##指令：GET /bill/:loginname/info 查看用户账单信息
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
		actual_balance:余额
		available_balance:可用余额
		credit_limit:信用额度

	返回数据示例：

		{"data":{
			"available_balance":1000,
			"available_balance":800,
			"credit_limit":500
			},
		"code":0,"msg":"ok"
		}
##指令：GET /bill/:loginname/detail 查看用户账单明细
	说明：
		【自己，管理员】查看用户会员的相关信息
	输入参数说明：
		start_time:账单开始时间
		end_time:账单结束时间
		trade_type:交易类型，1：充值；2：消费；3：收入
		status：账单状态，1:待生效;2：生效；3：退款待审核；4退款成功；5：退款审核失败
		
	Example Request：
		GET /bill/foo HTTP/1.1 
		Accept: text/json;charset=UTF-8
		Authorization: token
		USER:foo
		{
			"start_time":"2015-09-02",
			"end_time":"2015-10-01",
			"trade_type":"1",
			"status":"2"
		}
	返回数据说明：
		order_id:订单号
		plan_id:套餐计划ID（充值时为空）
		trade_time:交易时间
		trade_type:交易类型，1：充值；2：消费；3：收入
		status:账单状态，1:待生效;2：生效；3：退款待审核；4退款成功；5：退款审核失败
		trade_user:与当前用户交易的用户（充值时为自己）
		trade_amount:交易金额
		

	返回数据示例：

		{"data":[{"order_id":111,"plan_id":"11","trade_time":"2015-09-02","trade_type":2,"status":2,"trade_user":"user1","trade_amount":100},
				 {"order_id":112,"plan_id":"","trade_time":"2015-09-02","trade_type":1,"status":2,"trade_user":"me","trade_amount":100},
			    ]
		"code":0,"msg":"ok"
		}



#指令：PUT /bill/:loginname/recharge 充值
	说明：
		【管理员,自己】充值
	输入参数说明：
		trade_amount:充值金额
	Example Request：
		PUT /bill/foo HTTP/1.1 
		Accept: text/json;charset=UTF-8
		Authorization: token
		USER:admin
		{
			"trade_amount":"100"
		}
	返回数据说明：
		code:状态码
		msg:操作信息，用来记录失败信息
	返回数据示例：
		{"code":0,"msg":"ok"}
		
#指令：PUT /bill/:loginname/trade 购买交易
	说明：
		【管理员,自己】购买交易，执行操作成功后，会生成两条记录，一个是消费用户的消费记录，一个是商家的收费记录
					   如果购买金额不足，会提示余额不足，交易失败
					   loginname：购买方
	输入参数说明：
		trade_amount:充值金额
		trade_user:与该用户交易的用户
	Example Request：
		PUT /bill/foo HTTP/1.1 
		Accept: text/json;charset=UTF-8
		Authorization: token
		USER:admin
		{
			"trade_amount":"100","trade_user":"user1"
		}
	返回数据说明：
		code:状态码
		msg:操作信息，用来记录失败信息
	返回数据示例：
		{"code":0,"msg":"ok"}
		
#指令：PUT /bill/:loginname/cancel 取消交易
	说明：
		【管理员,自己】取消交易，会产生退款记录，退款审核通过后会将钱退换给消费者账户
	输入参数说明：
		order_id:取消交易的订单ID
	Example Request：
		PUT /bill/foo HTTP/1.1 
		Accept: text/json;charset=UTF-8
		Authorization: token
		USER:admin
		{
			"order_id":"110"
		}
	返回数据说明：
		code:状态码
		msg:操作信息，用来记录失败信息
	返回数据示例：
		{"code":0,"msg":"ok"}
		
#指令：PUT /bill/:loginname/status 退款审核
	说明：
		【管理员,自己】审核退款交易：退款审核通过后会将钱退换给消费者账户
	输入参数说明：
		order_id:取消交易的订单ID
		status：账单状态，1:待生效; 2：生效；3：退款待审核；4退款成功;5：退款审核失败
	Example Request：
		PUT /bill/foo HTTP/1.1 
		Accept: text/json;charset=UTF-8
		Authorization: token
		USER:admin
		{
			"order_id":"110","status":"4"
		}
	返回数据说明：
		code:状态码
		msg:操作信息，用来记录失败信息
	返回数据示例：
		{"code":0,"msg":"ok"}
