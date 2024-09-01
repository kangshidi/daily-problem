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
如何创建BFC：
1. float的值不是none。
2. position的值不是static和relative。
3. display的值是inline-block、table-cell、flex或者inline-flex。
4. overflow的值不是visible。
开启BFC的作用：
1. 开启BFC的元素不会被浮动元素覆盖。
2. 取消盒子的margin塌陷（父子外边距不会合并）。
3. 开启BFC的元素可以包含浮动的子元素（解决浮动高度塌陷）。

### 6. CSS哪些属性能继承？
1. color
2. font-开头的
3. text-开头的
4. line-开头的
5. list-开头的

### 7. 消除图片底部间隙的方法
1. 图片块状化 - 无基线对齐： img {display: block;}
2. 图片底线对齐： img {vertical-align: bottom;}
3. 父级设置font-size: 0;
4. 行高足够小 - 基线位置上移： .father {line-height: 0}

### 8. CSS中的渐进增强，优雅降级之间的区别
1. 渐进增强（从下往上）：针对低版本的浏览器进行构建页面，保证最基本的功能，然后再针对高版本的浏览器进行效果、交互等改进和追加功能，达到更好的用户体验。
2. 优雅降级（从上往下）：一开始就构建完整的功能，然后再针对低版本的浏览器进行兼容。

### 9. 防抖
```javascript
function debounce(delay) {
  let timer;
  return function (value) {
    clearTimeout(timer);
    timer = setTimeout(function () {
      console.log(value);
    }, delay);
  }
}

const input = document.querySelector('#input');
const debounceFunc = debounce(500);
input.addEventListener('keyup', function(e) {
  debounceFunc(e.target.value);
});
```

### 10. 节流
```javascript
function throttle(delay) {
  let timer;
  return function (value) {
    if (timer) {
      return;
    }
    timer = setTimeout(function() {
      console.log(value);
      timer = null;
    }, delay);
  }
}
const throttleFunc = throttle(500);
window.addEventListener('resize', function(e) {
  throttleFunc(document.documentElement.clientHeight);
});
```

### 11. 手动实现call方法
```javascript
Function.prototype.myCall = function (context) {
  const args = [...arguments].splice(1);
  context.foo = this;
  const result = context.foo(...args);
  delete context.foo;
  return result;
};

const user = {
  name: 'xxx'
};
function bar (value1, value2) {
  console.log(this.name, value1, value2);
}
bar.myCall(user, 1, 2);
```

### 12. Event Loop 事件循环/事件轮询
1. 执行栈 + Web APIs（事件队列） + 宏任务队列。
2. 执行栈 + 浏览器管理的一个ES6的队列 + 微任务队列。
3. 执行栈中先执行同步任务，遇到微任务，放到浏览器的ES6管理的队列中，等时机到了，推到微任务队列，然后触发event loop机制进行轮询，将微任务队列中的任务放到执行栈中执行，之后进行DOM渲染。
4. 遇到宏任务，放到Web APIs队列中，等时机到了，推到宏任务队列，然后触发event loop机制进行轮询，将宏任务队列中的任务放到执行栈中执行。
5. 执行顺序：先在执行栈中执行同步任务 --> 微任务 --> DOM渲染 --> 宏任务。
6. await后面的内容相当于then的回调，属于微任务！


### 13. textarea标签默认支持换行，但是value值如果被trim的话，会有问题，展示不出来换行，只有第一行的字符。

### 14. 在react的jsx中，`0 && 'xxx'` 的运行之后结果，页面展示是0。
```javascript
0 && 'xxx'
// 页面展示：0
null && 'xxx'
// 页面什么都不展示
undefined && 'xxx'
// 页面什么都不展示
false && 'xxx'
// 页面什么都不展示
'' && 'xxx'
// 页面什么都不展示
```

### 15. 解决iOS手机端底部小黑线遮挡的问题。
```javascript
// html中需要设置viewport-fit=cover
<meta name="viewport" content="... viewport-fit=cover" />
// CSS
padding-bottom: env(safe-area-inset-bottom);
```

### 16. 解决项目中组件被重复挂载的问题。
描述：业务组件中，虽然useEffect监听的是[]空数组，但useEffect包裹的代码却被执行了多次（导致同样入参的接口被执行了多次），也就是说业务组件被重复挂载了多次。
原因：生成Route的组件中存在useState，或者其父组件存在render行为，导致该组件被更新（render），所以Route组件指定的component或者Route组件的指定的render函数被重新执行，导致业务组件被重复挂载。
解决方案：生成Route的组件中，缓存Route组件指定的component或者render函数。本项目中指定的是render函数（使用useCallback缓存）。
![Uploading image.png…]()


















