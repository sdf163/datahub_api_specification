## DataHub API简介 ##

**DataHub**是一个数据P2P流动的平台，详情请见hub.dataos.io.
本文规定了包括认证、版本控制、流量控制、协议内容等信息。

### 认证方式 ###

支持两种认证方式：对于CLI和CLI-WEB可以采用用户名密码的简单认证方式；对于SDK，必须采用OAUTH2协议下利用Token的第三方认证模式，其中Token在Server端生成（通过User服务）。

由于REST协议是没有状态的，所以每一次认证信息必须在协议中涵盖，利用Header中的Authorization字段来传递认证信息，Basic对应简单认证模式，Token对应Token认证模式。

**例如:**
**Authorization: Basic akmklmasadalkm==**

### 版本控制 ###
在请求的消息头中明确API的版本。

**例如:**
**X-DataHub-Version: 1**

### 流量控制 ###
在返回的消息头中给出流量控制参数.

**周期内还能调用的次数:X-RateLimit-Remaining: 1234**

**周期重置时间：X-RateLimit-Reset: 1350085300**

### 返回信息 ###
HTTP状态码

200 OK

400 Errors (内部错误，具体在数据体中进行说明) 

401 Unauthorized

数据体返回格式：

{

    "code": 0000,
    "msg": "OK",
    "data": {具体返回信息}
}


## DataHub API内容 ##

### repositories ###
编号：1

名称：数据中心API

描述文件：repositories.md

**编号10 [get /repositories](/repositories.md/)** 【拥有者|任意】 **这是一个特殊需求**如果后面没有username的参数，则返回本人创建或具备写权限的所有repository，如果带有参数?username=XXX，则表示查询XXX的所有repository，这里只能反馈查询者具备读权限的repositories名字（比如public或者在private白名单中的）

**编号11 [get /repositories/:repname](/repositories.md/)** 【任意】返回repository详细信息

**编号12 [post /repositories/:repname](/repositories.md/)** 【任意】创建repository

**编号13 [delete /repositories/:repname](/repositories.md/)** 【拥有者】删除repository

**编号14 [get /repositories/:repname/:itemname](/repositories.md/)** 【任意】返回此DataItem的详细情况

**编号15 [post /repositories/:repname/:itemname](/repositories.md/)** 【拥有者】发布DataItem

**编号16 [delete /repositories/:repname/:itemname](/repositories.md/)** 【拥有者】删除DataItem

**编号17 [get /repositories/:repname/:itemname/:tag](/repositories.md/)** 【任意】查询DataItem下的Tag详情，**注意Tag需要按照UTF8编码后传递**

**编号18 [post /repositories/:repname/:itemname/:tag](/repositories.md/)** 【拥有者】发布DataItem下的Tag详情，**注意Tag需要按照UTF8编码后传递**

**编号19 [delete /repositories/:repname/:itemname/:tag](/repositories.md/)** 【拥有者】删除DataItem下的Tag详情，**注意Tag需要按照UTF8编码后传递**

编号：1a

名称： Label

描述文件：label.md

**编号1a1 [delete /label/:repname](/label.md/)**删除Repositories label

**编号1a2 [get  /label/:repname](/label.md/)**更新Repositories label

**编号1a3 [post  /label/:repname](/label.md/)**增加Repositories label

**编号1a4 [put  /label/:repname](/label.md/)**查询Repositories label

**编号1a5 [delete /label/:repname/:itemname](/label.md/)**删除Dataitem label

**编号1a6 [get /label/:repname/:itemname](/label.md/)**更新Dataitem label

**编号1a7 [post /label/:repname/:itemname](/label.md/)**增加Dataitem label

**编号1a8 [put /label/:repname/:itemname](/label.md/)**查询Dataitem label

   
### selects ###
编号：2

名称：精选API

描述文件：selects.md

**编号20 [get /select_labels](/selects.md/)** 【任意】返回精选栏目

