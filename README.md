![1690427234672](https://github.com/kangshidi/daily-problem/assets/10253051/cfe83509-8a0a-412e-80fd-58cec549f745)# 日常问题

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

### 4. 滚动同步
![1690427120289](https://github.com/kangshidi/daily-problem/assets/10253051/d5d61b80-ee5e-4a2f-89e0-8955ee8b4ffa)

![1690427169013](https://github.com/kangshidi/daily-problem/assets/10253051/3dc63a8f-1008-48f9-b561-0343265ee009)

![1690427234672](https://github.com/kangshidi/daily-problem/assets/10253051/79b31df9-79cc-401f-a152-a4dad0fb5138)
