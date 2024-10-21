
# 接口调用与鉴权

<！-->QQ BOT服务端开放的OpenAPI接口，均使用https方式进行调用，通过'access token'机制实现对OpenAPI接口调用的鉴权。-->

**小费说明
`QQ机器人` 服务端开放的 `OpenAPI`接口，均使用`HTTPS`方式进行调用，通过`AccessToken` 机制实现对 `OpenAPI`接口调用的鉴权。
:::

## 获取调用凭证

- **请求**

<桌子>
	<TR>
	  <thcolspan="2">基本</th>
	</TR>
	<TR>
    <TD>HTTP URL</TD>
    <TD>https://bots.qq.com/app/getAppAccessToken</TD>
	</TR>
	<TR>
    <TD>HTTP方法</TD>
    <TD>邮件</TD>
	</TR>
	<！--<tr>
<td>接口频率限制</td>
<td></td>
</tr>-->
</桌子>

- **请求参数**

| **属性** | **类型** | **必填** | **说明** |
| --- | --- | --- | --- |
|AppID|线| 是 |在开放平台管理端上获得。|
|ClientSecret|线| 是 |在开放平台管理端上获得。|

- **返回参数**

| **属性** | **类型** | **说明** |
| --- | --- | --- |
|access_token|线|获取到的凭证。|
|到期日(_I)|数量|凭证有效时间，单位：秒。 目前是7200秒之内的值。|

- **错误码**

| **错误码** | **错误码取值** |
| --- | --- |
|0|好的|

- **调用示例**

```壳
curl-位置‘https://bots.qq.com/app/getAppAccessToken'\
--header'Content-Type:application/json'\
--data‘{
"appId"："APPID"，
"clientSecret"："ClientSecret"
}'
```

- **返回示例**
```JSON
{
"access_token"："ACCESS_TOKEN"，
"expires_in"："7200"
}
```

- **其他说明**

目前 `access_token` 生命周期默认 `7200`秒，每次请求不会刷新新的`access_token`，开发者需要在过期后自行刷新`access_token`，保证调用链路权限正常。

在上一个 `access_token` 接近过期时间 `60`秒内，获取`access_token`时，会获得一个新的`access_token`，老的`access_token` 在这个`60`秒内仍然有效。

## 鉴权方式

在每次调用https的OpenAPI开放接口请求的时候，需要在页眉内引入`access_token`进行调用权限验证。

**统一地址**

```
https://api.sgroup.qq.com
```


**请求头**

| 名称 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
|授权|线| 是 |格式值："QQBot ACCESS_TOKEN"|

**示例**
```JSON
{
"标头"：{
"授权"："QQBot{ACCESS_TOKEN}"
}
}
```

<! -- ## 调用权限错误码
与‘访问令牌'权限有关的错误码。-->
