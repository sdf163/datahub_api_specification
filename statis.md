###repositor服务

    数据说明    
    	id                  数据序列号
    	repuser             rep创建者
    	repname             rep名称
    	repaccesstype       rep访问权限
    	itemuser            item创建者
    	itemname            item名称
    	tags                item下tag数量
    	itemaccesstype      item访问权限
    	supplestyle         item服务形式
    	selectlabel         item精选名称
    	
    Example	
    	{
        	"service":"repository",
        	"date":"2015-01-02",
        	"columns":[
        		        {
        			        "column_name":"id",
        			        "column_type":"int",
        		        },	
        		        {
                            "column_name":"repuser",
                            "column_type":"string",
                        },
                        {
                            "column_name":"repname",
                            "column_type":"string",
                        },        		
        		        {
                            "column_name":"repaccesstype",
                            "column_type":"string",
                        },
        		        {
                            "column_name":"itemuser",
                            "column_type":"string",
                        },
        		        {
                            "column_name":"itemname",
                            "column_type":"string",
                        },
        		        {
                            "column_name":"tags",
                            "column_type":"int",
                        },
        		        {
                            "column_name":"itemaccesstype",
                            "column_type":"string",
                        },
                        {
                            "column_name":"supplestyle",
                            "column_type":"string",
                        },
                        {
                            "column_name":"itemaccesstype",
                            "column_type":"selectlabel",
                        }                        		        	
        	        ], 
        	"result":[
        			    {
        					"id": 0,             
                            "repuser": "panxy3@asiainfo.com",
                            "repname": "test", 
                            "repaccesstype" : "public",
                            "itemuser": "liuxu@asiainfo.com",            
                            "itemname": "test2",            
                            "tags" : "12",               
                            "itemaccesstype" : "private",     
                            "supplestyle": "batch",         
                            "selectlabel" : "征信专题",        
        			    },	
        	]
        }
	
## topic: to_repositories.json

### 增加repository rank

	{
		"repname": "repo001",
        "rank": 10.5		
	}
	注意:rank不是字符串

### 增加dataitem rank

	{
		"repname": "repo001",
		"itemname": "item002",
        "rank": 10.2		
	}	
	注意:rank不是字符串
        