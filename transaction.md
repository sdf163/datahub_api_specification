
### POST /transaction/:repname/:itemname/:tag (61)

说明

	需求者请求一个pull token

输入参数说明：
	
	无

Example Request：

	POST /transaction/repo1/item123/tag2 HTTP/1.1 
	Accept: application/json
	Authorization: Basic akmklmasadalkm==

Example Response 1：
        
	{
		"error":"",
		"token":"a1a2a3a4a5a6a7a8"
	}


返回状态码：

	200 OK
	400 Errors (invalid json, missing or invalid fields, etc) 

返回数据说明：

	error：出错信息，空表示没出错
	token：可选，pull token


### GET /transaction/:repname/:itemname/:tag?token=a1a2a3a4a5a6a7a8 (62)

说明

	供应者验证一个pull token

输入参数说明：
	
	token: 需求者发送给数据提供者的access token

Example Request：

	GET /transaction/repo1/item123/tag2 HTTP/1.1 
	Accept: application/json
	Authorization: Basic akmklmasadalkm==

Example Response 1：
        
	{
		"error":"",
		"valid":true
	}


返回状态码：

	200 OK
	400 Errors (invalid json, missing or invalid fields, etc) 
	401 Unauthorized

返回数据说明：

	error：出错信息，空表示没出错.
	valid：可选，输入token的有效性

### GET /transactions/buyer (71)

说明

	查询当前用户作为一个需求者的流水

输入参数说明：
	
	无

Example Request：

	GET /transactions/buyer HTTP/1.1 
	Accept: application/json
	Authorization: Basic akmklmasadalkm==

Example Response 1：
        
	{
		"error":"",
		"transactions":
		[
			{
				"transactionid":123,
				"buyername": "Zhang3",
				"sellername": "Li4",
				"repname": "repo1231",
				"itemname": item9883,
				"tag": "tag8W",
				"pulltime": "2015-11-09",
				"pulltimes": 2,
				"paymentid": 0,
			},
			{
				"transactionid":111,
				"buyername": "John",
				"sellername": "Smith",
				"repname": "repo121",
				"itemname": item989,
				"tag": "tag09",
				"pulltime": "2015-11-09",
				"pulltimes": 0,
				"paymentid": 0,
			}
		]
	}


返回状态码：

	200 OK
	400 Errors (invalid json, missing or invalid fields, etc) 
	401 Unauthorized

返回数据说明：

	error：出错信息，空表示没出错.
	transactions：可选，流水列表
		transactionid: 流水id
		buyername: 需求者用户名
		sellername: 提供者用户名
		repname: repository name
		itemname: data item name
		tag: tag名
		pulltime: 最近一次pull时间
		pulltimes: pull次数

### GET /transaction_stat/:repname/:itemname/:tag (41)

说明

	查询一个dataitem tag上的pull次数

输入参数说明：
	
	无

Example Request：

	POST /transaction_stat/repo1/item123/tag3 HTTP/1.1 
	Accept: application/json
	Authorization: Basic akmklmasadalkm==

Example Response 1：
        
	{
		"error":"",
		"num_pulls":567
	}


返回状态码：

	200 OK
	400 Errors (invalid json, missing or invalid fields, etc) 

返回数据说明：

	error：出错信息，空表示没出错
	num_pulls：可选，pull次数

### GET /transaction_stat/:repname/:itemname (41)

说明

	查询一个dataitem下的tags上的总pull次数

输入参数说明：
	
	无

Example Request：

	POST /transaction_stat/repo1/item123 HTTP/1.1 
	Accept: application/json
	Authorization: Basic akmklmasadalkm==

Example Response 1：
        
	{
		"error":"",
		"num_pulls":567
	}


返回状态码：

	200 OK
	400 Errors (invalid json, missing or invalid fields, etc) 

返回数据说明：

	error：出错信息，空表示没出错
	num_pulls：可选，pull次数

### GET /transaction_stat/:repname (41)

说明

	查询一个repository下的tags上的总pull次数

输入参数说明：
	
	无

Example Request：

	POST /transaction_stat/repo1 HTTP/1.1 
	Accept: application/json
	Authorization: Basic akmklmasadalkm==

Example Response 1：
        
	{
		"error":"",
		"num_pulls":567
	}


返回状态码：

	200 OK
	400 Errors (invalid json, missing or invalid fields, etc) 

返回数据说明：

	error：出错信息，空表示没出错
	num_pulls：可选，pull次数







