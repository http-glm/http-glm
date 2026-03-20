# http-glm
参考 http/1.0 http/1.1 响应，作为 glm 的输出格式，代替 json/xml，速度、扩展、简单。

## 报文结构
| 特点 | 说明 |
|------|------|
| **简单快速** | 报文格式为文本，易于理解 |
| **灵活** | 通过 `Content-Type` 可传输任意数据类型（HTML、JSON 等） |

### 响应报文示例
```http
HTTP/glm 200 OK                  ← 状态行（版本 + 状态码 + 短语）
Content-Type: text/html; charset=utf-8

<html>...</html>                 ← 响应体（Body）
```

### 状态码
* **2xx 成功**：最常见的是 **200 OK**（请求成功）。

### ContentType
* **text/html; charset=utf-8**
* **application/json**
* **application/x-ndjson** 或旧版 application/jsonlines 或更宽松的 application/stream+json
* **application/xml**

## 提示词
将代码块内容添加到到提示词最开头（不包含代码块的标记），按需调整内容
````
按以下代码块中的格式输出，输出不包含代码块
```
HTTP/glm 200 OK
Content-Type: text/plain

(output)
```
输出由 4 部分组成
```
[start line]
[headers]
[empty line]
[body]
```
- start line 是固定字符串 `HTTP/glm 200 OK`。
- headers 是零个或多个键值对，格式为 Name: Value，以 CRLF 结尾。
- empty line 是一个 CRLF（\r\n），用于分隔头部和正文，请务必不要丢失。
- body 是可选的实体数据，格式由 headers 中的 Content-Type 决定(默认是 text/plain)。

````
