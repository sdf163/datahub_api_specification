# API 列表
	

- [GET] /repositories

- [GET] [POST] [DELETE] /repositories/:repname

- [GET] [POST] [DELETE] /repositories/:repname/:itemname

- [GET] [POST] [DELETE] /repositories/:repname/:itemname/:tag

	
----------

## 1 指令：GET /Repositories

说明

	【拥有者】
	 		如果后面没有username的参数,则返回本人创建或具备写权限的所有repository
	【任意】 
			如果带有参数?username=XXX，则表示查询XXX的所有repository，这里只能反馈查询者具备读权限的repositories名字（比如public或者在private白名单中的）

输入参数说明：
	
	page (分页页数) : 			1 - N，  默认=1（page=1可以不传）
	size（页面大小）: 			1 - N，  默认=6 (-1 返回全部)
	username: 					数据提供者username（header 中为登录用户的username）

Example Request：

	GET /repositories?page=5&size=8 HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb


返回数据说明：
	
	repname：数据仓库的名字
	
返回值示例
        
	[
		{
			"repname": "mobile"
		}，
		{
			"repname": "mobile"
		},
		{
			"repname": "mobile"
		}
	]

----------

## 2 指令：GET /Repositories/:repname
	
说明：
	
	【任意】查询repository详情

输入参数说明：

	items							查询repname的所有dataitem开关
	page (分页页数) : 			1 - N，  默认=1（page=1可以不传）
	size（页面大小）: 			1 - N，  默认=6 (-1 返回全部)
	
Example Request：

	GET /repositories/myrep1?items=1 HTTP/1.1 
	Accept: application/json

返回数据说明：
	
	create_user			创建者
   	itemaccesstype      对外开放类型[public(默认), private]
    comment 			详情
	optime				更新时间
	items				dataitem数量	
	label				标签
	dataitems			dataitem的名称集	
	
返回值示例

	{
	    "create_user": "panxy3@asiainfo.com",
	    "itemaccesstype": "public",
	    "comment": "详情",
	    "optime": "2015-10.1122: 10: 20",
	    "items": 3000,
	    "label": {},
	    "dataitems": [
	        "dataitem1",
	        "dataitem2"
	    ]
	}


## 3 指令：POST /Repositories/:repname
	
说明：
	
	【任意】创建repository

输入参数说明：

   	repaccesstype       访问权限[public(默认), private]
    comment 			详情
	label				label自定义json标签
    
Example Request：

	POST /repositories/chinamobile HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb
	
	{
        "repaccesstype": "public",
        "comment": "中国移动北京终端详情",
        "label": {
            "sys": {
                "loc": "北京"
            },
            "opt": {
                "age": 22
            },
            "owner": {
                "name": "michael"
            },
            "other": {
                "friend": 22
            }
        }
    }

## 4 指令：DELETE /Repositories/:repname
	
说明：
	
	【拥有者】删除repository

输入参数说明：

	repname[必选]		
	
Example Request：

	GET /repositories/chinamobile HTTP/1.1 
	Accept: application/json
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb

Example Response：

	无

## 5 指令：GET /Repositories/:repname/:itemname
	
说明：
	
	【任意】返回dataitem详细信息

输入参数说明：

	page (taglist分页页数) : 			1 - N，  默认=1（page=1可以不传）
	size（taglist页面大小）: 				1 - N，  默认=6

Example Request：

	GET /repositories/chinamobile/beijingphone HTTP/1.1 
	Accept: application/json

返回数据说明：
	
	create_user 			Dataitem创建者
	itemaccesstype  		访问权限[public(默认), private]
	optime   				更新时间
	meta					元数据
	sample					样例数据
	comment					详情
    tags					tag量
	label.sys.supply_style	服务形式[api；batch；flow]
	Tags.tag				tag名称
	Tags.comment			tag详情
	Tags.optime				tag上传日期
	taglist					item下所有tag的详细信息

