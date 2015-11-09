# API 列表
[你好](#jump33)

[[get]] /select_lables

[post](#jump2) [put](#jump) [delete](#jump3) /select_lables/:lablename


----------
定义一个锚(id)： 跳转到的地方


## <span id="jump">查询符合精选名称的repname/itemname列表</span>
	
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
## <span id="jump2">查询符合精选名称的repname/itemname列表</span>

 <span id="jump3">查询符合精选名称的repname/itemname列表</span>

<span id = "jump33">hehe</span>