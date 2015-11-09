
## API列表 ##
[GET] [POST] [DELETE] [PUT] /msg/:msgName
## 添加消息 ##
### 指令 ###
[POST] /msg/:msgName
### 说明 ###
添加一条消息
### 输入参数说明 ###
msgName：消息名字
### Example Request ###
POST /msg/hello HTTP/1.1 
[
    "label": {
          "sys": {
                   "supply_style": 1
                 },
          "opt": {},
          "owner": {},
          "other": {}
          }
]
### Example Response ###
HTTP/1.1 200 
Vary: Accept 
Content-Type: application/json

[
    {"msg":""}
]

### Status Codes ###
200 OK
400 Errors (invalid json, missing or invalid fields, etc) 
401 Unauthorized

### 返回数据说明 ###
msg：可选，具体出错信息描述

## 修改消息 ##
### 指令 ###
[PUT]   /msg/:msgName
### 说明 ###
修改一条消息
### 输入参数说明 ###
msgName：消息名字
### Example Request ###
PUT /msg/hello HTTP/1.1 
[
    "label": {
          "sys": {
                   "supply_style": 1
                 },
          "opt": {},
          "owner": {},
          "other": {}
          }
]
### Example Response ###
HTTP/1.1 200 
Vary: Accept 
Content-Type: application/json

[
    {"msg":""}
]

### Status Codes ###
200 OK
400 Errors (invalid json, missing or invalid fields, etc) 
401 Unauthorized

### 返回数据说明 ###
msg：可选，具体出错信息描述

## 删除消息 ##
### 指令 ###
[DELETE]   /msg/:msgName
### 说明 ###
修改一条消息
### 输入参数说明 ###
msgName：消息名字
### Example Request ###
DELETE /msg/hello HTTP/1.1 

### Example Response ###
HTTP/1.1 200 
Vary: Accept 
Content-Type: application/json

[
    {"msg":""}
]

### Status Codes ###
200 OK
400 Errors (invalid json, missing or invalid fields, etc) 
401 Unauthorized

### 返回数据说明 ###
msg：可选，具体出错信息描述


## 查询消息 ##
### 指令 ###
[GET]   /msg/:msgName
### 说明 ###
修改一条消息
### 输入参数说明 ###
msgName：消息名字
### Example Request ###
GET /msg/hello HTTP/1.1 

### Example Response ###
HTTP/1.1 200 
Vary: Accept 
Content-Type: application/json

[
    {"msg":""}
]

### Status Codes ###
200 OK
400 Errors (invalid json, missing or invalid fields, etc) 
401 Unauthorized

### 返回数据说明 ###
msg：可选，具体出错信息描述

