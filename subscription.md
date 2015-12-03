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

### GET /subscriptions (40)

说明

	【需求者】查询所有订阅的DataItem

输入参数说明：
	
	无

输入样例：

	GET /subscriptions HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb

输出样例：
        
	[
		{
			"repname":"NBA",
			"itemname":"bear",
			"subtime":"2015-11-08"
		},
		{
			"repname":"CBA",
			"itemname":"triger",
			"subtime":"2015-11-08"
		}
	]

返回数据说明：

	repname: repository name
	itemname: data item name
	subtime: 订阅时间

### GET /subscriptions/:repname (46)

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

### GET /subscription/:repname/:itemname (41)

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
	
	无

输入样例：

	POST /subscription/repo1/item123 HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb

输出样例：
        
	null

### DELETE /subscription/:repname/:itemname (43)

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

