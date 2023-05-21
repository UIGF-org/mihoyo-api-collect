# 鉴权

- [请求头](#请求头)
- [Cookie](#cookie)

---

大多数API需要验证请求头。

部分API（例如点赞文章、《原神》米游社签到、米游币等）需要使用Cookie鉴权。

## 请求头

### 米游社

大多数API需要验证的请求头：`x-rpc-app_version`、`x-rpc-client_type`、`x-rpc-device_id`、`X-Requested-With`、`Origin`、`Referer`、`Host`、`DS`、`User-Agent`。
 
少数API才需要验证的额外的请求头：`x-rpc-page`、`x-rpc-challenge`。

可选请求头：`x-rpc-device_fp`、`x-rpc-device_name`、`x-rpc-device_model`、`x-rpc-sys_version`、`x-rpc-channel`。


#### `x-rpc-app_version`

米游社版本号，例如`2.44.1`。

与DS字段相关，DS生成需要`salt`，而每个米游社版本的`salt`都不同。

因此1个米游社版本只能使用对应的1个`salt`用于生成DS。

#### `x-rpc-client_type`

APP为`2`或`5`，网页为`4`。

根据请求的API不同而变化。

将会在需要验证请求头的API进行标注。

与DS字段相关，DS生成需要`salt`，而不同的`x-rpc-client_type`对应该版本米游社的`salt`也不同。


#### `x-rpc-sys_version`（可选）

安卓系统大版本版本号，例如Android 13则为`13`。

#### `x-rpc-channel`（可选）

手机厂商，例如小米则为`xiaomi`。

#### `x-rpc-device_name`（可选）

手机厂商和手机型号，例如小米11青春版则为`Xiaomi M2101K9C`。

#### `x-rpc-device_model`（可选）

手机型号。

#### `x-rpc-device_fp`（可选）

向`https://public-data-api.mihoyo.com/device-fp/api/getFp`发送一些设备信息以获得。

#### `x-rpc-device_id`

未知其规律，可以从请求中复制。

#### `x-rpc-page`

少数API需要验证，未知其规律。

`3.1.3_#/ys`

`/ys`

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

一般情况下，国内版APP为

若`x-rpc-client_type`为`5`，则`https://webstatic.mihoyo.com/`

若`x-rpc-client_type`为`2`，则`https://app.mihoyo.com`

国际版APP为

`https://webstatic-sea.hoyolab.com`。

#### `User-Agent`

无需验证请求头或`x-rpc-client_type`为`2`的API不需要设置请求头。

但尽量避免带有`python`等字样。

需要验证请求头的API的用户代理为`Mozilla/5.0 (Linux; Android 安卓大版本号; 手机型号 Build/TKQ1.220829.002; wv) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/108.0.5359.128 Mobile Safari/537.36 miHoYoBBS/米游社版本号`。

例如`Mozilla/5.0 (Linux; Android 13; M2101K9C Build/TKQ1.220829.002; wv) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/108.0.5359.128 Mobile Safari/537.36 miHoYoBBS/2.44.1`

#### `DS`

_DS（Dynamic Secret，动态密钥）_

大多数API需要验证请求头中的`DS`字段。

DS值通过一系列算法得出。

##### 生成`DS`

`DS`的生成方式由以下因素影响：

* 网页、中国版APP和国际版APP的生成算法不同。
* 请求头的`x-rpc-client_type`字段，每个值都有其对应的生成算法。
* 少数API有其单独的生成算法。

生成`DS`需要`salt`（为32个包含大写字母、小写字母、数字的字符串）。

`salt`在以下情况下不同：

* 网页、中国版APP和国际版APP使用的`salt`不同。
* 每个APP版本都存有其独有的`salt`。
* 请求头的`x-rpc-client_type`字段，每个值使用的`salt`不同。
* 少数API有其单独的`salt`（例如米游社社区签到）。

请在[这里](https://github.com/Kamisato-Ayaka-233/mihoyo-api-collect/issues/1#issue-1571906738)获取`salt`。


###### 中国版APP：

**当`x-rpc-client_type`为`5`时**：

整体思路：

1. 获取当前的Unix时间戳（整数）。
1. 在100000到200000中选取随机整数，但是如果随机到100000，则加上542367，得到642367。
1. 若将发送Post请求，则将发送的数据转为JSON字符串，存储至变量（下文称`body`）。若将发送Get请求，则将URL参数进行英文字母顺序排序（键）后存储至变量（下文称`query`），例如URL参数为`server=cn_gf01&role_id=114514191`则结果为`role_id=222681079&server=cn_gf01`。若不需要传递数据或URL参数，则为空字符串。
1. 格式化字符串：`salt={salt值}&t={第1步的结果}&r={第2步的结果}&b={第3步的body}&q={第3步的query}`。
1. 将第4步的结果进行UTF-8编码，再进行MD5编码。
1. 格式化字符串：`{第1步的结果},{第2步的结果},{第5步的结果}`。

Python：
```python
import time
import random
from hashlib import md5

# 将要使用的salt，此为2.44.1版本的salt。
salt = "xV8v4Qu54lUKrEYFZkJhB8cuOh9Asafs"
# body和query一般来说不会同时存在。
# 可以使用json库的dumps函数将对象转为JSON字符串。
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

final = f"{t},{r},{ds}" # 最终结果。
```

**当`x-rpc-client_type`为`2`时**：

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

# 将要使用的salt，此为2.35.2版本的salt。
salt = "ZSHlXeQUBis52qD1kEgKt5lUYed4b7Bb"

t = int(time.time())
r = ""
for _ in range(6):
  r += random.choice(lettersAndNumbers)
main = f"salt={salt}&t={t}&r={r}"
ds = md5(main.encode(encoding='UTF-8')).hexdigest()

final = f"{t},{r},{ds}" # 最终结果。
```

**当`x-rpc-client_type`为`4`（网页）时**：

未知

## Cookie

一些API（例如文章点赞、签到等）需要登录账号，为Cookie的形式。

需要验证Cookie的API会进行标注。

若API无需登录账号，就不需要设置Cookie。

### 米游社

网页（`x-rpc-client_type`为`4`）、APP端（`x-rpc-client_type`为`2`）的Cookie形式不同。

`x-rpc-client_type`为`5`则与网页的Cookie相同。

**网页：**

以下字段必须有，否则服务器返回`10001`：

* `ltoken_v2`
* `ltmid_v2`

以下字段可选：

* `cookie_token_v2` - **米游社签到福利（游戏内道具）需要验证该字段**
* `account_mid_v2` - 与`ltmid_v2`相同
* `account_id_v2` - 米游社UID
* `ltuid_v2` - 米游社UID
* `login_ticket` - 米游社的登录凭证
* `_MHYUUID`
* `DEVICEFP`
* `acw_tc`

**APP：**

以下字段必须有：

* `stoken`
* `mid`

以下字段可选：

* `stuid` - 米游社UID
