# Transactions

### POST /transaction/:repname/:itemname/:tag (50)

说明

	【需求者】返回该请求的access token
	
	注意：tag需要UTF8编码，注意后面没有s

输入参数说明：
	
	无

输入样例：

	POST /transaction/repo1/item123/tag2 HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb

输出样例：

	"accesstoken":"a1a2a3a4a5a6a7a8"
	"remainingtime":"72h3m0.5s"
	"entrypoint":"http://www.exaple.com:5678"

### GET /transaction/:repname/:itemname/:tag?cypt_accesstoken={cypt_accesstoken}&username={username} (51)

说明

	【拥有者】校验该access_token的有效性，此access_token被需求者的私有证书加密
	注意：本组api接口只有这个不需要验证用户身份。
	注意：tag需要UTF8编码

输入参数说明：
	
	accesstoken: 需求者的access token
	username: 需求者用户名

样例输入：

	GET /transaction/repo1/item123/tag2 HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb

样例输出：
        
	"valid":true
	"remainingtime":"33h3m0.5s"

返回数据说明：

	valid: 输入access token是否有效
	remainingtime: 剩余有效期。可能的结果："33h3m0.5s", "3m2s", "0"

### GET /transaction_stat/:repname/:itemname (52)

说明

	【任意】返回该DataItem的pull量

输入参数说明：
	
	无

输入样例：

	POST /transaction_stat/repo1/item123 HTTP/1.1 
	Accept: application/json

输出样例：

	"numpulls":567
	
### GET /transaction_stat/:repname (53)

说明

	【任意】返回该repositories的pull量

输入参数说明：
	
	无

输入样例：

	POST /transaction_stat/repo1 HTTP/1.1 
	Accept: application/json

输入样例：

	"numpulls":567

### GET /transaction_stat/:repname/:itemname/:tag (54)

说明

	【任意】返回该tag的pull量

输入参数说明：
	
	无

输入样例：

	POST /transaction_stat/repo1/item123/tag3 HTTP/1.1 
	Accept: application/json

输出样例：

	"numpulls":567

### GET /transactions/pull?groupbydate=[0|1]  (55)

说明

	【需求者】返回该用户所有的pull的信息

输入参数说明：
	
	无

输入样例：

	GET /transactions/pull?groupbydate=1 HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb

输出样例(groupbydate=1)：

	[
		{
			"date":"2015-11-18",
			"pulls":[
				{
					"sellername":"li4",
					"repname":"repo001",
					"itemname":"item002",
					"tag":"tag008",
					"pulltime":"2015-11-18T11:48:07Z"
				},
				{
					"sellername":"li4",
					"repname":"repo001",
					"itemname":"item002",
					"tag":"tag008",
					"pulltime":"2015-11-18T11:29:38Z"
				},
				{
					"sellername":"li4",
					"repname":"repo001",
					"itemname":"item002",
					"tag":"tag008",
					"pulltime":"2015-11-18T11:29:31Z"
				}
			]
		},
		{
			"date":"2015-11-10",
			"pulls":[
				{
					"sellername":"li4",
					"repname":"repo001",
					"itemname":"item002",
					"tag":"tag008",
					"pulltime":"2015-11-10T10:10:10Z"
				}
			]
		}
	]

输出样例(groupbydate=0)：
        
	[
		{
			"sellername": "Li4",
			"repname": "repo1231",
			"itemname": "item9883",
			"tag": "tag8W",
			"pulltime": "2015-11-10T15:04:05Z07:00"
		},
		{
			"sellername": "Li4",
			"repname": "repo121",
			"itemname": "item989",
			"tag": "tag09",
			"pulltime": "2015-11-10T15:04:05Z07:00"
		}
	]
	
	

返回数据说明：

	sellername: 提供者用户名
	repname: repository name
	itemname: data item name
	tag: tag名
	pulltime: pull time, RFC3339 format

### GET /transactions/pull/:repname/:itemname?groupbydate=[0|1]  (56)

