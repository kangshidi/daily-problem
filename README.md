# 日常问题

### 1. 老项目yarn install成功之后，yarn start报错，可能是因为node版本有问题。
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

### 2. 可以通过css中的`content`属性修改`<img>`标签中的src属性。
```css
img {
  content: url('./images/empty.png');
}
```

### 3. js中媒体查询。
```javascript
// 返回值为MediaQueryList对象。包含matches属性（boolean），以及media属性（string）。
const mqList = window.matchMedia('(max-width: 1920px)');
```
