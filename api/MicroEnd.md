# 微端游戏接口文档

>## 数填写说明：
   
Y---->必须,N---非必须

>## 商户密钥（key）:
商户密钥是通讯中用户数据加密及签名验证过程中所需的加密钥匙，该钥匙由双方接口技术人员约定。

>## 接口前缀：
 测试地址：http://XXX.xcloudgame.com/
 正式地址：http://XXX. xcloudgame.com/
 
>## 必须实现接口

同步接口、

游戏登录接口、

游戏注册接口、
 
>### 注：其他接口实现视联运商各自的需求而定

>## 接口调用地址及接口关系：
>#### 同步接口（post方式）向游戏数据库写入ID信息，以标志用户身份。
>#### 游戏登陆接口（post方式）（http://域名/Pt/login）
>#### 游戏注册接口（post方式）（http://域名/Pt/registrar）

>## 返回值类型：
 json
 
 

>#### 同步接口参数

既将用户数据从商户导入到游戏数据库，后续所用到的user必须和此user一致。

参数名    | 参数类型 | 最大长度 | 是否必填 | 描述 |
---      | ---     | ---     | ---     | --- | 
uid      | int     | 11      | Y       | 用户编号 |
email    | String  | 50      | Y       | 用户email（用户账号)|
password | String  | 50      | Y       | 用户密码 | 
time     | int     | 11      | Y       | 用户注册时间 unix 时间戳（以秒为单位) | 
sing     | String  | 50      | Y       | 数字签名：双方需要验证此信息的正确性 |

>##### sign=md5($uid $email $password $time $key)

>##### Status：200、100、101......108、109、（见返回值代码说明）





>## 登录接口参数

参数名    | 参数类型 | 最大长度 | 是否必填 | 描述 |
---      | ---     | ---     | ---     | --- | 
email    | String  | 50      | Y       | 用户email
password | String  | 50      | Y       | 用户密码 | 
sid      | int     | 11      | Y       | 游戏服ID |
time     | int     | 11      | Y       | 用户登录时间 unix 时间戳（以秒为单位） | 
sing     | String  | 50      | Y       | 数字签名：双方需要验证此信息的正确性 |

>#### sign=md5($email $password $sid $time $key)

>##### Status：200、100、101......108、109、（见返回值代码说明）
 



>## 注册接口参数

参数名    | 参数类型 | 最大长度 | 是否必填 | 描述 |
---      | ---     | ---     | ---     | --- | 
email    | String  | 50      | Y       | 用户email |
password | String  | 50      | Y       | 用户密码 | 
time     | int     | 11      | Y       | 用户注册时间 unix 时间戳（以秒为单位) |
sing     | String  | 50      | Y       | 数字签名：双方需要验证此信息的正确性 |

>##### sing=md5( $email $password $time $key)

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
