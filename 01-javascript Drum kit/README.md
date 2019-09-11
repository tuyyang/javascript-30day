# Day01 DRUM KIT

实现效果：按下"A~L"其中的一个键，会发出不同的声音，并实现动画效果。

## 关键事件
1. 播放声音
2. 动画效果

## 页面基础布局
 * `data-key="" ` --填写对应的keyCode
 * `transition: all .07s ease;` --定义动画时间
 * `transform: scale(1.2);` 
 * 动画时间和改变大小可以自定义
 
 ## JS
* 使用了ES6模板字符串：`${e.keyCode}`,可以使audio动态的获取每一个按键keyCode，从而找到对应的audio。
* `audio.currentTime = 0` 每一次点击前重置音效
* `key.classList.add('playing')` 给元素添加 `playing` 类

