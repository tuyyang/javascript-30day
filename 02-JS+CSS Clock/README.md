# Day-02  Clock时钟



## 实现效果

制作一个时钟显示实时时间

## 关键要点

1. 表盘上指针的样式：旋转的效果
2. 获取实时的时间
3. 每一秒改变一次指针状态

**涉及到的特性：**
- `transform-origin`
- `transform: rotate()`
- `transition`
- `transition-timing-function: cubic-bezier(x, x, x, x)`
- `setInterval(callback, time)`
- `new Date()`

## 过程指南

### CSS 部分

1. 调整指针的初始位置以及旋转的轴点
    [transform-origin](https://developer.mozilla.org/en-US/docs/Web/CSS/transform-origin)
    
    ```css
    transform-origin: 100%; // 或者可以用 right
    ```

2. 调整时钟指针跳动时的过渡效果
    ```css
    transition: all .5s;
    ```

3. 设置指针成为回弹的形式
	设置 `transition-time-function` 的值，以实现秒针“滴答滴答”的效果。此外注意 `transform` 中的 `rotate` （旋转）属性由角度来控制，可以试着在页面上修改这个参数来查看效果。
	
   
	
4. 用伪元素给表盘添加一个中心点
    ```css
     .clock-face::after{
            width: 1em;
            height: 1em;
            left: 50%;
            top: 50%;
            position: absolute;
            display: block;
            content: '' ;
            background-color: rgb(185, 123, 123);
            border-radius: 50%;
            box-shadow:
                    0 0 0 2px rgba(0,0,0,.1),
                    0 0 10px rgba(0,0,0,.2); 
            transform: translate(-50%, -50%);
            z-index: 15; 
        }
    ```

    

### JS 部分

1. 利用定时器自动更新时间
	定时器 `setInterval` 可以每隔一段固定的时间将操作放入执行队列，利用这个特性，加入页面后每秒更新一次时间，以实现秒针转动的效果。
	
	```javascript
	 setInterval(setDate, 1000);
	 // setDate 为每 1000 毫秒触发的 function
	```
	
2. 获取三个指针对应的 HTML 元素，留待后续操作
	
3. 编写 setTime 方法
	1. 创建 Date 对象
	
	2. 获取当前时间的小时、分钟、秒
	
	3. 利用此刻的数据，计算每个指针对应的角度
		```javascript
		const secondDeg = 90 + (second / 60) * 360;
		```
		以秒针为例，由于此页面初始状态中秒针为水平的，所以零点时（时间起始位置）应用到元素上的 `rotate` 旋转角度值应该为 90°。秒针转一圈为 60s，所以每一秒对应表盘上的角度值即为 (...s / 60s) * 360°。
		
		Wes Bos 给出的解决方案中，时针是和秒针一样每一小时跳动一次，若要模拟更加真实的时钟，要使时针在一小时内缓慢的移动到下一个时间点。所以可以利用上分钟，计算每一分钟对时针的角度影响，将加到时针角度上即可。
		
		```javascript
		const hourDeg = (90 + (hour / 12) * 360 + (min / 12 / 60) * 360);
		```
		
	4. 将角度值赋值给 HTML 元素的 `style` 中的 `transform` 属性

## 延伸思考

可以实现点开网页就显示实时时间

```js
setTime();

setInterval(function(){
	setTime();
}, 1000); 
```



关于解决时针跳转的办法，可以参考[soyaine](https://github.com/soyaine/JavaScript30)