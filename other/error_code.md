# 公共错误码

- [米游社](#米游社)

## 米游社

错误码为API返回JSON中的`retcode`字段。

### `api-takumi-record.mihoyo.com`

| 错误码 | 消息 | 原因 |
| ----- | ---- | ---- |
| -10001 | invalid request | 该API需要验证请求头，请求头的一些字段缺失或错误<br/>请查看[绕过检测与鉴权](other/authentication.md) |
| -1 | param error<br>param XXX error: value must be greater than X<br>param XXX error: value must be in list [X ...] | 传递的参数值错误<br>传递的参数XXX缺失<br>传递的参数XXX的值只能是X、...中 |
| 1008 | 用户信息不匹配 | 传递的参数不正确<br/>（例如获取用户游戏账号信息的`role_id`为无效UID） |
| 10001 | Please login | 该API需要验证Cookie<br/>请查看[绕过检测与鉴权](other/authentication.md#cookie) |
| 1034 | | 请求遇到验证码 |

### `api-takumi.miyoushe.com`

| 错误码 | 消息 | 原因 |
| ----- | ---- | ---- |
| -10001 | invalid request | 该API需要验证请求头，请求头的一些字段缺失或错误<br/>请查看[绕过检测与鉴权](other/authentication.md) |
| -502 | Something went wrong...please retry later | 传递的参数错误 |
| -100 | 登录失效，请重新登录 | 