---
title: python的requests库
---

## NOW 学习python的requests模块，尝试向飞书中通过api写入内容。
:PROPERTIES:
:todo: 1606454996926
:done: 1606455311056
:later: 1606455312042
:END:
## `import requests`
## ## 发起请求
## `r = requests.get(url)`
## `r = requests.get(url=url, params = dict)`, 其中dict是一个python的字典类型
### 响应的内容：
#### r.encoding # 当前的编码
#### r.encoding = 'utf-8' 设置编码
#### r.text # 以encoding解析返回的内容
#### r.content # 以字节形式返回
