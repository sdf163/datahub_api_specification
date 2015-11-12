# API 列表
	

- [GET] /daemon/id/:user 获取user的daemonid。
- [GET] /daemon/ep/:user 获取user的entrypoint。

----------

## 指令：GET /daemon/id/:user 获取user的daemonid。

说明
	给用户分配一个唯一标识并返回，用于在用户安装Daemon并启动时向server表明自己的身份。

输入参数说明：
	
    无

Example Request：

	GET /daemon/id/datahub HTTP/1.1 
	Accept: application/json 
	Content-Type: application/json 
	

返回数据示例
        
	HTTP/1.1 200 OK
	Accept: application/json 
	Content-Type: application/json 

    {
        "daemonid":"0aef69daefb06d0afbe6c"
    }



## 指令：GET /daemon/ep/:user 获取user的入口地址。

说明
	返回作为数据提供方user的入口地址。

输入参数说明：
	
    无

Example Request：

	GET /daemon/ep/cmcc HTTP/1.1 
	Accept: application/json 
	Content-Type: application/json 
	

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


