# 订阅

### POST /subscription/:repname/:itemname (41)

说明
	当前用户创建一个订阅

输入参数说明：
	
	无

Example Request：

	GET /subscription/repo1/item123 HTTP/1.1 
	Accept: application/json
	Authorization: Basic akmklmasadalkm==

Example Response：

	[
	    {
	        "repname": "myrep",
	        "repaccesstype": "private",
	        "items": []
	    },
	    {
	        "repname": "myrep2",
	        "repaccesstype": "private",
	        "items": []
	    },
	    {
	        "msg": ""
	    }
	]


返回状态码：

	200 OK
	400 Errors (invalid json, missing or invalid fields, etc) 
	401 Unauthorized

返回数据说明：

	repname：数据仓库的名字
	repaccesstype：数据仓库的访问类型
	items：数据仓库中包含的数据项
	msg：可选，具体出错信息描述

返回值示例1
        
	{
		"error":"",
		"succeeded":true
	}

返回值示例2
        
	{
		"error":"already subscribed"
	}

### 当前用户取消订阅 (41)

> DELETE /subscription/:repname/:itemname

输入参数

* USER-NAME in header

输出样例

```
{"error":"","succeeded":true}
```

### 查询当前用户是否已经订阅某个dataitem (41)

> GET /subscription/:repname/:itemname

输入参数

* USER-NAME in header
optime
输出样例

```
{"error":"","subscribed":true}
```

### 取得当前用户的订阅列表 (42)

> GET /subscriptions

输入参数

* USER-NAME in header

输出样例

```
{
	"error":"",
	"subscriptions":[
		{
			"subscription_id":1,
			"username":"John", 
			"repname":"NBA",
			"itemname":"bear",
			"optime":"2015-11-08"
		}
		{
			"subscription_id":2,
			"username":"Zhang3", 
			"repname":"CBA",
			"itemname":"triger",
			"optime":"2015-11-08"
		}
	]
}
```

### 查询一个dataitem的订阅数 (51)

> GET /subscription_stat/:repname/:itemname

输入参数

> 无

输出样例

```
```

### 查询一个respository下的dataitems的总订阅数 (52)

> GET /subscription_stat/:repname

输入参数optime

> 无

输出样例

```
```

