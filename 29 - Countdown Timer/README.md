# Day-29 Countdown Timer #



## 实现效果 ##

显示时钟倒计时，以及计时于何时结束

## 过程指南

1. `timer`函数使用计时器实现倒计时

   ```js
   function timer(seconds) {
       //clear any existing timers
       clearInterval(countdown);
   
       const now = Date.now();
       const then = now + seconds * 1000;
       displayTimeLeft(seconds);
       displayEndTime(then);
       
       countdown = setInterval(() => {
           const secondsLeft = Math.round((then - Date.now()) / 1000);
           //check if we should stop it
           if(secondsLeft < 0) {
               clearInterval(countdown);
               return;
           }
           //display it
           displayTimeLeft(secondsLeft);
           
       }, 1000);
   }
   ```

   * `Date.noe()`：显示当前时间的时间戳，等同于`(new Date()).getTime()`

   * 调用两次`displayTimerLeft`是让界面显示从倒计时开始显示，而不会少一秒

   * `clearInterval(countdown)`在函数开始就先清除所有的计时器

     

2. `displayTimeLeft`函数实现页面的更新，并以分：秒的形式显示

   ```js
   function displayTimeLeft(seconds) {
       const minutes = Math.floor(seconds / 60);
       const remainderSeconds = seconds % 60;
       const display = `${minutes}:${remainderSeconds < 10 ? '0' : ''}${remainderSeconds}`;
       document.title = display;
       timerDisplay.textContent = display;
       // console.log(minutes,remainderSeconds);
   }
   ```

3. `displayEndTime`函数实现倒计时将于何时结束

   ```js
   function displayEndTime(timestamp) {
       const end = new Date(timestamp);
       const hour = end.getHours();
       const minutes = end.getMinutes();
       endTime.textContent = `Be Back At ${hour}:${minutes < 10 ? '0' : ''}${minutes}`;
   }
   ```

4. 通过对固定时间按钮的监听，获取该按钮所对应的时间

   ```js
   function startTimer() {
       const seconds = parseInt(this.dataset.time);
       timer(seconds);
         
   }
   
   buttons.forEach(button => button.addEventListener('click', startTimer));
   ```

5. 对用户自定义输入框监听实现自定义倒计时

   ```js
   document.customForm.addEventListener('submit', function(e) {
       e.preventDefault();
       const mins = this.minutes.value;
       console.log(mins);
       timer(mins * 60);
       this.reset();
   })      
   ```

   * `document.customForm`：若`form`或`input`元素具有`name`属性，可以通过`document.[name]`来获取该DOM元素。如`document.customForm.minutes`获取`name`属性值为`minutes`的`input`元素
   * `submit`事件默认会使页面刷新，使用`e.preventDefault`阻止默认事件的触发
   * ES6的箭头函数会默认绑定父级作用域，因此在事件监听中，若要使用`this`的值，须使用匿名函数，以防错误