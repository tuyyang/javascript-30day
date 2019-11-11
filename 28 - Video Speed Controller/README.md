# Day-28 Video Speed Scrubber #



## 实现效果

控制视频的播放速率，并在速率导航条中显示速率大小

## 过程指南

​	通过计算当前鼠标位置占滚动条的百分比，算出当前播放速率，利用[playbackRate](https://developer.mozilla.org/zh-CN/docs/Web/Guide/Audio_and_video_delivery/WebAudio_playbackRate_explained)属性实现速率的控制

```js
const speed = document.querySelector('.speed');
const bar = document.querySelector('.speed-bar');
const video = document.querySelector('.flex');

function handleMove(e) {
	const y = e.pageY - this.offsetTop;
    // console.log(y);
    const percent = y / this.offsetHeight;
    // console.log(percent);
    const min = 0.4;
    const max = 4;
    const height = Math.round(percent * 100) + '%';
    // console.log(height);
    const playbackRate = percent * (max - min) + min;
    bar.style.height = height;
    bar.textContent = playbackRate.toFixed(2) + 'x'; //toFixed(2) 返回两位小数
    video.playbackRate = playbackRate;
}

speed.addEventListener('mousemove', handleMove);
```

* `toFixed()`：用定点表示法来格式化一个数值，我个人理解是返回值的小数位数
* `playbackRate`：b表示视频的播放速率，可直接为该属性赋值

