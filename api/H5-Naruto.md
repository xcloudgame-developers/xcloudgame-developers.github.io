# H5游戏接口文档
>## 流程图

![](/assets/img/H5login.jpg)

>## 数填写说明：
   
Y---->必须,N---非必须

>## 商户密钥（key）:
商户密钥是通讯中用户数据加密及签名验证过程中所需的加密钥匙，该钥匙由双方接口技术人员约定。
>## 接口前缀：
 测试地址：https://XXX.xcloudgame.com/
 正式地址：https://XXX.xcloudgame.com/
 登录页面地址：https://XXX.xcloudgame.com/（平台提供）



>## 登录成功进入游戏战斗服（游戏提供，平台调用）

>#### 请求方式：get

>#### 参数

参数名 | 参数类型 | 最大长度 | 是否必填 | 描述 |
---  | --- | --- | --- | --- | 
uid | String | 50 | Y | 用户uid |
logid | int | 11 | Y | 用户登陆log ID |
time | int | 11 | Y | 登录时间 unix 时间戳（以秒为单位） | 
sign | String | 50 | Y | md5($uid $sid $time & $key) 注意加&符号 |

>### 
>#### 返回结果
>#### 游戏战斗服



>## 选服成功回调（平台提供，游戏调用）

>#### 请求方式：post

>#### 返回值类型：json

>#### 参数

参数名 | 参数类型 | 最大长度 | 是否必填 | 描述 |
---  | --- | --- | --- | --- | 
uid | String | 50 | Y | 用户uid
sid | String | 50 | Y | 用户当前所在游戏服ID | 
time | int | 11 | Y | 回调时间 unix 时间戳（以秒为单位） | 
sign | String | 50 | Y | md5($uid $sid $time & $key)注意加&符号

>### 
>#### 返回结果
>##### {
>#####    "uid": "10019648178",//成功返回用户uid，失败为空
>#####     "status": "200",
>##### }
>##### Status：200、100、101......108、109、（见返回值代码说明）


>## 游戏发奖通知接口（游戏提供，平台调用）
>#### 请求方式：post
>#### 返回值类型：json

参数名 | 参数类型 | 最大长度 | 是否必填 | 描述 |
---  | --- | --- | --- | --- | 
uid | bigint | 110 | Y | 用户编号
sid | int | 11 | Y | 区ID | 
game_order | string | 20 | Y | 游戏订单号 |
game_money | int | 10 | Y | 游戏币数量 |
data | string | 100 | Y | 透传参数 | 
sign | String | 50 | Y | md5($uid $sid $game_order $game_money & $Key)注意加&符号

>### 
>#### 返回结果
>##### {
>#####   
>#####     "status": "200",//成功返回用户uid，失败为空
>##### }
>##### Status：200、100、101......108、109、（见返回值代码说明）


>## 下单接口 （平台提供，游戏调用）
>#### 请求方式：post
>#### 返回值类型：json

参数名 | 参数类型 | 最大长度 | 是否必填 | 描述 |
---  | --- | --- | --- | --- | 
uid | bigint | 110 | Y | 用户编号
sid | int | 11 | Y | 区ID | 
game_order | string | 20 | Y | 游戏订单号 |
product_id | string | 20 | Y | 游戏套餐编号 |
amount | float | 10 | Y | 订单金额 |
currency | string | 3 | Y | 订单号币种 例如BRL |
game_money | int | 10 | Y | 游戏币数量 |
data | string | 100 | Y | 透传参数 | 
sign | String | 50 | Y | md5($uid $sid $game_order $game_money & $Key)注意加&符号

>### 
>#### 返回结果
>##### {
>#####    "url": "xxxx",//成功返回下单跳转地址
>#####     "status": "200",//返回成功
>##### }
>##### Status：200、100、101......108、109、（见返回值代码说明）



>## 验证用户uid（平台提供，游戏调用）

>#### 请求方式：post

>#### 返回值类型：json

>#### 参数

参数名 | 参数类型 | 最大长度 | 是否必填 | 描述 |
---  | --- | --- | --- | --- | 
uid | String | 50 | Y | 用户uid
token | String | 50 | Y | 登录时sdk提供的token | 
time | int | 11 | Y | 回调时间 unix 时间戳（以秒为单位） | 
sign | String | 50 | Y | md5($uid $token $time & $key)注意加&符号


>## 游戏内分享js方法（平台提供，游戏调用）

>#### 方法名：share

参数名 | 参数类型 | 最大长度 | 是否必填 | 描述 |
---  | --- | --- | --- | --- | 
image | String | 50 | Y | 游戏内当前页面图片 |
type | String | 50 | Y | （facebook,google）|
time | int | 11 | Y | 回调时间 unix 时间戳（以秒为单位） | 

>### 
>#### 直接分享不需要返回结果


>## 错误码

错误码 | 描述 | 
---  | ---  | 
200 | 成功 |
100 | uid为空 |
101 | uid不存在 |
102 | sid为空 |
103 | sid不存在 |
104 | time为空 |
105 | sign信息不完整或信息有误 | 
106 | 数据库操作失败 | 
105 | Key错误 | 
