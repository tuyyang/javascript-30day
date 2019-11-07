# Day-20 Speech Detection 



## 实现效果
利用浏览器内置`API`，将说的话输出在页面上。仅chrome浏览器支持。

## 相关知识
有关语音识别接口`SpeechRecognition`的说明，可查看[MDN](https://developer.mozilla.org/zh-CN/docs/Web/API/SpeechRecognition)中的相关解释。

## 过程指南
1.由于目前只有chrome浏览器实现了此功能，故直接使用带有前缀的构造函数来构建一个语音识别对象。   
```js
const recognition = new SpeechRecognition();
```
2.设置语音识别对象的基本属性

```js
  //创建P标签，附加到DOM树
let p = document.createElement('p');
const words = document.querySelector('.words');
words.appendChild(p);

       
//监听recognition的result事件，获取到语音输入的文字
//e.results中保存的是识别的结果。转换为数组方便使用map join等方法
recognition.addEventListener('result', (e) => {
	const results = Array.from(e.results)
		.map(results => result[0]) 
		.map(results => result.transcript) //获取到没一段话
		.join('');

	//可以动态的将其中的一个词语替换
	const poopScript = results.replace(/good/gi, '👍');
	p.textContent = poopScript;

	//当前输入结束，有停顿时，会新建一个p标签
	if(e.results[0], isFinal) {
		p = document.createElement('p');
		words.appendChild(p);
	}
} )

//监听recognition的end事件，当输入结束后，再次开始，保持输入状态
recognition.addEventListener('end'. recognition.start);

recognition.start();
```
* `SpeechRecognition.lang = 'en-US';`

  该属性控制语音识别的语言，将其设置为英文，那么它就会以英文来识别出你所说的话。

* `e.results[0].isFinal`

  该值代表当前段的话有没有说完，当你在说话的时候，该值一直未false，但你停止时，该值变为true。可以用来判断是否为一段话。

## 延伸思考

由于国内网络原因，可考虑使用[科大讯飞的语音识别sdk](http://www.xfyun.cn/)，感兴趣的同学可自行尝试实现。
