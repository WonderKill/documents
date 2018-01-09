
- 设备表 t_charge_device

序号 |	字段名称|	字段说明|	类型|	备注| 
---|---|---|---|---|
1	|gid	|自增|	bigint(20)	|主键|
2	|imei	|设备唯一标识	|char(15)	|盒子二维码包含的信息，和mac地址相同|
3	|deviceid	|设备编号	|varchar(8)	|根据gid补全到6位|
4	|webid 	|设备二维码编号	|varchar(64)	|此二维码编号来自微信|
5	|selfnumber|	设备自编号	|varchar(8)	|3位，由操作员激活设备时输入|
6	|type	|设备类型	|varchar(32)|	标明设备类型，四路机，可投币等|
7	|mark	|设备标识	|varchar(64)	|selfnumber+type+imei号后五位|
8	|chargetype|	充电桩类型|	tinyint(2)	|1表示慢充，2表示快充|
9	|version	|硬件版本号	|varchar(32)	|设备激活时发来|
10	|status|	状态	|tinyint(2)|	10表示在线，11表示离线，12表示下单中|
11	|activation	|激活状态	|tinyint（1）	|0表示未激活，1表示激活|
12	|siteid|网点编号	|bigint(20)	||
13	|sitename	|网点名称|	varchar(32)	||
**14**  |**freequota** |**免费额度**| **decimal(8,2)**|**设备每天的免费使用额度**| 
14	|simid	|SIM卡号,未启用|	char(15)||	
15	|simremain	|SIM卡余额，未启用|	decimal(8，2)	||
16	|gmtcreate	|创建时间	|datetime	||
17	|gmtactivation	|激活时间|	datetime	||

> sql语句

```
create table t_charge_device(
gid BIGINT(20) NOT NULL PRIMARY KEY AUTO_INCREMENT,
imei CHAR(15) NOT NULL UNIQUE,
deviceid VARCHAR(8) NULL UNIQUE,
webid VARCHAR(64) NULL UNIQUE,
selfnumber VARCHAR(8) NULL,
type VARCHAR(8) NULL,
mark VARCHAR(64) NULL,
chargetype TINYINT(2) NULL,
version VARCHAR(32) NULL,
status TINYINT(2) NOT NULL,
activation TINYINT(1) NOT NULL,
siteid BIGINT(20) NULL,
sitename VARCHAR(32) NULL,
freequota DECIMAL(8,2) NULL,
simid CHAR(15) NULL,
simremain DECIMAL(8,2) NULL,
gmtcreate DATETIME NULL,
gmtactivation DATETIME NULL,
INDEX MULTI(siteid, activation),
INDEX MULTI(sitename, activation),
INDEX(gmtactivation)
)
```
---

- 用户表  t_charge_user

序号 |	字段名称|	字段说明|	类型|	备注| 
---|---|---|---|---|
1	|	gid	|	自增	|	bigint(20)	|	主键	|
2	|	openid	|	用户唯一标识	|	varchar(64)	|	唯一键索引	|
3	|	nickname	|	用户昵称	|	varchar(64)	|		|
4	|	phone	|	用户电话	|	varchar(16)	|	唯一键索引	|
5	|	recharge	|	充值余额	|	decimal(8,2)	|		|
6	|	present	|	赠送余额	|	decimal(8,2)	|		|
7	|	sex	|	性别	|	tinyint(1)	|	1表示男性，2表示女性	|
8	|	language	|	语言	|	varchar(16)	|		|
9	|	city	|	城市	|	varchar(32)	|		|
10	|	province	|	省份	|	varchar(32)	|		|
11	|	country	|	国家	|	varchar(32)	|		|
12	|	headimgurl	|	头像	|	varchar(255)	|		|
13	|	gmtcreate	|	用户注册时间	|	datetime	|		|
14	|	gmtmodified	|	用户最近一次登入主页时间	|	datetime	|		|
**15**  | **usequota** | **用户当天已使用的免费额度** | **int(8)**|  |

> sql语句

```
create table t_charge_user(
gid BIGINT(20) NOT NULL PRIMARY KEY AUTO_INCREMENT,
openid VARCHAR(64) NOT NULL UNIQUE,
nickname VARCHAR(64) NULL,
phone VARCHAR(16) NULL UNIQUE,
recharge DECIMAL(8,2) NULL,
present DECIMAL(8,2) NULL,
sex TINYINT(1) NULL,
language VARCHAR(16) NULL,
city VARCHAR(32) NULL,
province VARCHAR(32) NULL,
country VARCHAR(32) NULL,
headimgurl VARCHAR(255) NULL, 
usequota DECIMAL(8,2) NULL,
gmtcreate DATETIME NULL,
gmtmodified DATETIME NULL
)

```
---

- 用户消费记录

序号 |	字段名称|	字段说明|	类型|	备注| 
---|---|---|---|---|
1	|	gid	|	自增	|	bigint(20)	|	主键	|
2	|	consumeorderno	|	订单号	|	varchar(32)	|	CPXF+YYYYMMDDHHmmss+3位随机数	|
3	|	openid	|	用户唯一标识	|	varchar(64)	|	和gmtcreate建联合索引	|
4	|	phone	|	用户手机号	|	varchar(16)	|	和gmtcreate建联合索引	|
5	|	imei	|	设备imei号	|	char(15)	|		|
6	|	deviceid	|	设备编号	|	varchar(6)	|		|
7	|	sitename	|	网点名称	|	varchar(32)	|		|
8	|	payment	|	**付费充电金额**	|	decimal(8,2)	|**订单中付费部分**		|
**9**   |  **freepayment** | **免费金额**  |  **decimal(8,2)**  | **订单中免费部分**    |
10	|	prebalance	|	消费前余额	|	decimal(8,2)	|		|
11	|	postbalance	|	消费后余额	|	decimal(8,2)	|		|
12	|	type	|	消费类型	|	tinyint(2)	|	20表示余额消费，21表示微信消费，22表示投币消费，用户未知	|
13	|	orderid	|	消费编号，与微信支付记录表orderid相同	|	varchar(32)	|		|
14	|	status	|	支付状态	|	tinyint(2)	|	23表示下单中， 66表示成功	|
15	|	gmtcreate	|	创建时间	|	datetime	|	索引	|
16	|	gmtmodified	|	第一次收到硬件回复时间	|	datetime	|		|

> sql语句

```
create table t_charge_consumerecord(
gid BIGINT(20) NOT NULL PRIMARY KEY AUTO_INCREMENT,
consumeorderno VARCHAR(32) NULL UNIQUE,
openid VARCHAR(64) NULL,
phone VARCHAR(16) NULL,
imei CHAR(15) NOT NULL,
deviceid VARCHAR(8) NOT NULL,
sitename VARCHAR(32) NOT NULL,
payment DECIMAL(8,2) NOT NULL,
freepayment DECIMAL(8,2) NOT NULL,
prebalance DECIMAL(8,2) NULL,
postbalance DECIMAL(8,2) NULL,
type TINYINT(2) NOT NULL,
orderid VARCHAR(32) NULL,
status TINYINT(2) NULL,
gmtcreate DATETIME NULL,
gmtmodified DATETIME NULL,
INDEX(gmtcreate),
INDEX MULTI_OPENID(openid, gmtcreate),
INDEX MULTI_PHONE(phone, gmtcreate),
INDEX MULTI_IMEI(imei, gmtcreate)
)

```
