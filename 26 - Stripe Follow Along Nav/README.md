# Day-26 Strip Follow Along Nav 



## 实现效果
当鼠标移动导航栏时，出现下拉菜单的动画。

## 过程指南   

```js
const triggers = document.querySelectorAll('.cool>li');
const background = document.querySelector('.dropdownBackground');
const nav = document.querySelector('.top')

function handleEnter() {
	// console.log(this);
	this.classList.add('trigger-enter');
	setTimeout( () => this.classList.contains('trigger-enter') && 		this.classList.add('trigger-enter-active'),150); //延迟添加下拉菜单的类名
     background.classList.add('open');

     const dropdown = this.querySelector('.dropdown');
     const dropdownCoords = dropdown.getBoundingClientRect();
     const navCoords = nav.getBoundingClientRect();
     // console.log(dropdownCoords);
     // console.log(navCoords);
                      
      const coords = {
 			width: dropdownCoords.width,
            height: dropdownCoords.height,
            left: dropdownCoords.left - navCoords.left,
            top: dropdownCoords.top - navCoords.top
       };
       background.style.setProperty('width', `${coords.width}px`);
       background.style.setProperty('height', `${coords.height}px`);
  	        background.style.setProperty('transform',`translate(${coords.left}px,${coords.top}px)`);
}

function handleLeave() {
	this.classList.remove('trigger-enter','trigger-enter-active');
	background.classList.remove('open');
}

triggers.forEach(trigger => trigger.addEventListener('mouseenter', handleEnter)) ;
triggers.forEach(trigger => trigger.addEventListener('mouseleave', handleLeave)) ;
```

1. 使用一个白色的`div`块做背景实现滑动效果，如果直接设置下拉菜单为白色背景，那么鼠标的每次移动都会有一个消失间隙，不能达到预期效果

   

2. 设置`150ms`延迟之后再添加`trigger-enter-active`类，避免鼠标在各选项中间快速移动而出现下拉菜单显示错误

   ```js
   this.classList.add('trigger-enter');
   setTimeout( () => this.classList.contains('trigger-enter') && this.classList.add('trigger-enter-active'),150); 
   ```

3. 在为白色背景块设置左边距和上边距时，需要减去导航栏的左边距和上边距，避免造成偏移





