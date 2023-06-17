# 公共错误码

- [米游社](#米游社)

## 米游社

错误码为API返回JSON中的`retcode`字段。

### `api-takumi-record.mihoyo.com`

| 错误码 | 消息 | 原因 |
| ----- | ---- | ---- |
| -10001 | invalid request | 该API需要验证请求头，请求头的一些字段缺失或错误<br/>请查看[绕过检测与鉴权](other/authentication.md) |
| -1 | param error<br>param {param} error: value must be greater than {max}<br>param {param} error: value must be in list [{n1} {n2} ... {nn}] | 传递的参数值错误<br>传递的参数`param`的值必须大于`max`<br>传递的参数`param`的值只能是`n1`、`n2`至`nn`其中之一 |
| 1008 | 用户信息不匹配 | 传递的参数不正确<br/>（例如获取用户游戏账号信息的`role_id`为无效UID） |
| 10001 | Please login | 该API需要验证Cookie<br/>请查看[绕过检测与鉴权](other/authentication.md#cookie) |
| 1034 | | 请求遇到验证码 |
### `api-takumi.miyoushe.com`

| 错误码 | 消息 | 原因 |
| ----- | ---- | ---- |
| -10001 | invalid request | 该API需要验证请求头，请求头的一些字段缺失或错误<br/>请查看[绕过检测与鉴权](other/authentication.md) |
| -502 | Something went wrong...please retry later | 传递的参数错误 |
| -100 | 登录失效，请重新登录 | Cookie失效或不正确 |
| 1034 | | 请求遇到验证码 |

### `api-takumi.mihoyo.com`

| 错误码 | 消息 | 原因 |
| ----- | ---- | ---- |
| -502 | Something went wrong...please retry later | 传递的参数错误 |
| -101 | 参数错误 | 传递的参数缺失或错误 |
| -100 | 登录失效，请重新登录<br>-100 | Cookie失效或不正确 |
| 1000 | 参数错误 | 传递的参数缺失或错误 |