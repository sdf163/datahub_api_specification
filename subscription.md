# 订阅

## Errors

	ErrorCodeUnkown                = 5000
	ErrorCodeJsonBuilding          = 5001
	ErrorCodeUrlNotSupported       = 5002
	ErrorCodeDbNotInitlized        = 5003
	ErrorCodeAuthFailed            = 5004
	ErrorCodePermissionDenied      = 5005
	ErrorCodeInvalidParameters     = 5006
	ErrorCodeGetDataItem           = 5007
	ErrorCodeCreateSubscription    = 5008
	ErrorCodeGetSubscription       = 5009
	ErrorCodeRemoveSubscription    = 5010
	ErrorCodeQuerySubscription     = 5011
	ErrorCodeSubscriptionNotFound  = 5012
	ErrorCodeCreateTransaction     = 5013
	ErrorCodeGetTransaction        = 5014
	ErrorCodeQueryTransaction      = 5015
	ErrorCodeGetStatistics         = 5016
	ErrorCodeParseJsonFailed       = 5017
	ErrorCodeFailedToConnectRemote = 5018
	ErrorCodeNotOkRemoteResponse   = 5019
	ErrorCodeInvalidRemoteResponse = 5020
	ErrorCodeTokenNotFound         = 5021
	ErrorCodeTokenExpired          = 5022
	ErrorCodeInvalidEntryPoints    = 5023
	ErrorCodeInsufficientBalance   = 5024
	ErrorCodeFailedToInitUserTrade = 5025
	ErrorCodeGetUserBillInfo       = 5026
	ErrorCodeModifyUserUsedPullNum = 5027
	ErrorCodeSignSubscription      = 5028
	ErrorCodeComsumeSubscription   = 5029

## APIs

### (40) GET /subscriptions/pull?phase={phase}&beforetime={beforetime}

说明

	【需求者】查询所有订阅

输入参数说明：
	
	phase:[可选] 整数(consuming: 1, freezed: 2, finished: 3, cancelled: 5, removed: 6)。
	beforetime: [可选] 最晚时间, 格式：2015-11-23T09:02:52Z

输入样例：

	GET /subscriptions/pull HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb

输出样例：
        
	[
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
			"phase":"consuming",
			"plan":{
				"money":5,
				"times":3,
				"time":0,
				"used":0,
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
			"expiretime":"2015-11-04T15:04:05Z08:00"
			"freezetime":"2015-12-04T15:04:05Z08:00",
			"finishtime":"2016-01-04T15:04:05Z08:00",
			"phase":"consuming",
			"plan":{
				"money":5,
				"times":0,
				"time":3,
				"used":0,
				"expire":30
			}
		}
	]

返回数据说明：

	sellername: 数据提供者
	repname: repository name
	itemname: data item name
	supply_style: flow | batch 
	signtime: 订阅时间
	expiretime: 自动过期时间
	freezetime: 交易成功时间（在未达到freezed phase之前，此值为空）
	finishtime: 交易完成时间（在未达到freezed phase之前，此值为空）
	phase: pending | consuming | freezed | finished | cancelled | removed
	plan.money: 交易金额
	plan.times: 最大下载次数（只对supply_style=batch有效）
	plan.time: 最大下载天数（只对supply_style=flow有效)
	plan.used: 已经使用量　
	plan.expire: 交易有效期（天数）

### (41) GET /subscriptions/pull/:repname?phase={phase}&beforetime={beforetime}

说明

	【需求者】查询在某个respository中的所有订阅

输入参数说明：
	
	phase:[可选] 整数(consuming: 1, freezed: 2, finished: 3, cancelled: 5, removed: 6)。
	beforetime: [可选] 最晚时间, 格式：2015-11-23T09:02:52Z

输入样例：

	GET /subscriptions/pull/repo001 HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb

