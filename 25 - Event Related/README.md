# Day-25 Event Related 



## 实现效果
本次练习目的是了解DOM的事件机制，包括事件捕获，事件冒泡，单次执行事件。

## 过程指南   
```js
const divs = document.querySelectorAll('div');
const button = document.querySelector('button');

function logText(e) {
	console.log(this.classList.value);
            
}

divs.forEach(div => div.addEventListener('click', logText,{
	capture: true
}));
```

```html
<div class="one">
	<div class="two">
		<div class="three"></div>
	</div>
</div>
```

1. ### [EventTarget.addEventListener](https://developer.mozilla.org/zh-CN/docs/Web/API/EventTarget/addEventListener) ###

   * 接收三个参数：`type`、`listener`、`options`

     * `type`：事件的名称，如`click`、`dbclick`、`change`等

     * `listener`：该事件的回调函数

     * `options`

       ​			 `captrue` ：是否事件捕获，默认`false`

       ​			  `once`：单次执行事件，默认`false`，为`true`时只执行一							次

2. 当为某个元素注册了事件时，会将从外至内的元素监听器放在一个栈内。如当点击了最里面的`three`，相当于先点到`body`，如果`body`上注册了事件，入栈；接着是`one`，注册了事件，入栈；`two`注册了事件，入栈；然后是`three`，注册了事件，入栈。

   当`captrue`为`false`时，事件在冒泡阶段才被执行，先进后出，输出：`three two one`；为`true`时，事件在捕获阶段就会被执行，输出：`one two three`

3. ### `stopPropagation`  ###

   事件不在捕获阶段执行，不进行事件冒泡，只执行最内层的监听器



