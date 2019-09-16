# Day-05 Flex 实现可伸缩的图片墙 



## 实现效果

点击任意一张图片，图片展开，同时从图片上下两方分别移入文字。点击已经展开的图片后，图片被压缩，同时该图片上下两端的文字被挤走。

## 过程指南

### CSS 部分

1. 将```.panels```以及每个```panel```设置 ```display：flex```

2. 设定每个```panel```的```flex```值为1，使用```flex-direction: column```使文字纵向排列

   ```css
   .panel {
         background:#6B0F9C;
         box-shadow:inset 0 0 0 5px rgba(255,255,255,0.1);
         color:white;
         text-align: center;
         align-items:center;
         /* Safari transitionend event.propertyName === flex */
         /* Chrome + FF transitionend event.propertyName === flex-grow */
         transition:
           font-size 0.7s cubic-bezier(0.61,-0.19, 0.7,-0.11),
           flex 0.7s cubic-bezier(0.61,-0.19, 0.7,-0.11),
           background 0.2s;
         font-size: 20px;
         background-size:cover;
         background-position:center;
         display: flex;
         flex: 1;
         justify-content: center;
         flex-direction: column;
         /* border: 1px solid #000; */
       }
   
   	.panel > * {
         margin:0;
         width: 100%;
         transition:transform 0.5s 0.7s;
         display: flex;
         flex: 1 0 auto;
         justify-content: center;
         align-items: center;
       }
   
       .panel p {
         text-transform: uppercase;
         font-family: 'Amatic SC', cursive;
         text-shadow:0 0 4px rgba(0, 0, 0, 0.72), 0 0 14px rgba(0, 0, 0, 0.45);
         font-size: 2em;
         /* border: 1px solid #000; */
       }
       .panel p:nth-child(2) {
         font-size: 4em;
       }
   
       .panel p:first-child{
           transform: translateY(-100%)
       }
   
       .panel.open p:first-child{
           transform: translateY(0);
       }
   
       .panel p:last-child{
           transform: translateY(100%);
       }
   
       .panel.open p:last-child{
           transform: translateY(0);
       }
   
       .panel.open {
           flex: 5;
           font-size:40px;
       }
   ```

   

### JS 部分

1. 获取所有类名为 `panel` 的元素
2. 为其添加 `click` 事件监听，编写触发事件调用的函数（给触发的 DOM 元素添加/去掉样式，实现拉伸/压缩的效果）
3. 为其添加 `transitionend` 事件监听，编写调用的函数（添加/去掉样式，实现文字的飞入/飞出效果）

## 相关知识

这一部分还没有太明白，等弄清楚了再补充



