# Day-21 Geolocation 



## 实现效果
练习`NavigatorGeolocation.geolocation`的使用，通过此`API`可以访问用户位置。
由于笔记本电脑一般不带速度及方向传感器，从结果中可以看到返回值中`heading`及`speed`键值均为`null`,为演示可视化效果，代码中采用手动赋值的方式进行演示。   

## 过程指南

```js
const arrow = document.querySelector('.arrow');
const speed = document.querySelector('.speed-value');

    navigator.geolocation.watchPosition((data) => {
      console.log(data);
      speed.textContent = data.coords.speed;
      arrow.style.transform = `rotate(${data.coords.heading}deg)`;
    }, (err) => {
      console.error(err);
    });
可以看到只要通过调
```
* `navigator API`的使用与说明

  * `Geolocation.watchPosition()`用于注册监听器，在设备的地理位置发生改变的时候自动被调用。

  [Geolocation API](https://developer.mozilla.org/zh-CN/docs/Web/API/Geolocation/watchPosition)

  * `Geolocation.getCurrentPosition()`只可获取一次当前的位置。

  

  [MDN](https://developer.mozilla.org/zh-CN/docs/Web/API/Geolocation)

  

  

  


