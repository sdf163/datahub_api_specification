# API 列表
	
	
- [GET] [DELETE] [PUT] /permission/:repname

- [GET] [DELETE] [PUT] /permission/:repname/:itemname

	
----------

##  1 指令：GET /permission/:repname

说明

	【rep拥有者】查询自己rep白名单的username列表，及相应的读写权限

输入参数说明：
	
	无

Example Request：

	GET /permission/rep HTTP/1.1 
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb

Example Response：
	
	[
		{"username":"user1", "opt_permission": 1},
		{"username":"user2", "opt_permission": 1},
		{"username":"user3", "opt_permission": 0}
	]

返回数据说明：

	username					rep白名单用户名
	opt_permission				rep白名单用户所具有的权限[0:读,1:写]

----------

## 2 指令：PUT /permission/:repname
	
说明：
	
	【rep拥有者】将某用户（非自己）加入或更新rep白名单中

输入参数说明：

	username 		被加入白名单的用户名
	opt_permission	默认不传（只有读权限），传1具有写
	
Example Request：

	PUT /permission/rep00001 HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb
	[
		{"username":"user1","opt_permission":1}
	]

返回数据说明：
	
	无
		
## 3 指令：DELETE /permission/:repname
	
说明：
	
	【rep拥有者】将某些用户（非自己）从rep白名单中删除

输入参数说明：

	username 		被从白名单删除的用户名,可以传多个username
	delall          是否删除所有白名单用户[delall=1 删除所有]
   
Example Request：

	DELETE /permission/rep00001?username=nike&username=peter HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb
	
	DELETE /permission/rep00001?delall=1 HTTP/1.1 
    Accept: application/json
    Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb
	
## 4 指令：GET /permission/:repname/:itemname

说明

	【item拥有者】查询自己item白名单中username列表

输入参数说明：
	

Example Request：

	GET /permission/repname1/itemname1 HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb
    

返回数据说明：
	[
		{"username":"user1"},
		{"username":"user2"},
		{"username":"user3"}
	]
	
----------

## 5 指令：PUT /permission/:repname/:itemname
	
说明：
	
	【item拥有者】将某用户（非自己）加入item白名单中

输入参数说明：

	username 		被加入白名单的用户名
	
Example Request：

	POST /permission/repname1/itemname1 HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb
	[
	    {"username":"user1"}
	]

返回数据说明：
	
	无

## 6 指令：DELETE /permission/:repname/:itemname
	
说明：
	
	【item拥有者】将某些用户（非自己）从item白名单中移除

输入参数说明：

	username 		被从白名单删除的用户名
	delall          是否删除所有白名单用户[delall=1 删除所有]
   
Example Request：

	DELETE /permission/repname1/itemname1?username=abc HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb
    
    DELETE /permission/repname1/itemname1?delall=1 HTTP/1.1 
    Accept: application/json
    Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb