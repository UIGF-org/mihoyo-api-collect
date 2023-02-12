# 公共错误码

- [米游社](#米游社)

## 米游社

错误码为API返回JSON中的`retcode`字段。

| 错误码 | 消息 | 原因 |
| ------------------------------ | ---- | --- |
| -10001 | invalid request | 该API需要验证请求头，请求头的`DS`字段缺失<br/>请查看[鉴权](other/authentication.md#请求头) |
| -1 | param XXX error: value must be greater than X<br/>param XXX error: value must be in list [X ...] | 传递的参数XXX缺失<br/>传递的参数XXX的值只能在X、...中 |
| 1008 | 用户信息不匹配 | 传递的参数不正确<br/>（例如获取用户游戏账号信息的`role_id`为无效UID） |
| 10001 | Please login | 该API需要验证Cookie<br/>请查看[鉴权](other/authentication.md#cookie) |