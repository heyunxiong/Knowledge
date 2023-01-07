> Web Knowledge： jwt 认证了解

官网： [https://jwt.io/introduction](https://jwt.io/introduction)
## What is JSON Web Token
JSON Web Token (JWT) is an open standard (RFC 7519) that defines a compact and self-contained way **for securely transmitting information** between parties as a JSON object. This information can be verified and trusted because it is digitally signed. JWTs can be signed using a secret (with the **HMAC** algorithm) or a public/private key pair using **RSA** or **ECDSA**.

Json web token (JWT), 是为了在网络应用环境间传递声明而执行的一种基于JSON的开放标准（(RFC 7519)
该token被设计为紧凑且安全的，特别适用于分布式站点的单点登录（SSO）场景。
JWT的声明一般被用来在身份提供者和服务提供者间传递被认证的用户身份信息，以便于从资源服务器获取资源，也可以增加一些额外的其它业务逻辑所必须的声明信息，该token也可直接被用于认证，也可被加密

简单来说：

- JWT是一个数字签名，生成的信息是可以验证并被信任的。
- 使用密钥(使用HMAC算法)或使用RSA或ECDSA的公钥/私钥对JWT进行签名。
- JWT是目前最流行的跨域认证解决方案
## JWT 结构
jwt是一串字符串，由 . 分隔成三个部分，没有换行。
Header.Payload.Signature
（头部.负载.签名）
```
// 无换行符，便于展示
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.
eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiYWRtaW4iOnRydWV9.
TJVA95OrM7E2cBab30RMHrHDcEfxjoYZgeFONFh7HgQ
```
### Header
The header typically consists of two parts: the type of the token, which is JWT, and the signing algorithm being used, such as HMAC SHA256 or RSA.
即系header由两部分组成，签证算法+token的类型
```
{
  "alg": "HS256",
  "typ": "JWT"
}

// 上述json使用Base64Url加密jwt的第一部分
```
### Payload
payload就是存放有效信息的地方，有效信息包含三个部分

- 标准中注册的声明（不强制）
   - iss (issuer)：签发人
   - exp (expiration time)：过期时间
   - sub (subject)：主题
   - aud (audience)：受众
   - nbf (Not Before)：生效时间
   - iat (Issued At)：签发时间
   - jti (JWT ID)：编号
- 公共的声明
   - 公共的声明可以添加任何的信息，在客户端可被解密
- 私有的声明
   - 私有声明是提供者和消费者所共同定义的声明，一般不建议存放敏感信息，因为base64是对称解密的，意味着该部分信息可以归类为明文信息
```
{
  "sub": "1234567890",
  "name": "John Doe",
  "admin": true
}
```
### Signature
Signature 部分是对前两部分的签名，防止数据篡改。
签证信息由三部分组成：

- header (base64后的)
- payload (base64后的)
- secret
```
HMACSHA256(
  base64UrlEncode(header) + "." +
  base64UrlEncode(payload),
  secret)
```
## JWT 应用
一般是在请求头里加入**Authorization**，并加上**Bearer**标注：
```
fetch('api/user/1', {
  headers: {
    'Authorization': 'Bearer ' + token
  }
})
```
![](_assets/JWT%20-%20JSON%20Web%20Token/1637673470215-f01413c7-2e23-4051-8e7a-e9378d04b673.png)
![](_assets/JWT%20-%20JSON%20Web%20Token/1637672869790-5d9610d8-1913-4c51-b939-0d7816cc9d42.png)

## JWT 优点

- 因为json的通用性，所以JWT是可以进行跨语言支持的，像JAVA,JavaScript,NodeJS等很多语言都可以使用
- 因为有了payload部分，所以JWT可以在自身存储一些其他业务逻辑所必要的非敏感信息
- 便于传输，jwt的构成非常简单，字节占用很小，所以它是非常便于传输的
- 它不需要在服务端保存会话信息, 所以它易于应用的扩展

参考资料：

- [https://jwt.io/introduction](https://jwt.io/introduction)
- [https://en.wikipedia.org/wiki/JSON_Web_Token](https://en.wikipedia.org/wiki/JSON_Web_Token)
- [https://www.ruanyifeng.com/blog/2018/07/json_web_token-tutorial.html](https://www.ruanyifeng.com/blog/2018/07/json_web_token-tutorial.html)
- [https://www.cnblogs.com/lizm166/p/7844110.html](https://www.cnblogs.com/lizm166/p/7844110.html)
- [https://juejin.cn/post/6986133226532110350](https://juejin.cn/post/6986133226532110350)
