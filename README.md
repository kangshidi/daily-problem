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

### 4. 滚动同步
![1690427120289](https://github.com/kangshidi/daily-problem/assets/10253051/d5d61b80-ee5e-4a2f-89e0-8955ee8b4ffa)

![1690427169013](https://github.com/kangshidi/daily-problem/assets/10253051/3dc63a8f-1008-48f9-b561-0343265ee009)

![1690427234672](https://github.com/kangshidi/daily-problem/assets/10253051/79b31df9-79cc-401f-a152-a4dad0fb5138)

### 5. BFC
块级格式化上下文，它指的是一个独立的块级渲染区域，只有Block-level box参与。该区域拥有一条渲染规则来约束块级盒子的布局，且与区域外部无关。  
现象：  
一个盒子不设置height，当内容子元素都浮动时，无法撑起自身，这个盒子没有形成BFC。  
如何创建BFC：  
1. float的值不是none。
2. position的值不是static和relative。
3. display的值是inline-block、flex或者inline-flex。
4. overflow：hidden。 <br>
BFC的其他作用：
1. 取消盒子的margin塌陷。
2. 阻止元素被浮动元素覆盖。

















