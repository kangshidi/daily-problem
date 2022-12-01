# 日常问题

### 1. 老项目yarn install成功之后，yarn start报错，可能应为node版本有问题。
![yarn start错误](/images/node_error.png "")

解决方法：<br>
1. 可以修改package.json中的scripts。
```
// package.json文件

"scripts": {
  "start": "set NODE_OPTIONS=–-openssl-legacy-provider & node scripts/start.js"
}
```
2. 添加操作系统的环境变量。 <br>
`NODE_OPTIONS : -–openssl-legacy-provider`


