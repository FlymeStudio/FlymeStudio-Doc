# Doc | [Web](https://github.com/FlymeStudio/FlymeStudio-Web/blob/master/README.md) | [Server](https://github.com/FlymeStudio/FlymeStudio-Server/blob/master/README.md) | [Database](https://github.com/FlymeStudio/FlymeStudio-Database/blob/master/README.md)
---

## [Home](https://github.com/FlymeStudio/FlymeStudio-Doc/blob/master/README.md) | [Introduce](https://github.com/FlymeStudio/FlymeStudio-Doc/blob/master/introduce.md) | Standard

---
## UML

![](https://github.com/FlymeStudio/FlymeStudio-Doc/blob/master/assets/uml.png?raw=true)

---
## Security

<table>
  <tr>
    <th width=10%, bgcolor=lightgrey>Number</th>
    <th width=20%, bgcolor=lightgrey>Attack</th>
    <th width=20%, bgcolor=lightgrey>Theory</th>
    <th width=50%, bgcolor=lightgrey>Defense</th>
  </tr>
  <tr>
    <td>1</td>
    <td>用户登录时，获取请求信息</td>
    <td>前端请求参数暴露</td>
    <td>使用可逆加密方式对参数的key和value加密，在一定程度上提高安全性。</td>
  </tr>
  <tr>
    <td>2</td>
    <td>高频访问服务器导致瘫痪</td>
    <td>前端请求地址暴露</td>
    <td>该问题无法解决。</td>
  </tr>
  <tr>
    <td>3</td>
    <td>传输过程中捕获信息</td>
    <td>传输信息未加密</td>
    <td>前端的请求参数和后端的返回信息进行可逆加密，这样即使中途被捕获也无法获取原始信息。</td>
  </tr>
  <tr>
    <td>4</td>
    <td>多终端登录</td>
    <td>未对登录设备标记</td>
    <td>登录成功时服务器存储一个token并返回，每次操作需要认证token，不匹配则跳转到登录页。</td>
  </tr>
  <tr>
    <td>5</td>
    <td>非法操作</td>
    <td>未经登录直接请求</td>
    <td>由问题4解决，未登录的情况下由于没有token导致请求无效。</td>
  </tr>
</table>

---
## Feedback

- [Issues](https://github.com/FlymeStudio/FlymeStudio-Doc/issues)
