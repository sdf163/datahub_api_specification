# 订购

## Errors

	ErrorCodeUnkown                 = 5000
	ErrorCodeJsonBuilding           = 5001
	ErrorCodeUrlNotSupported        = 5002
	ErrorCodeDbNotInitlized         = 5003
	ErrorCodeAuthFailed             = 5004
	ErrorCodePermissionDenied       = 5005
	ErrorCodeInvalidParameters      = 5006
	ErrorCodeGetDataItem            = 5007
	ErrorCodeCreateSubscription     = 5008
	ErrorCodeGetSubscription        = 5009
	ErrorCodeRemoveSubscription     = 5010
	ErrorCodeQuerySubscription      = 5011
	ErrorCodeSubscriptionNotFound   = 5012
	ErrorCodeCreateTransaction      = 5013
	ErrorCodeGetTransaction         = 5014
	ErrorCodeQueryTransaction       = 5015
	ErrorCodeGetStatistics          = 5016
	ErrorCodeParseJsonFailed        = 5017
	ErrorCodeFailedToConnectRemote  = 5018
	ErrorCodeNotOkRemoteResponse    = 5019
	ErrorCodeInvalidRemoteResponse  = 5020
	ErrorCodeTokenNotFound          = 5021
	ErrorCodeTokenExpired           = 5022
	ErrorCodeInvalidEntryPoints     = 5023
	ErrorCodeInsufficientBalance    = 5024
	ErrorCodeFailedToInitUserTrade  = 5025
	ErrorCodeGetUserBillInfo        = 5026
	ErrorCodeModifyUserUsedPullNum  = 5027
	ErrorCodeSignSubscription       = 5028
	ErrorCodeComsumeSubscription    = 5029
	ErrorCodeGetUserPullNumInfo     = 5030
	ErrorCodeCreateTdoken           = 5031
	ErrorCodeGetPlanSigningTimes    = 5032
	ErrorCodeUpdatePlanSigningTimes = 5033
	ErrorCodeGetSubscriptionApply    = 5034
	ErrorCodeCreateSubscriptionApply = 5035
	ErrorCodeModifySubscriptionApply = 5036

## APIs

### (40) GET /subscriptions/pull?groupbydate=[0|1]&phase={phase}&page={page}&size={size}

说明

	【需求者】查询所有订购

输入参数说明：
	
	groupbydate: (可选，默认为0) 是否按日期分组
	phase: (可选) 整数(consuming: 1, freezed: 2, finished: 3, cancelled: 5, removed: 6, applying: 7, wthdrawn: 8, denied: 9, agreed_but_insufficient_balance: 10)。
	page: (可选) 第几页，最小值为1
	size: (可选) 每页最多返回多少条数据

输入样例：

	GET /subscriptions/pull HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb

输出样例：
        
	{
		"total": 100,
		"results": [
			{
				"subscriptionid": 1234567,
				"sellername": "li4@example.com"
				"repname":"NBA",
				"itemname":"bear",
				"supply_style":"batch",
				"signtime":"2015-11-10T15:04:05Z08:00",
				"expiretime":"2016-01-15T11:28:21Z",
				"freezetime":"2015-12-11T10:51:11Z",
				"finishtime":"2016-01-10T10:51:11Z",
				"phase":1,
				"plan":{
					"money":5,
					"units":3,
					"used":0,
					"limit":0,
					"subs":1,
					"expire":30
				}
			},
			{
				"subscriptionid": 1234568,
				"sellername": "zhang3@example.com"
				"repname":"CBA",
				"itemname":"triger",
				"supply_style":"batch",
				"signtime":"2015-11-01T15:04:05Z08:00",
				"expiretime":"2015-12-01T15:04:05Z08:00"
				"freezetime":"2015-11-22T15:04:05Z08:00",
				"finishtime":"2016-01-22T15:04:05Z08:00",
				"phase":1,
				"plan":{
					"money":5,
					"units":3,
					"used":0,
					"limit":0,
					"subs":1,
					"expire":30
				}
			}
		]
	}

