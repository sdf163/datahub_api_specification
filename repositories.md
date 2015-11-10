# API 列表
	

- [GET] /repositories

- [GET] [POST] [DELETE] /repositories/:repname

- [GET] [POST] [DELETE] /repositories/:repname/:itemname

- [GET] [POST] [DELETE] /repositories/:repname/:itemname/:tag

	
----------

## 指令：GET /Repositories

说明

	【拥有者】
	 		如果后面没有username的参数,则返回本人创建或具备写权限的所有repository
	【任意】 
			如果带有参数?username=XXX，则表示查询XXX的所有repository，这里只能反馈查询者具备读权限的repositories名字（比如public或者在private白名单中的）

输入参数说明：
	
	page (分页页数) : 1 - N，  默认=1
	size（页面大小）: 1 - N，  默认=5,  -1 返回全部
	username: 	数据提供者username
	（header 中为登录用户的username）

Example Request：

	GET /repositories?page=1&size=3 HTTP/1.1 
	Accept: application/json
	Authorization: Basic akmklmasadalkm==


返回数据说明：
	
	repname：数据仓库的名字
	
返回值示例
        
	[
	    "repname1",
	    "repname2",
	    "repname3"
	]

----------

## 指令：GET /Repositories/:repname
	
说明：
	
	【任意】查询repository详情

输入参数说明：

	无
	
Example Request：

	GET /repositories/myrep1 HTTP/1.1 
	Accept: application/json

返回数据说明：
	
	create_user			创建者
   	itemaccesstype      对外开放类型[public(默认), private]
  	deposit         	托管类型[no默认)，yes]
    comment 			详情
	optime				更新时间
	stars				关注量
	views				浏览量
	items				dataitem数量	
	label				标签
	
	
返回值示例

	{
	    "create_user": "panxy3@asiainfo.com",
	    "itemaccesstype": "public",
	    "deposit": "no",
	    "comment": "详情",
	    "optime": "2015-10.1122: 10: 20",
	    "star": 500,
	    "view": 600,
	    "item_num": 3000,
	    "tag_num": 900,
	    "rank": 12,
	    "status": "up",
	    "label": {}
	}


## 指令：POST /Repositories/:repname
	
说明：
	
	【任意】创建repository

输入参数说明：

   	repaccesstype      访问权限[public(默认), private]
  	deposit         	托管类型[no默认)，yes]
    comment 			详情
	label.user.age		label标签下user下的age自定义标签
   
   
Example Request：

	POST /repositories/chinamobile HTTP/1.1 
	Accept: application/json
	Authorization: Basic akmklmasadalkm==
	
	[
   		itemaccesstype      public
  		deposit      		no
    	comment 			中国移动北京终端详情
		label.user.age		22
	]


## 指令：DELETE /Repositories/:repname
	
说明：
	
	【拥有者】删除repository

输入参数说明：

	repname[必选]		
	
Example Request：

	GET /repositories/chinamobile HTTP/1.1 
	Accept: application/json
	Authorization: Basic akmklmasadalkm==

Example Response：

	[
	    {
	        "msg": ""
	    }
	]	


## 指令：GET /Repositories/:repname/:itemname
	
说明：
	
	【任意】返回dataitem详细信息

输入参数说明：

	无

Example Request：

	GET /repositories/chinamobile/beijingphone HTTP/1.1 
	Accept: application/json

返回数据说明：
	
	create_user 			Dataitem创建者
	itemaccesstype  		访问权限[public(默认), private]
	price  					定价协议
	optime   				更新时间
	meta					元数据
	sample					样例数据
	comment					详情
	label.sys.supply_style	服务形式[single；batch；flow]
	label.sys.refresh 		更新周期(3天)
	Tags.tag				tag名称
	Tags.comment			tag详情
	Tags.optime				tag上传日期
	
返回值示例
        
	{
	    "create_user": "panxy3",
	    "itemaccesstype": "private",
	    "price": {},
	    "optime": "2015-08-0100: 00: 00",
	    "meta": {},
	    "sample": {},
	    "comment": "对终端使用情况、变化情况进行了全方面的分析。包括分品牌统计市场存量、新增、机型、数量、换机等情况。终端与ARPU、DOU、网龄的映射关系。终端的APP安装情况等。",
		"label": {
	        "sys": {
	            "supply_style": "api",
	            "refresh": "3日"
	        },
	        "opt": {},
	        "owner": {},
	        "other": {}
	    },
	    "Tags": [
	        {
	            "tag": "20151030",
	            "comment": "50M",
	            "optime": "2015-08-0300: 00: 00"
	        },
	        {
	            "tag": "20151010",
	            "comment": "501M",
	            "optime": "2015-08-0100: 00: 00"
	        }
	    ]
	}

----------

## 指令：POST /repositories/:repname/:itemname

说明

	【拥有者】发布DataItem

输入参数说明
	
	itemaccesstype  		访问权限[public(默认), private]
	price  					定价协议(目前可以不填)
	meta					元数据
	sample					样例数据
	comment					详情
	label.sys.supply_style	服务形式[single；batch；flow]
	label.sys.refresh 		更新周期(3天)
		
Example Request：

	POST /repositories/chinamobile/beijingphone HTTP/1.1 
	Authorization: Basic akmklmasadalkm==
	[
		{
		    "itemaccesstype": "private",
		    "meta": {},
		    "sample": {},
		    "comment": "对终端使用情况、变化情况进行了全方面的分析。包括分品牌统计市场存量、新增、机型、数量、换机等情况。终端与ARPU、DOU、网龄的映射关系。终端的APP安装情况等。"，
			"label": {
		        "sys": {
		            "supply_style": "api",
		            "refresh": "3日"
		        },
		        "opt": {},
		        "owner": {},
		        "other": {}
		    },
		}
	]
	
返回值示例

	无

----------

## 指令：DELETE /repositories/:repname/:itemname

说明

	【拥有者】删除DataItem

输入参数说明

	无

Example Request：

	DELETE /repositories/chinamobile/beijingphone HTTP/1.1 
	Authorization: Basic akmklmasadalkm==
	
返回值示例
	
	无
----------

## GET /repositories/:repname/:itemname/:tag

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
	    "comment": "50M ",
	    "optime": "2015-08-03 00:00:00"
	}

## POST /repositories/:repname/:itemname/:tag

说明

	【拥有者】发布DataItem下的Tag详情，注意Tag需要按照UTF8编码后传递

输入参数说明：

	comment  tag相关详情

Example Request：

	POST /repositories/chinamobile/beijingphone/000 HTTP/1.1
	Authorization: Basic akmklmasadalkm== 
	[
		{
			comment="2001MB"
		}
	]
	
Example Response：
	
	HTTP/1.1 200 
	Vary: Accept 
	Content-Type: application/json
	
	
返回数据说明：

	msg：可选，具体出错信息描述

## DELETE /repositories/:repname/:itemname/:tag

说明

	【拥有者】删除DataItem下的Tag详情，注意Tag需要按照UTF8编码后传递

输入参数说明：

	无

Example Request：

	POST /repositories/chinamobile/beijingphone/TAG000 HTTP/1.1
	Authorization: Basic akmklmasadalkm== 
	
Example Response：
	
	HTTP/1.1 200 
	Vary: Accept 
	Content-Type: application/json


