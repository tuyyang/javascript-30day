# day-16 Mouse Shadow #



## 实现效果 ##

移动鼠标时，字体阴影随鼠标移动。

## 过程指南 ##

```js
const hero = document.querySelector('.hero');
const text = hero.querySelector('h1');
const walk = 100;  // 鼠标左右移动共移动的距离，改变这个值会出现不同的效果

function draw(e){
  const { offsetWidth: width, offsetHeight: height} = hero;
  let { offsetX: x, offsetY: y} = e;

  // 使鼠标移动到中间元素上，x、y的值连续变化
  if(e.target !== this){
  // if(e.target == text){
    x = x + e.target.offsetLeft;
    y = y + e.target.offsetTop;
  }
  // const xaisx = (x/width*walk)-(walk/2);
  // const yaisx = (y/height*walk)-(walk/2);
  const xaisx = Math.floor((x/width*walk)-(walk/2));
  const yaisx = Math.floor((y/height*walk)-(walk/2));
  text.style.textShadow = `
    ${xaisx}px ${yaisx * -1}px 2px rgba(0,255,0,0.7),
    ${xaisx * -1}px ${yaisx}px 2px rgba(255,0,0,0.7),
    ${yaisx}px ${xaisx * -1}px 2px rgba(188,188,188,0.7),
    ${yaisx * -1}px ${xaisx}px 2px rgba(0,0,255,0.7)      
    `; // 多写几个就有了霓虹灯的效果
}
hero.addEventListener('mousemove',draw);
```

* HTMLElement.offsetTop：指的是当前元素到其offsetParent指向元素的__上边距__的距离。
* HTMLElement.offsetLeft：指的是当前元素到其offsetParent指向元素的__左边距__的距离。
* HTMLElement.offsetHeight：指的是当前元素的__高度__，包含__content，padding，border__的高度值，但不包括__margin__的值。
* HTMLElement.offsetWidth：指的是当前元素的__宽度__，包含__content，padding，border__的高度值，但不包括__margin__的值。