返回数据说明：

	sellername: 数据提供者
	repname: repository name
	itemname: data item name
	supply_style: flow | batch 
	signtime: 订购时间
	expiretime: 自动过期时间
	phase: 1-3, 5-10 (意义：consuming: 1, freezed: 2, finished: 3, cancelled: 5, removed: 6, applying: 7, wthdrawn: 8, denied: 9, complained: 10)
	plan.money: 交易金额
	plan.units: 最大下载次数（supply_style=batch）,最大下载天数（supply_style=flow)
	plan.used: 已经使用量　
	plan.limit: 最多可以订购次数
	plan.subs: 当前订购次数
	plan.expire: 交易有效期（天数）
	
	不同的时间只在特定phase有效

	consuming, 1: signtime, expiretime 有效
	freezed, 2: signtime, expiretime, freezetime 有效
	finished, 3: signtime, expiretime, freezetime, finishtime 有效
	cancelled, 5: signtime, expiretime, canceltime 有效
	removed, 6: signtime, expiretime, freezetime, removetime 有效
	applying, 7: applytime, expiretime 有效
	wthdrawn, 8: applytime, withdrawtime 有效
	denied, 9: applytime, denytime 有效
	agreed_but_insufficient_balance, 10: applytime, agreetime 有效

### (41) GET /subscriptions/pull/:repname?groupbydate=[0|1]&phase={phase}&page={page}&size={size}

说明

	【需求者】查询在某个respository中的所有订购

输入参数说明：
	
	groupbydate: (可选，默认为0) 是否按日期分组
	phase: (可选) 整数(consuming: 1, freezed: 2, finished: 3, cancelled: 5, removed: 6, applying: 7, wthdrawn: 8, denied: 9, complained: 10)。
	page: (可选) 第几页，最小值为1
	size: (可选) 每页最多返回多少条数据

输入样例：

	GET /subscriptions/pull/repo001 HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb

输出样例：
        
	{
		"total": 100,
		"results": [
			{
				"subscriptionid": 1234567,
				"sellername": "zhang3@example.com",
				"itemname":"bear",
				"supply_style":"batch",
				"signtime":"2015-11-10T15:04:05Z08:00",
				"expiretime":"2016-01-15T11:28:21Z",
				"freezetime":"2015-12-11T10:51:11Z",
				"finishtime":"2016-01-10T10:51:11Z",
				"phase":1,
				"plan":{
					"money":5,
					"units":3,
					"used":0,
					"limit":0,
					"subs":1,
					"expire":30
				}
			},
			{
				"subscriptionid": 1234568,
				"sellername": "zhang3@example.com",
				"itemname":"triger",
				"supply_style":"batch",
				"signtime":"2015-11-01T15:04:05Z08:00",
				"expiretime":"2015-11-04T15:04:05Z08:00"
				"freezetime":"2015-12-04T15:04:05Z08:00",
				"finishtime":"2016-01-04T15:04:05Z08:00",
				"phase":1,
				"plan":{
					"money":5,
					"units":3,
					"used":0,
					"limit":0,
					"subs":1,
					"expire":30
				}
			}
		]
	}

### (42) GET /subscriptions/pull/:repname/:itemname?groupbydate=[0|1]&phase={phase}&page={page}&size={size}

说明

	【需求者】查询在某个dataitem上的所有订购

输入参数说明：
	
	groupbydate: (可选，默认为0) 是否按日期分组
	phase: (可选) 整数(consuming: 1, freezed: 2, finished: 3, cancelled: 5, removed: 6, applying: 7, wthdrawn: 8, denied: 9, complained: 10)。
	page: (可选) 第几页，最小值为1
	size: (可选) 每页最多返回多少条数据

输入样例：

	GET /subscriptions/pull HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb

输出样例：
        
	{
		"total": 100,
		"results": [
			{
				"subscriptionid": 1234567,
				"sellername": "li4@example.com",
				"supply_style":"batch",
				"signtime":"2015-11-10T15:04:05Z08:00",
				"expiretime":"2016-01-15T11:28:21Z",
				"freezetime":"2015-12-11T10:51:11Z",
				"finishtime":"2016-01-10T10:51:11Z",
				"phase":1,
				"plan":{
					"money":5,
					"units":3,
					"used":0,
					"limit":0,
					"subs":1,
					"expire":30
				}
			},
			{
				"subscriptionid": 1234568,
				"sellername": li4@example.com",
				"supply_style":"flow",
				"signtime":"2015-11-01T15:04:05Z08:00",
				"expiretime":"2015-11-04T15:04:05Z08:00"
				"freezetime":"2015-12-04T15:04:05Z08:00",
				"finishtime":"2016-01-04T15:04:05Z08:00",
				"phase":1,
				"plan":{
					"money":5,
					"units":3,
					"used":0,
					"limit":0,
					"subs":1,
					"expire":30
				}
			}
		]
	}

