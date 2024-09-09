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
描述：业务组件中，虽然useEffect监听的是[]空数组，但useEffect包裹的代码却被执行了多次（导致同样入参的接口被执行了多次），也就是说业务组件被重复挂载了多次。<br/>
原因：生成Route的组件中存在useState，或者其父组件存在render行为，导致该组件被更新（render），所以Route组件指定的component或者Route组件的指定的render函数被重新执行，导致业务组件被重复挂载。<br/>
解决方案：生成Route的组件中，缓存Route组件指定的component或者render函数。本项目中指定的是render函数（使用useCallback缓存）。<br/>
```javascript
// 缓存render函数
const pureRender = useCallback((props) => (
  <routeObj.component {...props} />
), []); // 在项目中导致了其他的问题（No.17），非最终解决方案。
return (
  <Route
    path={path}
    render={pureRender}
  />
);
```

### 17. 解决项目中浏览器地址栏url查询参数发生变化，但哈希路由没有发生变化时，组件没有响应变化的问题。
该问题是由No16的修改方法不恰当而导致的。<br />
原因：由于Route组件指定的render函数被useCallback缓存住了，而useCallback监听是空数组，所以不管url是否发生变化，都不会重新挂载路由组件。<br />
这样做其实没有问题，**<big>因为Route组件会自动给路由组件传参：location，history和match。url发生变化，也就是说location参数发生了变化，也就是说路由组件的入参发生了变化，路由组件虽然不会重新挂载，但是会执行update。如果路由组件中存在监听url查询参数的逻辑，就会执行相应的操作。</big>**<br />
但是项目中的大部分组件都没有做监听url参数的处理逻辑，导致url中的查询参数发生了变化（一般是code或者id），业务组件都没有感知到（重新下发接口）。
由于修改量太大，所以考虑回避方案：当url中查询参数发生变化，而哈希路由并没有发生变化时，也需要重新挂载组件。<br />
解决方案：<br />
在生成Route的组件中做修改，useCallback监听location或者location中的查询参数search（更精准）的变化，如果location或者search发生变化了，就重新生成render函数，Route组件监听到入参render发生了变化，会重新执行render函数，从而得到一个新的component（路由组件被重新挂载）。
```javascript
import loadable from '@loadable/component';
// Switch组件会自动给其children组件传参location。
// 当url中的哈希路由发生变化时，Switch组件会自动挂载对应的children组件。
// 但是url中哈希路由没有发生变化，只是查询参数发生变化时，Switch不会重新挂载children组件，只会更新location参数。
const { location: { search } } = props;
// routeObj.component是通过loadable函数动态加载的。
const routeObj = {
  component: loadable('./xxx.js');
};
// props一定要透传给路由组件，这样Route组件才可以自动给路由组件传参（location，history和match）
const pureRender = useCallback((props) => (
  <routeObj.component {...props} />
), [search]); // 监听查询参数，重新生成render函数，返回新的路由组件，也就是重新挂载路由组件

return (
  <Route
    path={path}
    render={pureRender}
  />
);
```

### 18.  自定义表单控件。

由于项目中联合查询的场景比较多，每个查询条件改变时都需要下发查询接口，每次写一大堆下拉框，input框相当耗时。<br />

优化：采用Form接管这些查询框，通过**onValuesChange** 直接抛出所有的查询条件。<br />

常规的一些查询框可以直接使用antd的组件，把下拉框的数据获取等操作用组件封装起来。<br />

组件的一些参数如下：<br />

（1）dataSource参数，数组类型，每个查询条件是一个对象，包含如下字段：<br />

dataIndex：查询字段名，Form.Item的name<br />

type：input还是select还是treeSelect等等，可以自定义表单控件，来完成一些业务操作<br />

还有查询组件的一些配置项，allowClear，maxLength，options，onChange等等**直接透传给各个组件。** <br />

（2）onAllChange参数，当任何一个查询框发生改变时触发，抛出所有查询条件(**在onValuesChange回调函数中获取allValues**)。<br />

{dataIndex1: value1, dataIndex2: value2, ...}<br />

