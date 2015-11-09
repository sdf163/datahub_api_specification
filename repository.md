# 主机地址
	
    http://ec2-54-223-244-55.cn-north-1.compute.amazonaws.com.cn
    http://54.223.244.55:8088
    
# API 列表
	

- 查询所有repositories  

- 查询repo下的item

- 创建dataitem

- 创建tag 
	
----------

## 查询所有repositories
	
	GET /repositories

可选参数
	
	page(分页页数): 1 - N， 默认=1
	size（页面大小）:1 - N， 默认=5

请求示例

	GET /repositories?page=1&size=2

返回值 Json Object

	{[item:{},item:{},item:{}]}

返回值示例
        
            {
                "item": {
                    "repname": "NBA",
                    "user_id": 1002,
                    "dataitem_id": 1000002,
                    "dataitem_name": "全国终端换机分析",
                    "ico_name": "terminal.png",
                    "permit_type": 2,
                    "key_words": "手机;iphone",
                    "supply_style": 1,
                    "priceunit_type": 1,
                    "optime": "2015-08-01 00:00:00",
                    "data_format": 1,
                    "refresh_type": "1",
                    "refresh_num": 1,
                    "meta_filename": "meta_terminal2.txt",
                    "sample_filename": "sample_terminal2.txt",
                    "comment": "对终端使用情况、变化情况进行了全方面的分析。包括分品牌统计市场存量、新增、机型、数量、换机等情况。终端与ARPU、DOU、网龄的映射关系。终端的APP安装情况等。"
                }
            },
            {
                "item": {
                    "repname": "NBA",
                    "user_id": 1002,
                    "dataitem_id": 1000002,
                    "dataitem_name": "全国终端换机分析",
                    "ico_name": "terminal.png",
                    "permit_type": 2,
                    "key_words": "手机;iphone",
                    "supply_style": 1,
                    "priceunit_type": 1,
                    "optime": "2015-08-01 00:00:00",
                    "data_format": 1,
                    "refresh_type": "1",
                    "refresh_num": 1,
                    "meta_filename": "meta_terminal2.txt",
                    "sample_filename": "sample_terminal2.txt",
                    "comment": "对终端使用情况、变化情况进行了全方面的分析。包括分品牌统计市场存量、新增、机型、数量、换机等情况。终端与ARPU、DOU、网龄的映射关系。终端的APP安装情况等。"
                }
            }
 
----------


## 查询repo下的item
	
	GET /repositories/:repname/:itemname

请求示例

	GET /repositories/chinamobile/beijingphone

返回值 Json Object

	{item:{}}

返回值示例
        
	{
	    "item": {
	        "repname": "chinamobile",
	        "login_name": 1004,
	        "dataitem_id": 1011,
	        "dataitem_name": "beijingphone",
	        "ico_name": "terminal.png",
	        "permit_type": 2,
	        "label": "手机;iphone",
	        "supply_style": 3,
	        "priceunit_type": 1,
	        "optime": "2015-08-01 00:00:00",
	        "data_format": 2,
	        "refresh_type": "1",
	        "refresh_num": 1,
	        "meta_filename": "meta_terminal.doc",
	        "sample_filename": "sample_terminal.doc",
	        "comment": "对终端使用情况、变化情况进行了全方面的分析。包括分品牌统计市场存量、新增、机型、数量、换机等情况。终端与ARPU、DOU、网龄的映射关系。终端的APP安装情况等。"
	    }
	}

----------

## 创建dataitem

	POST /repositories/:repname/:itemname

必选参数

	repname
	itemname

可选参数

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
	mample_filename 存放样例数据的文件名  文件内容可以是json格式，显示时可以根据特定的关键字在web上进行渲染
	comment         概要


请求示例

	POST /repositories/NBA/bear

----------

## 创建tag 

	POST /repositories/:repname/:itemname/:tag

必选参数

	repname
	itemname
	tag

可选参数

	filename 在文件系统上存储时，存tag_filename

请求示例

	POST /repositories/NBA/bear/27
