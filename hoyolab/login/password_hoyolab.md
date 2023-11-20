# 米游社密码登录

- [密码登录](#密码登录)
  - [操作步骤](#操作步骤)
  - [获取设备指纹（`device_fp`）](#获取设备指纹)
  - [发送登录请求](#发送登录请求)
  - [新设备验证](#新设备登录验证)

---

## 密码登录

### 操作步骤

1. [获取设备指纹信息](#获取设备指纹)，记录返回`data`对象的`device_fp`。
2. 向服务器传入账号密码以[获取登录信息](#发送登录请求)，获取响应头中所有`Set-Cookie`。可获取的Cookie有：Account ID、MiHoYo id、LToken（V2）、特定Cookie Token。

### 获取设备指纹

**国服：**

_请求方式：POST_

`https://public-data-api.mihoyo.com/device-fp/api/getFp`

**JSON请求：**

| 字段       | 类型 | 内容                                | 备注                                                      |
| ---------- | ---- | ----------------------------------- | --------------------------------------------------------- |
| device_id  | str  | 设备ID                              |                                                           |
| seed_id    | str  | 一般为随机值                              |                                           |
| seed_time  | str  | 当前的Unix时间戳                      |                                                           |
| platform   | str  | 设备平台<br>1 iOS<br>2 安卓<br>4 网页 | 不同的设备平台需要在`ext_fields`字段中填写的的内容不同                      |
| device_fp  | str  | 设备指纹                        | 在此处可随机生成                                                |
| app_name   | str  | 请求的应用标识符<br>bbs_cn 米游社 |                                                           |
| ext_fields | str  | 一些设备信息 | 为JSON字符串。若`platform`为`4`，则必须包含`userAgent`字段；若`platform`为`2`，则需要包含['cpuType', 'romCapacity', 'productName', 'romRemain', 'manufacturer', 'appMemory', 'hostname', 'screenSize', 'osVersion', 'aaid', 'vendor', 'accelerometer', 'buildTags', 'model', 'brand', 'oaid', 'hardware', 'deviceType', 'devId', 'serialNumber', 'buildTime', 'buildUser', 'ramCapacity', 'magnetometer', 'display', 'ramRemain', 'deviceInfo', 'gyroscope', 'vaid', 'buildType', 'sdkVersion', 'board']字段 |

<details>
<summary>查看示例</summary>

```json
{
    "device_id": "2d356b22f39b708c",
    "seed_id": "d81de6f4-6aa3-4e5f-b8e8-6a4f98e15a76",
    "seed_time": "1692248006205",
    "platform": "2",
    "device_fp": "38d7efe8b7f79",
    "app_name": "bbs_cn",
    "ext_fields": "{
    \"cpuType\":\"arm64-v8a\",
    \"romCapacity\":\"512\",
    \"productName\":\"ishtar\",
    \"romRemain\":\"459\",
    \"manufacturer\":\"Xiaomi\",
    \"appMemory\":\"512\",
    \"hostname\":\"xiaomi.eu\",
    \"screenSize\":\"1440x3022\",
    \"osVersion\":\"13\",
    \"aaid\":\"a945fe0c-5f49-4481-9ee8-418e74508414\",
    \"vendor\":\"中国电信\",
    \"accelerometer\":\"0.061016977x0.8362915x9.826724\",
    \"buildTags\":\"release-keys\",
    \"model\":\"2304FPN6DC\",
    \"brand\":\"Xiaomi\",
    \"oaid\":\"67b292338ad57a24\",
    \"hardware\":\"qcom\",
    \"deviceType\":\"ishtar\",
    \"devId\":\"REL\",
    \"serialNumber\":\"unknown\",
    \"buildTime\":\"1690889245000\",
    \"buildUser\":\"builder\",
    \"ramCapacity\":\"229481\",
    \"magnetometer\":\"80.64375x-14.1x77.90625\",
    \"display\":\"TKQ1.221114.001 release-keys\",
    \"ramRemain\":\"110308\",
    \"deviceInfo\":\"Xiaomi/ishtar/ishtar:13/TKQ1.221114.001/V14.0.17.0.TMACNXM:user/release-keys\",
    \"gyroscope\":\"7.9894776E-4x-1.3315796E-4x6.6578976E-4\",
    \"vaid\":\"4c10d338150078d8\",
    \"buildType\":\"user\",
    \"sdkVersion\":\"33\",
    \"board\":\"kalama\"
  }",
    "bbs_device_id": "b66a6178-f56d-30ed-97aa-297560c98fc1"
}
```

</details>

**JSON返回：**

根对象：

| 字段    | 类型 | 内容             | 备注 |
| ------- | ---- | --------------- | ---- |
| retcode | num  | 返回码<br>-502 传入的内容有误 | |
| message | str  | 返回消息         |      |
| data    | obj  | 设备指纹 |      |

`data`对象：

| 字段   | 类型 | 内容               | 备注                |
| ------ | ---- | ------------------ | ------------------- |
| device_fp | str  | 设备指纹 |  |
| code | num | 返回码 | |
| msg | str | 错误消息 | |

<details>
<summary>查看示例</summary>

```json
{
  "message": "OK",
  "retcode": 0,
  "data": {
    "code": 200,
    "device_fp": "ui33vcedffou",
    "msg": "ok"
  }
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
> `x-rpc-device_fp`：刚获取的设备指纹
>
> `x-rpc-device_id`：与上个步骤传递的设备ID相同

`https://passport-api.mihoyo.com/account/ma-cn-passport/app/loginByPassword`

**JSON请求：**

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| account | str | 将登录账户的绑定邮箱或绑定手机 | 使用RSA + Base64加密，加密方式[详见该页面](password_passport.md#获取login-ticket) |
| password | str | 将登录账户的密码 | 使用RSA + Base64加密，加密方式[详见该页面](password_passport.md#获取login-ticket) |

**JSON返回：**

根对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| retcode | num | 返回码 | -3235新设备登录([需手机短信验证](#新设备登录验证)) |
| message | str | 返回消息 |  |
| data | obj | 账号信息 | |

`data`对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| login_ticket    | str  | Login Ticket             | 在一些情况下没有该字段 |
| need_realperson | str  | 是否要求用户进行实名认证 |      |
| token           | obj  | 该账户的SToken（V2） | 在一些情况下没有该字段 |
| user_info       | obj  | 用户信息                 |      |
| reactivate_info | obj | 待调查 | |
| realname_info | obj | 待调查 | |

`data`对象→`user_info`对象：

| 字段            | 类型 | 内容                                         | 备注         |
| --------------- | ---- | -------------------------------------------- | ------------ |
| account_name    | str  | 账号名称                                       | 总是为空字符串 |
| aid             | str  | Account ID                                   |              |
| area_code       | str  | 账号所绑定的电话号码对应的国家区号           |              |
| country         | str  | 国家                                         | 总是为空字符串 |
| email           | str  | 账号所绑定的邮箱                             |              |
| identity_code   | str  | 账号的实名认证身份证号                                   |              |
| is_email_verify | str  | 邮箱是否通过认证<br>1 已认证<br>0 未认证 |              |
| links           | str  | 第三方绑定信息                               |              |
| mid             | str  | MiHoYo ID                                    |              |
| mobile          | str  | 账号的绑定手机                         |              |
| realname        | str  | 账号的实名认证姓名                               |              |

`data`对象→`token`对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | --- | ---- | ---- |
| token_type | num | 1 | |
| token | str | SToken（V2） | |

<details>
<summary>查看示例</summary>

```json
{
  "data": {
    "login_ticket": "***",
    "need_realperson": false,
    "reactivate_info": {
      "required": false,
      "ticket": ""
    },
    "realname_info": {
      "action_ticket": "",
      "action_type": "",
      "required": false
    },
    "token": {
      "token": "***",
      "token_type": 1
    },
    "user_info": {
      "account_name": "",
      "aid": "311526738",
      "area_code": "+86",
      "country": "",
      "email": "**********",
      "identity_code": "******************",
      "is_email_verify": 1,
      "links": [
        {
          "email": "",
          "nickname": "***",
          "subType": "",
          "thirdparty": "tp",
          "union_id": "***"
        }
      ],
      "mid": "******",
      "mobile": "***********",
      "realname": "***",
      "rebind_area_code": "",
      "rebind_mobile": "",
      "rebind_mobile_time": "0",
      "safe_area_code": "",
      "safe_mobile": ""
    }
  },
  "message": "OK",
  "retcode": 0
}
```
</details>    

### 新设备登录验证 


**国服：**  

前提->[获取登录信息接口响应头](#获取登录信息)(在recode返回-3235时)：

`x-rpc-verify`:  

```json 
{
  "action_ticket":"106ffc83feb64f5f9bfa9e0dd1c91dca",
  "verify_str":
    {
      "ticket":"23123433c12e1bf40f2a76bb2",
      "verify_type":"2"
    }
}
```


| 字段            | 类型 | 内容                                         | 备注         |
| --------------- | ---- | -------------------------------------------- | ------------ |
| action_ticket   | str  | 设备通过后用于请求获取用户登录信息              |               |  

`verify_str`根对象
| 字段            | 类型 | 内容                                         | 备注         |
| --------------- | ---- | -------------------------------------------- | ------------ |
| ticket          | str  | 用户验证标识符                                |  |
| verify_type     | str  | 验证类型                                      |              |  

<details>
<summary>查看示例</summary>


```json
// 响应头
// x-rpc-verify
{
  "action_ticket": "106ffc83f123asdzfa9e0dd1c91dca",
  "verify_str": "{\"ticket\":\"23123433c12e1bf40f2a76bb2\",\"verify_type\":\"2\"}"
}


// 响应体：
{
  "data": null,
  "message": "您正在新设备上登录，为保障您的账号安全，请先使用手机短信验证身份",
  "retcode": -3235
}
```
</details>  



_请求方式：POST_    

> _需要验证请求头_
>
> `x-rpc-app_id`：`bll8iq97cem8`
>
> `x-rpc-client_type`：`2`
>
> `x-rpc-game_biz`：`bbs_cn`
>
> `x-rpc-device_fp`：刚获取的设备指纹
>
> `x-rpc-device_id`：与上个步骤传递的设备ID相同  


`https://passport-api.mihoyo.com/account/ma-cn-verifier/verifier/createMobileCaptchaByActionTicket`   

**JSON请求：**  

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| action_ticket | str | 登录信息响应体中的ticket |  |
| action_type | str | 操作 |此处为verify_for_component |


<details>  
<summary>查看示例</summary>

```json
{
  "action_ticket":"fbca6ce757964296be7b0d0a3c558c5c",
  "action_type":"verify_for_component"
}
```
</details>


**JSON返回：**
| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| retcode | num | 返回码 | 为-3101触发人机验证 |
| message | str | 返回信息 |  |


<details>
<summary>查看示例</summary>

```json
{
  "retcode":0,
  "message":"OK",
  "data":{}
}
```
</details>


**触发人机验证：**  

**响应头**  
[参考极验文档](https://docs.geetest.com/gt4/deploy/server#%E8%AF%B7%E6%B1%82%E5%8F%82%E6%95%B0)


`x-rpc-aigis`: 

```json
{
  "session_id":"12131231231aa028d9c",
  "mmt_type":1,
  "data":
        {
          "success":1,
          "gt":"123123123123123b162892",
          "challenge":"123123123123ea064ed3a76",
          "new_captcha":1
        }
}
```

#### 设备验证请求  

_请求方式：POST_  

`https://passport-api.mihoyo.com/account/ma-cn-verifier/verifier/verifyActionTicketPartly`

**json请求**  

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| action_ticket | str | 响应体下verify_str的ticket参数 |  |
| action_type | str | 操作 |此处为verify_for_component |
| verify_method | num | 验证模式 | 此处参考米游社为1 |
| mobile_captcha | str | 设备接收到的验证码 |  |  


<details>
<summary>查看示例</summary>

```json
{
  "action_ticket":"23123433c12e1bf40f2a76bb2",
  "action_type":"verify_for_component",
  "verify_method":1,
  "mobile_captcha":"980243"
}
```
</details>


**JSON返回：**
| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| retcode | num | 返回码 |  |
| message | str | 返回信息 |  |


<details>
<summary>查看示例</summary>

```json
{
  "retcode":0,
  "message":"OK",
  "data":{}
}
```
</details>


#### 通过Ticket获取登录信息
_请求方式：POST_   

`https://passport-api.mihoyo.com/account/ma-cn-passport/app/checkRiskVerified`

**json请求**

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| action_ticket | str | 响应体下的action_ticket |  |

<details>
<summary>查看示例</summary>

```json
{
  "action_ticket":"106ffc83f123asdzfa9e0dd1c91dca"
}
```
</details>

**JSON返回：**

与[获取登录信息](#获取登录信息)一致




