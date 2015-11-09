# API 列表
	

- [GET] /repositories

- [GET] [POST] /repositories/:repname

- [GET] [POST] /repositories/:repname/:itemname

- [POST] /repositories/:repname/:itemname/:tag

	
----------

## 指令：GET /Repositories

说明

	返回具备写权限的Repository的详细情况，因是向DataHub Server查询，故需要认证信息。

输入参数说明：
	
	page (分页页数) : 1 - N，  默认=1
	size（页面大小）: 1 - N，   默认=5

Example Request：

	GET /repositories?page=1&size=3 HTTP/1.1 
	Accept: application/json
	Authorization: Basic akmklmasadalkm==

Example Response：

	[
	    {
	        "repname": "myrep",
	        "repaccesstype": "private",
	        "items": []
	    },
	    {
	        "repname": "myrep2",
	        "repaccesstype": "private",
	        "items": []
	    },
	    {
	        "msg": ""
	    }
	]


返回状态码：

	200 OK
	400 Errors (invalid json, missing or invalid fields, etc) 
	401 Unauthorized

返回数据说明：

	repname：数据仓库的名字
	repaccesstype：数据仓库的访问类型
	items：数据仓库中包含的数据项
	msg：可选，具体出错信息描述

返回值示例
        
	[
	    {
	        "repname": "myrep",
	        "repaccesstype": "Public",
	        "items": [
	            {
	                "repname": "NBA",
	                "login_name": "panxy3",
	                "dataitem_id": 1000002,
	                "dataitem_name": "NBA",
	                "ico_name": "terminal.png",
	                "repaccesstype": "private",
	                "label": {
	                    "sys": {
	                        "supply_style": 1
	                    },
	                    "opt": {},
	                    "owner": {},
	                    "other": {}
	                },
	                "priceunit_type": 1,
	                "optime": "2015-08-01 00:00:00",
	                "data_format": 1,
	                "refresh_type": "1",
	                "refresh_num": 1,
	                "meta_filename": "meta_terminal2.txt",
	                "sample_filename": "sample_terminal2.txt",
	                "comment": "对终端使用情况、变化情况进行了全方面的分析。包括分品牌统计市场存量、新增、机型、数量、换机等情况。终端与ARPU、DOU、网龄的映射关系。终端的APP安装情况等。"
	            }
	        ]
	    },
	    {
	        "repname": "myrep2",
	        "repaccesstype": "private",
	        "items": []
	    },
	    {
	        "msg": ""
	    }
	]

 
----------


## 指令：GET /Repositories/:repname/:itemname
	
	GET /repositories/:repname/:itemname

说明：
	
	查询数据项详细信息	

输入参数说明：

	repname		
	itemname

Example Request：

	GET /repositories/chinamobile/beijingphone HTTP/1.1 

Example Response：

	[
	    {
	        		"repname": "NBA",
	                "login_name": "panxy3",
	                "dataitem_id": 1000002,
	                "dataitem_name": "NBA",
	                "ico_name": "terminal.png",
	                "repaccesstype": "private",
	                "label": {
	                    "sys": {
	                        "supply_style": 1
	                    },
	                    "opt": {},
	                    "owner": {},
	                    "other": {}
	                },
	                "priceunit_type": 1,
	                "optime": "2015-08-01 00:00:00",
	                "data_format": 1,
	                "refresh_type": "1",
	                "refresh_num": 1,
	                "meta_filename": "{}",
	                "sample_filename": "{}",
	                "comment": "对终端使用情况、变化情况进行了全方面的分析。包括分品牌统计市场存量、新增、机型、数量、换机等情况。终端与ARPU、DOU、网龄的映射关系。终端的APP安装情况等。"
	        "Tags": [
	            {
	                "tag": "20151030",
	                "sourcename": "mydata "
	            },
	            {
	                "tag": "20151030",
	                "sourcename": "mydata2"a
	            }
	        ]
	    }
	]


返回值示例
        
	{
			{
	                "repname": "NBA",
	                "login_name": "panxy3",
	                "dataitem_id": 1000002,
	                "dataitem_name": "NBA",
	                "ico_name": "terminal.png",
	                "repaccesstype": "private",
	                "label": {
	                    "sys": {
	                        "supply_style": 1
	                    },
	                    "opt": {},
	                    "owner": {},
	                    "other": {}
	                },
	                "priceunit_type": 1,
	                "optime": "2015-08-01 00:00:00",
	                "data_format": 1,
	                "refresh_type": "1",
	                "refresh_num": 1,
	                "meta_filename": "{}",
	                "sample_filename": "{}",
	                "comment": "对终端使用情况、变化情况进行了全方面的分析。包括分品牌统计市场存量、新增、机型、数量、换机等情况。终端与ARPU、DOU、网龄的映射关系。终端的APP安装情况等。"
					"Tags": [
					            {
					                "tag": "20151030",
					                "sourcename": "mydata "
					            },
					            {
					                "tag": "20151030",
					                "sourcename": "mydata2"a
					            }
				        ]
	          }	  
	}

----------

## 指令：POST /repositories/:repname/:itemname

说明

	发布数据项

输入参数说明

	repname：数据仓库名字
	itemname：数据项名字

	login_name    	数据提供者起的名字
	ico_name      	图标文件名
	permit_type   	访问权限-public,所有用户可见,但用户黑名单不可见，3-private,所有用户不可见,但白名单用户可见'
	supply_style  	实时单条；批量； 流
	priceunit_type 	定价单位
	price 定价 
	data_format   	数据格式，1-txt、2-xls、3-ppt、4-doc、...
	refresh_type  	数据的刷新周期，月、日、时、分、秒
	refresh_num   	刷新周期refresh_type的个数
	meta_filename  	新增字段用于数据项描述 存json格式较好，否则显示没有渲染
	sample_filename 存放样例数据的文件名  文件内容可以是json格式，显示时可以根据特定的关键字在web上进行渲染
	comment         概要

Example Request：

	POST /repositories/chinamobile/beijingphone HTTP/1.1 
	[
		{
			"ico_name":"item1","permit_type":"2"
			"supply_style":"1","priceunit_type":"1","price":"0",
			"data_format":"1","refresh_type":"1","refresh_num":"1",
			"meta_filename":"{}","sample_filename":"{}",comment:"cc"
		}
	]
	
Example Response：
	
	HTTP/1.1 200 
	Vary: Accept 
	Content-Type: application/json
	
	[
		{"msg":""}
	]

----------

## POST /repositories/:repname/:itemname/:tag

输入参数说明：

	repname：数据仓库名字
	itemname：数据项名字
	tag： tag名


可选参数

	filename 在文件系统上存储时，存tag_filename

Example Request：

	POST /repositories/chinamobile/beijingphone/000 HTTP/1.1 
	[
		{
			filename="xxx.txt"
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

