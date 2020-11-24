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
>#### 链接：url/game/callback
>#### 返回值类型：json

>#### 参数

参数名 | 参数类型 | 最大长度 | 是否必填 | 描述 |
---  | --- | --- | --- | --- | 
uid | String | 50 | Y | 用户uid
sid | String | 50 | Y | 用户当前所在游戏服ID | 
logid | int | 11 | Y | 用户登陆log ID |
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
>#### 请求方式：调用父集js方法 （doclick）

参数名 | 参数类型 | 最大长度 | 是否必填 | 描述 |
---  | --- | --- | --- | --- | 
uid | bigint | 110 | Y | 用户编号
username | string | 110 | Y | 用户编号
sid | int | 11 | Y | 区ID | 
servername | string | 50 | Y | 区名称 | 
game_order | string | 20 | Y | 游戏订单号 |
product_id | string | 20 | Y | 游戏套餐编号 |
amount | float | 10 | Y | 订单金额 |
currency | string | 3 | Y | 订单号币种 例如BRL |
game_money | int | 10 | Y | 游戏币数量 |
product_desc | string | 100 | Y | 商品描述 | 
data | string | 100 | Y | 透传参数 | 
sign | String | 50 | Y | md5($uid $sid $game_order $game_money & $Key)注意加&符号

>### 
>#### 返回结果
>##### 成功 弹出下单页面


>## 创建或更新角色信息接口（平台提供，游戏调用）

>#### 请求方式：post
>#### 链接：url/game/userinfo
>#### 返回值类型：json

>#### 参数

参数名 | 参数类型 | 最大长度 | 是否必填 | 描述 |
---  | --- | --- | --- | --- | 
uid | String | 50 | Y | 用户uid |
sid | String | 50 | Y | 游戏服id |
rolename | String | 50 | Y | 角色名 |
rid | String | 50 | Y | 角色id |
profession | String | 50 | Y | 职业 |
dph | String | 50 | Y | DPH值 |
grade | String | 50 | Y | 等级 |
combat | String | 50 | Y | 战力 |
data | String | 50 | Y | data等级 | 
moditime | int | 11 | Y | 修改时间 | 
sign | String | 50 | Y | 字典顺序排序后md5($ke1=$val1 &$key2=$val2 ... & $key)注意加&符号

>### 
>#### 返回结果
>##### {
>#####   
>#####     "status": "200",//成功返回用户uid，失败为空
>##### }
>##### Status：200、100、101......108、109、（见返回值代码说明）


>## 埋点接口（平台提供，游戏调用）

>#### 请求方式：post
>#### 链接：url/game/buried

>#### 返回值类型：json

>#### 参数

参数名 | 参数类型 | 最大长度 | 是否必填 | 描述 |
---  | --- | --- | --- | --- | 
uid | String | 50 | Y | 用户uid |
sid | String | 50 | Y | 用户sid |
rid | String | 50 | Y | 用户角色id |
mainclass | String | 50 | Y | 主类 | 
subclass | String | 50 | Y | 主类 | 
moditime | int | 11 | Y | 修改时间 | 
sign | String | 50 | Y | md5($uid $sid $rid $mainclass $subclass $time & $key)注意加&符号



>## 游戏内分享js方法（平台提供，游戏调用）

>#### 方法名：share

参数名 | 参数类型 | 最大长度 | 是否必填 | 描述 |
---  | --- | --- | --- | --- | 
image | String | 50 | Y | 游戏内当前页面图片 |
type | String | 50 | Y | （facebook,google）|
time | int | 11 | Y | 回调时间 unix 时间戳（以秒为单位） | 

>### 
>#### 直接分享不需要返回结果


>## xcg平台账户登陆（平台提供，sdk调用）

>#### 请求方式：post
>#### 链接：url/Pt/getxcg_login
>#### 返回值类型：json

>#### 参数

