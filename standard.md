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
## Deploy

### Vue.js部分修改build相关参数

** 1. /config/index.js**

build部分，将"assetsPublicPath"值改为"./"

```
build: {
    // Template for index.html
    index: path.resolve(__dirname, '../dist/index.html'),

    // Paths
    assetsRoot: path.resolve(__dirname, '../dist'),
    assetsSubDirectory: 'static',
    assetsPublicPath: './',

    /**
     * Source Maps
     */

    productionSourceMap: true,
    // https://webpack.js.org/configuration/devtool/#production
    devtool: '#source-map',

    // Gzip off by default as many popular static hosts such as
    // Surge or Netlify already gzip all static assets for you.
    // Before setting to `true`, make sure to:
    // npm install --save-dev compression-webpack-plugin
    productionGzip: false,
    productionGzipExtensions: ['js', 'css'],

    // Run the build command with an extra argument to
    // View the bundle analyzer report after build finishes:
    // `npm run build --report`
    // Set to `true` or `false` to always turn it on or off
    bundleAnalyzerReport: process.env.npm_config_report
  }
```

** 2. /build/utils.js**

"if (options.extract)"中，"ExtractTextPlugin.extract"参数列表增加"publicPath: '../../'"

```
if (options.extract) {
  return ExtractTextPlugin.extract({
    use: loaders,
    fallback: 'vue-style-loader',
    publicPath: '../../'
  })
} else {
  return ['vue-style-loader'].concat(loaders)
}
```

### Spring工程修改servlet配置文件

** 1. spring-servlet.xml增加页面资源**

```
<!-- 静态资源访问 -->
<mvc:resources mapping="/pages/**"
  location="/WEB-INF/pages/" />
<mvc:annotation-driven />
```

** 2. 迁移静态网页资源**

放到/WEB-INF/pages/下

### Tomcat部署

** 1. eclipse中对工程使用"Maven install"打包war文件**

** 2. tomcat服务器设置开机自启**

复制/tomcat/bin/catalina.sh
```
sudo mv catalina.sh tomcat
```

修改权限a+x
```
sudo chmod a+x tomcat
```

移动到/etc/init.d/下
```
sudo cp tomcat /etc/init.d/
```

设置自启
```
sudo sysv-rc-conf tomcat on
```

检查
```
sysv-rc-conf  --list|grep tomcat
```

取消
```
sysv-rc-conf tomcat off
```

删除
```
sysv-rc-conf tomcat remove
```

监听
```
netstat -nltp|grep <tomcat端口>
```

启动
```
/etc/init.d/tomcat start
```

关闭
```
/etc/init.d/tomcat stop
```

---
## Feedback

- [Issues](https://github.com/FlymeStudio/FlymeStudio-Doc/issues)
