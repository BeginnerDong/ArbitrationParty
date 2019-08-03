# 仲裁帮项目开发文档

### 目录

- 功能概述
- 数据对照表


---

**1\. 功能概述**

&emsp;&emsp;项目主要功能包括：
包含用户管理、案件管理、进度管理、流水管理等基本模块；


---
**2\. 数据对照表**

### 通用字段说明

| 字段 | 类型 | 说明 |
| ------ | ------  | ------ | 
| id | int(11)| 主键：该数据ID |
| listorder | int(11) | 自定义排序 |
| img_array | varchar(100) | 图片组 |
| create_time | int(11) | 创建时间 |
| update_time | int(11) | 更新时间 |
| delete_time | int(11) | 删除时间 |
| thirdapp_id | int(11) | 关联thirdapp |
| user_no | varchar(255) | 关联user |
| user_type | tinyint(2) | 用户类型0.前端2.cms |
| status | tinyint(2) | 状态:1正常；-1删除 |



### user表

| 字段 | 类型 | 说明 |
| ------ | ------  | ------ | 
| nickname | varchar(255) | 微信昵称 |
| openid | varchar(255) | 微信openid |
| headImgUrl | varchar(9999) | 微信头像 |
| primary_scope | int(255) | 权限级别：90平台管理员;10用户 |
| user_type | tinyint(2) | 0,前端用户;2,cms用户; |
| user_no | varchar(255) | 用户编号 |
| behavior | int(2) | 0.公众号用户1.注册用户 |



### user_info表-update

| 字段 | 类型 | 说明 |
| ------ | ------  | ------ | 
| phone | varchar(255) | 电话 |
| level | tinyint(2) | 0.普通1.仲裁员 |
| name | varchar(255) | 收款姓名 |
| bank | varchar(100) | 开户行 |
| idCard | varchar(60) | 银行卡号 |
| score | int(11) | 信誉分，默认100 |



### label表

| 字段 | 类型 | 说明 |
| ------ | ------  | ------  | 
| title | varchar(40) | 菜单名称 |
| description| varchar(255) | 描述 |
| parentid| int(11) | 父级菜单ID |
| type | tinyint(2) |  1,menu;2,menu_item; |



### article表

| 字段 | 类型 | 说明 |
| ------ |  :------:  | ------  | 
| title | varchar(100) | 文章标题 |
| menu_id | int(11) | 关联label表 |
| description | varchar((255) | 描述 |
| content | text | 文章内容 |
| mainImg | varchar(9999) | 文章主图 |



### project表-new

| 字段 | 类型 | 说明 |
| ------ |  :------:  | ------  | 
| title | varchar(100) | 产品名称 |
| project_no | varchar(100) | 项目编号 |
| type | tinyint(2) | 类型1.cpa2.cps3.uv |
| price | decimal(10,2) | 项目金额 |
| phone | varchar(100) | 手机号 |
| content | text | 说明 |
| mainImg | text | 附件 |
| step | tinyint(2) | 1.进行中2.完结 |
| arbitration_step | tinyint(2) | 0.无1.进行中2.完结 |
| arbitration_type | tinyint(2) | 0.无1.平台仲裁2.全民仲裁 |
| arbitration_result | tinyint(2) | 0.无1.甲方胜2.乙方胜3.平局 |
| finish_time | int(11) | 完结时间 |
| deadline | int(11) | 仲裁截止时间 |

#### 请求参数
| partner_no | 对方user_no |
| role | tinyint(2) | 1.甲方2.乙方 |


### process表-new（type=1）

| 字段 | 类型 | 说明 |
| ------ |  :------:  | ------  | 
| type | tinyint(2) | 类型1.动态2.仲裁证据3.申请付款4.付款凭证5.流水 |
| project_no | varchar(100) | 项目编号 |
| content | text | 说明 |
| mainImg | text | 图片文档 |
| role | tinyint(2) | 1.甲方2.乙方 |



### process表-new（type=2）

| 字段 | 类型 | 说明 |
| ------ |  :------:  | ------  | 
| type | tinyint(2) | 类型1.动态2.仲裁证据3.申请付款4.付款凭证5.流水 |
| project_no | varchar(100) | 项目编号 |
| content | text | 证据 |
| mainImg | text | 图片文档 |
| role | tinyint(2) | 1.甲方2.乙方 |



### process表-new（type=3）

| 字段 | 类型 | 说明 |
| ------ |  :------:  | ------  | 
| type | tinyint(2) | 类型1.动态2.仲裁证据3.申请付款4.付款凭证5.流水 |
| project_no | varchar(100) | 项目编号 |
| content | text | 申请理由 |
| mainImg | text | 验收附件 |
| role | tinyint(2) | 1.甲方2.乙方 |
| price | decimal(10,2) | 付款金额 |
| fee | decimal(10,2) | 手续费 |
| pay_type | tinyint(2) | 0.无1.甲方2.乙方3.平摊 |



### process表-new（type=4）

| 字段 | 类型 | 说明 |
| ------ |  :------:  | ------  | 
| type | tinyint(2) | 类型1.动态2.仲裁证据3.申请付款4.付款凭证5.流水 |
| project_no | varchar(100) | 项目编号 |
| content | text | 证据 |
| mainImg | text | 图片文档 |
| role | tinyint(2) | 1.甲方2.乙方 |
| pay_status | tinyint(2) | （付款证据特有）0.未支付1.已支付 |



### process表-new（type=5）

| 字段 | 类型 | 说明 |
| ------ |  :------:  | ------  | 
| type | tinyint(2) | 类型1.动态2.仲裁证据3.申请付款4.付款凭证5.流水 |
| project_no | varchar(100) | 项目编号 |
| price | decimal(10,2) | 金额 |
| content | text | 说明 |
| role | tinyint(2) | 1.甲方2.乙方 |



### relation表-update

| 字段 | 类型 | 说明 |
| ------ |  :------:  | ------  | 
| relation_one | varchar(255) | 项目编号 |
| relation_one_table | varchar(255) | project |
| relation_two | varchar(255) | 用户NO |
| relation_two_table | varchar(255) | user |
| role | tinyint(2) | 1.甲方2.乙方 |
| arbitration | tinyint(2) | 0.未执行1.胜出2.败诉3.平局 |



### log表-update

| 字段 | 类型 | 说明 |
| ------ |  :------:  | ------ | 
| type | int(11) | 类别:1.仲裁投票 |
| project_no | varchar(100) | 关联project |
| role | tinyint(2) | 1.甲方2.乙方 |



### flow_log表-update

| 字段 | 类型 | 说明 |
| ------ |  :------:  | ------ | 
| type | int(11) | 类别:1.微信支付3.信誉分 |
| project_no | varchar(100) | 关联project |
| trade_info | varchar(255) | 说明 |



### thirdapp表-update

| 字段 | 类型 | 说明 |
| ------ | ------  | ------ | 
| name | varchar(255) | 姓名 |
| account | varchar(255) | 账号 |
| ratio | decimal(10,2) | 手续费（百分比） |


---