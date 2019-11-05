# Day-18 使用reduce进行时间累加



## 实现效果
将所有的时间累加在一起，并用时：分：秒来表示计算的结果

## 过程指南

```js
//转换时间格式并累加时间
var result = Array.from(document.querySelectorAll('li')).map(function(item){
	var tempStr = item.dataset.time.split(':');
	return parseInt(tempStr[0],10) * 60 + parseInt(tempStr[1],10);
}).reduce(function(a,b){
	return a + b;
},0);

showRes(result);

//结果格式化函数
function showRes(seconds){
	var sec = seconds % 60;
	var hour = Math.floor(seconds/3600);
	var min = (seconds - 3600*hour - sec)/60;
	document.querySelector('#totaltime').innerHTML = `${hour}小时${min}分${sec}秒`;
}
```

* 使用`split(":")`将分钟和秒钟分开