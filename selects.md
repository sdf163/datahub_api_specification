# 主机地址
	
    http://ec2-54-223-244-55.cn-north-1.compute.amazonaws.com.cn
    http://54.223.244.55:8088
    
# API 列表
	
- 查询符合精选项的repname/itemname列表
- 为repname/itemname的Label添加精选属性
- 为repname/itemname的Label删除精选属性
- 
- 为精选列表增加精选项
- 为精选列表删除精选项
 

----------


## 查询符合精选名称的repname/itemname列表
	
	GET /digest

可选参数
	
	name(精选名称)

请求示例
	
	GET /digest?name=终端

返回值 Json Object

	{{repname:，dataitem:}，{repname:，dataitem:}，{repname:，dataitem:}}

返回值示例

	{{repname: NBA，dataitem: bear}，{repname: NBA，dataitem: fox}，{repname: NBA，dataitem: hourse}}


## 为repname/itemname的Label添加精选属性
	
	POST /digest/：repname/:itemname

请求示例

	POST /digest/NBA/bear

必选参数

	repname
	itemname

可选参数
	
	name（精选项名称）


## 为repname/itemname的Label删除精选属性
	
	DELETE /digest/：repname/:itemname

请求示例

	DELETE /digest/NBA/bear

必选参数

	repname
	itemname

可选参数
	
	name（精选项名称）


## 为精选列表增加精选项
	
	POST /digest/:name

请求示例

	POST /digest/终端

必选参数

	name（精选项）
	

## 为精选列表删除精选项
	
	DELETE /digest/:name

请求示例

	DELETE /digest/终端

必选参数

	name（精选项）
