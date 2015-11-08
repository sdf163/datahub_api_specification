# 主机地址
	
    http://ec2-54-223-244-55.cn-north-1.compute.amazonaws.com.cn
    http://54.223.244.55:8088
    
# API 列表
	

- 查询所有repositories  

	
- 查询repo下的item



----------

## 查询所有repositories
	
	GET /repositories

请求示例

	GET /repositories

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
                },
                "statis": {
                    "dataitem_id": 1000003,
                    "dataitem_name": "APP使用情况",
                    "views": 100,
                    "follows": 50,
                    "stars": 1,
                    "refresh_date": "2015-10-20 10:10:10",
                    "usability": 1
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
                },
                "statis": {
                    "dataitem_id": 1000002,
                    "dataitem_name": "全国终端换机分析",
                    "views": 100,
                    "follows": 50,
                    "stars": 1,
                    "refresh_date": "2015-10-20 10:10:10",
                    "usability": 1
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