# 订阅

### POST /subscription/:repname/:itemname (41)

说明

	当前用户创建一个订阅

输入参数说明：
	
	无

Example Request：

	POST /subscription/repo1/item123 HTTP/1.1 
	Accept: application/json
	Authorization: Basic akmklmasadalkm==

Example Response 1：
        
	{
		"error":"",
		"succeeded":true
	}

Example Response 2：
        
	{
		"error":"already subscribed"
	}


返回状态码：

	200 OK
	400 Errors (invalid json, missing or invalid fields, etc) 
	401 Unauthorized

返回数据说明：

	error：出错信息，空表示没出错
	succeeded：可选，成功与否

### DELETE /subscription/:repname/:itemname (41)

说明

	当前用户删除一个订阅

输入参数说明：
	
	无

Example Request：

	DELETE /subscription/repo1/item123 HTTP/1.1 
	Accept: application/json
	Authorization: Basic akmklmasadalkm==

Example Response：
        
	{
		"error":"",
		"succeeded":true
	}


返回状态码：

	200 OK
	400 Errors (invalid json, missing or invalid fields, etc) 
	401 Unauthorized

返回数据说明：

	error：出错信息，空表示没出错
	succeeded：可选，成功与否

### GET /subscription/:repname/:itemname (41)

说明

	查询当前用户是否已经订阅某个dataitem

输入参数说明：
	
	无

Example Request：

	GET /subscription/repo1/item123 HTTP/1.1 
	Accept: application/json
	Authorization: Basic akmklmasadalkm==

Example Response 1：
        
	{
		"error":"",
		"subscribed":true
	}


返回状态码：

	200 OK
	400 Errors (invalid json, missing or invalid fields, etc) 
	401 Unauthorized

返回数据说明：

	error：出错信息，空表示没出错
	succeeded：可选，是否已经订阅

### GET /subscriptions (42)

说明

	取得当前用户的订阅列表

输入参数说明：
	
	无

Example Request：

	GET /subscriptions HTTP/1.1 
	Accept: application/json
	Authorization: Basic akmklmasadalkm==

Example Response：
        
	{
		"error":"",
		"subscriptions":
		[
			{
				"subscription_id":1,
				"username":"John", 
				"repname":"NBA",
				"itemname":"bear",
				"optime":"2015-11-08"
			},
			{
				"subscription_id":2,
				"username":"Zhang3", 
				"repname":"CBA",
				"itemname":"triger",
				"optime":"2015-11-08"
			}
		]
	}


返回状态码：

	200 OK
	400 Errors (invalid json, missing or invalid fields, etc) 
	401 Unauthorized

返回数据说明：

	error：出错信息，空表示没出错
	subscriptions：可选， 订阅列表
		subscription_id: 订阅id
		username: 订阅者
		repname: repository name
		itemname: data item name
		optime: 订阅时间


### GET /subscription_stat/:repname/:itemname (51)

说明

	查询一个dataitem的订阅数

输入参数说明：
	
	无

Example Request：

	POST /subscription_stat/repo1/item123 HTTP/1.1 
	Accept: application/json
	Authorization: Basic akmklmasadalkm==

Example Response 1：
        
	{
		"error":"",
		"num_subs":567
	}


返回状态码：

	200 OK
	400 Errors (invalid json, missing or invalid fields, etc) 

返回数据说明：

	error：出错信息，空表示没出错
	num_subs：可选，订阅数


### GET /subscription_stat/:repname (5)

说明

	询一个respository下的dataitems的总订阅数

输入参数说明：
	
	无

Example Request：

	POST /subscription_stat/repo1 HTTP/1.1 
	Accept: application/json
	Authorization: Basic akmklmasadalkm==

Example Response 1：
        
	{
		"error":"",
		"num_subs":567
	}


返回状态码：

	200 OK
	400 Errors (invalid json, missing or invalid fields, etc) 

返回数据说明：

	error：出错信息，空表示没出错
	num_subs：可选，订阅数





