##同步服务
	将统计所需数据从kafka中同步到mysql中
	每天的数据存储到日表中，如果出现历史数据，删除历史信息，再插入统计数据
    
	kafka消息格式参考如下：
    数据说明
		server:服务名
        date：统计的日期
		columns：字段名称，与后面result里面的名字对应
		result：统计结果
    Example
		{"server":"user","date":"2015-01-02","columns":  {"column_a":"string","column_b":"int"},"result":[{"column_a":"aaa"}{"column_b":1}]}
	
###user服务
	数据说明
		login_name：用户登录名称
		user_type：用户级别(1：普通用户，2：管理员用户，3:认证会员,4：金卡会员，5：钻石会员)
	Example
		{"server":"user","date":"2015-01-02","columns":  {"login_name":"string","user_type":"int"},"result":[{"login_name":"aa@126.com","user_type":3},{"login_name":"bb@126.com","user_type":4}]}
