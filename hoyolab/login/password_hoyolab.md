# 米游社密码登录

- [密码登录](#密码登录)
  - [操作步骤](#操作步骤)
  - [获取设备指纹信息（device_fp）](#获取设备指纹信息)
  - [发送登录请求](#发送登录请求)

---

## 密码登录

### 操作步骤

1. [获取设备指纹信息](#获取设备指纹信息)，记录返回`data`对象的`device_fp。
2. 向服务器传入账号密码以获取登录信息。

### 获取设备指纹信息

**国服：**

_请求方式：POST_

`https://public-data-api.mihoyo.com/device-fp/api/getFp`

**JSON请求：**

| 字段       | 类型 | 内容                                | 备注                                                      |
| ---------- | ---- | ----------------------------------- | --------------------------------------------------------- |
| device_id  | str  | 设备id                              |                                                           |
| seed_id    | str  | 种子id                              | 可随机生成                                                |
| seed_time  | str  | 当前UNIX时间戳                      |                                                           |
| platform   | str  | 设备平台                            | 不同的设备平台需要包含的请求内容不同                      |
| device_fp  | str  | 设备指纹信息                        | 可随机生成                                                |
| app_name   | str  | 请求的应用名称<br />  bbs_cn 米游社 |                                                           |
| ext_fields | str  | 拓展字段                            | 为使用字符串包裹的 json 字段，其中必须包含 userAgent 字段 |

**JSON 返回：**

根对象：

| 字段    | 类型 | 内容             | 备注 |
| ------- | ---- | --------------- | ---- |
| retcode | num  | 返回码          | -502 传入的内容有误 |
| message | str  | 返回消息         |      |
| data    | obj  | 设备指纹 |      |

`data`对象：

| 字段   | 类型 | 内容               | 备注                |
| ------ | ---- | ------------------ | ------------------- |
| device_fp | str  | 设备指纹 |  |
| code | num | 回传的http状态码 |                     |
| msg | str | 错误消息 | |

<details>
<summary>查看示例</summary>

```json
{
    'data':{
            	'code': 200, 
           		'device_fp': 'ui33vcedffou', 
            	'msg': 'ok'
        	},
 	'message': 'OK',
 	'retcode': 0
}
```

</details>

### 获取登录信息

**国服：**

_请求方式：POST_

> _需要验证请求头_
>
> `x-rpc-app_id`：`bll8iq97cem8`
>
> `x-rpc-client_type`：`2`
>
> `x-rpc-game_biz`：`bbs_cn`
>
> `x-rpc-device_fp`
>
> `x-rpc-device_id`
>
> *其中`x-rpc-device_fp`的值为刚才获取的`device_fp`的值*

`https://passport-api.mihoyo.com/account/ma-cn-passport/app/loginByPassword`

**JSON请求：**

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| account | str | 要登录的账户 | 使用RSA + Base64加密，加密方式[详见该页面](https://github.com/Error063/mihoyo-api-collect/blob/main/hoyolab/login/password.md#%E8%8E%B7%E5%8F%96login-ticket) |
| password | str | 密码 | 使用RSA + Base64加密，加密方式[详见该页面](https://github.com/Error063/mihoyo-api-collect/blob/main/hoyolab/login/password.md#%E8%8E%B7%E5%8F%96login-ticket) |

**JSON返回：**

根对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| retcode | num | 返回码<br> | |
| message | str | 返回消息 | |
| data | obj | 账户x'x | |

`data`对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| login_ticket    | str  | Login Ticket             |      |
| need_realperson | str  | 是否要求用户进行实名认证 |      |
| token           | obj  | 包含cookie token?的对象  |      |
| user_info       | obj  | 用户信息                 |      |

`user_info`对象：

| 字段            | 类型 | 内容                                         | 备注         |
| --------------- | ---- | -------------------------------------------- | ------------ |
| account_name    | str  | 账户名                                       | 国服默认为空 |
| aid             | str  | Account ID                                   |              |
| area_code       | str  | 账户所绑定的电话号码对应的国家区号           |              |
| country         | str  | 国家                                         | 国服默认为空 |
| email           | str  | 账户所绑定的邮箱                             |              |
| identity_code   | str  | 身份证号码                                   |              |
| is_email_verify | str  | 邮箱是否认证通过<br />1 已认证<br />0 未认证 |              |
| links           | str  | 第三方绑定信息                               |              |
| mid             | str  | MiHoYo ID                                    |              |
| mobile          | str  | 账户所绑定的电话号码                         |              |
| realname        | str  | 用户的真实姓名                               |              |

<details>
<summary>查看示例</summary>

```json
{
    'data': {'login_ticket': '***',
          'need_realperson': False,
          'reactivate_info': {'required': False, 'ticket': ''},
          'realname_info': {'action_ticket': '',
                            'action_type': '',
                            'required': False},
          'token': {'token': '***',
                    'token_type': 1},
          'user_info': {'account_name': '',
                        'aid': '311526738',
                        'area_code': '+86',
                        'country': '',
                        'email': '***@***.****',
                        'identity_code': '******************',
                        'is_email_verify': 1,
                        'links': [{'email': '',
                                   'nickname': '***',
                                   'subType': '',
                                   'thirdparty': 'tp',
                                   'union_id': '***'}],
                        'mid': '0d5cf7piru_mhy',
                        'mobile': '***********',
                        'realname': '***',
                        'rebind_area_code': '',
                        'rebind_mobile': '',
                        'rebind_mobile_time': '0',
                        'safe_area_code': '',
                        'safe_mobile': ''}},
 'message': 'OK',
 'retcode': 0
}
```
</details>
