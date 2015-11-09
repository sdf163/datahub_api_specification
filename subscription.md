## 订阅

### 当前用户创建订阅 (41)

> POST /subscription/:reponame/:itemname

#### 输入参数

* USER-NAME in header

#### 输出样例

```
```

### 当前用户取消订阅 (41)

> GET /subscription/:reponame/:itemname

#### 输入参数

* USER-NAME in header

#### 输出样例

```
```

### 查询当前用户是否已经订阅某些dataitems (41)

> DELETE /subscription/:reponame/:itemname

#### 输入参数

* USER-NAME in header

#### 输出样例

```
```

### 取得当前用户的订阅列表 (42)

> GET /subscriptions

#### 输入参数

* USER-NAME in header

#### 输出样例

```
```

### 查询一个dataitem的订阅数 (51)

> GET /subscription-stat/:reponame/:itemname

#### 输入参数

> 无

#### 输出样例

```
```

### 查询一个respository下的dataitems的总订阅数 (52)

> GET /subscription-stat/:reponame

#### 输入参数

> 无

#### 输出样例

```
```


## Pull

### 需求者请求一个pull token (61)

> POST /transaction/:reponame/:itemname/:tag

#### 输入参数

* USER-NAME in header

#### 输出样例

```
```

### 供应者查询一个pull token的详细信息 (62)

> GET /transaction/:reponame/:itemname/:tag?token=xxxxx

#### 输入参数

* USER-NAME in header

#### 输出样例

```
```

### 查询需求者的流水 (71)

> GET /transactions/buyer

#### 输入参数

* USER-NAME in header

#### 输出样例

```
```

### 查询供应者的流水 (71)

> GET /transactions/seller

#### 输入参数

* USER-NAME in header

#### 输出样例

```
```

### 查询一个dataitem上的流水 (71)

> GET /transactions/dataitem/:reponame/:itemname

#### 输入参数

* USER-NAME in header

#### 输出样例

```
```

### 查询一个dataitem tag上的pull次 (72)

> GET /transaction-stat/:reponame/:itemname/:tag

#### 输入参数

* USER-NAME in header

#### 输出样例

```
```

### 查询一个dataitem上的tags上的总pull次 (72)

> GET /transaction-stat/:reponame/:itemname

#### 输入参数

> 无

#### 输出样例

```
```

### 查询一个respository上的tags的总pull次 (72)

> GET /transaction-stat/:reponame

#### 输入参数

> 无

#### 输出样例

```
```

