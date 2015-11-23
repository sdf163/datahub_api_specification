# Star APIs

### (A0) GET /star/:repname/:itemname

说明

	【用户】查询是否star某个DataItem

输入参数说明：
	
	无

输入样例：

	GET /star/repo1/item123 HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb

输出样例：

	"starred":true

### (A1) PUT /star/:repname/:itemname?star=[0|1]

说明

	【用户】更改对一个DataItem的star状态 

输入参数说明：
	
	star: 0表示unstar, 1表示star

输入样例：

	PUT /star/repo1/item123?star=1 HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb

输出样例：
        
	"starred":true

### (A2) GET /star_stat/:repname/:itemname

说明

	【任意】返回该DataItem的star量

输入参数说明：
	
	无

输入样例：

	GET /star_stat/repo1/item123 HTTP/1.1 
	Accept: application/json

输出样例：

	"numstars":567

### (A3) GET /star_stat/:repname

说明

	【任意】返回该Drepository的star量

输入参数说明：
	
	无

输入样例：

	GET /star_stat/repo1 HTTP/1.1 
	Accept: application/json

输出样例：

	"numstars":567

