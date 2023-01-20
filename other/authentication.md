# 鉴权

部分API需要使用Cookie鉴权。

## 米游社

大多数API需要验证请求头部的`X-rpc-app_version`、`X-rpc-client_type`、`X-Requested-With`、`Origin`、`Referer`、`DS`、`User-Agent`、`Cookie`。

- `X-rpc-app_version`：APP版本，国际版APP与国内版APP版本不一样。国际版APP与国内版APP每个版本对应生成DS所用的`salt`也不一样。
- `X-rpc-client_type`：国内版APP则为`5`，国际版APP则为`2`。
- `X-Requested-With`：国内版APP则为`com.mihoyo.hyperion`，国际版APP则为`com.mihoyo.hoyolab`。
- `Origin`：国内版APP则为`https://webstatic.mihoyo.com`，国际版APP则为`https://webstatic-sea.hoyolab.com`。
- `Referer`：国内版APP则为`https://webstatic.mihoyo.com`，国际版APP则为`https://webstatic-sea.hoyolab.com`。
- `DS`：见[DS值](#ds值)。
- `User-Agent`：用户代理，为`Mozilla/5.0 (iPhone; CPU iPhone OS 13_2_3 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) miHoYoBBS/2.11.1`。
- `Cookie`：见[Cookie](#cookie)

### DS值

DS值通过一系列算法得出。

大致步骤如下（伪代码）：

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

### Cookie

登录账号后服务器设置的Cookie值。

- `_MHYUUID`
- `DEVICEFP_SEED_ID`
- `DEVICEFP_SEED_TIME`
- `_ga`
- `cookie_token_v2`
- `account_mid_v2`
- `account_id_v2`
- `ltoken_v2`
- `ltmid_v2`
- `ltuid_v2`
- `DEVICEFP`
- `_ga_XXXXXXXX`