返回值示例
        
	{
	    "create_user": "panxy3",
	    "itemaccesstype": "private",
	    "optime": "2015-08-0100: 00: 00",
	    "meta": {},
	    "sample": {},
	    "comment": "对终端使用情况、变化情况进行了全方面的分析。包括分品牌统计市场存量、新增、机型、数量、换机等情况。终端与ARPU、DOU、网龄的映射关系。终端的APP安装情况等。",
		"tags":10
		"label": {
	        "sys": {
	            "supply_style": "api"
	        },
	        "opt": {},
	        "owner": {},
	        "other": {}
	    },
	   "taglist":[
			{
				"tag": "tag001",
				"comment": "2022201MB",
				"optime": "2015-11-16 10:50:31.779460404 +0000 UTC|3小时以前"
			},
			{
				"tag": "tag002",
				"comment": "2001MB",
				"optime": "2015-11-17 02:14:55.241920929 +0000 UTC|10分钟以前"
			},
			{
				"tag": "tag003",
				"comment": "2001MB",
				"optime": "2015-11-17 02:14:59.491811069 +0000 UTC|6天以前"
			}
			]
	}

----------

## 6 指令：POST /repositories/:repname/:itemname

说明

	【拥有者】发布DataItem

输入参数说明
	
	itemaccesstype  				访问权限[public(默认), private]
	meta							元数据
	sample							样例数据
	comment							详情
	label.sys.supply_style			服务形式[api；batch；flow]【必选】
	label.sys.supply_style.api		实时单条
	label.sys.supply_style.batch	批量
	label.sys.supply_style.flow		流式
	
		
Example Request：

	POST /repositories/chinamobile/beijingphone HTTP/1.1 
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb
	{
        "itemaccesstype": "private",
        "meta": "{}",
        "sample": "{}",
        "comment": "对终端使用情况、变化情况进行了全方面的分析。包括分品牌统计市场存量、新增、机型、数量、换机等情况。终端与ARPU、DOU、网龄的映射关系。终端的APP安装情况等。",
        "label": {
            "sys": {
                "supply_style": "batch"
            },
            "opt": {},
            "owner": {},
            "other": {}
        }
    }
	
返回值示例

	无

----------

## 7 指令：DELETE /repositories/:repname/:itemname

说明

	【拥有者】删除DataItem

输入参数说明

	无

Example Request：

	DELETE /repositories/chinamobile/beijingphone HTTP/1.1 
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb
	
返回值示例
	
	无
----------

## 8 GET /repositories/:repname/:itemname/:tag

说明

	【任意】查询DataItem下的Tag详情，注意Tag需要按照UTF8编码后传递

输入参数说明：

	无

Example Request：

	GET /repositories/chinamobile/beijingphone/TAG000 HTTP/1.1

返回参数说明：
	
	comment  daemon提交tag相关详情
	optime	 daemon提交tag时间
	
返回值示例
	
	{
	    "comment": "50M",
	    "optime": "2015-08-03 00:00:00|6天以前"
	}

## 9 POST /repositories/:repname/:itemname/:tag

说明

	【拥有者】发布DataItem下的Tag详情，注意Tag需要按照UTF8编码后传递

输入参数说明：

	comment  tag相关详情

Example Request：

	POST /repositories/chinamobile/beijingphone/000 HTTP/1.1
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb 
	[
		{
			"comment":"2001MB"
		}
	]
	
Example Response：
	
	HTTP/1.1 200 
	Vary: Accept 
	Content-Type: application/json
	
	
返回数据说明：

	msg：可选，具体出错信息描述

## 10 DELETE /repositories/:repname/:itemname/:tag

说明

	【拥有者】删除DataItem下的Tag详情，注意Tag需要按照UTF8编码后传递

输入参数说明：

	无

Example Request：

	POST /repositories/chinamobile/beijingphone/TAG000 HTTP/1.1
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb 
	
Example Response：
	
	HTTP/1.1 200 
	Vary: Accept 
	Content-Type: application/json