![image](https://github.com/user-attachments/assets/d6b28a91-11a3-47ce-8e5f-a471d689dd71)


原生antd组件可直接被form表单接管，但自定义表单控件如何通知form表单，它的值被修改了呢？<br />

**被设置了name属性的Form.Item包装的控件，表单控件会自动添加value和onChange，数据同步将被Form接管。** <br />

**自定义控件只需要接收到value后给内部赋值，之后如果用户改变了值，自定义控件需要将改变后的值，当作参数触发onChange回调以通知表单。** <br />

**此时表单就收集到自定义控件的value发生了变化，从而触发onValuesChange，同时会将收集到的value再传给自定义控件以便更新。** <br />

重要：**自定义控件内部不要使用setState来维护value，只需要告知表单即可，表单来通知控件更新value。** <br />

自定义控件应该注意以下几点：<br />

（1）你不再需要也不应该用 onChange 来做数据收集同步（你可以使用 Form 的 onValuesChange），但还是可以继续监听 onChange 事件。<br />

（2）你不能用控件的 value 或 defaultValue 等属性来设置表单域的值，默认值可以用 Form 里的 initialValues 来设置。注意 initialValues 不能被 setState 动态更新，你需要用 setFieldsValue 来更新。<br />

（3）你不应该用 setState，可以使用 form.setFieldsValue 来动态改变表单值。<br />

![image](https://github.com/user-attachments/assets/ac6d2c70-ea8a-4bde-a44e-7ce584c19a81)

### 19. 表单控件回填。
假如No18中的查询框存在默认值，并且这个默认值还是异步获取到的，应该如何去给各个表单控件回填默认值呢？<br />
误区：每个表单控件追加入参defaultValue，组件内部去监听defaultValue的变化，然后自行通过setState赋值给value。<br />
正确方式：<br />
每个表单控件的defaultValue应当是一次性的（antd原生组件都是如此），不需要监听变化。<br />
**只有value是受控属性，表单控件内部也不去使用setState来维护value，通过onChange通知Form接管，Form会自动给表单控件传value用来更新。** <br />
**通过Form的setFieldsValue来动态改变每个组件的回填值。**


### 20. 自定义表单控件校验失败时，如何设置红框？

原生antd组件有一些提供status参数，可以手动设置error或者warning，表单校验失败时，也可以自动红框。<br />
但是自定义表单控件如何获取到校验结果呢？<br />
**Form.Item会自动给其包装的控件传值aria-invalid，如果校验失败，该值为一个字符串‘true’，此时控件可以根据这个值来设置error时的class。** <br />
![image](https://github.com/user-attachments/assets/ec4bcd11-b856-426f-a153-4004c1a4c1a6)

如果校验成功，Form.Item就不给包装组件传这个值了。<br />
​
![image](https://github.com/user-attachments/assets/9d27655d-e7f9-4680-afb3-e884d786d5f5)

### 21. 框架布局整改。
修改前的布局：浏览器顶部固定展示菜单栏，剩下的内容区域高度auto，超过浏览器的高度后内容区域右侧出现纵向滚动条。<br />
项目中有很多写死的高度，以及一些calc的计算，也是写死的，页面很多模块都使用fixed定位，非常不好维护。<br />
修改后的布局：浏览器顶部固定展示菜单，底部固定展示实时滚动新闻，中间为路由页面的内容区域，内容区页面超长的话，只有中间部分的右侧出现滚动条。<br />
顶部菜单和底部新闻采用固定高度和fixed定位，除此之外的其他各页面模块如果需要固定使用absolute定位，方便维护。<br />
微服务嵌入的页面高度设置为height: 100%。<br />

难点：
1. z-index的设置。<br />
（1）由于内容区域有全屏展示的功能，所以内容区域的z-index需要高于顶部菜单和底部新闻。<br />
（2）由于工具箱需要展示在任何页面的最上方，所以要高于内容区域的z-index的设置。<br />
（3）由于antd的message组件的z-index为1010，所以内容区域的z-index需要小于antd-message的z-index。<br />
（4）由于antd的modal组件z-index为1000，所以内容区域的z-index需要小于antd-modal-mask的z-index。<br />
2. 高度自适应。<br />
采用flex布局，flex-direction设置为column，高度设置为100%，overflow设置为hidden。<br />
其第一个child高度为auto，第二个高度设置为100%，overflow设置为auto（自动撑满整个父节点，高度超出时出现纵向滚动条）。<br />

PS：为什么z-index设置无效？<br />
（1）需要建立层叠上下文，同一个层叠上下文中的z-index大的值会盖在小的上面。<br />
（2）同一个层叠上下文中的相同z-index节点，后来者居上。<br />
（3）嵌套的层叠上下文，比如z-index为2的节点下面存在一个z-index为99的节点的节点，永远不会盖在跟z-index为2的节点是同一个层叠上下文的z-index为3的节点上方。<br />
<br />

以下几种元素可以产生层叠上下文，z-index的值才有效：
<img width="623" alt="image" src="https://github.com/user-attachments/assets/dafc93b0-6fa8-4619-a91c-e615ace95de1">

参考文献：https://zhuanlan.zhihu.com/p/340371083



















