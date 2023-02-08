# 鉴权

- [请求头](#请求头)
  - [米游社](#米游社)
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

#### `x-rpc-app_version`

米游社版本号，例如`2.44.1`。

与DS字段相关，DS生成需要`salt`，而每个米游社版本的`salt`都不同。

因此1个米游社版本只能使用对应的1个`salt`用于生成DS。

#### `x-rpc-client_type`

APP为`2`或`5`，网页为`4`。

根据请求的API不同而变化。

将会在需要验证请求头的API进行标注。

与DS字段相关，DS生成需要`salt`，而不同的`x-rpc-client_type`对应该版本米游社的`salt`也不同。


- `x-rpc-sys_version`（可选）：安卓系统大版本版本号，例如Android 13则为`13`。
- `x-rpc-channel`（可选）：手机厂商，例如小米则为`xiaomi`。
- `x-rpc-device_name`（可选）：手机厂商和手机型号，例如小米11青春版则为`Xiaomi M2101K9C`。
- `x-rpc-device_model`（可选）：手机型号。


#### `x-rpc-page`

少数API需要验证，未知其规律。

`3.1.3_#/ys`

#### `X-Requested-With`

国内版APP为`com.mihoyo.hyperion`。

国际版APP为`com.mihoyo.hoyolab`。

#### `Origin`

请求网站的协议与主机名。

#### `Host`

请求的网站的主机名。

#### `Referer`

在哪个网页发起的请求。

一般情况下，国内版APP为

若`x-rpc-client_type`为`5`，则`https://webstatic.mihoyo.com/`

若`x-rpc-client_type`为`2`，则`https://app.mihoyo.com`

国际版APP为

`https://webstatic-sea.hoyolab.com`。

#### `User-Agent`

无需验证请求头或`x-rpc-client_type`为`2`的API不需要设置请求头。

但还是最好避免带有`python`等字样。

用户代理，为`Mozilla/5.0 (Linux; Android 13; M2101K9C Build/TKQ1.220829.002; wv) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/108.0.5359.128 Mobile Safari/537.36 miHoYoBBS/米游社版本号`。

#### `DS`

DS值通过一系列算法得出。



## Cookie

