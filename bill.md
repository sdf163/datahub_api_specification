# API 列表
- GET /bill/:loginname/info 查看用户账户信息

- GET /bill/:loginname/recharge/detail 查看用户账单明细

- GET /bill/:loginname/trade/detail 查看用户交易明细

- PUT /bill/:loginname/creditLimit 修改信用额度

- PUT /bill/:loginname/recharge 充值，提现

- PUT /bill/:loginname/cancel 取消交易

- PUT /bill/:loginname/status 退款审核

- PUT /bill/:loginname/trade/init 发起购买交易

- PUT /bill/:loginname/trade/commit 提交交易（交易结束）

- PUT /bill/:loginname/trade/cancel 取消交易

- PUT /bill/:loginname/trade/cancel/audit 取消交易审核

##指令：GET /bill/:loginname/info 查看用户账单信息
	说明：
		【自己，管理员】查看用户会员的相关信息
	输入参数说明：
		无
	Example Request：
		GET /bill/foo/info HTTP/1.1 
		Accept: text/json;charset=UTF-8
		Authorization: token
		USER:foo
	返回数据说明：
		actualBalance:余额
		availableBalance:可用余额
		creditLimit:信用额度

	返回数据示例：

		{"data":{
			"actualBalance":1000,
			"availableBalance":800,
			"creditLimit":500
			},
		"code":0,"msg":"ok"
		}
##指令：GET /bill/:loginname/recharge/detail 查看用户账单明细
	说明：
		【自己，管理员】查看用户会员的相关信息
	输入参数说明：
		start_time:账单开始时间
		end_time:账单结束时间
		type:类型，1：充值；2：提现
		
	Example Request：
		GET /bill/foo/recharge/detail HTTP/1.1 
		Accept: text/json;charset=UTF-8
		Authorization: token
		USER:foo
		{
			"start_time":"2015-09-02",
			"end_time":"2015-10-01",
			"type":1
		}
	返回数据说明：
		orderId:订单号
		rechargeTime:时间
		rechargeType:类型，1：充值；2：提现
		rechargeAmount:金额
		channel:渠道
		
	返回数据示例：

		{"data":[{"orderId":"111","rechargeTime":"2015-09-02","rechargeType":1,"rechargeAmount":100,"channel":"网银"},
				 {"orderId":"112","rechargeTime":"2015-09-03","rechargeType":1,"rechargeAmount":200,"channel":"网银"},
			    ]
		"code":0,"msg":"ok"
		}

