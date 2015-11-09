# 主机地址
	
    http://ec2-54-223-244-55.cn-north-1.compute.amazonaws.com.cn
    http://54.223.244.55:8088
    
# API 列表
	

- 根据Label查询符合条件的repname和itemname
- 为repname/itemname创建Label
- 为repname/itemname删除Label某属性
- 为repname/itemname更新Label某属性


----------

## 根据Label查询符合条件的repname和itemname
	
	GET /label


请求示例

	GET /label?digest=移动终端

返回值 Json Object

	{{repname:，dataitem:}，{repname:，dataitem:}，{repname:，dataitem:}}

返回值示例

	{{repname: NBA，dataitem: bear}，{repname: NBA，dataitem: fox}，{repname: NBA，dataitem: hourse}}

----------


## 为repname/itemname创建Label
	
	POST /label/:repname/:itemname

请求示例

	POST /label/NBA/bear

必选参数

	repname
	itemname


可选参数
	
	digest（数据精选）

----------

## 为repname/itemname删除Label某属性
	
	DELETE /label/：repname/：itemname

请求示例

	DELETE /label/NBA/bear

必选参数

	repname
	itemname

可选参数
	
	digest（数据精选）

----------

## 为repname/itemname更新Label某属性
	
	PUT /label/：repname/：itemname

请求示例

	PUT /label/NBA/bear

必选参数

	repname
	itemname

可选参数
	
	digest（数据精选）
	
