# 鉴权

- [请求头](#请求头)
  - [米游社](#hoyolab_header)
    - [`x-rpc-app_version`](#x-rpc-app_version)
    - [`x-rpc-client_type`](#x-rpc-client_type)
    - [`x-rpc-sys_version`](#x-rpc-sys_version)
    - [`x-rpc-channel`](#x-rpc-channel)
    - [`x-rpc-device_name`](#x-rpc-device_name)
    - [`x-rpc-device_model`](#x-rpc-device_model)
    - [`x-rpc-device_fp`](#x-rpc-device_fp)
    - [`x-rpc-app_id`](#x-rpc-app_id)
    - [`x-rpc-verify_key`](#x-rpc-verify_key)
    - [`x-rpc-device_id`](#x-rpc-device_id)
    - [`X-Requested-With`](#x-requested-with)
    - [`Origin`](#origin)
    - [`Host`](#host)
    - [`Referer`](#referer)
    - [`User-Agent`](#user-agent)
    - [`DS`](#ds)
- [Cookie](#cookie)
  - [米游社](#hoyolab_cookie)
    - [LToken](#ltoken)
    - [SToken](#stoken)
    - [MiHoYo ID](#mihoyo-id)
    - [Account ID](#account-id)
    - [Login Ticket](#login-ticket)
    - [Cookie Token](#cookie-token)
    - [Action Ticket](#action-ticket)
    - [Auth Key](#auth-key)
    - [Game Token](#game-token)
    - [Hk4e Token](#hk4e-token)

---

大多数API需要验证请求头。

部分API（例如点赞文章、米游社签到福利、米游币等）需要使用Cookie鉴权。

## 请求头

<h3 id="hoyolab_header">米游社</h3>

大多数API需要验证的请求头：
- `x-rpc-app_version`
- `x-rpc-client_type`
- `x-rpc-device_id`
- `X-Requested-With`
- `Origin`
- `Referer`
- `Host`
- `DS`
- `User-Agent`
 
少数API才需要验证的额外的请求头：
- `x-rpc-device_fp`
- `x-rpc-challenge`
- `x-rpc-app_id`
- `x-rpc-verify_key`

可选请求头：
- `x-rpc-device_name`
- `x-rpc-device_model`
- `x-rpc-sys_version`
- `x-rpc-channel`
- `x-rpc-game_biz`

**说明：**

“需要验证请求头”意味着这个接口需要传递`Host`、`Referer`、`Origin`、`User-Agent`。此句之后才会标识需要传递的其它请求头。

出现`DS`类型时，需要传递`DS`、`x-rpc-app_version`、`x-rpc-client_type`、`X-Requested-With`。

#### `x-rpc-app_version`

米游社版本号，例如`2.50.1`。

与`DS`字段相关，`DS`生成需要`salt`，而每个米游社版本的`salt`都不同。

因此米游社版本只能使用对应的`salt`用于生成DS。

#### `x-rpc-client_type`

有`1`、`2`、`4`和`5`这些值。

_注：以下列表只是说明该请求头的值通常在哪些平台出现，并不是平台一定只使用对应的值。具体的值请查看接口说明的标注_

| 值 | 意义 | 备注 |
| -- | --- | ---- |
| 1 | 苹果端APP | 一般不需要使用 |
| 2 | 安卓端APP | |
| 4 | 网页端 | |
| 5 | 其它 | |

根据请求的API不同而变化。

将会在需要验证请求头的API进行标注。

与`DS`字段相关，`DS`生成需要`salt`，而不同的`x-rpc-client_type`对应该版本米游社的`salt`也不同。


#### `x-rpc-sys_version`

安卓系统（或iOS）大版本号，例如Android 13则为`13`。

#### `x-rpc-channel`

手机厂商，例如小米则为`xiaomi`。

#### `x-rpc-device_name`

手机厂商和手机型号，例如`Xiaomi M2101K9C`。

#### `x-rpc-device_model`

手机型号。

#### `x-rpc-device_fp`

发送POST请求至`https://public-data-api.mihoyo.com/device-fp/api/getFp`以获得。

#### `x-rpc-app_id`

为应用ID，具体值需查看请求头标识与[ID对照表](other/id.md#应用id)。

#### `x-rpc-verify_key`

一般为应用ID，具体值需查看请求头标识与[ID对照表](other/id.md#应用id)。

#### `x-rpc-device_id`

设备ID，由使用的设备决定。

在安卓设备上，一般为一串由`ANDROID_ID`生成的`UUID`，Kotlin （Java同理）中可以这样获取：

```kotlin
import android.content.Context
import android.provider.Settings
import java.util.UUID

@SuppressLint("HardwareIds")
fun getDeviceId(context: Context): String {
    val androidId = Settings.Secure.getString(context.contentResolver, Settings.System.ANDROID_ID)
    val uuid = UUID.nameUUIDFromBytes(androidId.toByteArray())
    return uuid.toString()
}
```
电脑上可以
```python
import uuid
def getDevice():
    return uuid.uuid4()
```

#### `X-Requested-With`

国内版APP为`com.mihoyo.hyperion`。

国际版APP为`com.mihoyo.hoyolab`。

#### `Origin`

请求网站的协议与主机名。

例如请求`https://api-takumi-record.mihoyo.com/game_record/app/genshin/api/index`（通过原神UID获取角色信息）则该字段为`https://api-takumi-record.mihoyo.com`。

#### `Host`

请求的网站的主机名。

例如请求`https://api-takumi.mihoyo.com/account/auth/api/webLoginByPassword`（网页登录米游社）则该字段为`api-takumi.mihoyo.com`。

#### `Referer`

在哪个网页发起的请求。

一般情况下，国内版APP：

若`x-rpc-client_type`为`5`，则为`https://webstatic.mihoyo.com`。

若`x-rpc-client_type`为`4`，则为`https://www.miyoushe.com`。

若`x-rpc-client_type`为`2`，则为`https://app.mihoyo.com`。

国际版APP：

若`x-rpc-client_type`为`5`，则为`https://webstatic-sea.hoyolab.com`。

若`x-rpc-client_type`为`4`，则为`https://www.hoyolab.com`。

若`x-rpc-client_type`为`2`，则为`https://www.hoyolab.com`

#### `User-Agent`

需要验证请求头的API的用户代理格式为`Mozilla/5.0 (Linux; Android 安卓系统大版本号; 手机型号 Build/TKQ1.220829.002; wv) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/108.0.5359.128 Mobile Safari/537.36 miHoYoBBS/米游社版本号`。

例如`Mozilla/5.0 (Linux; Android 13; M2101K9C Build/TKQ1.220829.002; wv) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/108.0.5359.128 Mobile Safari/537.36 miHoYoBBS/2.51.1`

#### `DS`

动态签名（Dynamic Sign），别称“数据签名（Data Sign）”“动态密钥（Dynamic Secret）”

大多数API需要验证请求头中的`DS`字段。

`DS`值通过一系列算法得出。

##### 生成`DS`

`DS`的生成方式由以下因素影响：

* 网页、中国版APP和国际版APP的生成算法不同。
* 请求头的`x-rpc-client_type`字段，每个值都有其对应的生成算法。

生成`DS`需要`salt`（为32个包含大写字母、小写字母、数字的字符串）。

`salt`在以下情况下不同：

* 网页、中国版APP和国际版APP使用的`salt`不同。
* 每个APP版本都存有其独有的`salt`。
* 请求头的`x-rpc-client_type`字段，每个值使用的`salt`不同。
* 少数API有其单独的`salt`（例如米游社签到福利）。

请在[这里](https://github.com/Kamisato-Ayaka-233/mihoyo-api-collect/issues/1)获取`salt`。


###### 中国版APP

`DS`有多个生成算法，分别为`DS1`和`DS2`。

**`DS2`**：

在请求头中的`x-rpc-client_type`为`5`时使用。

整体思路：

1. 获取当前的Unix时间戳（整数）。
1. 在100000到200000中选取随机整数，但是如果随机到100000，则加上542367，得到642367。
1. 若将发送POST请求，则将发送的数据转为JSON字符串并使用对象的键进行英文字母顺序排序，存储至变量（下文称`body`）。若将发送GET请求，则将URL参数进行英文字母顺序排序（键）后存储至变量（下文称`query`），例如URL参数为`server=cn_gf01&role_id=114514191`则结果为`role_id=222681079&server=cn_gf01`。若不需要传递数据或URL参数，则为空字符串。
1. 格式化字符串：`salt={salt值}&t={第1步的结果}&r={第2步的结果}&b={第3步的body}&q={第3步的query}`。
1. 将第4步的结果进行UTF-8编码，再进行MD5编码。
1. 格式化字符串：`{第1步的结果},{第2步的结果},{第5步的结果}`。

Python：
```python
import time
import random
from hashlib import md5
# JSON模块用于处理POST请求的JSON数据
# import json

# 将要使用的salt，此为4X salt
salt = "xV8v4Qu54lUKrEYFZkJhB8cuOh9Asafs"
# body和query一般来说不会同时存在
# 可以使用json库的dumps函数将对象转为JSON字符串
# body = json.dumps({"role": "123456789"}, sort_keys=True)
body = '{"role": "123456789"}'
# 可以使用urllib中的parse库的urlparse函数，传入URL，得到返回值中的query字段。
# 将其转为列表（通过str.split("&")），通过sorted函数来排序，再用"&".join来将其转为最终值
query = "&".join(sorted("server=cn_gf01&role_id=123456789".split("&")))

t = int(time.time())
r = random.randint(100000, 200000)
if r == 100000:
  r = 642367
# 也可以直接用更简单粗暴的方法
# r = random.randint(100001, 200000)
main = f"salt={salt}&t={t}&r={r}&b={body}&q={query}"
ds = md5(main.encode(encoding='UTF-8')).hexdigest()

final = f"{t},{r},{ds}" # 最终结果
```

JavaScript：
```javascript
import md5 from 'md5'

const salt = "xV8v4Qu54lUKrEYFZkJhB8cuOh9Asafs"
// body和query一般来说不会同时存在
// 可以使用内置的JSON.stringify函数将对象或数组转换为JSON字符串
// const body = JSON.stringify({role: "123456789"})
const body = '{"role": "123456789"}'
// 需要对URL参数进行排序
const query = "server=cn_gf01&role_id=123456789".split('&').sort().join('&')

const t = Math.floor(Date.now() / 1000)
let r = Math.floor(Math.random() * 100001 + 100000)
if (r == 100000) {
  r = 642367
}
// const r = Math.floor(Math.random() * 100001 + 100001)

const main = `salt=${salt}&t=${t}&r=${r}&b=${body}&q=${query}`
const ds = md5(main)

const final = `${t},${r},${ds}` // 最终结果
```

**`DS1`**：

在请求头中的`x-rpc-client_type`为`5`时使用。

整体思路：

1. 获取当前的Unix时间戳（整数）。
1. 在大写字母、小写字母、数字中随机抽出6个。
1. 格式化字符串：`salt={salt值}&t={第1步的结果}&r={第2步的结果}`。
1. 将第3步的结果进行UTF-8编码，再进行MD5编码。
1. 格式化字符串：`{第1步的结果},{第2步的结果},{第4步的结果}`。

Python：
```python
import time
import random
from hashlib import md5


lettersAndNumbers = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789'

# 将要使用的salt，此为2.35.2版本的K2 salt。
salt = "ZSHlXeQUBis52qD1kEgKt5lUYed4b7Bb"

t = int(time.time())
r = "".join(random.choices(lettersAndNumbers, k=6))
main = f"salt={salt}&t={t}&r={r}"
ds = md5(main.encode(encoding='UTF-8')).hexdigest()

final = f"{t},{r},{ds}" # 最终结果。
```

JavaScript：
```javascript
import md5 from 'md5'

const salt = "ZSHlXeQUBis52qD1kEgKt5lUYed4b7Bb"
const lettersAndNumbers = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789'

const t = Math.floor(Date.now() / 1000)
let r = ""
for (let i; i < 6; i++) {
  r += lettersAndNumbers[Math.floor(Math.random() * lettersAndNumbers.length)]
}

const main = `salt=${salt}&t=${t}&r=${r}`
const ds = md5(main)

const final = `${t},${r},${ds}` // 最终结果
```

## Cookie

一些API（例如文章点赞、签到和获取用户的游戏账号信息等API）需要登录账号，则表示为请求头Cookie的形式。

需要验证Cookie的API会进行标注。

若API无需登录账号，就不需要设置Cookie。

**API的Cookie标识格式**

像SToken，只有1种字段值，或是像LToken，2种字段值都被兼容，则只标识Cookie名。

```markdown
> _需要验证Cookie_
> 
> SToken
```

若像Account ID，有多种字段值，将会在其之后标识需要的字段名。若有多个兼容的字段或有多个值相同的字段，使用“、”分隔。

```markdown
> _需要验证Cookie_
> 
> Account ID：`account_id`、`account_id_v2`
```

<h3 id="hoyolab_cookie">米游社</h3>

需要哪些Cookie取决于以下因素：

* API是否要求登录账号。
* `x-rpc-client_type`的不同值。
* 一些API要求特殊的Cookie。

#### LToken

即`ltoken_v2`和`ltoken`。

`ltoken_v2`和`ltoken`并不总是使用相同的值，多用于查询用户的游戏账号信息。其被命名为“LToken（V1）”与“LToken（V2）”。

`ltoken_v2`必须与[`ltmid_v2`](#mihoyo-id)一起使用，`ltoken`必须与[`ltuid`](#account-id)一起使用。

`ltoken_v2`的开头通常带有“v2_”字样，且长度较长；`ltoken`的长度则较短。

在修改米游社账号的密码后将会发生变化。

#### SToken

即`stoken`。

`stoken`多用于在米游社内的操作。有两种类型的值：以`v2_`开头和不以`v2_`开头，分别被命名为“SToken（V2）”与“SToken（V1）”。

“SToken（V2）”必须与[`mid`](#mihoyo-id)一起使用，“SToken（V1）”必须与[`stuid`](#account-id)一起使用。

在修改米游社账号的密码后将会发生变化。

#### MiHoYo ID

分为与[LToken](#ltoken)一起使用的`ltmid_v2`，和与[SToken](#stoken)一起使用的`mid`。其被命名为“SToken（V1）”与“SToken（V2）”。

`ltmid_v2`和`mid`的值是相同，对应一个账号。

#### Account ID

有`account_id_v2`、`account_id`、`login_uid`、`ltuid`、`ltuid_v2`和`stuid`。

UID即米游社UID。这个Cookie不是必须传递的。

#### Login Ticket

即`login_ticket`。

`login_ticket`是米游社的登录凭证，可用于获取[SToken](#stoken)和[LToken](#ltoken)。

通常在[米游社通行证](https://user.mihoyo.com/)中登录获得。

有效期为30分钟。

#### Cookie Token

分为`cookie_token`和`cookie_token_v2`。

`cookie_token`与`cookie_token_v2`的值不相同。

#### Action Ticket

Action Ticket通常不在Cookie中使用，而是作为URL参数或请求体的一部分传递，类似于凭证。

Action Ticket通常用于米游社内的部分网页操作。

#### Auth Key

Auth Key通常不在Cookie中使用，而是作为URL参数或请求体的一部分传递，类似于凭证。

Auth Key通常用于米游社的联系客服页面。

#### Game Token

即`game_token`。

`game_token`为游戏登录凭证，通常用于获取其它Token。

#### Hk4e Token

即`e_hk4e_token`。

`e_hk4e_token`为米游社账号的《原神》账号标识，通常可以在《原神》的网页活动中见到。

