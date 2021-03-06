# API 列表
	

- [GET] /daemon/id 获取登陆用户的daemonid。
- [GET] /daemon/ep/:user 获取user的entrypoint，普通用户只能获取自己的entrypoint。
- [GET] /daemon/log/:index 获取登陆用户的log。
- [GET] /daemon/status 获取登陆用户的daemon status以及entrypoint。

----------

## 指令：GET /daemon/id/ 获取登陆用户的daemonid。

说明
	给用户分配一个唯一标识并返回，用于在用户安装Daemon并启动时向server表明自己的身份。

输入参数说明：
	
    无

Example Request：

	GET /daemon/id HTTP/1.1 
	Accept: application/json 
	Content-Type: application/json 
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb 
	

返回数据示例
        
	HTTP/1.1 200 OK
	Accept: application/json 
	Content-Type: application/json 

    {
        "daemonid":"0aef69daefb06d0afbe6c"
    }



## 指令：GET /daemon/ep/:user 获取user的入口地址，普通用户只能获取自己的entrypoint。

说明
	返回作为数据提供方user的入口地址。

输入参数说明：
	
    无

Example Request：

	GET /daemon/ep/cmcc HTTP/1.1 
	Accept: application/json 
	Content-Type: application/json 
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb 

返回数据示例
        
	HTTP/1.1 200 OK
	Accept: application/json 
	Content-Type: application/json 

    {
        "entrypoint":[
            "http://211.10.23.23:35800",
            "http://211.10.23.24:35800"
        ]
    }



## 指令：GET /daemon/log/:index 获取登陆用户的daemon日志。

说明
	返回以index为起始索引的用户daemon日志，索引范围为[index, index+9]。

输入参数说明：
	
    range： 可选参数，指定索引范围，若不指定则以index开始索引，返回10条。

Example Request：

	GET /daemon/log/5?range=2 HTTP/1.1 
	Accept: application/json 
	Content-Type: application/json 
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb 

返回数据示例
        
	HTTP/1.1 200 OK
	Accept: application/json 
	Content-Type: application/json 

    {
        "log":[
        "2015/12/01 14:58:29 testlog7",
        "2015/12/01 14:56:21 testlog6",
        "2015/12/01 14:52:54 testlog5"
        ]
    }


## 指令：GET /daemon/status/ 获取登陆user的daemon status。

说明
	返回登陆用户的datahub daemon在线状态：online，offline， 以及entrypoint。

输入参数说明：
	
    无

Example Request：

	GET /daemon/status HTTP/1.1 
	Accept: application/json 
	Content-Type: application/json 
	Authorization: Token dcabfefb6ad8feb68e6fbce876fbfe778fb 
	

返回数据示例
        
	HTTP/1.1 200 OK
	Accept: application/json 
	Content-Type: application/json 

    {
        "status":"online",
        "entrypoint":[
            "http://211.10.23.23:35800",
            "http://211.10.23.24:35800"
        ]
    }


