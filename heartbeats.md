# API 列表
	

- [POST] /heartbeats 发送心跳信息

----------

## 指令：POST /heartbeats 发送心跳信息

说明
	心跳信息由Daemon根据配置的心跳周期发送给Server，作用之一为新Daemon上线后向Server注册；二为汇报Daemon的健康情况；三为从Server取回需要Daemon执行的指令，比如自动配置、自动升级、告警信息展示等

输入参数说明：
	
	daemonid: DaemonID，从网页端获取的安装脚本中获取。用于识别用户。
    entrypoint: Daemon提供的入口信息。


Example Request：

	POST /heartbeats HTTP/1.1 
	Accept: application/json 
	Content-Type: application/json 
	

    {
        "daemonid":"0aef69daefb06d0afbe6c",
        "entrypoint":[
            "http://211.10.23.23:35800"
        ]
    }

返回数据说明：

    无

返回数据示例
        
	HTTP/1.1 200 OK
	Accept: application/json 
	Content-Type: application/json 



