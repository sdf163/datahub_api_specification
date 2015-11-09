# API 列表

[GET] /select_labels

[POST] [DELETE] /select_labels/:labelname

[POST] [PUT] [DELETE] [GET] /selects

----------

## 指令：[GET] /select_labels

说明
	
	【任意】返回精选栏目
		
Example Request：
	
	GET /select_labels HTTP/1.1 
	Accept: application/json
	
Example Response：
	
	[
	    {
	     	"labels":[]
	        "msg": ""
	    }
	]	

返回状态码：
	
	200 OK
	400 Errors (invalid json, missing or invalid fields, etc) 
	401 Unauthorized

返回数据说明：
	
	labels  数据精选栏目名称数组

返回值示例
	
	[
	    {
	     	"labels":["股市行情","终端信息","天气预报","医疗"]
	        "msg": ""
	    }
	]	
        
## 指令：[POST] /select_labels/:labelname

说明
	
	【管理员】创建精选栏目

输入参数说明：
	
	labelname 精选栏目条目名称
		
Example Request：
	
	POST /select_labels HTTP/1.1 
	Accept: application/json
	Authorization: Basic akmklmasadalkm==

Example Response：
	
	[
    	{
    	   "msg": ""
    	}
    ]	
    	
返回状态码：
	
	200 OK
	400 Errors (invalid json, missing or invalid fields, etc) 
	401 Unauthorized

返回数据说明：
	
	[
	    {
	        "msg": ""
	    }
	]	

## 指令：[DELETE] /select_labels/:labelname

说明

	【管理员】删除精选栏目
	
输入参数说明：
	
	labelname 精选栏目条目名称
		
Example Request：
	
	DELETE /select_labels HTTP/1.1 
	Accept: application/json
	Authorization: Basic akmklmasadalkm==

Example Response：
	
	[
	    {
	        "msg": ""
	    }
	]	
	
返回状态码：
	
	200 OK
	400 Errors (invalid json, missing or invalid fields, etc) 
	401 Unauthorized

返回数据说明：
	
	[
	    {
	        "msg": ""
	    }
	]	

## 指令：[GET] /selects

说明
	
	【任意】返回精选内容
		
Example Request：
	
	GET /selects HTTP/1.1 
	Accept: application/json

Example Response：

	[
	    {
	        "selects": [
	            {
	                "repname": "",
	                "itemname": ""
	            },
	            {
	                "repname": "",
	                "itemname": ""
	            },
	            {
	                "repname": "",
	                "itemname": ""
	            }
	        ],
	        "msg": ""
	    }
	]

返回状态码：
	
	200 OK
	400 Errors (invalid json, missing or invalid fields, etc) 
	401 Unauthorized

返回数据说明：
	
	selects： repname和itemname的数组

返回值示例
	
	[
	    {
	        "selects": [
	            {	
	                "repname": "上海",
	                "itemname": "上海终端"
	            },
	            {
	                "repname": "北京",
	                "itemname": "北京终端"
	            },
	            {
	                "repname": "深圳",
	                "itemname": "深圳终端"
	            }
	        ],
	        "msg": ""
	    }
	]

## 指令：[POST] /selects

说明
	
	【管理员】创建精选内容

输入参数说明：
	
	 repname[必选]: 		　
	 itemname[必选]: 
	 select_labels[必选]：　精选栏目项
		
Example Request：
	
	POST /selects HTTP/1.1 
	Accept: application/json
	Authorization: Basic akmklmasadalkm==

Example Response：

	[
	    {
	        "msg": ""
	    }
	]

返回状态码：
	
	200 OK
	400 Errors (invalid json, missing or invalid fields, etc) 
	401 Unauthorized

返回值示例
	
	[
	    {
	        "msg": ""
	    }
	]

## 指令：[PUT] /selects

说明

	【管理员】更新精选内容

输入参数说明：
	
	 repname[必选]: 		　
	 itemname[必选]: 
	 select_labels[必选]：　精选栏目项
		
Example Request：
	
	PUT /selects HTTP/1.1 
	Accept: application/json
	Authorization: Basic akmklmasadalkm==

Example Response：

	[
	    {
	        "msg": ""
	    }
	]

返回状态码：
	
	200 OK
	400 Errors (invalid json, missing or invalid fields, etc) 
	401 Unauthorized


返回值示例
	
	[
	    {
	        "msg": ""
	    }
	]
	
## 指令：[DELETE] /selects

说明

	【管理员】删除精选内容

输入参数说明：
	
	 repname[必选]: 		　
	 itemname[必选]: 
	 select_labels[必选]：　精选栏目项
		
Example Request：
	
	DELETE /selects HTTP/1.1 
	Accept: application/json
	Authorization: Basic akmklmasadalkm==

Example Response：

	[
	    {
	        "msg": ""
	    }
	]

返回状态码：
	
	200 OK
	400 Errors (invalid json, missing or invalid fields, etc) 
	401 Unauthorized

返回值示例
	
	[
	    {
	        "msg": ""
	    }
	]

