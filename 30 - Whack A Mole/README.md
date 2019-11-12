# Day-30 Whack A Mole



## 实现效果

打地鼠

## 过程指南

1. 随机的一只鼹鼠从随机的洞里冒出来

   ```js
   const holes = document.querySelectorAll('.hole');
   const scoreBoard = document.querySelector('.score');
   const moles = document.querySelectorAll('.mole');
   let lastHole;
   let timeUp = false;
   let score = 0;
   
   function randomTime(min, max) {
   	// return Math.round(Math.random() * (max - min) + min);
   	return Math.floor(Math.random() * (max - min + 1) + min);
   }
   
   function randomHole(holes) {
   	const index = Math.floor(Math.random() * holes.length);
       const hole = holes[index];
       if(lastHole === hole) {
   		return randomHole(holes);
       } //防止连续两次生成相同的洞
       lastHole = hole;
       return hole;
   }
   
   function peep() {
   	const hole = randomHole(holes);
       const time = randomTime(200,2000);
       hole.classList.add('up');
       setTimeout(() => {
   		hole.classList.remove('up');
           if(!timeUp) {
   			peep();
           }
        },time)
   }
   ```

   * `return Math.floor(Math.random() * (max - min + 1) + min)`：使用`Math.round()`会导致随机整数处于一个分布不均匀的分布，可根据喜好选择不同的方法
   * `lastHole === hole` 防止两次随机生成同一个洞

   

2. `startGame`函数

   ```js
   function startGame() {
   	timeUp = false;
       scoreBoard.textContent = 0;
       score = 0;
       peep();
       setTimeout(() => {
       timeUp = true;
       },10000)
   }
   
   function bonk(e) {
   	if(!e.isTrusted) {
   		return;
        }
        score ++;
        this.parentNode.classList.remove('up');
        scoreBoard.textContent = score;
   }
   
   moles.forEach(mole => {
   	mole.addEventListener('click', bonk, false);
   });
   ```

   * `e.isTrusted`：返回一个布尔值，为`true`表明当前事件是由用户行为触发，如鼠标点击；为`false`表明事件由一个脚本生成，如`event.initEvent`

