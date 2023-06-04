# 鉴权

- [请求头](#请求头)
- [Cookie](#cookie)

---

大多数API需要验证请求头。

部分API（例如点赞文章、米游社签到福利、米游币等）需要使用Cookie鉴权。

## 请求头

### 米游社

大多数API需要验证的请求头：`x-rpc-app_version`、`x-rpc-client_type`、`x-rpc-device_id`、`X-Requested-With`、`Origin`、`Referer`、`Host`、`DS`、`User-Agent`。
 
少数API才需要验证的额外的请求头：`x-rpc-device_fp`、`x-rpc-challenge`。

可选请求头：`x-rpc-device_name`、`x-rpc-device_model`、`x-rpc-sys_version`、`x-rpc-channel`。

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

手机厂商和手机型号，例如小米11青春版则为`Xiaomi M2101K9C`。

#### `x-rpc-device_model`

手机型号。

#### `x-rpc-device_fp`

发送POST请求至`https://public-data-api.mihoyo.com/device-fp/api/getFp`以获得。

#### `x-rpc-device_id`

设备ID，由使用的设备决定。

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


###### 中国版APP：

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
# body和query一般来说不会同时存在。毕竟body只有POST请求才有，query只有GET请求才有
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
```js
import md5 from 'md5'

const salt = "xV8v4Qu54lUKrEYFZkJhB8cuOh9Asafs"

const body = '{"role": "123456789"}'
const query = "server=cn_gf01&role_id=123456789"

const t = Math.floor(Date.now() / 1000)
let r = Math.floor(Math.random() * 100001 + 100000)
if (r == 100000) {
  r = 642367
}
// const r = Math.floor(Math.random() * 100001 + 100001)

const main = f"salt={salt}&t={t}&r={r}&b={body}&q={query}"
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
```js
import md5 from 'md5'

const salt = "ZSHlXeQUBis52qD1kEgKt5lUYed4b7Bb"
const lettersAndNumbers = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789'

const t = Math.floor(Date.now() / 1000)
let r = ""
for (let i;i < 6;i++) {
  r += lettersAndNumbers[Math.floor(Math.random() * lettersAndNumbers.length)]
}

const main = f"salt={salt}&t={t}&r={r}"
const ds = md5(main)

const final = `${t},${r},${ds}` // 最终结果
```

## Cookie

一些API（例如文章点赞、签到和获取用户的游戏账号信息等API）需要登录账号，则表示为请求头Cookie的形式。

需要验证Cookie的API会进行标注。

若API无需登录账号，就不需要设置Cookie。

### 米游社

需要哪些Cookie取决于以下因素：

* API是否要求登录账号。
* `x-rpc-client_type`的不同值。
* 一些API要求特殊的Cookie。

#### LToken

即`ltoken_v2`和`ltoken`。

`ltoken_v2`多用于查询用户的游戏账号信息。

必须与[`ltmid_v2`](#mihoyo-id)一起使用。

#### SToken

即`stoken`。

`stoken`多用于在米游社内的操作。

必须与[`mid`](#mihoyo-id)一起使用。

#### Mihoyo ID

分为与[LToken](#ltoken)一起使用的`ltmid_v2`，和与[SToken](#stoken)一起使用的`mid`

`ltmid_v2`和`mid`的值是相同，对应一个账号。

#### Login Ticket

即`login_ticket`。

`login_ticket`是米游社的登录凭证，隔一段时间刷新。作用未知。

#### Cookie Token

即`cookie_token_v2`。

`cookie_token_v2`隔一段时间刷新。作用未知。


