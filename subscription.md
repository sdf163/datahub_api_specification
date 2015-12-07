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
	ErrorCodeCancelSubscription    = 5010
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
	ErrorCodeTokenExpird           = 5022
	ErrorCodeInvalidEntryPoints    = 5023

## APIs

### GET /subscriptions?asconsumer=[0|1]&repname={repname}&itemname={itemname} (40)

说明

	【需求者】查询所有订阅的别人的DataItem
	【提供者】查询所有被被人订阅的DataItem
	
	
	如果repname和itemname都没有被指定，返回当前用户的所有订阅
	如果repname被指定但itemname没有被指定，返回当前用户在repname中的订阅
	如果repname和itemname都被指定，返回当前用户在repname/itemname上的订阅

输入参数说明：
	
	asconsumer: 必选，0或者1
	repname: 可选，但如果itemname参数存在，则repname也必须存在
	itemname: 可选

输入样例：

	GET /subscriptions HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb

输出样例(asconsumer=1)：
        
	[
		{
			"repname":"NBA",
			"itemname":"bear",
			"subtime":"2015-11-10T15:04:05Z08:00"
		},
		{
			"repname":"CBA",
			"itemname":"triger",
			"subtime":"2015-11-01T15:04:05Z08:00"
		}
	]

输出样例(asconsumer=1)：
        
	[
		{
			"buyer":"zhang3@example.com",
			"repname":"NBA",
			"itemname":"bear",
			"subtime":"2015-11-10T15:04:05Z08:00"
		},
		{
			"buyer":"li4@example.com",
			"repname":"CBA",
			"itemname":"triger",
			"subtime":"2015-09-10T15:04:05Z08:00"
		}
	]

返回数据说明：

	buyer: 数据消费者
	seller: 数据提供者
	repname: repository name
	itemname: data item name
	subtime: 订阅时间

### GET /subscriptions/:repname (46)(将废除，合并到40中)

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
			"subtime":"2015-11-08"
		},
		{
			"itemname":"triger",
			"subtime":"2015-11-08"
		}
	]

### GET /subscription/:repname/:itemname (41) (将废除，将并入40)

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

### POST /subscription/:repname/:itemname (42)

说明

	【需求者】订阅该DataItem 

输入参数说明：
	
	planid: DataItem上的某个收费计划

输入样例：

	POST /subscription/repo1/item123 HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb
	
	{
		"planid": "a0a1a2a3a4a5a6a7a8a9aaabacad"
	}
输出样例：
        
	null

### DELETE /subscription/:repname/:itemname (43) (将废除，将被46取代)

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

### GET /subscription_stat/:repname/:itemname (44)

说明

	【任意】返回该DataItem的订阅量

输入参数说明：
	
	无

输入样例：

	POST /subscription_stat/repo1/item123 HTTP/1.1 
	Accept: application/json

输出样例：

	"numsubs":567

### GET /subscription_stat/:repname (45)

说明

	【任意】返回该repositories的订阅量

输入参数说明：
	
	无

输入样例：

	POST /subscription_stat/repo1 HTTP/1.1 
	Accept: application/json

输出样例：

	"numsubs":567

### PUT /subscription/:subid?action=[cancel|remove|flag] (46)

说明

	【需求者】取消订阅cancel
	【提供者】投诉订阅flag
	【管理员】取消订阅remove

输入参数说明：
	
	无

输入样例：

	PUT /subscription/1234567 HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb

输出样例：
        
	null


