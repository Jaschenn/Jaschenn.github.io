---
title: python的requests库
---

## DONE 学习python的requests模块，尝试向飞书中通过api写入内容。
:PROPERTIES:
:todo: 1606454996926
:done: 1606456835651
:later: 1606455312042
:id: 5fc08e89-7499-49fa-a84e-954b41c5d15d
:END:
## `import requests`
## 发起请求
### `r = requests.get(url)`
### `r = requests.get(url=url, params = dict)`, 其中dict是一个python的字典类型
### 响应的内容：
#### `r.encoding` # 当前的编码
#### `r.encoding = 'utf-8'` 设置编码
#### `r.text` # 以encoding解析返回的内容
#### `r.content` # 以字节形式返回
#### `r.status_code` # 响应状态码
#### `r.ok` # 查看是否登陆成功
#### 特殊的方法
##### `r.json()`  内置的JSON解码器，返回一个json形式，前提是返回的内容是json格式，否则会抱错误
## 定制header和cookie
###
```python
header={'user-agent':'my-app/0.0.1'}
cookie = {'k':'v'}
```
###
```python
r=request.get(url, header = header, cookie = cookie)
```
## ## 使用session
###
```python
r = requests.Session()
s.auth = ('auth', 'pwd')
s.headers = {'k':'v'}
r = s.get('url')
r1 = s.get('url1')
 ```
