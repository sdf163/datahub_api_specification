# API 列表
	
	
- [GET] [POST] [DELETE] [PUT] /permit/:repname

- [GET] [POST] [DELETE] /permit/:repname/:itemname

	
----------

## 指令：GET /permit/:repname

说明

	【rep拥有者】查询自己rep白名单列表，及相应的读写权限

输入参数说明：
	
	无

Example Request：

	GET /permit/rep HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb


返回数据说明：
	[
		{"username":"user1", "write": 1},
		{"username":"user2", "write": 1},
		{"username":"user3"}
	]
	
----------

## 指令：POST PUT /permit/:repname
	
说明：
	
	【rep拥有者】将某用户（非自己）加入或更新rep白名单中

输入参数说明：

	username 		被加入白名单的用户名
	write			默认不传只有读权限，传1具有写
	
Example Request：

	POST /permit/rep00001 HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb
	[
		{"username":"user1","write":1}
	]

返回数据说明：
	
	无
		

## 指令：DELETE /permit/:repname
	
说明：
	
	【rep拥有者】将某用户（非自己）从rep白名单中删除

输入参数说明：

	username 		被从白名单删除的用户名
   
Example Request：

	DELETE /permit/rep00001 HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb

	
## 指令：GET /permit/:repname/:itemname

说明

	【item拥有者】查询自己item白名单中用户列表

输入参数说明：
	

Example Request：

	GET /permit/repname1/itemname1 HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb


返回数据说明：
	[
		{"username":"user1"},
		{"username":"user2"},
		{"username":"user3"}
	]
	
----------

## 指令：POST /permit/:repname/:itemname
	
说明：
	
	【item拥有者】将某用户（非自己）加入item白名单中

输入参数说明：

	username 		被加入白名单的用户名
	
Example Request：

	POST /permit/repname1/itemname1 HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb

返回数据说明：
	
	无

## 指令：DELETE /permit/:repname/:itemname
	
说明：
	
	【item拥有者】将某用户（非自己）从item白名单中移除

输入参数说明：

	username 		被从白名单删除的用户名
   
Example Request：

	DELETE /permit/repname1/itemname1 HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb