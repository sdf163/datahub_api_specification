# datahub_api_specification
REST API接口说明书

## subsciption


 指令：GET /Subscriptions
 
 说明：返回在Server上订购的所有数据项的简要信息。
 
 示例: curl http://10.1.235.96:8080/subscriptions -u panxy3@asiainfo.com:8ddcff3a80f4189ca1c9d4d902c3c909
 
 Example Response：
 ```json
 [
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
             "refresh_date": "{\"absolute\":\"2015-10-20 10:10:10\"}",
             "usability": 1
         }
     },
     {
         "item": {
             "repname": "NBA",
             "user_id": 1002,
             "dataitem_id": 1000003,
             "dataitem_name": "APP使用情况",
             "ico_name": "Apps.png",
             "permit_type": 2,
             "key_words": "app;应用",
             "supply_style": 3,
             "priceunit_type": 1,
             "optime": "2015-08-01 00:00:00",
             "data_format": 1,
             "refresh_type": "1",
             "refresh_num": 1,
             "meta_filename": "meta_apps.txt",
             "sample_filename": "sample_apps.txt",
             "comment": "统计全国智能终端APP的使用情况。按天统计用户APP的使用情况，包括APP类型、APP名称、独立访客访问次数、访问总次数等信息。"
         },
         "statis": {
             "dataitem_id": 1000003,
             "dataitem_name": "APP使用情况",
             "views": 100,
             "follows": 50,
             "stars": 1,
             "refresh_date": "{\"absolute\":\"2015-10-20 10:10:10\"}",
             "usability": 1
         }
     }
 ]
 ```
 