输出样例：
        
	[
		{
			"subscriptionid": 1234567,
			"sellername": "zhang3@example.com",
			"itemname":"bear",
			"supply_style":"batch",
			"signtime":"2015-11-10T15:04:05Z08:00",
			"expiretime":"2016-01-15T11:28:21Z",
			"freezetime":"2015-12-11T10:51:11Z",
			"finishtime":"2016-01-10T10:51:11Z",
			"phase":"consuming",
			"plan":{
				"money":5,
				"times":3,
				"time":0,
				"used":0,
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
			"phase":"consuming",
			"plan":{
				"money":5,
				"times":0,
				"time":3,
				"used":0,
				"expire":30
			}
		}
	]

### (42) GET /subscriptions/pull/:repname/:itemname?phase={phase}&beforetime={beforetime}

说明

	【需求者】查询在某个dataitem上的所有订阅

输入参数说明：
	
	phase:[可选] 整数(consuming: 1, freezed: 2, finished: 3, cancelled: 5, removed: 6)。
	beforetime: [可选] 最晚时间, 格式：2015-11-23T09:02:52Z

输入样例：

	GET /subscriptions/pull HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb

输出样例：
        
	[
		{
			"subscriptionid": 1234567,
			"sellername": "li4@example.com",
			"supply_style":"batch",
			"signtime":"2015-11-10T15:04:05Z08:00",
			"expiretime":"2016-01-15T11:28:21Z",
			"freezetime":"2015-12-11T10:51:11Z",
			"finishtime":"2016-01-10T10:51:11Z",
			"phase":"consuming",
			"plan":{
				"money":5,
				"times":3,
				"time":0,
				"used":0,
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
			"phase":"consuming",
			"plan":{
				"money":5,
				"times":0,
				"time":3,
				"used":0,
				"expire":30
			}
		}
	]

### (43) GET /subscriptions/push?phase={phase}&beforetime={beforetime}

说明

	【提供者】查询所有在自己的dataitem上的订阅

输入参数说明：
	
	phase:[可选] 整数(consuming: 1, freezed: 2, finished: 3, cancelled: 5, removed: 6)。
	beforetime: [可选] 最晚时间, 格式：2015-11-23T09:02:52Z

输入样例：

	GET /subscriptions/push HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb

输出样例：
        
	[
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
			"phase":"consuming",
			"plan":{
				"money":5,
				"times":0,
				"time":3,
				"used":0,
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
			"phase":"consuming",
			"plan":{
				"money":5,
				"times":0,
				"time":3,
				"used":0,
				"expire":30
			}
		}
	]

返回数据说明：

	buyername: 数据消费者
	repname: repository name
	itemname: data item name
	signtime: 订阅时间

### (44) GET /subscriptions/push/:repname?phase={phase}&beforetime={beforetime}

说明

	【提供者】查询在自己的某个respository中的所有订阅

输入参数说明：
	
	phase:[可选] 整数(consuming: 1, freezed: 2, finished: 3, cancelled: 5, removed: 6)。
	beforetime: [可选] 最晚时间, 格式：2015-11-23T09:02:52Z

输入样例：

	GET /subscriptions/push/repo001 HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb

输出样例：
        
	[
		{
			"subscriptionid": 1234567,
			"buyername":"zhang3@example.com",
			"itemname":"bear",
			"supply_style":"batch",
			"signtime":"2015-11-01T15:04:05Z08:00",
			"expiretime":"2015-11-04T15:04:05Z08:00"
			"freezetime":"2015-12-04T15:04:05Z08:00",
			"finishtime":"2016-01-04T15:04:05Z08:00",
			"phase":"consuming",
			"plan":{
				"money":5,
				"times":0,
				"time":3,
				"used":0,
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
			"phase":"consuming",
			"plan":{
				"money":5,
				"times":0,
				"time":3,
				"used":0,
				"expire":30
			}
		}
	]

### (45) GET /subscriptions/push/:repname/:itemname?phase={phase}&beforetime={beforetime}

说明

	【提供者】查询自己的某个dataitem上的所有订阅

输入参数说明：
	
	phase:[可选] 整数(consuming: 1, freezed: 2, finished: 3, cancelled: 5, removed: 6)。
	beforetime: [可选] 最晚时间, 格式：2015-11-23T09:02:52Z

输入样例：

	GET /subscriptions/push/repo001/item002 HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb

输出样例：
        
	[
		{
			"subscriptionid": 1234567,
			"buyername":"zhang3@example.com",
			"supply_style":"batch",
			"signtime":"2015-11-01T15:04:05Z08:00",
			"expiretime":"2015-11-04T15:04:05Z08:00"
			"freezetime":"2015-12-04T15:04:05Z08:00",
			"finishtime":"2016-01-04T15:04:05Z08:00",
			"phase":"consuming",
			"plan":{
				"money":5,
				"times":0,
				"time":3,
				"used":0,
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
			"phase":"consuming",
			"plan":{
				"money":5,
				"times":0,
				"time":3,
				"used":0,
				"expire":30
			}
		}
	]

### (46) PUT /subscriptions/clean

说明

	【管理员】清除无效订阅

输入参数说明：
	
	无

输入样例：

	PUT /subscriptions/clean HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb

输出样例：
        
	无

### (47) POST /subscription/:repname/:itemname

说明

	【需求者】取得预订阅信息

输入参数说明：
	
	purpose: subscribe | apply

输入样例：

	POST /subscription/repo1/item123 HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb
	
	{
		"purpose": "subscribe"
	}
	
输出样例：
        
	{
		"subscriptionid": 1234567890,
		“signtime": "2015-09-10T15:04:05Z08:00"
	}

返回数据说明：

	subscriptionid: 预订阅id
	signtime: 预订阅时间

### (48) PUT /subscription/:repname/:itemname (to remove)

说明

	【需求者】确定签署一个订阅

输入参数说明：
	
	purpose: subscribe | apply | cancelapply (可为空，表示默认subscribe)
	subscriptionid: 预订阅id
	planid: DataItem上的某个收费计划的uuid

输入样例：

	PUT /subscription/repo1/item123 HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb
	
	{
		“purpose": "subscribe",
		"subscriptionid": 1234567890,
		"planid": "a0a1a2a3a4a5a6a7a8a9aaabacad"
	}
	
输出样例：
        
	无

### (49) PUT /subscription/:subscriptionid 

说明

	【管理员】取消订阅action=remove

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

### (4a) GET /subscription_stat/:repname/:itemname 

说明

	【任意】返回该DataItem的订阅量

输入参数说明：
	
	无

输入样例：

	GET /subscription_stat/repo1/item123 HTTP/1.1 
	Accept: application/json

输出样例：

	"numsubs":567

### (4b) GET /subscription_stat/:repname 

说明

	【任意】返回该repositories的订阅量

输入参数说明：
	
	无

输入样例：

	GET /subscription_stat/repo1 HTTP/1.1 
	Accept: application/json

输出样例：

	"numsubs":567


	
## 已经废除的

### (41) ~~~GET /subscription/:repname/:itemname~~~  (将废除，将并入40)

说明

	【需求者】查询该DataItem是否订阅过

输入参数说明：
	
	无

输入样例：

	GET /subscription/repo1/item123 HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb

输出样例：

	"subscribed":true

### (43) ~~~DELETE /subscription/:repname/:itemname~~~  (将废除，将被47取代)

说明

	【需求者】取消订阅该DataItem

输入参数说明：
	
	无

输入样例：

	DELETE /subscription/repo1/item123 HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb

输出样例：
        
	null

### (46) ~~~GET /subscriptions/:repname~~~ (将废除，合并到40中)

说明

	【需求者】查询在指定repository中所有订阅的DataItem

输入参数说明：
	
	无

输入样例：

	GET /subscriptions/repo001 HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb

输出样例：
        
	[
		{
			"itemname":"bear",
			"signtime":"2015-11-08"
		},
		{
			"itemname":"triger",
			"signtime":"2015-11-08"
		}
	]