**编号21 [post /select_labels/:labelname](/selects.md/)** 【管理员】创建精选栏目

**编号22 [put /select_labels/:labelname](/selects.md/)** 【管理员】更新精选栏目

**编号23 [delete /select_labels/:labelname](/selects.md/)** 【管理员】删除精选栏目

**编号24 [get /selects](/selects.md/)** 【任意】返回精选内容

**编号25 [post /selects](/selects.md/)** 【管理员】创建精选内容

**编号26 [put /selects](/selects.md/)** 【管理员】更新精选内容

**编号27 [delete /selects](/selects.md/)** 【管理员】删除精选内容

### search ###
编号：3

名称：搜索API

描述文件：search.md

**编号30 get /search** 【任意】搜索


### subscriptions ###
编号：4

名称：订阅API

描述文件：subscriptions.md

**编号40 get /subscriptions** 【需求者】查询所有订阅的DataItem

**编号41 get /subscription/:repname/:itemname** 【需求者】查询该DataItem是否订阅过 **注意没有s**

**编号42 post /subscription/:repname/:itemname** 【需求者】订阅该DataItem **注意没有s**

**编号43 delete /subscription/:repname/:itemname** 【需求者】取消订阅该DataItem **注意没有s**

**编号44 get /subscription_stat/:repname/:itemname** 【任意】返回该DataItem的订阅量

**编号45 get /subscription_stat/:repname** 【任意】返回该repositories的订阅量

### transactions ###
编号：5

名称：交易API

描述文件：transactions.md

**编号50 post /transaction/:repname/:itemname/:tag** 【需求者】返回该请求的access_token，**注意tag需要UTF8编码，注意后面没有s**

**编号51 get /transaction/:repname/:itemname/:tag?cypt_accesstoken=???&username=???** 【拥有者】校验该access_token的有效性，此access_token被需求者的私有证书加密，注意后面没有s

**编号52 get /transactions_stat/:repname/:itemname** 【任意】返回该DataItem的pull量

**编号53 get /transactions_stat/:repname** 【任意】返回该repositories的pull量

**编号54 get /transactions_stat/:repname/:itemname/:tag** 【任意】返回该tag的pull量

**编号55 get /transactions/pull** 【需求者】返回该用户所有的pull的信息

**编号56 get /transactions/pull/:repname/:itemname** 【需求者】返回该用户pull的该DataItem的tag信息

**编号57 get /transactions/push** 【拥有者】返回该用户所有的被人家Pull的信息

**编号58 get /transactions/push/:repname/:itemname** 【拥有者】返回该用户所有的被人家Pull的该DataItem的tag信息

### heartbeats ###
编号：6

名称：心跳API

描述文件：heartbeats.md

**编号61 post /heartbeats** 【Daemon】心跳信息由Daemon根据配置的心跳周期发送给Server，作用之一为新Daemon上线后向Server注册；二为汇报Daemon的健康情况；三为从Server取回需要Daemon执行的指令，比如自动配置、自动升级、告警信息展示等

### users ###
编号：7

名称：用户API

描述文件：users.md

### msg ###
编号：8

名称：消息通知API

描述文件：msg.md


## DataHub API应用 ##

### WEB ###
**数据精选** 20，24，14，44，52

**Item详情** 14，17,41，56

**Repo详情** 11,44,45,52,53

**数据拥有者详情** 7 10

**搜索页面** 30,14,44,52

**我的发布** 10,14,44,52

**我发布的Repo详情** 11,44,45,52,53

**我发布的Item详情** 14,17,44,52,54

**我的订阅** 40，14，（41），52

**我的流水**  55或57

### Daemon ###

**repo**  10

**repo create**  12

**repo rm**  13

**subs**  40

**subs :repo/:item**  14

**pub :repo/:item**  15

**pub :repo/:item/:tag**  18

**pull :repo/:item/:tag**  50或51

**login**  7