### (43) GET /subscriptions/push?groupbydate=[0|1]&phase={phase}&page={page}&size={size}

说明

	【提供者】查询所有在自己的dataitem上的订购

输入参数说明：
	
	groupbydate: (可选，默认为0) 是否按日期分组
	phase: (可选) 整数(consuming: 1, freezed: 2, finished: 3, cancelled: 5, removed: 6, applying: 7, wthdrawn: 8, denied: 9, complained: 10)。
	page: (可选) 第几页，最小值为1
	size: (可选) 每页最多返回多少条数据

输入样例：

	GET /subscriptions/push HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb

输出样例：
        
	{
		"total": 100,
		"results": [
			{
				"subscriptionid": 1234567,
				"buyername":"zhang3@example.com",
				"repname":"NBA",
				"itemname":"bear",
				"supply_style":"batch",
				"signtime":"2015-11-01T15:04:05Z08:00",
				"expiretime":"2015-11-04T15:04:05Z08:00"
				"freezetime":"2015-12-04T15:04:05Z08:00",
				"finishtime":"2016-01-04T15:04:05Z08:00",
				"phase":1,
				"plan":{
					"money":5,
					"units":3,
					"used":0,
					"limit":0,
					"subs":1,
					"expire":30
				}
			},
			{
				"subscriptionid": 1234568,
				"buyername":"li4@example.com",
				"repname":"CBA",
				"itemname":"triger",
				"supply_style":"batch",
				"signtime":"2015-11-01T15:04:05Z08:00",
				"expiretime":"2015-11-04T15:04:05Z08:00"
				"freezetime":"2015-12-04T15:04:05Z08:00",
				"finishtime":"2016-01-04T15:04:05Z08:00",
				"phase":1,
				"plan":{
					"money":5,
					"units":3,
					"used":0,
					"limit":0,
					"subs":1,
					"expire":30
				}
			}
		]
	}

返回数据说明：

	buyername: 数据消费者

### (44) GET /subscriptions/push/:repname?groupbydate=[0|1]&phase={phase}&page={page}&size={size}

说明

	【提供者】查询在自己的某个respository中的所有订购

输入参数说明：
	
	groupbydate: (可选，默认为0) 是否按日期分组
	phase: (可选) 整数(consuming: 1, freezed: 2, finished: 3, cancelled: 5, removed: 6, applying: 7, wthdrawn: 8, denied: 9, complained: 10)。
	page: (可选) 第几页，最小值为1
	size: (可选) 每页最多返回多少条数据

输入样例：

	GET /subscriptions/push/repo001 HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb

输出样例：
        
	{
		"total": 100,
		"results": [
			{
				"subscriptionid": 1234567,
				"buyername":"zhang3@example.com",
				"itemname":"bear",
				"supply_style":"batch",
				"signtime":"2015-11-01T15:04:05Z08:00",
				"expiretime":"2015-11-04T15:04:05Z08:00"
				"freezetime":"2015-12-04T15:04:05Z08:00",
				"finishtime":"2016-01-04T15:04:05Z08:00",
				"phase":1,
				"plan":{
					"money":5,
					"units":3,
					"used":0,
					"limit":0,
					"subs":1,
					"expire":30
				}
			},
			{
				"subscriptionid": 1234568,
				"buyername":"li4@example.com",
				"itemname":"triger",
				"supply_style":"batch",
				"signtime":"2015-11-01T15:04:05Z08:00",
				"expiretime":"2015-11-04T15:04:05Z08:00"
				"freezetime":"2015-12-04T15:04:05Z08:00",
				"finishtime":"2016-01-04T15:04:05Z08:00",
				"phase":1,
				"plan":{
					"money":5,
					"units":3,
					"used":0,
					"limit":0,
					"subs":1,
					"expire":30
				}
			}
		]
	}

### (45) GET /subscriptions/push/:repname/:itemname?groupbydate=[0|1]&phase={phase}&page={page}&size={size}

说明

	【提供者】查询自己的某个dataitem上的所有订购

输入参数说明：
	
	groupbydate: (可选，默认为0) 是否按日期分组
	phase: (可选) 整数(consuming: 1, freezed: 2, finished: 3, cancelled: 5, removed: 6, applying: 7, wthdrawn: 8, denied: 9, complained: 10)。
	page: (可选) 第几页，最小值为1
	size: (可选) 每页最多返回多少条数据

