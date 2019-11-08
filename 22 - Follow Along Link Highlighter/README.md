# Day-22 Follow Along Link Highliter 



## 实现效果
白色高亮背景框随鼠标在不同标签之间移动。

## 过程指南
1.生成绝对定位块元素

```js
const triggers =document.querySelectorAll('a');
const highlight = document.createElement('span');
highlight.classList.add('highlight');
document.body.append(highlight);

//避免第一次高亮方块会从左上角移动至对应标签处
highlight.style.display = 'none';
```
2.获取对应标签的位置信息

```js
function highlightLink() {
	const linkCoords = this.getBoundingClientRect();
	console.log(linkCoords);
	const coords = {
		width: linkCoords.width,
		height: linkCoords.height,
        top: linkCoords.top + window.scrollY,
        left: linkCoords.left + window.scrollX
    };

    highlight.style.width = `${coords.width}px`;
    highlight.style.height = `${coords.height}px`;
    highlight.style.transform = `translate(${coords.left}px, ${coords.top}px)`

     highlight.style.display = 'inline';
}

          
```
3.绑定事件

```js
triggers.forEach(a => a.addEventListener('mouseenter', highlightLink));  
```

## 相关知识

1. `rectObject = object.getBoundingClientRect()` 

| Attribute | Type  | Description                                                  |
| --------- | ----- | ------------------------------------------------------------ |
| bottom    | float | Y 轴，相对于视口原点（viewport origin）矩形盒子的底部。只读。 |
| height    | float | 矩形盒子的高度（等同于 bottom 减 top）。只读。               |
| left      | float | X 轴，相对于视口原点（viewport origin）矩形盒子的左侧。只读。 |
| right     | float | X 轴，相对于视口原点（viewport origin）矩形盒子的右侧。只读。 |
| top       | float | Y 轴，相对于视口原点（viewport origin）矩形盒子的顶部。只读。 |
| width     | float | 矩形盒子的宽度（等同于 right 减 left）。只读。               |
| x         | float | X轴横坐标，矩形盒子左边相对于视口原点（viewport origin）的距离。只读。 |
| y         | float | Y轴纵坐标，矩形盒子顶部相对于视口原点（viewport origin）的距离。只读。 |

2. 当滚动位置发生了改变，`top`、`left`需要加上当前的滚动位置（`window.scrollY`、`window.scrollX`）

   

> [getBoundingClientRect](https://developer.mozilla.org/zh-CN/docs/Web/API/Element/getBoundingClientRect)





