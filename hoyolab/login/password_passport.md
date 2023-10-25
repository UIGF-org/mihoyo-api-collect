# 米哈游通行证密码登录

- [密码登录](#密码登录)
  - [操作步骤](#pwd-step)
  - [申请人机验证任务](#申请人机验证任务)
  - [获取Login Ticket](#获取login-ticket)

---

## 密码登录

<h3 id="pwd-step">操作步骤</h3>

1. [申请人机验证任务](#申请人机验证任务)，获取`gt`、`mmt_key`等验证数据
2. 登录[获取Login Ticket](#获取login-ticket)

### 申请人机验证任务

_请求方式：GET_

`https://webapi.account.mihoyo.com/Api/create_mmt`

**参数：**

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| scene_type | num | 暂不知道具体含义，可直接使用值 `1` | 必须传入，可参考[米哈游通行证密码登录页](https://user.mihoyo.com/#/login/password)使用的值为 `1` |
| now | num | 当前的Unix时间戳 | 必须传入 |
| reason | str | 调用API的网页链接 | 可参考[米哈游通行证密码登录页](https://user.mihoyo.com/#/login/password)使用`user.mihoyo.com%2523%252Flogin%252Fpassword`（已进行URL编码） |
| action_type | str | 登录方式<br>login_by_password 密码登录 | |
| t | num | 当前的Unix时间戳 | |
| account | str | 绑定手机或绑定邮箱 | |

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
| mmt_type | num | 验证任务类型<br>1 需要进行人机验证<br>0 无需进行人机验证 | |
| msg | str | 返回消息 | |
| scene_type | num | 与URL请求参数中的`scene_type`相同 | |
| status | num | 返回码<br>1 成功 | |

`data`对象→`mmt_data`对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| mmt_key | str | 验证任务 | 当 `mmt_data` 对象仅包含该字段时，说明不需要进行人机验证，可直接使用该值进行登录 |
| gt | str | 验证ID | 验证ID，即[极验文档](https://docs.geetest.com/gt4/deploy/server#%E8%AF%B7%E6%B1%82%E5%8F%82%E6%95%B0)中的`captchaId`，通常为服务器申请得到（服务器要求使用极验第四代行为验证时）；验证ID，通常为`6697d9dd2614c8a2a55752732494fd56`（服务器要求使用极验第三代行为验时） |
| challenge | str | 验证流水号 | 服务器要求使用极验第三代行为验时需要用到 |
| new_captcha | num | 极验验证码相关的参数，是否为新验证码类型的离线情况下使用 | 一般为 `1` |
| risk_type | str | 结合风控融合，指定验证形式<br>slide 拖动滑块完成拼图 | 服务器要求使用极验第三代行为验时不返回该项 |
| success | num | 是否成功<br>1 成功 | |
| use_v4 | bool | 是否使用[极验第4代适应性验证](https://www.geetest.com/adaptive-captcha) | 服务器要求使用极验第三代行为验时不返回该项 |

**备注：**

- 若直接访问该api，将有很大概率要求使用极验第三代行为验
- 通常首次申请验证任务返回的`mmt_data`对象只会包含`mmt_key`，不会返回`gt`等其他字段，这说明不需要进行人机验证，可直接使用`mmt_key`字段值进行登录（也可通过`mmt_type`判断）
- JSON返回数据的`mmt_data`对象中一些字段说明参考自[极验官方文档](https://docs.geetest.com/gt4/apirefer/api/web)

<details>
<summary>查看示例</summary>

```json
// 无需进行验证时：
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

// 需要进行验证时 - 要求使用第四代验证
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
// 需要进行验证时 - 要求使用第三代验证
{
    "code": 200,
    "data": {
        "mmt_data": {
            "challenge": "6697d9dd2614c8a2a55752732494fd56",
            "gt": "ae0942d9463f21fb73d27d49ed2f1154",
            "mmt_key": "gdfjQZgTpYAJbI7XpqV5vBtmFwHXttR2",
            "new_captcha": 1,
            "success": 1
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

**JSON请求：**

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| mmt_key | str | 验证任务 | |
| geetest_v4_data   | obj  | 验证结果数据                                                 | 即 [极验文档](https://docs.geetest.com/gt4/apirefer/api/web/#getValidate) 中 `getValidate()` 返回的对象<br>具体内容：[请求参数](https://docs.geetest.com/gt4/deploy/server#%E8%AF%B7%E6%B1%82%E5%8F%82%E6%95%B0)<br />若使用第三代验证时无需传入此项 |
| geetest_challenge | str | [极验第三代行为验的sdk返回]([geetest-Web-sensebot-api](https://docs.geetest.com/sensebot/apirefer/api/web#getValidate))的验证流水号 | 若使用第四代验证时无需传入此项                               |
| geetest_validate | str | [极验第三代行为验的sdk返回]([geetest-Web-sensebot-api](https://docs.geetest.com/sensebot/apirefer/api/web#getValidate))的validate | 若使用第四代验证时无需传入此项 |
| geetest_seccode | str | [极验第三代行为验的sdk返回]([geetest-Web-sensebot-api](https://docs.geetest.com/sensebot/apirefer/api/web#getValidate))的seccode | 若使用第四代验证时无需传入此项 |
| account | str | 要登录的账户 | |
| password | str | 密码（使用RSA + Base64加密或不加密） |      |
| is_crypto | bool | 密码是否被加密 |  |
| source | str | 登录操作来源 | 可参考 [米哈游通行证密码登录页](https://user.mihoyo.com/#/login/password) 使用的是 `user.mihoyo.com` |
| t | num | 当前的秒级时间戳 | |

`geetest_v4_data`对象：

| 字段           | 类型 | 内容           | 备注 |
| -------------- | ---- | -------------- | ---- |
| lot_number     | str  | 验证流水号     |      |
| captcha_output | str  | 验证输出信息   |      |
| pass_token     | str  | 验证通过标识   |      |
| gen_time       | str  | 验证通过时间戳 |      |
| captcha_id     | str  | 验证 ID        |      |
| sign_token     | str  | 验证签名       |      |


注：

若需加密密码，需要使用的RSA公钥[参见该提议](https://github.com/UIGF-org/mihoyo-api-collect/issues/1)。

加密的示例代码如下（Python，需要安装pycryptodome库）

```python
from Crypto.PublicKey import RSA
from Crypto.Cipher import PKCS1_v1_5 as Cipher_pkcs1_v1_5
import base64

public_key = '''-----BEGIN PUBLIC KEY-----
MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQDDvekdPMHN3AYhm/vktJT+YJr7
cI5DcsNKqdsx5DZX0gDuWFuIjzdwButrIYPNmRJ1G8ybDIF7oDW2eEpm5sMbL9zs
9ExXCdvqrn51qELbqj0XxtMTIpaCHFSI50PfPpTFV9Xt/hmyVwokoOXFlAEgCn+Q
CgGs52bFoYMtyi+xEQIDAQAB
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
| status | num | 返回码<br>1 成功 | |

`data`对象→`account_info`对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| account_id | num | 米游社账号ID | |
| area_code | str | 绑定手机的国家区号 | |
| create_time | num | 账号注册时间的Unix时间戳 | |
| email | str | 账号的绑定邮箱 | 该值的中间部分将以星号隐藏 |
| identity_code | str | 账号实名认证的身份证号 |  |
| is_adult | num | 实名认证对应信息是否为成年<br>1 是 | |
| is_email_verify | num | 绑定邮箱是否已验证<br>1 是 | |
| mobile | str | 账号的绑定手机 | 该值的中间部分将以星号隐藏 |
| real_name | str | 账号实名认证的真实姓名 | 该值的中间部分将以星号隐藏   |
| safe_area_code | str | 安全手机的国家区号 | 该字段已弃用 |
| safe_level | num | 安全级别 | 该账号的安全级别<br>3 高    |
| safe_mobile | str | 账号的安全手机 | 该字段已弃用 |
| weblogin_token | str | Login Ticket | 该字段也将出现在响应头的`Set-Cookie`字段中 |

**备注：**

可直接从响应Cookie中获取 Login Ticket

<details>
<summary>查看示例</summary>

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
      "weblogin_token": "QDDgghjghHydhdxyduf875UIDYDYq"
    },
    "msg": "成功",
    "status": 1
  }
}
```

</details>
