# 手机SDK接口文档

>## 数填写说明：
   
Y---->必须,N---非必须

>## 商户密钥（key）:
商户密钥是通讯中用户数据加密及签名验证过程中所需的加密钥匙，该钥匙由双方接口技术人员约定。

>## 接口前缀：
 测试地址：http://XXX.xcloudgame.com/
 正式地址：http://XXX.xcloudgame.com/


>##接口调用地址及接口关系：
 同步接口（post方式）向游戏数据库写入ID信息，以标志用户身份。
 游戏登陆接口（post方式）（http://域名/Pt/login）
 游戏注册接口（post方式）（http://域名/Pt/registrar）

>## 返回值类型：
 json
 
 
 

>## 登录接口参数

参数名    | 参数类型 | 最大长度 | 是否必填 | 描述 |
---      | ---     | ---     | ---     | --- | 
email    | String  | 50      | Y       | 用户email |
password | String  | 50      | Y       | 用户密码 | 
app_id   | string  | 20      | Y       | App编号 |
time     | int     | 11      | Y       | 用户登录时间 unix 时间戳（以秒为单位） | 
sing     | String  | 50      | Y       | 数字签名：双方需要验证此信息的正确性 |

>#### sign=md5($email $password $app_id $time $key)

>##### Status：200、100、101......108、109、（见返回值代码说明）
 

 

>## 游客账户生成接口

参数名    | 参数类型 | 最大长度 | 是否必填 | 描述 |
email    | String  | 50      | Y       | 随机生成email |
password | String  | 50      | Y       | 随机生成用户密码 | 
time     | int     | 11      | Y       | 用户注册时间 unix 时间戳（以秒为单位) | 
sing     | String  | 50      | Y       | 数字签名：双方需要验证此信息的正确性 |

>##### sign=md5($email $password $time $key)

>##### Status：200、100、101......108、109、（见返回值代码说明）





>## 创建第三方授权账号接口
暂时无法提供




>## 注册接口参数

参数名    | 参数类型 | 最大长度 | 是否必填 | 描述 |
---      | ---     | ---     | ---     | --- | 
email    | String  | 50      | Y       | 用户email |
password | String  | 50      | Y       | 用户密码 | 
app_id   | string  | 20      | Y       | app编号 |
time     | int     | 11      | Y       | 用户注册时间 unix 时间戳（以秒为单位) |
sing     | String  | 50      | Y       | 数字签名：双方需要验证此信息的正确性 |

>##### sing=md5( $email $password $app_id $time $key)

>##### Status：200、100、101......108、109、（见返回值代码说明）



>## 游客绑定接口

参数名    | 参数类型 | 最大长度 | 是否必填 | 描述 |
---      | ---     | ---     | ---     | --- | 
email    | String  | 50      | Y       | 用户email |
password | String  | 50      | Y       | 用户密码 | 
uid      | string  | 20      | Y       | 游客标识 |
app_id   | string  | 20      | Y       | app编号 |
time     | int     | 11      | Y       | 用户注册时间 unix 时间戳（以秒为单位) |
sing     | String  | 50      | Y       | 数字签名：双方需要验证此信息的正确性 |

>##### sing=md5( $email $password $uid $app_id $time $key)

>##### Status：200、100、101......108、109、（见返回值代码说明）


>## 下单接口

参数名      | 参数类型 | 最大长度     | 是否必填 | 描述 |
---        | ---     | ---         | ---     | --- | 
uid        | int     | 11          | Y       | 用户UID |
sid        | int     | 10          | Y       | 游戏服ID | 
app_id     | string  | 20          | Y       | app编号 |
game_order | string  | 20          | Y       | 游戏订单号 |
amout      | float   |保留两位小数   | Y       | 订单金额 |
currency   | 金额币种  | 金额币种    | Y       | 币种（e.g. USD）|
game_money | int     | 11          | Y       | 游戏币数量 |
game_good_id | int   | 10          | Y       | 套餐编号（无默认1）|
channel    | string  | 20          | Y       | 下单渠道 |
data       | string  | 100         | N       | 传递参数 |
time       | int     | 11          | Y       | 用户注册时间 unix 时间戳（以秒为单位) |
sing       | String  | 50          | Y       | 数字签名：双方需要验证此信息的正确性 |

>##### sing=md5( $uid $game_order $amout $currency $game_good_id $Key)

>##### Status：200、100、101......108、109、（见返回值代码说明）

>## 发奖接口

参数名      | 参数类型 | 最大长度     | 是否必填 | 描述 |
---        | ---     | ---         | ---     | --- | 
uid        | int     | 11          | Y       | 用户UID |
sid        | int     | 10          | Y       | 游戏服ID | 
app_id     | string  | 20          | Y       | app编号 |
game_order | string  | 20          | Y       | 游戏订单号 |
amout      | float   |保留两位小数   | Y       | 订单金额 |
currency   | 金额币种  | 金额币种    | Y       | 币种（e.g. USD）|
game_money | int     | 11          | Y       | 游戏币数量 |
game_good_id | int   | 10          | Y       | 套餐编号（无默认1）|
channel    | string  | 20          | Y       | 下单渠道 |
data       | string  | 100         | N       | 传递参数 |
sing       | String  | 50          | Y       | 数字签名：双方需要验证此信息的正确性 |

>##### sing=md5( $uid $server_id $app_id $game_order $amout $currency $game_good_id $Key)

>##### Status：200、100、101......108、109、（见返回值代码说明）



>## 错误码

错误码 | 描述 | 
---   | ---  | 
100   | email信息不全 | 
101   | password信息不完整 |
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
114   | game_order为空或 | 
115   | game_money 或game_good_id有误 |
