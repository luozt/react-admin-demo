# react-admin-ctrl

本系统为基于ReactJS开发的后台管理系统，已实现前端数据库保存增删改查工作以及接收服务器推送消息的功能。

在消息列表模块中，每随机10秒内将接收到一个推送消息。服务器端的实现是采用express的node框架来做的。

##系统发布及运行

**在线预览**

已把APP部署到heroku上了，可直接点击 [heroku 预览地址](https://react-admin-ctrl.herokuapp.com/) 进行在线预览使用。

**本地预览**

1. 安装项目依赖插件：`npm i`
2. 更改server环境`/index.js`的env为`var env = "qa"`
2. 系统发布：`npm run build-qa`
3. 系统启动：`npm start`
4. 系统运行：打开<http://localhost:5000/>

##系统开发与调试

**环境配置**

本项目使用fis3前端构建工具，但已通过封装为**FIZ**插件，故请按照以下步骤进行环境安装及预览：

1. 安装插件：`npm i`
2. 进入前端系统的开发：`npm run dev`

注：进入前端系统的开发，会轮询的报socket.io的错误，是由于没有开发环境的socket服务引起的。这是个正常现象，因为已在`index.js`配置了针对本地打包后的环境的socket服务，只要项目进行本地打包发布后，启动`npm start`进入发布后的环境即为正常运行状态。如果开发过程中，不想看到这个报错，想临时停止客户端的socket，可在`src/js/app.jsx`里的`App.componentDidMount`方法里注释掉`MessageListen.init()`

**启动后台服务**

运行：`npm start`

**本地打包发布**

打包命令：`npm run build`

它将打包出一个正式环境的版本，将css合并成1个文件，将js合并为1个文件，并压缩为最小，减少HTTP体积和请求数。

打包后的路径为：`<project_path>/pr/`

**打包前进行的环境配置**

* fis-conf.js：`"cdn-path-release"`资源域名配置
* index.js：`env`的环境配置

##开发过程中的不足

后台管理系统：

* 在正式发布后，需对模块进行编译、压缩、合并等操作（目前已在本地打包后实现！）
* 数据获取过程的loading处理及提示
* 提交过程的submitting提示
* 错误的提示，使用了简单的window.alert提示
* 提交、查看、修改表单放在同一个Modal里，处理得有点复杂，需要再进行细分组件
* 数据库并无作严格字段验证、可选、必选字段验证
* 订阅/发布事件名应该以模块名为前缀，这样在模块卸载时能简单地通过模块名进行取消订阅事件的操作

由于时间仓促，系统多有不足之处，敬请指出~

##文件结构说明

```
fis-conf.js                             // fis3配置文件
|
index.js                                // node实现的后台主程序
|
src/                                    // 存放后台管理系统前端文件
```

