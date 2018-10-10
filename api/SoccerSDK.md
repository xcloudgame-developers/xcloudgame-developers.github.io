# 豪门足球对接文档
>## 流程图

![](/assets/img/soccer.jpg)

>## 更新：
UC接收Facebook信息接口添加参数：fbsource，last_name，first_name   -------------2018/8/21     
>## 数填写说明：

Y---->必须,N---非必须

>## 商户密钥（key）:
商户密钥是通讯中用户数据加密及签名验证过程中所需的加密钥匙，该钥匙由双方接口技术人员约定。

>## 接口前缀：
 地址：https://tecnofut.xcloudgame.com/


>## 调用登录及支付接口：
 H5页面地址：https://tecnofut.xcloudgame.com/Pt/landing<br/>
 下单接口（post）（https://域名/Pt/order）<br/>
 谷歌支付验证接口（post）（https://域名/Googlepay/check）<br/>
 苹果验证接口（post）（https://域名/Applepay/check）<br/>
 订单状态查询接口（post）（https://tecnofut.xcloudgame.com/Pt/checkorder）<br/>
 UC接收选服信息接口：https://tecnofut.xcloudgame.com/Pt/getsid<br/>
 UC接收Facebook信息接口：https://tecnofut.xcloudgame.com/Pt/getfb<br/>
 获取ios手机信息接口：https://tecnofut.xcloudgame.com/Pt/getios<br/>
 获取安卓手机信息接口：https://tecnofut.xcloudgame.com/Pt/getandroid<br/>
 找回密码接口（点击找回密码，跳转到浏览器，访问手机端网页版找回密码）

>## 返回值类型：
 json

>## 1、登录注册
 登录注册采用SDK调用H5登录注册页面方式展示登录注册页，在登录注册后给H5返回结果，H5根据结果与SDK交互
 >##### Status：200、100、101......108、109、（见返回值代码说明）
 >##### data：uid

 成功后 返回json串其中status状态码，data 用户信息

>## 2、SDK通知游戏客户端登录注册结果



>## 3、UC接收选服信息接口

参数名      | 参数类型 | 最大长度     | 是否必填 | 描述 |
---        | ---     | ---         | ---     | --- |
uid        | string  | 20          | Y       | 用户UID |
sid        | int     | 10          | Y       | 游戏服ID |
gid        | int     | 10          | Y       | 游戏编号 |
er         | string  | 50          | Y       | 创建gid的入口（游戏下载渠道） |
time       | int     | 11          | Y       | 操作时间 unix 时间戳（以秒为单位) |
sign       | String  | 50          | Y       | 数字签名：双方需要验证此信息的正确性 |

>##### 签名方法

所有字段按照字典顺序排序后经过两次md5加密 sign=md5(md5("key1=value1&key2=value2&$key")) 加密key直接拼接在字符串后

>##### Status：200、100、101......108、109、（见返回值代码说明）

成功后 返回json串其中status状态码

安卓获取IMEI参考：https://blog.csdn.net/u013059863/article/details/49847109


>## UC接收Facebook信息接口

参数名       | 参数类型 | 最大长度     | 是否必填 | 描述 |
---          | ---     | ---         | ---     | --- |
fbid         | String  | 50          | Y       | facebookID |
fbmail       | String  | 50          | N       | facebook email |
fbname       | String  | 50          | Y       | facebook fbname   |
last_name    | String  | 50          | Y       | facebook last_name |
first_name   | String  | 50          | Y       | facebook first_name |
busid        | String  | 50          | Y       | facebook token_for_business (facebook 唯一标识) |
channel_from | String  | 50          | Y       | 下载渠道 |
gid          | int     | 10          | Y       | 游戏编号 |
time         | int     | 11          | Y       | 操作时间 unix 时间戳（以秒为单位) |
sign         | String  | 50          | Y       | 数字签名：双方需要验证此信息的正确性 |

>##### 签名方法

