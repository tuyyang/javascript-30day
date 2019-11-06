# Day-19 Webcam Fun 

   

## 实现效果
调用用户摄像头，实现保存、修改图片样式的效果。



## 过程指南
1.申请调用`WebCam `  

```js
function askWebcam() {
     navigator.getUserMedia = navigator.getUserMedia ||
        navigator.webkitGetUserMedia ||
        navigator.mozGetUserMedia;
    if (navigator.getUserMedia) {
        navigator.getUserMedia({
            audio: false,
            video: {
                width: 300,
                height: 200
            }
        }, function(stream) {
            //若成功
            video.srcObject = stream;
            video.onloadedmetadata = function(e) {
                video.play();
            }
        }, function(err) {
            console.log('Error occured:' + err.name);
        });
    } else {
        console.log('this navigator doesn\'t support webcam!');
    }
}
```
* `navigator.getUserMedia`

  `getUserMedia`方法为我们提供了访问网络摄像头或麦克风的权限，该方法接受一个对象作为参数，通过该对象即可获得来自多媒体设备的数据。

2.截图函数 `takePhoto()`，此处将原始图像数据保留一份，否则使用滤色函数处理后，被滤掉的颜色无法恢复，保存了原始图像数据后，只需要重新绘制在canvas上即可。   

```js
function takePhoto() {
    ctx.drawImage(video, 0, 0, 300, 200);
    //将原始截图保存,
    origindata = ctx.getImageData(0,0,300,200);
}
```
* 点击`takePhoto()`函数时调用`canvas`绘图上下文中的`drawImage()`方法将视频中当前帧的图像绘制在canvas上，该方法第一个参数可以为图像或视频

  

3.色彩过滤   

在所有滑块的父元素上监听`change`事件，当滑块的值发生改变时，先通过e.target.name确定是哪个颜色的范围要求发生了变化，再访问e.target.value获得变化值，通过与全局变量`filter`作比较来获得滤色值的上下限要求。
重点难点解释如下：   

```js
        /*startPos表示操作像素点数据时的起点，从canvas获取到的像素数据每四个值表示一个像素点例如滑块为红色，则只需要改变像素数组中第0,4,8......个元素的值。通过target.value的首字母即可判断滤色过程应该检查的颜色*/
        const startPos = {'r':0,'g':1,'b':2}[target.name[0]];
        /*filterMin和filterMax表示相应的滤色范围上下限，若修改了红色滤色范围则取红色范围值。若修改蓝色的滤色范围，则取蓝色。checkFilter()函数将改变后的值与滤色标准`filter`进行比较，将更改滤色标准后需要调整的颜色类别(r,g,b)对应的上下限返回给结果。*/
        var tempFilter = checkFilter(target.name, target.value);
        const filterMin = tempFilter.min;
        const filterMax = tempFilter.max;   
```


4.保存图片   

使用`canvas.toDataUrl()`方法将`canvas`画布保存为图片，默认为png格式，该数据可作为`img.src`的值，也可利用`a`标签将其下载.   

```js
//保存图片
function savePhoto() {
    img.src = canvas.toDataURL();
    a.href = canvas.toDataURL();
    a.setAttribute('download', 'handsome');
}
```
* 点击`savePhoto()`函数时调用`canvas`的`toDataUrl()`方法即可获得canvas中的图像数据，默认格式为png，也可修改为其他格式，生成的图像数据指定给`img.src`时即可预览图片
* 在`img`标签外添加`a`标签，并为其添加`download`属性，当点击链接时，即可将生成的图片保存至本地