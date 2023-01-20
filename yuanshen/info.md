# 原神玩家基本信息

- [获取玩家基本信息](#获取玩家基本信息)

## 获取玩家基本信息

**国服：**

_请求方式：GET_

`https://api-takumi-record.mihoyo.com/game_record/app/genshin/api/index`

参数

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| role_id | num | 玩家UID | |
| server | str | cn_gf01 官服<br/>cn_qd01 渠道服 | |

**国际服：**

_请求方式：GET_

`https://bbs-api-os.hoyolab.com/game_record/genshin/api/index`

参数

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| role_id | num | 玩家UID | |
| server | str | os_asia 亚服<br/>os_euro 欧服<br/>os_usa 美服<br/>os_cht 港澳台服 | |

返回

根对象

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
