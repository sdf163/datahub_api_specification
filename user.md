<h2>1、用户相关接口</h2>
<p>1.1.创建用户</p>
<pre><code>指令：/user/addUser.do
说明：用于创建用户
Example Request：
[
  {"userName":"HDFSDATAPOOL","passward":"HDFS"}
]


输入参数说明：
username：用户的名字
password：用户的密码
Example Response：
[{"msg":""}]

Status Codes：
200 OK
400 Errors (invalid json, missing or invalid fields, etc) 
401 Unauthorized
返回数据说明：
msg：必选，具体出错信息描述
</code></pre>

<p>1.2.删除用户</p>
<pre><code>指令：/user/deleteUser.do
说明：删除用户接口
Example Request：
[
 {"userName":"xxx"}
]
输入参数说明：
userName：用户的名字
输入数据说明：
Example Response：
[{"msg":""}]
Status Codes：
200 OK
400 Errors (invalid json, missing or invalid fields, etc) 
返回数据说明：
msg：返回的信息
</code></pre>

<p>1.3.更新用户</p>
<pre><code>指令：/user/updateUser.do
说明：用于更新用户信息
Example Request：
[
{"userName":"xxx","password":"xxx"}
]

输入数据说明：
userName：用户的名称
password：用户的密码
Example Response：
[{"msg":""}]
Status Codes：
200 OK
400 Errors (invalid json, missing or invalid fields, etc) 
返回数据说明：
msg：返回的信息
</code></pre>

<p>1.4.查询用户详细信息</p>
<pre><code>指令：/user/queryUserDetail.do
说明：用于查询用户详细信息
Example Request：
[
{"userName":"xxx"}
]

输入数据说明：
userName：用户的名称

Example Response：
[{"userName":"xxx","password":"xxx","email":"xxx","msg":"xxx"}]
Status Codes：
200 OK
400 Errors (invalid json, missing or invalid fields, etc) 
返回数据说明：
msg：返回的信息,200或400</code></pre>