输入样例：

	GET /subscriptions/push/repo001/item002 HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb

输出样例：
        
	{
		"total": 100,
		"results": [
			{
				"subscriptionid": 1234567,
				"buyername":"zhang3@example.com",
				"supply_style":"batch",
				"signtime":"2015-11-01T15:04:05Z08:00",
				"expiretime":"2015-11-04T15:04:05Z08:00"
				"freezetime":"2015-12-04T15:04:05Z08:00",
				"finishtime":"2016-01-04T15:04:05Z08:00",
				"phase":1,
				"plan":{
					"money":5,
					"units":3,
					"used":0,
					"limit":0,
					"subs":1,
					"expire":30
				}
			},
			{
				"subscriptionid": 1234568,
				"buyername":"li4@example.com",
				"supply_style":"batch",
				"signtime":"2015-11-01T15:04:05Z08:00",
				"expiretime":"2015-11-04T15:04:05Z08:00"
				"freezetime":"2015-12-04T15:04:05Z08:00",
				"finishtime":"2016-01-04T15:04:05Z08:00",
				"phase":1,
				"plan":{
					"money":5,
					"units":3,
					"used":0,
					"limit":0,
					"subs":1,
					"expire":30
				}
			}
		]
	}

### (46) GET /subscription/:repname/:itemname

说明

	【需求者】查询是否已经有有效订购存在

输入参数说明：
	
	无

输入样例：

	GET /subscription/repo01/item02 HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb

输出样例：
        
	true

### (46b) GET /subscription/:repname/:itemname/apply

说明

	【需求者】查询当前的订购申请，如果没有，返回空

输入参数说明：
	
	无

输入样例：

	GET /subscription/repo01/item02/apply HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb

输出样例1：
        
	{
		"subscriptionid": 1234568,
		"applytime":"2015-11-01T15:04:05Z08:00",
	}

输出样例2：
        
	null

### (47) POST /subscription/:repname/:itemname

说明

	【需求者】取得预订购信息

输入参数说明：
	
	无

输入样例：

	POST /subscription/repo1/item123 HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb
	
输出样例：
        
	{
		"subscriptionid": 1234567890,
		“signtime": "2015-09-10T15:04:05Z08:00"
	}

返回数据说明：

	subscriptionid: 预订购id
	signtime: 预订购时间

### (47b) POST /subscription/:repname/:itemname/apply

说明

	【需求者】为申请订购取得预订购信息

输入参数说明：
	
	无

输入样例：

	POST /subscription/repo1/item123/apply HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb
	
输出样例：
        
	{
		"subscriptionid": 1234567890,
		“applytime": "2015-09-10T15:04:05Z08:00"
	}

返回数据说明：

	subscriptionid: 预订购id
	applytime: 预订购时间

### (48) PUT /subscription/:repname/:itemname

说明

	【需求者】确定签署一个订购 (subscribe)

输入参数说明：
	
	action: (可选，默认为sign) sign | complain | deny_complain | accept_complain
	subscriptionid: 订购id (对于action=sign, 为预订购id)
	planid: DataItem上的某个收费计划的uuid (只对action=sign有效)
	reason: 对action的简短解释（小于255个字符，只对complain | deny_complain | accept_complain有意义）。

输入样例：

	PUT /subscription/repo1/item123 HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb
	
	{
		"subscriptionid": 1234567890,
		"planid": "a0a1a2a3a4a5a6a7a8a9aaabacad"
	}
	
输出样例：
        
	{
		"subscriptionid": 1234567,
		"sellername": "li4@example.com"
		"repname":"NBA",
		"itemname":"bear",
		"supply_style":"batch",
		"signtime":"2015-11-10T15:04:05Z08:00",
		"expiretime":"2016-01-15T11:28:21Z",
		"freezetime":"2015-12-11T10:51:11Z",
		"finishtime":"2016-01-10T10:51:11Z",
		"phase":1,
		"plan":{
			"money":5,
			"units":3,
			"used":0,
			"limit":0,
			"subs":1,
			"expire":30
		}
	}

### (48b) PUT /subscription/:repname/:itemname/apply