##指令：GET /bill/:loginname/trade/detail 查看用户交易明细
	说明：
		【自己，管理员】查看用户会员的相关信息
	输入参数说明：
		start_time:账单开始时间
		end_time:账单结束时间
		trade_type:交易类型，1：消费；2：收入
		status：账单状态，1:待生效;2：生效；3:失效；4：退款待审核；5退款成功；6：退款审核失败
		
	Example Request：
		GET /bill/foo/trade/detail HTTP/1.1 
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
		orderId:订单号
		planId:套餐计划ID
		tradeItem:交易的item
		tradeTime:交易时间
		effectTime:生效时间
		tradeType:交易类型，1：消费；2：收入
		status:账单状态，1:待生效;2：生效；3:失效；4：退款待审核；5退款成功；6：退款审核失败
		tradeUserName:与当前用户交易的用户
		tradeAmount:交易金额
		

	返回数据示例：

		{"data":[{"orderId":111,"planId":"11","tradeItem":"repo1_item","tradeTime":"2015-09-02","effectTime":"2015-09-10""tradeType":2,"status":2,"tradeUserName":"user1","tradeAmount":100},
				 {"orderId":112,"planId":"21","tradeItem":"repo2_item","tradeTime":"2015-09-02","effectTime":"",tradeType":1,"status":1,"tradeUserName":"me","tradeAmount":100},
			    ]
		"code":0,"msg":"ok"
		}


#指令：PUT /bill/:loginname/recharge 充值，提现
	说明：
		【管理员,自己】充值
	输入参数说明：
		order_id:订单
		amount:金额
		type:类型，1：充值；2：提现; 3：扣年费
		channel:渠道
	Example Request：
		PUT /bill/foo/recharge HTTP/1.1 
		Accept: text/json;charset=UTF-8
		Authorization: token
		USER:admin
		{
			"order_id":"recharge_11",
			"trade_amount":"100",
			"type":1,
			"channel":"支付宝"
		}
	返回数据说明：
		code:状态码
		msg:操作信息，用来记录失败信息
	返回数据示例：
		{"code":0,"msg":"ok"}
#指令：PUT /bill/:loginname/creditLimit
	说明：
		【管理员】修改用户信用额度
	输入参数说明：
		creditLimit:信用额度（可透支金额）
	Example Request：
		PUT /bill/foo/creditLimit HTTP/1.1 
		Accept: text/json;charset=UTF-8
		Authorization: token
		USER:admin
		{
			"creditLimit":"1000"
		}
	返回数据说明：
		code:状态码
		msg:操作信息，用来记录失败信息
	返回数据示例：
		{"code":0,"msg":"ok"}
#指令：PUT /bill/:loginname/trade/init 发起购买交易
	说明：
		【管理员,自己】购买交易，执行操作成功后，会生成两条记录，一个是消费用户的消费记录，一个是商家的收费记录
					   如果购买金额不足，会提示余额不足，交易失败
					   loginname：购买方
	输入参数说明：
		order_id:订单ID
		plan_id:套餐计划Id
		trade_item:交易item
		trade_amount:充值金额
		trade_user:卖方
	Example Request：
		PUT /bill/foo/trade/init HTTP/1.1 
		Accept: text/json;charset=UTF-8
		Authorization: token
		USER:admin
		{
			"order_id":"trade_11","plan_id":""111","trade_item":"repo1_item1","trade_amount":"100","trade_user":"user1"
		}
	返回数据说明：
		code:状态码
		msg:操作信息，用来记录失败信息
	返回数据示例：
		{"code":0,"msg":"ok"}

#指令：PUT /bill/:loginname/trade/commit 提交交易（交易结束）
	说明：
		【管理员,自己】购买交易，执行操作成功后，会生成两条记录，一个是消费用户的消费记录，一个是商家的收费记录
					   如果购买金额不足，会提示余额不足，交易失败
					   loginname：购买方
	输入参数说明：
		order_id:订单ID
		status：账单状态，2：生效；3:失效
	Example Request：
		PUT /bill/foo/trade/commit HTTP/1.1 
		Accept: text/json;charset=UTF-8
		Authorization: token
		USER:admin
		{
			"order_id":"trade_11","status":"2"
		}
	返回数据说明：
		code:状态码
		msg:操作信息，用来记录失败信息
	返回数据示例：
		{"code":0,"msg":"ok"}
		
#指令：PUT /bill/:loginname/trade/cancel 取消交易
	说明：
		【管理员,自己】取消交易，会产生退款记录，退款审核通过后会将钱退换给消费者账户
	输入参数说明：
		order_id:取消交易的订单ID
	Example Request：
		PUT /bill/foo/trade/cancel HTTP/1.1 
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
		
#指令：PUT /bill/:loginname/trade/cancel/audit 取消交易审核
	说明：
		【管理员,自己】审核退款交易：退款审核通过后会将钱退换给消费者账户
	输入参数说明：
		order_id:取消交易的订单ID
		status：账单状态，4取消成功;5：取消失败
	Example Request：
		PUT /bill/foo/trade/cancel/audit HTTP/1.1 
		Accept: text/json;charset=UTF-8
		Authorization: token
		USER:admin
		{
			"order_id":"110","status":"4"
		}
	返回数据说明：
		code:状态码
		msg:操作信息，用来记录失败信息