所有字段按照字典顺序排序后经过两次md5加密 sign=md5(md5("key1=value1&key2=value2&$key")) 加密key直接拼接在字符串后

>##### Status：200、100、101......108、109、（见返回值代码说明）
>##### data: uid
成功后 返回json串其中status状态码,uid为用户ID



>## 接收ios设备信息接口 

参数名       | 参数类型 | 最大长度     | 是否必填 | 描述 |
---          | ---     | ---         | ---     | --- |
devicename   | String  | 50          | Y       | 设备名称（XXX的手机） |
sysname      | String  | 50          | N       | 系统名称（iPhone OS） |
sysversion   | String  | 50          | Y       | 系统版本（9.2）  |
deviceuuid   | String  | 50          | Y       | 设备唯一标识 |
devicemodel  | String  | 50          | Y       | 手机类型（iPhone 6 plus） |
ua           | String  | 50          | Y       | 客户ua |
ip           | String  | 50          | Y       | 客户ip |
time         | int     | 11          | Y       | 操作时间 unix 时间戳（以秒为单位) |
sign         | String  | 50          | Y       | 数字签名：双方需要验证此信息的正确性 |

>##### 签名方法

所有字段按照字典顺序排序后经过两次md5加密 sign=md5(md5("key1=value1&key2=value2&$key")) 加密key直接拼接在字符串后

>##### Status：200、100、101......108、109、（见返回值代码说明）

成功后 返回json串其中status状态码



>## 接收安卓设备信息接口

参数名       | 参数类型 | 最大长度     | 是否必填 | 描述 |
---          | ---     | ---         | ---     | --- |
imei   | String  | 50          | Y       | IMEI号 |
model      | String  | 50          | N       | 手机型号 |
width   | String  | 50          | Y       | 手机内置分辨率getWidth  |
height   | String  | 50          | Y       | getHeight |
simoperatornam  | String  | 50          | Y       | 运营商名字 |
time         | int     | 11          | Y       | 操作时间 unix 时间戳（以秒为单位) |
sign         | String  | 50          | Y       | 数字签名：双方需要验证此信息的正确性 |

>##### 签名方法

所有字段按照字典顺序排序后经过两次md5加密 sign=md5(md5("key1=value1&key2=value2&$key")) 加密key直接拼接在字符串后

>##### Status：200、100、101......108、109、（见返回值代码说明）

成功后 返回json串其中status状态码


>## 下单接口
   
参数名      | 参数类型 | 最大长度     | 是否必填 | 描述 |
---        | ---     | ---         | ---     | --- | 
uid        | string     | 20          | Y       | 用户UID | 
sid        | int     | 10          | Y       | 游戏服ID | 
gid        | int     | 10          | Y       | 游戏编号 | 
app_id     | string  | 20          | Y       | app编号 |
game_order | string  | 20          | Y       | 游戏订单号 |
amount     | float   |保留两位小数   | Y       | 订单金额 |
currency   | 金额币种  | 金额币种    | Y       | 币种（e.g. BRL）|
game_money | int     | 11          | Y       | 游戏币数量 |
game_good_id | int   | 10          | Y       | 套餐编号（无默认1）|
channel    | string  | 20          | Y       | 下单渠道 |
data       | string  | 100         | Y       | 传递参数 |
time       | int     | 11          | Y       | 用户注册时间 unix 时间戳（以秒为单位) |
sign       | String  | 50          | Y       | 数字签名：双方需要验证此信息的正确性 |

>##### 签名方法

所有字段按照键值排序后经过两次md5加密 sign=md5(md5("key1=value1&key2=value2&$key")) 加密key直接拼接在字符串后

>##### Status：200、100、101......108、109、（见返回值代码说明）

成功后 返回json串其中status状态码，order_id 是支付成功返回的订单号 


>## google 支付验证接口 
    
