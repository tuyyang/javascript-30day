# Day-03  CSS Variable



## 实现效果

用 JavaScript 和 CSS3 实现拖动滑块时，实时调整图片的内边距、模糊度、背景颜色，同时标题中 JS 两字的颜色也随图片背景颜色而变化。

## 涉及特性

- [`:root`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:root)
- `var(--xxx)`：CSS 变量（[CSS Variables](https://developer.mozilla.org/zh-CN/docs/Web/CSS/Using_CSS_variables)）
- `filter: blur()`
- 事件 `change`、`mousemove`

## 过程指南

### CSS 部分准备

1. 声明全局（`:root`）的 CSS 变量

2. 将变量应用到页面中对应元素 `<img>` 、`<h1>`

   ```css
   :root{
           --spacing: 10px;
           --blur: 5px;
           --base: #8aa8af;
       }
   img{
           padding: var(--spacing);
           filter: blur(var(--blur));
           background: var(--base);
       }
   .h1{
           color: var(--base);
       }
   ```

   

### JS 实时更新 CSS 值
1. 获取页面中 `input` 元素

   ```js
   const inputs = document.querySelectorAll('.controls input');
   ```

   

2. 给每个 `input` 添加监听事件，触发更新操作；添加鼠标滑过时的事件监听

   ```js
   inputs.forEach( input => input.addEventListener('change', handleUpdate));
   inputs.forEach( input => addEventListener('mousemove', handleUpdate));
   ```

   

3. 实时更新的方法
  1.  获取参数值后缀
  - 获取参数名（blur、spacing、color）
  - 获取参数值（12px、#efefef）
  - 赋值给对应的 CSS 变量

```js
function handleUpdate(){
	const suffix = this.dataset.sizing || ''; 
    document.documentElement.style.setProperty(`--${this.name}`, this.value + suffix); 
    document.getElementById(`code-${this.name}`).innerText = this.value + suffix;  //页面参数实时显示
}
```



## 补充知识

1. 自定义数据属性 `dataset`

  HTML5 中可以为元素添加非标准的自定义属性，只需要加上 `data-` 前缀。可以通过元素的 `dataset` 属性来访问这些值，`dataset` 的值是 DOMStringMap 的一个实例化对象，其中包含之前所设定的自定义属性的“名-值”对。

2. [CSS variable](https://developer.mozilla.org/zh-CN/docs/Web/CSS/Using_CSS_variables)

  命名写法是 `--变量名`，在引用这个变量时写法是 `var(--变量名)`。

3. CSS 滤镜 [filter](https://developer.mozilla.org/zh-CN/docs/Web/CSS/filter)

  可以实现很多有意思的效果，具体可自行搜索。

