# API 列表
	

- [POST] /heartbeats 发送心跳信息

----------

## 指令：POST /heartbeats 发送心跳信息

说明
	心跳信息由Daemon根据配置的心跳周期发送给Server，作用之一为新Daemon上线后向Server注册；二为汇报Daemon的健康情况；三为从Server取回需要Daemon执行的指令，比如自动配置、自动升级、告警信息展示等

输入参数说明：
	
	DaemonInfo：Daemon本身的情况、连接的User情况、系统环境、关键日志
	HealthInfo：Daemon的健康情况、EntryPoint的健康报告，报告EntryPoint非常重要，入口信息就是通过这种方式发给Server，以便Server挑选发送给消费者的。这些健康历史数据提供者可以通过Server的WEB界面看到 
	CmdOutput：上次命令执行反馈


Example Request：

	POST /HeartBeats HTTP/1.1 
	Accept: application/json 
	Content-Type: application/json 
	
	[
	{"DaemonInfo":{},"HealthInfo":{},"CmdOutput":{}}
	]


返回数据说明：

	CMD：要求Daemon执行的指令
	msg：可选，具体出错信息描述

返回数据示例
        
	HTTP/1.1 200 
	Accept: application/json 
	Content-Type: application/json 

	{"CMD":{}}


