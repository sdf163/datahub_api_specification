# 订阅

### GET /subscriptions (40)

说明

	取得当前用户的订阅列表

输入参数说明：
	
	无

输入样例：

	GET /subscriptions HTTP/1.1 
	Accept: application/json
	Authorization: Basic akmklmasadalkm==

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

### GET /subscription/:repname/:itemname (41)

说明

	查询当前用户是否已经订阅某个dataitem

输入参数说明：
	
	无

输入样例：

	GET /subscription/repo1/item123 HTTP/1.1 
	Accept: application/json
	Authorization: Basic akmklmasadalkm==

输出样例：

	"subscribed":true

### POST /subscription/:repname/:itemname (42)

说明

	当前用户创建一个订阅

输入参数说明：
	
	无

输入样例：

	POST /subscription/repo1/item123 HTTP/1.1 
	Accept: application/json
	Authorization: Basic akmklmasadalkm==

输出样例：
        
	"succeeded":true

### DELETE /subscription/:repname/:itemname (43)

说明

	当前用户删除一个订阅

输入参数说明：
	
	无

输入样例：

	DELETE /subscription/repo1/item123 HTTP/1.1 
	Accept: application/json
	Authorization: Basic akmklmasadalkm==

输出样例：
        
	"succeeded":true

### GET /subscription_stat/:repname/:itemname (44)

说明

	查询一个dataitem的订阅数

输入参数说明：
	
	无

输入样例：

	POST /subscription_stat/repo1/item123 HTTP/1.1 
	Accept: application/json
	Authorization: Basic akmklmasadalkm==

输出样例：

	"numsubs":567

### GET /subscription_stat/:repname (45)

说明

	询一个respository下的dataitems的总订阅数

输入参数说明：
	
	无

输入样例：

	POST /subscription_stat/repo1 HTTP/1.1 
	Accept: application/json
	Authorization: Basic akmklmasadalkm==

输出样例：

	"numsubs":567





