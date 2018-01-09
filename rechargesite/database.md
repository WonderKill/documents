
- 设备表

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
**14**  |**freequota** |**免费额度**| **int(8)**|**设备每天的免费使用额度**| 
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
freequota INT(8) NULL,
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
