# API 列表
	
- [DELETE] [PUT] /repositories/:repname/:itemname/label

- [DELETE] [PUT] /repositories/:repname

----------

## [PUT] /repositories/:repname/:itemname/label
	
说明
	
	新增/更新dataitem的label的某条属性

输入参数说明：

	owner.xxx			xxx用户自定义属性。item的拥有者具有owner的操作权限
	other.yyy			yyy管理员自定义属性。管理员具有other的操作权限
	
Example Request：

	[PUT] /repositories/chinamobile/beijingphone/label HTTP/1.1 
	Content-Type：application/x-www-form-urlencoded
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb
	[
		owner.age=15
		owner.company="baidu.com"
		other.member="good"
	]

Example Response：
	
	HTTP/1.1 200 
	Vary: Accept 
	Content-Type: application/json
	
## [DELETE] /repositories/:repname/:itemname/label
	
说明
	
	删除dataitem的label的某条属性

输入参数说明：

	无
	
Example Request：

	[DELETE] /repositories/chinamobile/beijingphone/label HTTP/1.1 
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb
	
Example Response：
	
	HTTP/1.1 200 
	Vary: Accept 
	Content-Type: application/json
	
## [PUT] /repositories/:repname/label
	
说明
	
	新增/更新repository的label的某条属性

输入参数说明：

	owner.xxx			xxx用户自定义属性。item的拥有者具有owner的操作权限
	other.yyy			yyy管理员自定义属性。管理员具有other的操作权限
	
Example Request：

	[PUT] /repositories/repname1/label HTTP/1.1 
	Content-Type：application/x-www-form-urlencoded
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb
	[
		owner.age=15
		owner.company="baidu.com"
		other.member="good"
	]

Example Response：
	
	HTTP/1.1 200 
	Vary: Accept 
	Content-Type: application/json
	

## [DELETE] /repositories/:repname/:itemname/label
	
说明
	
	删除dataitem的label的某条属性

输入参数说明：

	无
	
Example Request：

	[DELETE] /repositories/repname1/label HTTP/1.1 
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb
	
Example Response：
	
	HTTP/1.1 200 
	Vary: Accept 
	Content-Type: application/json
	