参数名      | 参数类型 | 最大长度     | 是否必填 | 描述 | 
---        | ---     | ---         | ---     | --- | 
uid        | string     | 20          | Y       | 用户UID | 
gid        | int     | 10          | Y       | 游戏编号 | 
package_name    | string  | 50          | Y       | 包名字  | 
product_id    | string  | 50          | Y       | google product  | 
app_id     | string  | 20          | Y       | app编号 | 
token      | string  | 20          | Y       | google 验证token | 
game_order | string  | 20          | Y       | 游戏订单号 | 
google_order | string  | 20          | Y       | 谷歌订单号 | 
time       | int     | 11          | Y       | 验证时间 unix 时间戳（以秒为单位) | 
sign       | string  | 50          | Y       | 数字签名：双方需要验证此信息的正确性 | 

>##### 签名方法

所有字段按照键值排序后经过两次md5加密 sign=md5(md5("key1=value1&key2=value2&$key")) 加密key直接拼接在字符串后


>## apple pay 支付验证接口 
 
参数名      | 参数类型 | 最大长度     | 是否必填 | 描述 | 
---        | ---     | ---         | ---     | --- | 
uid        | string     | 20          | Y       | 用户UID | 
gid        | int     | 10          | Y       | 游戏编号 | 
package_name    | string  | 50          | Y       | apple pay bid  | 
product_id    | string  | 50          | Y       | apple pay product  | 
token      | string  | 20          | Y       | apple pay 验证token | 
game_order | string  | 20          | Y       | 游戏订单号 | 
time       | int     | 11          | Y       | 验证时间 unix 时间戳（以秒为单位) | 
sign       | string  | 50          | Y       | 数字签名：双方需要验证此信息的正确性 | 

>##### 签名方法

所有字段按照键值排序后经过两次md5加密 sign=md5(md5("key1=value1&key2=value2&$key")) 加密key直接拼接在字符串后


>## 订单状态查询接口 
 
参数名      | 参数类型 | 最大长度     | 是否必填 | 描述 | 
---        | ---     | ---         | ---     | --- | 
uid        | string     | 20          | Y       | 用户UID | 
gid        | int     | 10          | Y       | 游戏编号 | 
game_order | string  | 20          | Y       | 游戏订单号 | 
sign       | string  | 50          | Y       | 数字签名：双方需要验证此信息的正确性 | 

>##### 签名方法

所有字段按照键值排序后经过两次md5加密 sign=md5(md5("key1=value1&key2=value2&$key")) 加密key直接拼接在字符串后


>##### Status：200、100、101......108、109、（见返回值代码说明）

成功后 返回json串其中status状态码,200为支付成功 

>## 发奖接口（非必须）

参数名      | 参数类型 | 最大长度     | 是否必填 | 描述 |
---        | ---     | ---         | ---     | --- |
uid        | string  | 20          | Y       | 用户UID |
sid        | int     | 10          | Y       | 游戏服ID |
gid        | int     | 10          | Y       | 游戏编号 |
app_id     | string  | 20          | Y       | app编号 |
game_order | string  | 20          | Y       | 游戏订单号 |
amount     | float   |保留两位小数   | Y       | 订单金额 |
currency   | 金额币种  | 金额币种    | Y       | 币种（e.g. USD）|
game_money | int     | 11          | Y       | 游戏币数量 |
game_good_id | int   | 10          | Y       | 套餐编号（无默认1）|
channel    | string  | 20          | Y       | 下单渠道 |
data       | string  | 100         | N       | 传递参数 |
sign       | String  | 50          | Y       | 数字签名：双方需要验证此信息的正确性 |

>##### 签名方法

所有字段按照键值排序后经过两次md5加密 sign=md5(md5("key1=value1&key2=value2&$key")) 加密key直接拼接在字符串后

>##### Status：200、100、101......108、109、（见返回值代码说明）



>## 错误码

错误码 | 描述 |
---   | ---  |
100   | email信息不全 |
101   | password信息不完整 |·
102   | email 已被注册 |
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
