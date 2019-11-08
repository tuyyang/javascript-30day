# Day-23 Speech Synthesis 



## 实现效果
在文本域输入对应语言文字，点击`speak`浏览器可以阅读输入的文字，点击`stop`浏览器会停止阅读；拖动`rate`和`pitch`滑块可以改变阅读的速度和音调。

## 过程指南

1. 设置语言下拉框

   ```js
   function populateVoices() {
   	voices = this.getVoices();
   	voicesDropdown.innerHTML = voices
   		// .filter(voice => voice.lang.includes('en'))
   		.map(voice => `<option value="${voice.name}"> 				${voice.name} (${voice.lang}) </option>`)
   		.join('');
   }
   
   //设置当前语言
   function setVoice() {
   	msg.voice = voices.find(voice => voice.name === this.value);
       toggle();
    }
   ```

2. 播放和暂停

   ```js
   function toggle(startOver = true) {
   	speechSynthesis.cancel();
   	if(startOver){
   		speechSynthesis.speak(msg);
        }
   }
   ```

3. 切换语音的语速和语调

   ```js
   function setOption() {
   	console.log(this.name, this.value);
   	msg[this.name] = this.value;
   	toggle();
   }
   ```

4. ```js
   //监听语音对象的语言改变事件
   speechSynthesis.addEventListener('voiceschanged', populateVoices);
   //当切换语言选择下拉菜单时被调用
   voicesDropdown.addEventListener('change', setVoice);
   //语速、语调改变
   options.forEach(option => option.addEventListener('change', setOption));
   //播放、暂停
   speakButton.addEventListener('click', toggle);
   stopButton.addEventListener('click', () => toggle(false));
   ```

   

## 相关知识   
* [SpeechSynthesisUtterance](https://developer.mozilla.org/zh-CN/docs/Web/API/SpeechSynthesisUtterance)

* [SpeechSynthesis](https://developer.mozilla.org/zh-CN/docs/Web/API/SpeechSynthesis)












