# 用户Token

- [Token](#token)
  - [通过Login Ticket获取SToken和LToken](#通过login-ticket获取stoken和ltoken)
  - [通过SToken获取Cookie Token](#通过stoken获取cookie-token)
  - [通过Game Token获取SToken](#通过game-token获取stoken)
  - [通过Game Token获取Cookie Token](#通过game-token获取cookie-token)
  - [通过Cookie Token获取Hk4e Token](#通过cookie-token获取hk4e-token)
- [Action Ticket](#action-ticket)
  - [通过SToken获取Action Ticket](#通过stoken获取action-ticket)
- [Auth Key](#auth-key)
  - [通过SToken获取账号Auth Key A](#通过stoken获取账号auth-key-a)
  - [通过SToken获取账号Auth Key B](#通过stoken获取账号auth-key-b)

---

## Token

### 通过Login Ticket获取SToken和LToken

**国服：**

_请求方式：GET_

`https://api-takumi.mihoyo.com/auth/api/getMultiTokenByLoginTicket`

**参数：**

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| token_types | num | 获取的Token的类型<br>1 仅SToken<br>2 仅LToken<br>3 SToken和LToken<br>4 无 | |
| login_ticket | str | 有效的Login Ticket | |
| uid | num | 对应的米游社账号UID | |

**JSON返回：**

根对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| retcode | num | 返回码 | |
| message | str | 返回消息 | |
| data | obj | Token | |

`data`对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| list | arr | SToken或LToken | |

`data`对象→`list`数组→对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| name | str | Token类型<br>ltoken LToken<br>stoken SToken | |
| token | str | Token值 | |


<details>
<summary>查看示例</summary>

```json
{
  "retcode": 0,
  "message": "OK",
  "data": {
    "list": [
      {
        "name": "stoken",
        "token": "***"
      },
      {
        "name": "ltoken",
        "token": "***"
      }
    ]
  }
}
```
</details>

### 通过SToken获取Cookie Token

**国服：**

_请求方式：GET_

> _需要验证Cookie_
>
> SToken

`https://api-takumi.mihoyo.com/auth/api/getCookieAccountInfoBySToken`

**参数：**

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| stoken | str | 有效的SToken | |
| uid | num | 对应的米游社账号UID | |

**JSON返回：**

根对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| retcode | num | 返回码 | |
| message | str | 返回消息 | |
| data | obj | Cookie Token和米游社UID | |

`data`对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| uid | str | 米游社UID | |
| cookie_token | str | SToken对应账号的Cookie Token | |

<details>
<summary>查看示例</summary>

```json
{
  "retcode": 0,
  "message": "OK",
  "data": {
    "uid": "***",
    "cookie_token": "***"
  }
}
```
</details>

### 通过Game Token获取SToken

**国服：**

_请求方式：POST_

> _需要验证请求头_
> 
> `x-rpc-app_id`

`https://api-takumi.mihoyo.com/account/ma-cn-session/app/getTokenByGameToken`

**JSON请求：**

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| account_id | num | 对应的米游社账号UID | |
| game_token | str | 有效的Game Token | |

**JSON返回：**

根对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| retcode | num | 返回码<br>-3005 未传递`x-rpc-app_id`请求头 | |
| message | str | 返回消息 | |
| data | obj | 账号的Token与隐私信息 | |

`data`对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| token | obj | 米游社账号的SToken | |
| user_info | obj | 米游社账号敏感信息 | 一些个人信息已被隐藏 |
| realname_info | | 待调查 | |
| need_realperson | bool | 待调查 | |

`data`对象→`token`对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| token_type | num | 1 | |
| token | str | 账号的SToken | |

`data`对象→`user_info`对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| aid | str | 米游社账号UID | |
| mid | str | 米游社MiHoYo ID | |
| account_name | str | 空字符串 | |
| email | str | 被隐藏的账号的绑定邮箱 | |
| is_email_verify | num | 绑定邮箱是否通过验证 | |
| area_code | str | 账号绑定手机的国家号码 | |
| mobile | str | 被隐藏的账号的绑定手机 | |
| safe_area_code | str | 账号安全手机的国家号码 | 历史遗留字段，现在安全手机的功能已经被移除了 |
| safe_mobile | str | 被隐藏的账号安全手机 | 历史遗留字段，现在安全手机的功能已经被移除了 |
| realname | str | 被隐藏的账号实名认证姓名 | |
| identity_code | str | 被隐藏的账号实名认证身份证号 | |
| rebind_area_code | str | 账号的换绑手机号的国家号码 | |
| rebind_mobile | str | 被隐藏的账号的换绑手机号 | |
| rebind_mobile_time | str | 0 | |
| links | arr | 待调查 | |

<details>
<summary>查看示例</summary>

```json
{
  "retcode": 0,
  "message": "OK",
  "data": {
    "token": {
      "token_type": 1,
      "token": "***"
    },
    "user_info": {
      "aid": "*******",
      "mid": "*******",
      "account_name": "",
      "email": "*********",
      "is_email_verify": 1,
      "area_code": "+86",
      "mobile": "***********",
      "safe_area_code": "",
      "safe_mobile": "",
      "realname": "***",
      "identity_code": "******************",
      "rebind_area_code": "",
      "rebind_mobile": "",
      "rebind_mobile_time": "0",
      "links": []
    },
    "realname_info": null,
    "need_realperson": false
  }
}
```
</details>

### 通过Game Token获取Cookie Token

**国服：**

_请求方式：GET_

`https://api-takumi.mihoyo.com/auth/api/getCookieAccountInfoByGameToken`

**参数：**

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| account_id | num | 对应的米游社账号UID | |
| game_token | str | 有效的Game Token | |

**JSON返回：**

根对象：

与[通过SToken获取Cookie Token](#通过stoken获取cookie-token)→根对象的结构相同。

<details>
<summary>查看示例</summary>

```json
{
  "retcode": 0,
  "message": "OK",
  "data": {
    "uid": "***",
    "cookie_token": "***"
  }
}
```
</details>

### 通过Cookie Token获取Hk4e Token

**国服：**

_请求方式：POST_

> _需要验证Cookie_
> 
> Account ID：`account_id`
> 
> Cookie Token：`cookie_token`

`https://api-takumi.mihoyo.com/common/badge/v1/login/account`

**JSON请求：**

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| region | str | 《原神》账号对应的服务器名称 | |
| uid | str | Cookie对应米游社账号已绑定的《原神》账号的UID | |
| game_biz | str | hk4e_cn | |

**JSON返回：**

根对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| retcode | num | 返回码<br>-1002 游戏账号未绑定Cookie对应的账号 | |
| message | str | 返回消息 | |
| data | obj | 《原神》账号的基础信息 | |

`data`对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| game | str | hk4e | |
| region | str | 《原神》账号对应的服务器的名称 | |
| game_uid | str | 《原神》账号的UID | |
| game_biz | str | hk4e_cn | |
| level | num | 《原神》账号的冒险等级 | |
| nickname | str | 《原神》账号昵称 | |
| region_name | str | 《原神》账号对应服务器的称呼 | |

<details>
<summary>查看示例</summary>

```json
{
  "retcode": 0,
  "message": "OK",
  "data": {
    "game": "hk4e",
    "region": "cn_gf01",
    "game_uid": "222681079",
    "game_biz": "hk4e_cn",
    "level": 58,
    "nickname": "※青衫入雨※",
    "region_name": "天空岛"
  }
}
```
</details>

## Action Ticket

### 通过SToken获取Action Ticket

**国服：**

_请求方式：GET_

> _需要验证Cookie_
>
> SToken

`https://api-takumi.mihoyo.com/auth/api/getActionTicketBySToken`

**JSON请求：**

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| action_type | str | 获取Action Ticket的用途<br>game_role 获取绑定游戏账号信息 | |

**JSON返回：**

根对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| retcode | num | 返回码 | |
| message | str | 返回消息 | |
| data | obj | 对应用途的Action Ticket与部分账号个人信息 | 个人信息已隐藏 |

`data`对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| ticket | str | Action Ticket | |
| is_verified | bool | 待调查 | |
| account_info | obj | 部分个人信息 | 个人信息已隐藏 |

`data`对象→`account_info`对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| is_realname | bool | 待调查 | |
| mobile | str | 绑定手机的手机号 | |
| safe_mobile | str | 安全手机的手机号 | 历史遗留字段，现在安全手机的功能已经被移除了 |
| safe_area_code | str | 安全手机的国家号码 | 历史遗留字段，现在安全手机的功能已经被移除了 |
| account_id | str | Cookie对应米游社账号的ID | |
| account_name | str | 空字符串 | |
| email | str | 被隐藏的绑定邮箱 | |
| is_email_verify | bool | 绑定邮箱是否已通过验证 | |
| area_code | str | 绑定手机的国家号码 | |
| real_name | str | 被隐藏的实名认证中的姓名 | |
| identify_code | str | 被隐藏的实名认证中的身份证号 | |
| create_time | str | 该米游社账号创建时间的Unix时间戳 | |
| create_ip | str | 待调查 | |
| change_pwd_time | sr | 待调查 | |
| nickname | str | 空字符串 | |
| user_icon_id | num | 待调查 | |
| safe_level | num | 该账号的安全等级<br>3 高 | |
| black_endtime | str | 待调查 | |
| black_note | str | 待调查 | |
| gender | num | 性别 | |
| real_stat | num | 待调查 | |
| apple_name | str | 待调查 | |
| sony_name | str | 待调查 | |
| tap_name | str | 待调查 | |
| reactivate_ticket | str | 待调查 | |

<details>
<summary>查看示例</summary>

```json
{
  "retcode": 0,
  "message": "OK",
  "data": {
    "ticket": "***",
    "is_verified": false,
    "account_info": {
      "is_realname": false,
      "mobile": "***********",
      "safe_mobile": "",
      "account_id": "317832114",
      "account_name": "",
      "email": "262****725@qq.com",
      "is_email_verify": true,
      "area_code": "+86",
      "safe_area_code": "",
      "real_name": "***",
      "identity_code": "******************",
      "create_time": "1646740732",
      "create_ip": "",
      "change_pwd_time": "0",
      "nickname": "",
      "user_icon_id": 0,
      "safe_level": 3,
      "black_endtime": "0",
      "black_note": "",
      "gender": 0,
      "real_stat": 0,
      "apple_name": "",
      "sony_name": "",
      "tap_name": "",
      "reactivate_ticket": ""
    }
  }
}
```

</details>

**国际服：**

`未知`

## Auth Key

### 通过SToken获取账号Auth Key A

**国服：**

_请求方式：POST_

> _需要验证Cookie_
>
> SToken

`https://api-takumi.miyoushe.com/account/auth/api/genAuthKey`

**JSON请求：**

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| game_biz | str | 米游社区域<br>bbs_cn 国服 | |

**JSON返回：**

根对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| retcode | num | 返回码<br>1002 请求体中有字段不正确 | |
| message | str | 返回消息 | |
| data | obj | Auth Key A | |

`data`对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| sign_type | num | 2 | |
| authkey_ver | num | 1 | |
| authkey | str | Auth Key A | |

<details>
<summary>查看示例</summary>

```json
{
  "retcode": 0,
  "message": "OK",
  "data": {
    "sign_type": 2,
    "authkey_ver": 1,
    "authkey": "***"
  }
}
```

</details>

**国际服：**

`未知`

### 通过SToken获取账号Auth Key B

用例：获取用户的游戏抽卡记录等API需要使用到Auth Key B。

**国服：**

_请求方式：POST_

> _需要验证请求头_
>
> `x-rpc-client_type`：`5`
>
> LK2`salt`
>
> `DS1`

> _需要验证Cookie_
>
> SToken

`https://api-takumi.miyoushe.com/binding/api/genAuthKey`
<!--`https://hk4e-sdk.mihoyo.com/hk4e_cn/combo/granter/login/genAuthKey`-->

**JSON请求：**

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| game_biz | str | 获取的Auth Key B的游戏<br>hk4e_cn 《原神》国服<br>hkrpg_cn 《崩坏：星穹铁道》国服<br> | |
| game_uid | num | 用户的游戏UID | |
| region | str | 用户游戏ID对应的服务器的名称 | |
| auth_appid | str | 获取的Auth Key B的类型<br>im_ccs 米游社<br>csc 米游社联系客服页面<br>webview_gacha 游戏抽卡记录 | |

**JSON返回：**

根对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| retcode | num | 返回码<br>1002 请求体中有字段不正确<br>1016 游戏账号未绑定Cookie对应的账号 | |
| message | str | 返回消息 | |
| data | obj | Auth Key B | |

`data`对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| sign_type | num | 2 | |
| authkey_ver | num | 1 | |
| authkey | str | Auth Key B | |

<details>
<summary>查看示例</summary>

```json
{
  "retcode": 0,
  "message": "OK",
  "data": {
    "sign_type": 2,
    "authkey_ver": 1,
    "authkey": "***"
  }
}
```

</details>

**国际服：**

`未知`