说明

	【需求者】返回该用户pull的该DataItem上的tags

输入参数说明：
	
	无

输入样例：

	GET /transactions/pull/repo03/item56 HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb

输出样例：
        
	[
		{
			"tag": "tag8W",
			"pulltime": "2015-11-09T15:04:05Z07:00"
		},
		{
			"tag": "tag09",
			"pulltime": "2015-11-10T15:04:05Z07:00"
		}
	]

返回数据说明：

	tag: tag名
	pulltime: pull time, RFC3339 format

### GET /transactions/push?groupbydate=[0|1]  (57)

说明

	【拥有者】返回该用户所有的被人家Pull的信息

输入参数说明：
	
	无

输入样例：

	GET /transactions/push?groupbydate=1 HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb

输出样例(groupbydate=1)：

[
		{
			"date":"2015-11-18",
			"pulls":[
				{
					"buyername":"zhang3",
					"repname":"repo001",
					"itemname":"item002",
					"tag":"tag008",
					"pulltime":"2015-11-18T11:48:07Z"
				},
				{
					"buyername":"John",
					"repname":"repo001",
					"itemname":"item002",
					"tag":"tag008",
					"pulltime":"2015-11-18T11:29:38Z"
				}
			]
		},
		{
			"date":"2015-11-10",
			"pulls":[
				{
					"buyername":"zhang3",
					"repname":"repo001",
					"itemname":"item002",
					"tag":"tag008",
					"pulltime":"2015-11-10T10:10:10Z"
				},
				{
					"buyername":"zhang3",
					"repname":"repo001",
					"itemname":"item002",
					"tag":"tag008",
					"pulltime":"2015-11-10T10:10:10Z"
				},
			]
		}
	]

输出样例(groupbydate=0)：
        
	[
		{
			"buyername": "Li4",
			"repname": "repo1231",
			"itemname": "item9883",
			"tag": "tag8W",
			"pulltime": "2015-11-10T15:04:05Z07:00"
		},
		{
			"buyername": "Smith",
			"repname": "repo121",
			"itemname": "item989",
			"tag": "tag09",
			"pulltime": "2015-11-10T15:04:05Z07:00"
		}
	]

返回数据说明：

	buyername: 需求者用户名
	repname: repository name
	itemname: data item name
	tag: tag名
	pulltime: pull time, RFC3339 format

### GET /transactions/push/:repname/:itemname?groupbydate=[0|1]  (58)

说明

	【需求者】返回该用户用有的该DataItem被人家Pull的信息。

输入参数说明：
	
	无

输入样例：

	GET /transactions/push/repo03/item56?groupbydate=1 HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb

输出样例(groupbydate=1)：

	[
		{
			"date":"2015-11-10",
			"pulls"[
				{
					"buyername": "Li4",
					"tag": "tag8W",
					"pulltime": "2015-11-10T15:04:05Z07:00"
				},
				{
					"buyername": "Zhang3",
					"tag": "tag09",
					"pulltime": "2015-11-10T10:09:05Z07:00"
				}
			]
		},
		{
			"date":"2015-11-03",
			"pulls"[
				{
					"buyername": "Zhang3",
					"tag": "tag09",
					"pulltime": "2015-11-03T15:06:05Z07:00"
				}
			]
		}
	]

输出样例(groupbydate=0)：
        
	[
		{
			"buyername": "Li4",
			"tag": "tag8W",
			"pulltime": "2015-11-10T15:04:05Z07:00"
		},
		{
			"buyername": "Zhang3",
			"tag": "tag09",
			"pulltime": "2015-11-10T15:09:05Z07:00"
		},
		{
			"buyername": "Zhang3",
			"tag": "tag09",
			"pulltime": "2015-11-03T15:06:05Z07:00"
		}
	]
	
	

返回数据说明：

	buyername: 需求者用户名
	tag: tag名
	pulltime: pull time, RFC3339 format
	
