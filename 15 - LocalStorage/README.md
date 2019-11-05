# Day-15 LocalStorage #



## 实现效果 ##

​	练习本地存储以及时间委托的使用。模拟菜单效果，在页面中添加新的菜品，且在页面上刷新后也不会清空。

## 过程指南 ##

1. 为 `addItems`按钮添加事件函数，新增`item`并存储到本地缓存。

   ```js
   function addItem(e){
         e.preventDefault(); //阻止默认事件的触发，及点击提交按钮页面不会自动刷新
         const text = this.querySelector('[name=item]').value;
         const item = {
           text: text,
           done: false
         }
         items.push(item);
         this.reset(); //添加完数据后，重置输入框
         populateList(items, itemsList);
         localStorage.setItem('items', JSON.stringify(items));
         console.log(text);
   	}
   addItems.addEventListener('submit', addItem);
   ```

   * `localStorage`中只能存储字符串。可以用`JSON.stringify(object)`将一个对象转换为字符串，使用`JSON.parse(objecting)`将一个对象字符串转换为对象。
   * `localStorage.setItem('key', value)`：设置本地缓存
   * `localStorage.getItem('key')`：根据参数key取得本地缓存中对应的值

2. HTML内容更新

   ```js
   function populateList(plates = [], platesList) {
         platesList.innerHTML = plates.map((plate, i) => {
           return `
             <li>
               <input type="checkbox" data-index=${i} id="item${i}" ${plate.done ? 'checked' : ''} >
               <label for="item${i}"> ${plate.text} </label>
             </li>
           `;
         }).join('');
       }
   ```

   * 声明一个`populateList`方法来更新页面的内容。接受需要更新的数组作为参数，根据数组里的内容构造一组`<li>`组成的列表。

3. 切换状态事件

   ```js
   function toggleDone(e) {
         if(!e.target.matches('input')) return;
         const el = e.target;
         const index = el.dataset.index;
         items[index].done = !items[index].done;
         populateList(items, itemsList);
         localStorage.setItem('items', JSON.stringify(items));
         console.log(el.dataset.index);
       }
   ```

   * 通过`e.target.matches('input')`判断所点击的元素是否为`input`，根据所获取的点击元素列表序号，更爱其`done`属性，更新后完成存储。

4. 清除缓存

   ```js
   // 在关闭浏览器之后清除缓存
       window.onbeforeunload = function (e) {
         localStorage.removeItem('items');
         // let confirmationMessage = "\o/";
         e.returnValue = confirmationMessage; // Gecko, Trident, Chrome 34+
         // return confirmationMessage; // 如果有返回值的话，就会弹出确认框。
       };
   ```

   * 慎用，尤其在生产环境中


## 知识点 ##

* [event.preventDefault](https://developer.mozilla.org/zh-CN/docs/Web/API/Event/preventDefault)
* [eventTarget.addEventListener](https://developer.mozilla.org/zh-CN/docs/Web/API/EventTarget/addEventListener)
* [localStorage](https://developer.mozilla.org/zh-CN/docs/Web/API/Storage/LocalStorage)
* [JSON](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/JSON)

