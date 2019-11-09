# Day-24 Sticky Nav 



## 实现效果
页面滑动时导航栏能固定在顶部，页面logo向右滑出。一个比较实用的方法。

## 过程指南    
```js
const nav = document.querySelector('#main');
const topOfNav = nav.offsetTop;

function fixNav() {
	// console.log(topOfNav,scrollY);
	if(window.scrollY >= topOfNav){
		document.body.style.paddingTop = `${nav.offsetHeight}px`;
        document.body.classList.add('fixed-nav');
     } else {
         document.body.style.paddingTop = 0;
         document.body.classList.remove('fixed-nav');
         }
}

window.addEventListener('scroll', fixNav);
```

1. 获取导航栏到window顶部的距离
2. 当页面滚动距离大于或等于导航栏到顶部的距离时，为`body`添加类名`fixed-nav`
3. 在`fixed-nav`下的`nav`是`fixed`布局，因此会脱离文档流，在滚动至导航栏时会有上下跳动问题，在滚动至`nav`时，为`body`添加`paddingTop`的值等于导航栏高度`nav.offsetHeight`



```css
.fixed-nav .site-wrap{
  transform: scale(1);
}
.fixed-nav nav{
  position: fixed;
  box-shadow: 0 10px 10px rgba(0,0,0,0.2);
}
.fixed-nav li.logo{
  max-width: 500px;
}
```

* 当滑动到导航栏的位置时，要使导航列表最左侧的logo图标显示出来，所以设置`max-width`属性
* 列表使用了flex布局，`flex:1`代表让所有弹性盒模型对象的子元素都有相同的长度，并且忽略它们内部的内容。不管设置它的`width`属性值为多少，都不会有作用，因此使用`max-width`对其进行宽度上的限制

