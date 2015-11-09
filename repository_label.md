# API 列表

- [GET] /label/repositories

- [GET] /label/dataitem
	
- [GET] [POST] [DELETE] [PUT] /label/:repname/:itemname

- [GET] [POST] [DELETE] [PUT] /label/:repname


----------

## 根据label查询符合条件的repo
	
	[GET]	/label/repositories

说明
	
	根据label查询符合条件的repo

输入参数说明：

	label.sys.supply_style=1
	
Example Request：

	GET /label/repositories?label.opt.color=#000000 HTTP/1.1 
	
Example Response：
	
	HTTP/1.1 200 
	Vary: Accept 
	Content-Type: application/json
	
	[
		{"msg":""}
	]

Status Codes：

	200 OK
	400 Errors (invalid json, missing or invalid fields, etc) 
	401 Unauthorized

返回数据说明：

	msg：可选，具体出错信息描述

## 根据label条件查询符合条件的dataitem
	
	[GET]	/label/dataitem

说明
	
	根据label查询符合条件的dataitem

输入参数说明：

	label.sys.supply_style=1
	
Example Request：

	POST /label/dataitem?label.sys.supply_style=1 HTTP/1.1 

	
Example Response：
	
	HTTP/1.1 200 
	Vary: Accept 
	Content-Type: application/json
	
	[
		{"msg":""}
	]

Status Codes：

	200 OK
	400 Errors (invalid json, missing or invalid fields, etc) 
	401 Unauthorized

返回数据说明：

	msg：可选，具体出错信息描述

## 为repname下的itemname添加label
	
	[POST] 	/label/:repname/:itemname

说明
	
	为repname下的itemname添加label

输入参数说明：

	repname：数据仓库名字
	itemname：数据项名字
	
Example Request：

	POST /label/chinamobile/beijingphone HTTP/1.1 
	[
		"label": {
	          "sys": {
	                   "supply_style": 1
	                 },
	          "opt": {},
	          "owner": {},
	          "other": {}
	          }
	]
	
Example Response：
	
	HTTP/1.1 200 
	Vary: Accept 
	Content-Type: application/json
	
	[
		{"msg":""}
	]

Status Codes：

	200 OK
	400 Errors (invalid json, missing or invalid fields, etc) 
	401 Unauthorized

返回数据说明：

	msg：可选，具体出错信息描述


## 为repname下的itemname删除label
	
	[DELETE]/label/:repname/:itemname

说明
	
	为repname下的itemname删除label

输入参数说明：

	repname：数据仓库名字
	itemname：数据项名字

	"label": {
          "sys": {
                   "supply_style": 1
                 },
          "opt": {},
          "owner": {},
          "other": {}
    	}
	
Example Request：

	[DELETE] /label/chinamobile/beijingphone HTTP/1.1 

	
Example Response：
	
	HTTP/1.1 200 
	Vary: Accept 
	Content-Type: application/json
	
	[
		{"msg":""}
	]

Status Codes：

	200 OK
	400 Errors (invalid json, missing or invalid fields, etc) 
	401 Unauthorized

返回数据说明：

	msg：可选，具体出错信息描述

## 为repname下的itemname更新label
	
	[PUT]	/label/:repname/:itemname

说明
	
	为repname下的itemname更新label

输入参数说明：

	repname：数据仓库名字
	itemname：数据项名字
	"label": {
          "sys": {
                   "supply_style": 1
                 },
          "opt": {},
          "owner": {},
          "other": {}
          }
	
Example Request：

	[PUT] /label/chinamobile/beijingphone HTTP/1.1 
	[
		"label": {
	          "sys": {
	                   "supply_style": 1
	                 },
	          "opt": {},
	          "owner": {},
	          "other": {}
	          }
	]
	
Example Response：
	
	HTTP/1.1 200 
	Vary: Accept 
	Content-Type: application/json
	
	[
		{"msg":""}
	]

Status Codes：

	200 OK
	400 Errors (invalid json, missing or invalid fields, etc) 
	401 Unauthorized

返回数据说明：

	msg：可选，具体出错信息描述

## 查询repname下的itemname的label
	
	[GET]	/label/:repname/:itemname

说明
	
	查询repname下的itemnamee的label

输入参数说明：

	repname：数据仓库名字
	itemname：数据项名字
	
Example Request：

	[GET] /label/chinamobile/beijingphone HTTP/1.1 
	
Example Response：
	
	HTTP/1.1 200 
	Vary: Accept 
	Content-Type: application/json
	
	[
		{"msg":""}
	]

Status Codes：

	200 OK
	400 Errors (invalid json, missing or invalid fields, etc) 
	401 Unauthorized

返回数据说明：

	msg：可选，具体出错信息描述


## 为repname添加label
	
	[POST] 	/label/:repname

说明
	
	为repname添加label

输入参数说明：

	repname：数据仓库名字
	
Example Request：

	POST /label/chinamobile HTTP/1.1 
	[
		"label": {
	          "sys": {
	                   "supply_style": 1
	                 },
	          "opt": {},
	          "owner": {},
	          "other": {}
	          }
	]
	
Example Response：
	
	HTTP/1.1 200 
	Vary: Accept 
	Content-Type: application/json
	
	[
		{"msg":""}
	]

Status Codes：

	200 OK
	400 Errors (invalid json, missing or invalid fields, etc) 
	401 Unauthorized

返回数据说明：

	msg：可选，具体出错信息描述


## 为repname删除label
	
	[DELETE] /label/:repname

说明
	
	为repname删除label

输入参数说明：

	repname：数据仓库名字
	
Example Request：

	DELETE /label/repname HTTP/1.1 

	
Example Response：
	
	HTTP/1.1 200 
	Vary: Accept 
	Content-Type: application/json
	
	[
		{"msg":""}
	]

Status Codes：

	200 OK
	400 Errors (invalid json, missing or invalid fields, etc) 
	401 Unauthorized

返回数据说明：

	msg：可选，具体出错信息描述

## 为repname更新label
	
	[PUT]	/label/:repname

说明
	
	为repname更新label

输入参数说明：

	repname：数据仓库名字
	"label": {
	          "sys": {
	                   "supply_style": 1
	                 },
	          "opt": {},
	          "owner": {},
	          "other": {}
	          }
	
Example Request：

	[PUT] /label/rep1 HTTP/1.1 
	[
		"label": {
	          "sys": {
	                   "supply_style": 1
	                 },
	          "opt": {},
	          "owner": {},
	          "other": {}
	          }
	]
	
Example Response：
	
	HTTP/1.1 200 
	Vary: Accept 
	Content-Type: application/json
	
	[
		{"msg":""}
	]

Status Codes：

	200 OK
	400 Errors (invalid json, missing or invalid fields, etc) 
	401 Unauthorized

返回数据说明：

	msg：可选，具体出错信息描述

## 查询某repname下label
	
	[GET]	/label/:repname

说明
	
	查询repname下的label

输入参数说明：

	repname：数据仓库名字
	
Example Request：

	[GET] /label/rep1 HTTP/1.1 
	
Example Response：
	
	HTTP/1.1 200 
	Vary: Accept 
	Content-Type: application/json
	
	[
		{"msg":""}
	]

Status Codes：

	200 OK
	400 Errors (invalid json, missing or invalid fields, etc) 
	401 Unauthorized

返回数据说明：

	msg：可选，具体出错信息描述


