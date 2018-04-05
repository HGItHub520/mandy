# Mandy

📦 前端自动化部署工具



![mandy-demo](https://cloud.githubusercontent.com/assets/8110936/25962458/7b49f6f6-36b0-11e7-87ee-fd8765a58aec.gif)



## 功能

- 可视化的部署流程
- 可交互的回滚流程
- 多个前端环境管理
- 无缝切换部署回滚




## 安装

```Bash
# 全局安装
yarn global add mandy

# 本地安装
yarn add mandy --dev
```



## 使用

**命令格式**

```bash
mandy <command> <environment>
```

**命令列表**

- mandy deploy <environment>         //  部署
- mandy deployToQiniu <environment>  //  部署到七牛云
- mandy rollback <environment>       //  回滚
- mandy current <environment>        //  当前版本信息
- mandy generate                     //  生成配置文件



### 开始部署

**Step 0: 生成配置文件**

进入你的项目，运行 `mandy generate`命令，创建配置文件

执行后，将在当前目录建立 `mandy/production.js  `配置文件

```bash
mandy generate production
```



**Step 1: 编辑配置文件**

```javascript
// mandy/production.js
module.exports = {
  ssh: {
    host: 'github.com',
    username: 'root',
    password: 'password',
    // privateKey: '/Users/zzetao/.ssh/id_rsa'
    // 更多配置：https://github.com/mscdex/ssh2#client-methods
  },
  qiniu: {
    accessKey: 'key',
    secretKey: 'key',
    bucket: 'name',  // 存储空间名称
    bucketDomain: 'http://xxx.qiniudn.com',
    ignoreFiles: ['*.map', '*.html', './dist/**.js']
  },
  keepReleases: 10,    // 保存历史版本数量
  workspace: 'build', // {相对路径}  本地待发布文件目录
  deployTo: '/var/www/front_end/github.com', // {绝对路径}  线上部署目录
  qiniuDeployTo: '/static', // {绝对路径} 七牛云将部署到该目录
}
```



**Setp 2: 开始部署**

执行 `mandy deploy` 命令执行部署任务

```bash
mandy deploy production
```



**enjoy ~**



## 配置

在当前目录下建立 `mandy.config.js` 文件，可进行自定义配置



**🌰 例子**

```javascript
module.exports = {
  deploy: {
    info: `部署自定义提醒`
  },
  rollback: {
    info: `回滚自定义提醒`
  }
}
```




## Todo

- ~~回滚版本~~
- ~~查看当前版本信息~~
- ~~任务驱动~~
- 更多自定义配置
- 完善文档
- 调整错误信息抛出



## License

MIT © zzetao