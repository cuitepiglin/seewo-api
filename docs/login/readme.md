# 登录

## 登录前提

### 获取acw_tc

> https://id.seewo.com/auth/loginApi

*请求方式：GET*

**URL参数:**

| 参数名         | 类型 | 内容 | 必要性 | 备注              |
| -------------- | ---- | ---- | ------ | ----------------- |
| _time + 时间戳 | 无   | 无   | 非必要 | UNIX 毫秒级时间戳 |

**Cookie 回复:**

| 参数名                | 类型 | 内容           | 备注     |
| --------------------- | ---- | -------------- | -------- |
| acw_tc                | str  | 随机acw_tc     | 登录必需 |
| sw_sid                | str  | user_undefined |          |
| system                | str  | SeewoAccount   |          |
| systemCode            | str  | SeewoAccount   |          |
| _token                | str  |                |          |
| x-username            | str  |                |          |
| nickname              | str  |                |          |
| userUid               | str  |                |          |
| x-samesite-none-token | str  |                |          |
| action                |      |                |          |
| authCode              |      |                |          |

**示例:**

```shell
curl 'https://id.seewo.com/auth/loginApi?_time1727694976380'
```

<details>
<summary>查看响应示例：</summary>

```js
Web.authCallback && Web.authCallback('https://id.seewo.com');
```

</details>

**响应头部抓包信息：**

可明显看见设置了几个 cookie

<details>
<summary>查看响应示例：</summary>

```http
HTTP/1.1 200 OK
Date: Mon, 30 Sep 2024 11:16:18 GMT
Content-Type: application/javascript; charset=utf-8
Content-Length: 61
Connection: keep-alive
Set-Cookie: acw_tc=0aef812817276949785867003e003782669252a4517479a2625577517b1903;path=/;HttpOnly;Max-Age=1800
X-Powered-By: Express
P3P: CP="CAO PSA OUR"
Access-Control-Allow-Origin: https://id.seewo.com
Access-Control-Allow-Methods: GET,POST
Access-Control-Allow-Credentials: true
Access-Control-Allow-Headers: Content-Type, Access-Control-Allow-Headers, Authorization, X-Requested-With
Set-Cookie: sw_sid=user_undefined; Path=/; Expires=Thu, 25 Sep 2025 11:16:18 GMT
Set-Cookie: system=SeewoAccount; Path=/
Set-Cookie: systemCode=SeewoAccount; Path=/
Set-Cookie: _token=; Path=/; Expires=Thu, 01 Jan 1970 00:00:00 GMT
Set-Cookie: x-username=; Domain=.seewo.com; Path=/; Expires=Thu, 01 Jan 1970 00:00:00 GMT
Set-Cookie: x-username=; Path=/; Expires=Thu, 01 Jan 1970 00:00:00 GMT
Set-Cookie: nickname=; Domain=.seewo.com; Path=/; Expires=Thu, 01 Jan 1970 00:00:00 GMT
Set-Cookie: nickname=; Path=/; Expires=Thu, 01 Jan 1970 00:00:00 GMT
Set-Cookie: username=; Domain=.seewo.com; Path=/; Expires=Thu, 01 Jan 1970 00:00:00 GMT
Set-Cookie: username=; Path=/; Expires=Thu, 01 Jan 1970 00:00:00 GMT
Set-Cookie: userUid=; Domain=.seewo.com; Path=/; Expires=Thu, 01 Jan 1970 00:00:00 GMT
Set-Cookie: userUid=; Path=/; Expires=Thu, 01 Jan 1970 00:00:00 GMT
Set-Cookie: x-token=; Domain=.seewo.com; Path=/; Expires=Thu, 01 Jan 1970 00:00:00 GMT; HttpOnly
Set-Cookie: x-samesite-none-token=; Domain=.seewo.com; Path=/; Expires=Thu, 01 Jan 1970 00:00:00 GMT; HttpOnly
Set-Cookie: action=; Path=/; Expires=Thu, 01 Jan 1970 00:00:00 GMT
Set-Cookie: authCode=; Path=/; Expires=Thu, 01 Jan 1970 00:00:00 GMT
ETag: W/"3d-6j0IpckhZwZpt2Vx/n7GqrWTpDM"
Vary: Accept-Encoding
Server: cagw
x-apm-traceid: 6eb6e74f00e1efbc18deb5a18ba86bf5
```

</details>

### 继续登录

- [二维码登录](QR.md)