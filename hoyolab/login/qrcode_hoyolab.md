# 米游社扫码登录

- [扫码登录](#扫码登录)
  - [操作步骤](#操作步骤)
  - [生成二维码](#生成二维码)
  - [查询二维码扫描状态](#查询二维码扫描状态)

---

## 扫码登录

### 操作步骤

1. [生成二维码](#生成二维码)，记录返回`data`对象的`url`，和`data`对象的`ticket`字段（下称`ticket`）。
2. 生成二维码供用户扫描。
3. 不断[查询二维码扫描状态](#查询二维码扫描状态)。在用户扫描并确认登录后，获取请求头中所有`Set-Cookie`。可获取的Cookie有：Account ID、MiHoYo id、LToken、特定Cookie Token。

### 生成二维码

**国服：**

_请求方式：POST_

> _需要验证请求头_
>
> `x-rpc-app_id`：`bll8iq97cem8`
>
> `x-rpc-device_id`

`https://passport-api.miyoushe.com/account/ma-cn-passport/web/createQRLogin`

**JSON 返回：**

根对象：

| 字段    | 类型 | 内容             | 备注 |
| ------- | ---- | --------------- | ---- |
| retcode | num  | 返回码          | -3001 请求头缺少部分参数 |
| message | str  | 返回消息         |      |
| data    | obj  | 二维码指向的 URL |      |

`data`对象：

| 字段   | 类型 | 内容               | 备注                |
| ------ | ---- | ------------------ | ------------------- |
| url    | str  | 二维码指向的URL   | 经过Unicode转义 |
| ticket | str  | 查询扫码状态的参数 |                     |

<details>
<summary>查看示例</summary>

```json
{
  "retcode": 0,
  "message": "OK",
  "data": {
    "url": "https://user.mihoyo.com/login-platform/mobile.html?expire=1693555708\u0026tk=e8a6448c-6596-461c-884a-98fe84bd675b\u0026token_types=4#/login/qr",
    "ticket": "e8a6448c-6596-461c-884a-98fe84bd675b"
  }
}
```

</details>

### 查询二维码扫描状态

**国服：**

_请求方式：POST_

> _需要验证请求头_
>
> `x-rpc-app_id`：`bll8iq97cem8`
>
> `x-rpc-device_id`

`https://passport-api.miyoushe.com/account/ma-cn-passport/web/queryQRLoginStatus`

**JSON请求：**

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| ticket | str | 生成二维码时，返回数据中`ticket`字段的值 | |

**JSON返回：**

根对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| retcode | num | 返回码 | -3001 请求头缺少参数<br>-3501 二维码已过期<br>-3505 用户取消扫码 |
| message | str | 返回消息 | |
| data | obj | 二维码状态 | |

`data`对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| app_id | str | 请求时的`app_id`参数 | |
| client_type | num | 客户端类型 | |
| created_at | str | 创建时间戳 | |
| need_realperson | bool | | |
| realname_info | obj | | 确认登录之前为空 |
| scanned_at | str | 扫码时间戳 | 扫描之前为空 |
| status | str | 二维码状态 | Created 未扫描<br>Scanned 已扫描<br>Confirmed 已确认 |
| tokens | arr | | 总是为空 |
| user_info | obj | 登录用户的信息 | 确认登录之前为空 |

<details>
<summary>查看示例</summary>

```json
// 未扫描
{
    "retcode": 0,
    "message": "OK",
    "data": {
        "status": "Created",
        "app_id": "bll8iq97cem8",
        "client_type": 4,
        "created_at": "1693555708",
        "scanned_at": "0",
        "tokens": [],
        "user_info": null,
        "realname_info": null,
        "need_realperson": false
    }
}

// 已扫描
{
    "retcode": 0,
    "message": "OK",
    "data": {
        "status": "Scanned",
        "app_id": "bll8iq97cem8",
        "client_type": 4,
        "created_at": "1693555708",
        "scanned_at": "1693555708",
        "tokens": [],
        "user_info": null,
        "realname_info": null,
        "need_realperson": false
    }
}

// 已过期
{
    "data": null,
    "message": "二维码已失效，请刷新后重新扫描",
    "retcode": -3501
}

//取消扫码
{
    "data": null,
    "message": "扫码登录已取消，重新生成二维码",
    "retcode": -3505
}

// 已确认
{
  "retcode": 0,
  "message": "OK",
  "data": {
    "status": "Confirmed",
    "app_id": "bll8iq97cem8",
    "client_type": 4,
    "created_at": "1693555708",
    "scanned_at": "1693555708",
    "tokens": [],
    "user_info": {"aid":"xxxx","mid":"xxxx".....},
    "realname_info": {
      "required": false,
      "action_type": "",
      "action_ticket": ""
    },
    "need_realperson": false
  }
}
```
</details>
