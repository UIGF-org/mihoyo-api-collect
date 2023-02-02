# 鉴权

部分API需要使用Cookie鉴权。

## 米游社

大多数API需要验证的请求头：`x-rpc-app_version`、`x-rpc-client_type`、`x-rpc-sys_version`、`x-rpc-channel`、`x-rpc-device_id`、`x-rpc-device_fp`、`x-rpc-device_name`、`x-rpc-device_model`、`X-Requested-With`、`Origin`、`Referer`、`Host`、`DS`、`User-Agent`。
少数API才需要验证的额外的请求头：`x-rpc-page`、`x-rpc-challenge`。

- `x-rpc-app_version`：APP版本号，例如`2.44.1`。
国际版APP与国内版APP每个版本对应生成`DS`所用的`salt`也不一样。
- `x-rpc-client_type`：安卓APP为`2`或`5`，网页为`4`。
- `x-rpc-sys_version`：安卓系统大版本版本号，例如Android 13则为`13`。
- `x-rpc-channel`：手机厂商，例如小米则为`xiaomi`。
- `x-rpc-device_name`：手机厂商和手机型号，例如小米11青春版则为`Xiaomi M2101K9C`。
- `x-rpc-device_model`：手机型号。
- `x-rpc-page`：少数API需要验证，为`/ys`
- `X-Requested-With`：国内版APP则为`com.mihoyo.hyperion`，国际版APP则为`com.mihoyo.hoyolab`。
- `Origin`：与`Referer`字段的协议与主机名部分相同。
- `Host`：请求的网站的主机名。
- `Referer`：在哪个网页发起的请求。
一般情况下，国内版APP为
`https://webstatic.mihoyo.com/`
`https://app.mihoyo.com`等等。
国际版APP为
`https://webstatic-sea.hoyolab.com`。
- `DS`：见[DS值](#ds值)。
- `User-Agent`：用户代理，为`okhttp/4.9.3`或`Mozilla/5.0 (Linux; Android 13; M2101K9C Build/TKQ1.220829.002; wv) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/108.0.5359.128 Mobile Safari/537.36 miHoYoBBS/米游社版本号`。

### DS值

DS值通过一系列算法得出。

<!--大致步骤如下（伪代码）：

```
salt = APP版本所用的salt
timestamp = 当前Unix时间戳

if 是国服或渠道服 {
  random = 随机整数(100001, 200000)
}
else if 是国际服 {
  random = 随机6位字母()
}

if 要发送的请求 是 POST请求 则 {
  body = 转为JSON字符串(请求发送的数据)
}
else if 要发送的请求 是 GET请求 则 {
  query = '&'
  for k, v in 请求发送的数据 {
    query += k + "=" + v + "&"
  }
}
else {
  body = 空
  query = 空
}

if 是国服或渠道服 {
  to_be_encrypted = "salt=" + salt + "&t=" + time + "&r=" + random + "&b=" + body + "&q=" + query
  ds = 16位MD5加密(to_be_encrypted) // 小写
}
else if 是国际服 {
  to_be_encrypted = "salt=" + salt + "&t=" + time + "&r=" + random
  ds = 16位MD5加密(to_be_encrypted) // 小写
}

最终在请求头部的DS字段的内容 = timestamp + "," + random + "," + ds

``` 
-->

### Cookie

登录账号后服务器设置的Cookie值。