说明

	【需求者】申请一个订购 (apply)
	【需求者】取消申请一个订购 (withdraw)
	【提供者】同意一个订购申请 (agree)
	【提供者】否决一个订购申请 (deny)

输入参数说明：
	
	action: apply | withdraw | agree | deny
	subscriptionid: 订购id (对于action=apply, 为预订购id)
	planid: DataItem上的某个收费计划的uuid (只对action=apply有效)

输入样例：

	PUT /subscription/repo1/item123/apply HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb
	
	{
		“action": "apply",
		"subscriptionid": 1234567890,
		"planid": "a0a1a2a3a4a5a6a7a8a9aaabacad"
	}
	
输出样例：
        
	{
		"subscriptionid": 1234567,
		"sellername": "li4@example.com"
		"repname":"NBA",
		"itemname":"bear",
		"supply_style":"batch",
		"applytime":"2015-11-10T15:04:05Z08:00",
		"expiretime":"2016-11-17T15:04:05Z08:00",
		"phase":7,
		"plan":{
			"money":5,
			"units":3,
			"used":0,
			"limit":0,
			"subs":1,
			"expire":30
		}
	}

### (49) PUT /subscription/:subscriptionid (已废弃，请用api#48 with action=accept_complain instead)

说明

	【管理员】取消订购action=remove

输入参数说明：
	
	action: remove
	reason: 一段文本描述原因(<256个字符)

输入样例：

	PUT /subscription/1234567 HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb
	
	{
		"action": "remove",
		"reason": "bla bla ..."
	}

输出样例：
        
	null

### (4a) GET /subscription_stat/:repname/:itemname?phase={phase}

说明

	【任意】返回该DataItem的订购量

输入参数说明：
	
	phase: (可选) 限定订购的phase, 如果不忽略此参数，目前其值只能为1 (表示consuming)。如果此值被忽略，返回所有已扣款的订购的数量。
	
	注意：如果phase被指定，http header中必须加上auth头

输入样例：

	GET /subscription_stat/repo1/item123 HTTP/1.1 
	Accept: application/json

输出样例：

	"numsubs":567

### (4b) GET /subscription_stat/:repname?phase={phase}

说明

	【任意】返回该repositories的订购量

输入参数说明：
	
	phase: (可选) 订购的phase, 如果不忽略此参数，目前其值只能为1 (表示consuming)。如果此值被忽略，返回所有已扣款的订购的数量。
	
	注意：如果phase被指定，http header中必须加上auth头

输入样例：

	GET /subscription_stat/repo1 HTTP/1.1 
	Accept: application/json

输出样例：

	"numsubs":567

### (4c) GET /subscription_stat/:repname/:itemname/:planid

说明

	【需求者】返回对该DataItem上的某个价格计划的订购次数

输入参数说明：
	
	无

输入样例：

	GET /subscription_stat/repo1/item123/1000000001000 HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb

输出样例：

	"numsigns":1

### (4d) GET /subscriptions/subscribers/:repname?phase=1

说明

	【提供者】查询在自己的某个repo上的所有订购者

输入参数说明：
	
	phase: (必选) 订购的phase, 目前只能为1(生效中但没完成)

输入样例：

	GET /subscriptions/subscribers/repo001?phase=1 HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb

输出样例：
        
	{
		"total": 3,
		"results": [
			"zhang3@example.com",
			"li4@example.com",
			"johe@2xample.com"
		]
	}

### (4e) GET /subscriptions/subscribers/:repname/:itemname?phase=1

说明

	【提供者】查询在自己的某个date item上的所有订购者

输入参数说明：
	
	phase: (必选) 订购的phase, 目前只能为1(生效中但没完成)

输入样例：

	GET /subscriptions/subscribers/repo001/item002?phase=1 HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb

输出样例：
        
	{
		"total": 3,
		"results": [
			"zhang3@example.com",
			"li4@example.com",
			"johe@2xample.com"
		]
	}

### (4f) GET /subscriptions/dataitems?phase=1&repname={repname}

说明

	【提供者】查询自己所有订购的date items

输入参数说明：
	
	phase: (必选) 订购的phase, 目前只能为1(生效中但没完成)
	repname: (可选) 过滤条件，限定repository

输入样例：

	GET /subscriptions/dataitems?phase=1 HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb

输出样例：
        
	{
		"total": 2,
		"results": [
			{"repname":"CBA", "itemname":"triger"},
			{"repname":"repo0", "itemname":"item1"}
		]
	}

