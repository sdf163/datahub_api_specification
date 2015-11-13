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

### GET /transactions/pull  (55)

说明

	【需求者】返回该用户所有的pull的信息

输入参数说明：
	
	无

输入样例：

	GET /transactions/pull HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb

输出样例：
        
	[
		{
			"sellername": "Li4",
			"repname": "repo1231",
			"itemname": item9883,
			"tag": "tag8W",
			"pulltime": "2015-11-09",
			"pulltimes": 2
		},
		{
			"sellername": "Li4",
			"repname": "repo121",
			"itemname": item989,
			"tag": "tag09",
			"pulltime": "2015-11-09",
			"pulltimes": 0
		}
	]

返回数据说明：

	sellername: 提供者用户名
	repname: repository name
	itemname: data item name
	tag: tag名
	pulltime: 最近一次pull时间
	pulltimes: pull次数

### GET /transactions/pull/:repname/:itemname  (56)

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
			"pulltime": "2015-11-09",
			"pulltimes": 2
		},
		{
			"tag": "tag09",
			"pulltime": "2015-11-09",
			"pulltimes": 0
		}
	]

返回数据说明：

	tag: tag名
	pulltime: 最近一次pull时间
	pulltimes: pull次数

### GET /transactions/push  (57)

说明

	【拥有者】返回该用户所有的被人家Pull的信息

输入参数说明：
	
	无

输入样例：

	GET /transactions/push HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb

输出样例：
        
	[
		{
			"buyername": "Li4",
			"repname": "repo1231",
			"itemname": item9883,
			"tag": "tag8W",
			"pulltime": "2015-11-09",
			"pulltimes": 2
		},
		{
			"buyername": "Smith",
			"repname": "repo121",
			"itemname": item989,
			"tag": "tag09",
			"pulltime": "2015-11-09",
			"pulltimes": 0
		}
	]

返回数据说明：

	buyername: 需求者用户名
	repname: repository name
	itemname: data item name
	tag: tag名
	pulltime: 最近一次pull时间
	pulltimes: pull次数

### GET /transactions/push/:repname/:itemname  (58)

说明

	【需求者】返回该用户用有的该DataItem被人家Pull的信息。

输入参数说明：
	
	无

输入样例：

	GET /transactions/push/repo03/item56 HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb

输出样例：
        
	[
		{
			"buyername": "Li4",
			"tag": "tag8W",
			"pulltime": "2015-11-09",
			"pulltimes": 2
		},
		{
			"buyername": "Zhang3",
			"tag": "tag09",
			"pulltime": "2015-11-09",
			"pulltimes": 0
		}
	]

返回数据说明：

	buyername: 需求者用户名
	tag: tag名
	pulltime: 最近一次pull时间
	pulltimes: pull次数
