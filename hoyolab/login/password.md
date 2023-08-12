# 米游社密码登录

- [密码登录](#密码登录)
  - [操作步骤](#sms-step)
  - [申请人机验证任务](#申请人机验证任务)
  - [获取 Login Ticket](#获取login-ticket)

---

## 密码登录

<h3 id="sms-step">操作步骤</h3>

1. [申请人机验证任务](#申请人机验证任务)，获取 `gt`，`mmt_key` 等任务数据
2. 使用任务数据完成人机验证，得到 `geetest_v4_data` 验证结果数据（参考：https://docs.geetest.com/gt4/apirefer/api/web ）
4. 使用账号密码 [获取 Login Ticket](#获取login-ticket)

### 申请人机验证任务

_请求方式：GET_

`https://webapi.account.mihoyo.com/Api/create_mmt`

**参数：**

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| scene_type | num | 暂不知道具体含义，可直接使用值 `1` | 可参考 [米哈游通行证密码登录页](https://user.mihoyo.com/#/login/password) 使用的值为 `1` |
| now | num | 当前的秒级时间戳 | |
| reason | str | 调用API的网页链接 | 可参考 [米哈游通行证密码登录页](https://user.mihoyo.com/#/login/password) 使用的是 `user.mihoyo.com%2523%252Flogin%252Fpassword`（已进行URL编码） |
| action_type | str | 登陆方式<br>`login_by_password` 密码登录 | |
| t | num | 当前的秒级时间戳 | |
| account | str | 要登录的账户 | |

**JSON返回：**

根对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| code | num | 返回码 | |
| data | obj | 返回数据 | |

`data`对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| mmt_data | obj | 极验验证任务数据 | |
| mmt_type | num | 验证任务类型<br>`1` 需要进行人机验证<br>`0` 无需进行人机验证 | |
| msg | str | 返回消息 | |
| scene_type | num | 与URL请求参数中的 `scene_type` 相同 | |
| status | num | 返回码<br>`1` 成功 | |

`data`对象→`mmt_data`对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| mmt_key | str | 验证任务 | 当 `mmt_data` 对象仅包含该字段时，说明不需要进行人机验证，可直接使用该值进行登录 |
| gt | obj | 验证ID | 验证ID，即 [极验文档](https://docs.geetest.com/gt4/deploy/server#%E8%AF%B7%E6%B1%82%E5%8F%82%E6%95%B0) 中的`captchaId`，极验后台申请得到 |
| new_captcha | num | 宕机情况下使用 | 一般为 `1` |
| risk_type | str | 结合风控融合，指定验证形式<br>`slide` 拖动滑块完成拼图 | |
| success | num | 是否成功<br>`1` 成功 | |
| use_v4 | bool | 是否使用极验第四代适应性验证 | 极验官网：https://www.geetest.com/adaptive-captcha |

**备注：**

- 通常首次申请验证任务返回的 `mmt_data` 对象只会包含 `mmt_key`，不会返回 `gt` 等其他字段，这说明不需要进行人机验证，可直接使用 `mmt_key` 字段值调用短信验证码发送API（也可通过 `mmt_type` 判断）
- JSON返回数据的 `mmt_data` 对象中一些字段说明参考自 [极验官方文档](https://docs.geetest.com/gt4/apirefer/api/web)
- 在2023年5月左右[米哈游通行证验证码登录页](https://user.mihoyo.com/#/login/captcha)从极验GT3升级至GT4，目前 [短信验证码发送](#发送短信验证码) 接口不再支持GT3验证结果，因此文档不包含GT3验证结果的使用方法

<details>
<summary>查看示例</summary>

- 请求：`https://webapi.account.mihoyo.com/Api/create_mmt?scene_type=1&now=1691855137471&reason=user.mihoyo.com%23%2Flogin%2Fpassword&action_type=login_by_password&account=<你的账户>&t=1691855137471`
- 返回：
  - 无需进行人机验证的情况：
    ```json
    {
      "code": 200,
      "data": {
        "mmt_data": {
          "mmt_key": "nAZzNc45p76J85nz3PRV6tjGp0SX9TDc"
        },
        "mmt_type": 0,
        "msg": "成功",
        "scene_type": 1,
        "status": 1
      }
    }
    ```
  - 需要进行人机验证的情况：
    ```json
    {
      "code": 200,
      "data": {
          "mmt_data": {
              "gt": "0b3dbaab0ad3f8344ab45342c3f3d909",
              "mmt_key": "3hfbcdJd5K9g23Fu0hRFA7DDDRRzKJdC",
              "new_captcha": 1,
              "risk_type": "slide",
              "success": 1,
              "use_v4": true
          },
          "mmt_type": 1,
          "msg": "成功",
          "scene_type": 1,
          "status": 1
      }
    }
    ```

</details>

### 获取Login Ticket

_请求方式：POST_

`https://webapi.account.mihoyo.com/Api/login_by_password`

**参数：**

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| account | str | 要登录的账户 | |
| password | str | 密码（使用RSA + Base64加密） | 见下 |
| is_crypto | bool | 是否被加密                   | 应该填true，否则无法通过 |
| source | str | 登录操作来源 | 可参考 [米哈游通行证验证码登录页](https://user.mihoyo.com/#/login/captcha) 使用的是 `user.mihoyo.com` |
| t | num | 当前的秒级时间戳 | |

注：

需要的RSA公钥：

```
-----BEGIN PUBLIC KEY-----
MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQDDvekdPMHN3AYhm/vktJT+YJr7\ncI5DcsNKqdsx5DZX0gDuWFuIjzdwButrIYPNmRJ1G8ybDIF7oDW2eEpm5sMbL9zs\n9ExXCdvqrn51qELbqj0XxtMTIpaCHFSI50PfPpTFV9Xt/hmyVwokoOXFlAEgCn+Q\nCgGs52bFoYMtyi+xEQIDAQAB
-----END PUBLIC KEY-----
```

加密的示例代码如下（Python，需要安装pycryptodome库）

```python
from Crypto.PublicKey import RSA
from Crypto.Cipher import PKCS1_v1_5 as Cipher_pkcs1_v1_5
import base64

public_key = '''-----BEGIN PUBLIC KEY-----
MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQDDvekdPMHN3AYhm/vktJT+YJr7\ncI5DcsNKqdsx5DZX0gDuWFuIjzdwButrIYPNmRJ1G8ybDIF7oDW2eEpm5sMbL9zs\n9ExXCdvqrn51qELbqj0XxtMTIpaCHFSI50PfPpTFV9Xt/hmyVwokoOXFlAEgCn+Q\nCgGs52bFoYMtyi+xEQIDAQAB
-----END PUBLIC KEY-----'''

def rsa_encrypt(message):
    cipher = Cipher_pkcs1_v1_5.new(RSA.importKey(public_key))
    cipher_text = base64.b64encode(cipher.encrypt(message.encode())).decode()
    return cipher_text
```



**JSON返回：**

根对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| code | num | 返回码 | |
| data | obj | 返回数据 | |

`data`对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| account_info | obj | 账号信息 | |
| msg | str | 返回消息 | |
| status | num | 返回码<br>`1` 成功 | |

`data`对象→`account_info`对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| account_id | num | 通行证ID | |
| area_code | str | 手机号区号 | 如 `+86` |
| create_time | num | 注册日期 | 格式为秒级时间戳 |
| email | str | 邮箱 | 将会打码显示 |
| identity_code | str | 身份证号 | 将会打码显示 |
| is_adult | num | 用户是否为成人<br>`1` 是 | |
| is_email_verify | num | 是否已验证邮箱<br>`1` 是 | |
| mobile | str | 手机号 | 将会打码显示 |
| real_name | str | 真实姓名 | 将会打码显示 |
| safe_area_code | str | 绑定手机的区号 | 如 `+86` |
| safe_level | num | 安全级别 | 已知该值为 `3` 时，米游社通行证页面中显示为 “高” |
| safe_mobile | str | 绑定手机 | 将会打码显示 |
| weblogin_token | str | 即Cookie中的 Login Ticket 字段 | 该字段也将出现在响应Cookie中 |

**备注：**

- 可直接从响应Cookie中获取 Login Ticket

<details>
<summary>查看示例</summary>

- 请求：`https://webapi.account.mihoyo.com/Api/create_mobile_captcha?mobile=18199998888&mobile_captcha=834265&source=user.mihoyo.com&t=1691827148574`
- 返回：
  ```json
  {
    "code": 200,
    "data": {
        "account_info": {
            "account_id": 123456789,
            "area_code": "+86",
            "create_time": 1614948789,
            "email": "user****mail@mail.com",
            "identity_code": "111************000",
            "is_adult": 1,
            "is_email_verify": 1,
            "mobile": "181****8888",
            "real_name": "**川",
            "safe_area_code": "+86",
            "safe_level": 3,
            "safe_mobile": "181****8888",
            "weblogin_token": "QDDFDSOykvnoXXXXXihEghhWDssd2efsdSDryCq"
        },
        "msg": "成功",
        "status": 1
    }
  }
  ```

</details>
