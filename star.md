# Star APIs

### GET /star/:repname/:itemname

说明

	【需求者】查询该DataItem是否star过

输入参数说明：
	
	无

输入样例：

	GET /star/repo1/item123 HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb

输出样例：

	"subscribed":true

### POST /star/:repname/:itemname

说明

	【需求者】star该DataItem 

输入参数说明：
	
	无

输入样例：

	POST /star/repo1/item123 HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb

输出样例：
        
	null

### DELETE /star/:repname/:itemname

说明

	【需求者】取消star该DataItem

输入参数说明：
	
	无

输入样例：

	DELETE /star/repo1/item123 HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb

输出样例：
        
	null

### GET /star_stat/:repname/:itemname (44)

说明

	【任意】返回该DataItem的star量

输入参数说明：
	
	无

输入样例：

	POST /star_stat/repo1/item123 HTTP/1.1 
	Accept: application/json

输出样例：

	"numstars":567