参数名        | 参数类型 | 最大长度     | 是否必填 | 描述 |
---           | ---     | ---         | ---     | --- |
email        | String  | 50          | Y       | xcg账户 |
password     | String  | 50          | N       | xcg密码 |
entry_lang    | String  | 50          | Y       | pt/en |
entry_type    | String  | 50          | Y       | 入口类型 （ios：Appstore、androiddata:Google play）|
entry_name    | String  | 50          | Y       | 游戏包名 |
device        | int     | 10          | Y       | 设备信息（ios/android）json数据  不参与加密 |
source        | int     | 10          | Y       | 下载渠道  不参与加密 |
mainsource    | int     | 10          | Y       | 主渠道  不参与加密 |
subsource     | int     | 10          | Y       | 子渠道  不参与加密 |
time          | int     | 11          | Y       | 操作时间 unix 时间戳（以秒为单位) |
sign          | String  | 50          | Y       | 数字签名：双方需要验证此信息的正确性 |

>##### 签名方法

所有字段按照字典顺序排序后经过两次md5加密 sign=md5(md5("key1=value1&key2=value2&$key")) 加密key直接拼接在字符串后

>##### Status：200、100、101......108、109、（见返回值代码说明）
>##### data: uid
成功后 返回json串其中status状态码,uid为用户ID，token加密串


>## xcg平台账户注册（平台提供，sdk调用）

>#### 请求方式：post
>#### 链接：url/Pt/getxcg_reg
>#### 返回值类型：json

>#### 参数

参数名        | 参数类型 | 最大长度     | 是否必填 | 描述 |
---           | ---     | ---         | ---     | --- |
email        | String  | 50          | Y       | xcg账户 |
password     | String  | 50          | N       | xcg密码 |
entry_lang    | String  | 50          | Y       | pt/en |
entry_type    | String  | 50          | Y       | 入口类型 （ios：Appstore、androiddata:Google play）|
entry_name    | String  | 50          | Y       | 游戏包名 |
device        | int     | 10          | Y       | 设备信息（ios/android）json数据  不参与加密 |
source        | int     | 10          | Y       | 下载渠道  不参与加密 |
mainsource    | int     | 10          | Y       | 主渠道  不参与加密 |
subsource     | int     | 10          | Y       | 子渠道  不参与加密 |
time          | int     | 11          | Y       | 操作时间 unix 时间戳（以秒为单位) |
sign          | String  | 50          | Y       | 数字签名：双方需要验证此信息的正确性 |

>##### 签名方法

所有字段按照字典顺序排序后经过两次md5加密 sign=md5(md5("key1=value1&key2=value2&$key")) 加密key直接拼接在字符串后

>##### Status：200、100、101......108、109、（见返回值代码说明）
>##### data: uid
成功后 返回json串其中status状态码,uid为用户ID，token加密串


>## xcg平台账户忘记密码（平台提供，sdk调用）

>#### 请求方式：post
>#### 链接：url/Pt/get_reset
>#### 返回值类型：json

>#### 参数

参数名        | 参数类型 | 最大长度     | 是否必填 | 描述 |
---           | ---     | ---         | ---     | --- |
email        | String  | 50          | Y       | xcg账户 |
sign          | String  | 50          | Y       | 数字签名：双方需要验证此信息的正确性 |

>##### 签名方法

所有字段按照字典顺序排序后经过两次md5加密 sign=md5(md5("key1=value1&key2=value2&$key")) 加密key直接拼接在字符串后

>##### Status：200、100、101......108、109、（见返回值代码说明）
>##### data: uid
成功后 返回json串其中status状态码


>## 错误码

错误码 | 描述 |
---   | ---  |
200    |成功|
100   | email信息不全 |
101   | password信息不完整 |
102   | facebook账号重复 |
103   | password 错误 |
104   | time信息不完整 |
105   | sign信息不完整或信息有误 |
106   | 数据库操作失败 |
107   | 分区信息不全 |
108   | Key错误 |
109   | sid 有误 |
110   | app_id 有误 |
111   | game_order为空 |
112   | game_order重复 |
113   | amout 或currency错误 |
114   | 需求参数为空 |
115   | game_money 或game_good_id有误 |
116   | 用户不存在 |
117   | 系统错误 |
118    |渠道订单异常 |
119    |验证异常 |
120    |支付失败或未支付|
121    |当日已经分享过了|
122    |cpf已经验证过了|
123    |cpf错误|
124    |uid未注册|
125    |账号已被绑定或注册|
126    |cep 无效|
