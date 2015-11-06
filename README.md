# datahub_api_specification
REST API接口说明书
FORMAT: 1A
HOST: http://10.1.235.96:8080

# datahub

Public

## Subscription Collection [/subscriptions]

### List All Subscriptions [GET]

+ Response 200 (application/json)

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
]

### Create a New Question [POST]

You may create your own question using this action. It takes a JSON
object containing a question and a collection of answers in the
form of choices.

+ Request (application/json)

        {
            "question": "Favourite programming language?",
            "choices": [
                "Swift",
                "Python",
                "Objective-C",
                "Ruby"
            ]
        }

+ Response 201 (application/json)

    + Headers

            Location: /questions/2

    + Body

            {
                "question": "Favourite programming language?",
                "published_at": "2015-08-05T08:40:51.620Z",
                "choices": [
                    {
                        "choice": "Swift",
                        "votes": 0
                    }, {
                        "choice": "Python",
                        "votes": 0
                    }, {
                        "choice": "Objective-C",
                        "votes": 0
                    }, {
                        "choice": "Ruby",
                        "votes": 0
                    }
                ]
            }


 
