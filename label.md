# API 列表
	
- [GET] [POST] [DELETE] [PUT] /label/:repname/:itemname

- [GET] [POST] [DELETE] [PUT] /label/:repname


----------


## 为repname下的itemname添加label
	
	[POST] 	/label/:repname/:itemname

说明
	
	为repname下的itemname添加label

输入参数说明：

	label 为json Object
	
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
	

## 为repname下的itemname删除label
	
	[DELETE]/label/:repname/:itemname

说明
	
	为repname下的itemname删除label

输入参数说明：

	label 为json Object
	
Example Request：

	[DELETE] /label/chinamobile/beijingphone HTTP/1.1 
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
	

## 为repname下的itemname更新label
	
	[PUT]	/label/:repname/:itemname

说明
	
	为repname下的itemname更新label

输入参数说明：

	label 为json Object
	
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
	

## 查询repname下的itemname的label
	
	[GET]	/label/:repname/:itemname

说明
	
	查询repname下的itemnamee的label信息

输入参数说明：
	
	无
	
Example Request：

	[GET] /label/chinamobile/beijingphone HTTP/1.1 
	
Example Response：
	
	HTTP/1.1 200 
	Vary: Accept 
	Content-Type: application/json
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


## 为repname添加label
	
	[POST] 	/label/:repname

说明
	
	为repname添加label

输入参数说明：

	无
	
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
	

## 为repname删除label
	
	[DELETE] /label/:repname

说明
	
	为repname删除label


输入参数说明：

	label 为json Object
	
Example Request：

	[DELETE] /label/chinamobile HTTP/1.1 
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

Example Request：

	DELETE /label/repname HTTP/1.1 

	
Example Response：
	
	HTTP/1.1 200 
	Vary: Accept 
	Content-Type: application/json
	

## 为repname更新label
	
	[PUT]	/label/:repname

说明
	
	无

输入参数说明：

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
	

## 查询某repname下label
	
	[GET]	/label/:repname

说明
	
	查询repname下的label

输入参数说明：

	无
	
Example Request：

	[GET] /label/rep1 HTTP/1.1 
	
Example Response：
	
	HTTP/1.1 200 
	Vary: Accept 
	Content-Type: application/json
	
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
