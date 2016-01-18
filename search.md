# API 列表
	

- [GET] /search

----------

## 1 指令：GET /search

说明

	【任意】搜索item

输入参数说明：
	
	page (分页页数) : 			1 - N，  默认=1（page=1可以不传）
	size（页面大小）: 			1 - N，  默认=6 (-1 返回全部)
    text :                      搜索关键字
Example Request：

	GET /search?text=中国移动?page=5&size=8 HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb

返回数据说明：
	
	repnam: 数据仓库的名字
	itemname: dataitem名字 
	
返回值示例
        
	[
		{
			"repname": "mobile",
			"itemname": "tele1",
		}，
		{
			"repname": "mobile",
			"itemname": "tele2",
		},
		{
			"repname": "mobile",
			 "itemname": "tele3",
		}
	]

----------


