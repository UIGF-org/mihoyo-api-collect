# 米游社扫码登录

- [扫码登录](#扫码登录)
  - [操作步骤](#qrcode-step)
  - [生成二维码](#生成二维码)
  - [查询二维码扫描状态](#查询二维码扫描状态)

---

## 扫码登录

<h3 id="qrcode-step">操作步骤</h3>

1. [生成二维码](#生成二维码)，记录返回`data`对象的`url`，及其URL参数中的`ticket`字段（下称`ticket`）。
1. 生成二维码供用户扫描。
1. 不断[查询二维码扫描状态](#查询二维码扫描状态)。在用户扫描并确认登录后，获取`data`对象→`payload`对象的`raw`（即Game Token）。

### 生成二维码

**国服：**

_请求方式：POST_

`https://hk4e-sdk.mihoyo.com/hk4e_cn/combo/panda/qrcode/fetch`

**JSON请求：**

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| app_id | str | 登录的应用标识符<br>1 《崩坏3》<br>2 《未定事件簿》<br>4 《原神》<br>5 平台应用<br>7 《崩坏学园2》<br>8 《崩坏：星穹铁道》<br>9 云游戏<br>10 3NNN<br>11 PJSH<br>12 《绝区零》<br>13 HYG | 任何值都没有区别，但是必须传递此参数 |
| device | str | 设备ID | |

**JSON返回：**

根对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| retcode | num | 返回码 | |
| message | str | 返回消息 | |
| data | obj | 二维码指向的URL | |

`data`对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| url | str | 二维码指向的URL | 使用了Unicode转义 |

<details>
<summary>查看示例</summary>

```json
{
  "retcode": 0,
  "message": "OK",
  "data": {
    "url": "https://user.mihoyo.com/qr_code_in_game.html?app_id=7\u0026app_name=%E5%B4%A9%E5%9D%8F%E5%AD%A6%E5%9B%AD2&bbs=false\u0026biz_key=bh2_cn\u0026expire=1687002702\u0026ticket=648706ceff80ee663845a13d"
  }
}
```

</details>

<!-- **国际服：**

`未知` -->

### 查询二维码扫描状态

**国服：**

_请求方式：POST_

`https://hk4e-sdk.mihoyo.com/hk4e_cn/combo/panda/qrcode/query`

**JSON请求：**

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| app_id | str | 登录的应用标识符 | 与生成二维码时传递的值相同 |
| device | str | 设备ID | 与生成二维码时传递的值相同 |
| ticket | str | 生成二维码时从返回的URL的参数中，`ticket`字段的值 | |

**JSON返回：**

根对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| retcode | num | 返回码<br>-106 二维码已过期 | |
| message | str | 返回消息 | |
| data | obj | 二维码状态 | |

`data`对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| stat | str | 二维码状态<br>Init 未扫描<br>Scanned 已扫描<br>Confirmed 已确认 | |
| payload | obj | 登录数据 | |

`data`对象→`payload`对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| proto | str | 当前的数据类型<br>Raw 无数据<br>Account 已确认 | |
| raw | str | 确认登录之前为空字符串，之后则为米游社账号ID和Game Token（为JSON格式），其中的`token`字段即为账号的Game Token | |
| ext | str | 空字符串 | |

<details>
<summary>查看示例</summary>

```json
// 未扫描
{
  "retcode": 0,
  "message": "OK",
  "data": {
    "stat": "Init",
    "payload": {
      "proto": "Raw",
      "raw": "",
      "ext": ""
    }
  }
}

// 已扫描
{
  "retcode": 0,
  "message": "OK",
  "data": {
    "stat": "Scanned",
    "payload": {
      "proto": "Raw",
      "raw": "",
      "ext": ""
    }
  }
}

// 已过期
{
  "data": null,
  "message": "ExpiredCode",
  "retcode": -106
}

// 已确认
{
  "retcode": 0,
  "message": "OK",
  "data": {
    "stat": "Confirmed",
    "payload": {
      "proto": "Account",
      "raw": "{\"uid\":\"317832114\",\"token\":\"***\"}",
      "ext": ""
    }
  }
}
```
</details>

<!-- **国际服：**

`未知` -->