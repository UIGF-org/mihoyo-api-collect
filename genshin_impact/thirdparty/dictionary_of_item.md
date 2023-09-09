# 项目ID与名称的字典

- [UIGF API](#uigf-api)
- [Caughtwind API（已弃用）](#caughtwind-api已弃用)

---

## UIGF API

_请求方式：GET_

`https://api.uigf.org/dict/genshin/{lang}.json`

**导航参数：**

| 字段 | 内容 | 备注 |
| ---- | ---- | --- |
| lang | 返回数据中文本的语言，支持如下语言：<br>chs<br>cht<br>de<br>en<br>es<br>fr<br>id<br>jp<br>kr<br>pt<br>ru<br>th<br>vi | |

**JSON返回：**

根对象：

| 字段 | 类型 | 内容 | 备注 |
| --- | ---- | ---- | --- |
| “项目名称” | str | 项目ID | |

## Caughtwind API（已弃用）

_请求方式：GET_

`https://api.21cnt.cn/genshin/itemId`

**参数：**

| 字段 | 内容 | 备注 |
| ---- | ---- | --- |
| lang | 返回数据中文本的语言，支持如下语言：<br>chs | |

**JSON返回：**

根对象：

| 字段 | 类型 | 内容 | 备注 |
| --- | ---- | ---- | --- |
| “项目名称” | str | 项目ID | |
