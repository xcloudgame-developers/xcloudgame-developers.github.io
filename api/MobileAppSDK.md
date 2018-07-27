# 手机SDK接口文档

>## 数填写说明：
   
Y---->必须,N---非必须

>## 商户密钥（key）:
商户密钥是通讯中用户数据加密及签名验证过程中所需的加密钥匙，该钥匙由双方接口技术人员约定。

>## 接口前缀：
 测试地址：http://XXX.xcloudgame.com/
 正式地址：http://XXX.xcloudgame.com/


>## 接口调用地址及接口关系：
 游戏登陆接口（post）（https://域名/Pt/login）<br/>
 生成游客账户（post）(https://域名/Pt/tourist)<br/>
 游戏注册接口（post)（https://域名/Pt/registrar）<br/>
 游客绑定（post）（https://域名/Pt/touristdb）<br/>
 下单接口（post）（https://域名/Pt/order）<br/>
 
 

>## 返回值类型：
 json
 
 
 

>## 登录接口参数

参数名    | 参数类型 | 最大长度 | 是否必填 | 描述 |
---      | ---     | ---     | ---     | --- | 
email    | String  | 50      | Y       | 用户email |
password | String  | 50      | Y       | 用户密码 | 
app_id   | string  | 20      | Y       | App编号 |
time     | int     | 11      | Y       | 用户登录时间 unix 时间戳（以秒为单位） | 
channel  | string  | 50      | N       | 用户渠道（例：App Store、Google play）|
sign     | String  | 50      | Y       | 数字签名：双方需要验证此信息的正确性 |

>#### sign=md5(md5("app_id=$app_id&channel=$channel&email=$email&password=$password&time=$time&$key"))  按字典顺序排列加密

>##### Status：200、100、101......108、109、（见返回值代码说明）
>##### data：uid
 

 

>## 游客账户生成接口

参数名    | 参数类型 | 最大长度 | 是否必填 | 描述 |
channel  | String  | 50      | N       | 用户渠道（例：App Store、Google play) |
app_id   | String  | 20      | Y       | App编号 | 
gid      | int     | 11      | Y       | 游戏ID（游戏1、游戏2......） | 
time     | int     | 11      | Y       | 用户注册时间 unix 时间戳（以秒为单位) | 
sign     | String  | 50      | Y       | 数字签名：双方需要验证此信息的正确性 |

>##### sign=md5(md5("app_id=$app_id&channel=$channel&gid=$gid&time=$time&$key"))

>##### Status：200、100、101......108、109、（见返回值代码说明）
>##### data: email、password、uid（用户唯一标识）




>## 创建第三方授权账号接口
暂时无法提供




>## 注册接口参数

参数名    | 参数类型 | 最大长度 | 是否必填 | 描述 |
---      | ---     | ---     | ---     | --- | 
email    | String  | 50      | Y       | 用户email |
password | String  | 50      | Y       | 用户密码 | 
channel  | string  | 50      | N       | 用户渠道（例：App Store、Google play) |
app_id   | string  | 20      | Y       | app编号 |
gid      | int     | 11      | Y       | 游戏ID（游戏1、游戏2......） | 
time     | int     | 11      | Y       | 用户注册时间 unix 时间戳（以秒为单位) |
sign     | String  | 50      | Y       | 数字签名：双方需要验证此信息的正确性 |

>##### sign=md5(md5("app_id=$app_id&channel=$channel&email=$email&gid=$gid&password=$password&time=$time&$key"))

>##### Status：200、100、101......108、109、（见返回值代码说明）
>##### data: email、password、uid



>## 游客绑定接口

参数名    | 参数类型 | 最大长度 | 是否必填 | 描述 |
---      | ---     | ---     | ---     | --- | 
email    | String  | 50      | Y       | 用户绑定的email |
password | String  | 50      | Y       | 用户绑定的密码 | 
uid      | string  | 20      | Y       | 游客标识 |
channel  | string  | 50      | N       | 用户渠道（例：App Store、Google play) |
app_id   | string  | 20      | Y       | app编号 |
time     | int     | 11      | Y       | 用户注册时间 unix 时间戳（以秒为单位) |
sign     | String  | 50      | Y       | 数字签名：双方需要验证此信息的正确性 |

>##### sign=md5(md5("app_id=$app_id&channel=$channel&email=$email&password=$password&time=$time&uid=$uid&$key"))

>##### Status：200、100、101......108、109、（见返回值代码说明）
>##### data: email、password、uid


>## 下单接口

参数名      | 参数类型 | 最大长度     | 是否必填 | 描述 |
---        | ---     | ---         | ---     | --- | 
uid        | int     | 11          | Y       | 用户UID |
sid        | int     | 10          | Y       | 游戏服ID | 
gid        | int     | 10          | Y       | 游戏编号 | 
app_id     | string  | 20          | Y       | app编号 |
game_order | string  | 20          | Y       | 游戏订单号 |
amount      | float   |保留两位小数   | Y       | 订单金额 |
currency   | 金额币种  | 金额币种    | Y       | 币种（e.g. BRL）|
game_money | int     | 11          | Y       | 游戏币数量 |
game_good_id | int   | 10          | Y       | 套餐编号（无默认1）|
channel    | string  | 20          | Y       | 下单渠道 |
data       | string  | 100         | N       | 传递参数 |
time       | int     | 11          | Y       | 用户注册时间 unix 时间戳（以秒为单位) |
sign       | String  | 50          | Y       | 数字签名：双方需要验证此信息的正确性 |

>##### sign=md5(md5("uid=$uid&sid=$sid&app_id=$app_id&gid=$gid&game_order=$game_order&amount=$amount&currency=$currency&game_good_id=$game_good_id&&$key")) 

>##### Status：200、100、101......108、109、（见返回值代码说明）

>## 发奖接口（非必须）

参数名      | 参数类型 | 最大长度     | 是否必填 | 描述 |
---        | ---     | ---         | ---     | --- | 
uid        | int     | 11          | Y       | 用户UID |
sid        | int     | 10          | Y       | 游戏服ID | 
gid        | int     | 10          | Y       | 游戏编号 | 
app_id     | string  | 20          | Y       | app编号 |
game_order | string  | 20          | Y       | 游戏订单号 |
amount      | float   |保留两位小数   | Y       | 订单金额 |
currency   | 金额币种  | 金额币种    | Y       | 币种（e.g. USD）|
game_money | int     | 11          | Y       | 游戏币数量 |
game_good_id | int   | 10          | Y       | 套餐编号（无默认1）|
channel    | string  | 20          | Y       | 下单渠道 |
data       | string  | 100         | N       | 传递参数 |
sign       | String  | 50          | Y       | 数字签名：双方需要验证此信息的正确性 |

>##### sign=md5(md5("uid=$uid&sid=$sid&app_id=$app_id&gid=$gid&game_order=$game_order&amount=$amount&currency=$currency&game_good_id=$game_good_id&&$key")) 

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
114   | 需求参数为空 | 
115   | game_money 或game_good_id有误 |
116   | 用户不存在 |
117   | 系统错误 |

