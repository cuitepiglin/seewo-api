# 二维码登录

## web端扫码登录

### 申请二维码(web端)

> https://id.seewo.com/scan/qrcode

*请求方式：GET*

**URL参数:**

| 参数名 | 类型  | 内容                        | 必要性 | 备注 |
| ------ | ----- | --------------------------- | ------ | ---- |
| oriSys | str   | mis-admin                   | 非必要 |      |
| t      | float | UNIX 毫秒级时间戳 + 4位小数 | 非必要 |      |

**示例:**

```shell
curl 'https://id.seewo.com/scan/qrcode?oriSys=mis-admin&t=1727694978742.8574'
```

<details>
<summary>查看响应示例：</summary>

<img src="../../../assets/img/qrcode.png" width="150" height="150"/>

```
https://id.seewo.com/scan/middle?uid=barcode_EB8983F7-3EED-4E29-8751-2FEFF830A850&oriSys=mis-admin
```
</details>

**Cookie 回复:**
| 参数名 | 类型 | 内容                                         | 备注           |
| ------ | ---- | -------------------------------------------- | -------------- |
| qrkey  | str  | barcode_XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX | 二维码唯一密钥 |


### 获取登录状态(web端)

> https://id.seewo.com/scan/pcCheckQrcode?type=long&_=1727864084076

*请求方式：GET*
*鉴权方式：Cookie*

**URL参数:**

| 参数名 | 类型 | 内容              | 必要性 | 备注 |
| ------ | ---- | ----------------- | ------ | ---- |
| type   | str  | long              | 非必要 |      |
| _      | num  | UNIX 毫秒级时间戳 | 非必要 |      |


**Cookie参数**

| 参数名     | 类型 | 内容                                         | 必要性 | 备注           |
| ---------- | ---- | -------------------------------------------- | ------ | -------------- |
| acw_tc     | str  | 在[此处](readme.md)获取                      | 必要   |                |
| sw_sid     | str  | user_undefined                               | 非必要 |                |
| system     | str  | mis-admin                                    | 非必要 |                |
| systemCode | str  | mis-admin                                    | 非必要 |                |
| referer    | str  |                                              | 非必要 |                |
| qrkey      | str  | barcode_XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX | 必要   | 二维码唯一密钥 |

**示例:**
```shell
curl 'https://id.seewo.com/scan/pcCheckQrcode?type=long&_=1727864084076' \
-b 'acw_tc=xxx' \
-b 'qrkey=xxx'
```
当密钥错误或二维码失效时`statusCode`为`300`, 且响应无延迟
<details>
<summary>查看响应示例：</summary>


```json
{
    "data":
    {
        "statusCode":300,
        "message":"二维码已过期"
    }
}
```

</details>

当二维码未被扫描或已扫描时`statusCode`为`200`, 第一次响应有约20秒的延迟
<details>
<summary>查看响应示例：</summary>


```json
{
    "data":
    {
        "statusCode":200,
        "message":"二维码仍有效"
    }
}
```

</details>


当二维码已扫描并登录时`statusCode`为`201`, 响应无延迟，返回包含登录token的账号信息
<details>
<summary>查看响应示例：</summary>


```json
{
  "data": {
    "statusCode": 202,
    "result": "https://campus.seewo.com",
    "token": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx-1145", //登录需要的token信息
    "userName": "11451419198",
    "userId": "abcdefghijkmlnopqrstwv1234567890",
    "nickName": "seewo_1145",
    "phone": "11451419198",
    "message": "客户端已扫码并确认登录"
  }
}
```

</details>

**响应头部抓包信息：**

可明显看见设置了几个cookie

<details>
<summary>查看响应示例：</summary>

```http
HTTP/1.1 200 OK
Date: Mon, 30 Sep 2024 11:16:47 GMT
Content-Type: application/json; charset=utf-8
Content-Length: 272
Connection: keep-alive
X-Powered-By: Express
P3P: CP="CAO PSA OUR"
Access-Control-Allow-Origin: https://id.seewo.com
Access-Control-Allow-Methods: GET,POST
Access-Control-Allow-Credentials: true
Access-Control-Allow-Headers: Content-Type, Access-Control-Allow-Headers, Authorization, X-Requested-With
Set-Cookie: x-token=***; Domain=.seewo.com; Path=/; HttpOnly
Set-Cookie: x-samesite-none-token=***; Domain=.seewo.com; Path=/; HttpOnly; Secure; SameSite=None
Set-Cookie: userId=abcdefghijkmlnopqrstwv1234567890; Path=/
Set-Cookie: username=seewo_1145; Path=/
Set-Cookie: thirdLogoutUrl=; Domain=.seewo.com; Path=/; Expires=Thu, 01 Jan 1970 00:00:00 GMT
Vary: Accept-Encoding
Server: cagw
```

</details>
