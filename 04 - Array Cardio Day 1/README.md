# Day-04 Array Cardio 💪 指南一



## 实现效果

这一部分主要是熟悉 Array 的几个基本方法，其中有两个（filter、map）是 ES5 定义的迭代方法，这些迭代方法都有一个特点，就是对数组的每一项都运行给定函数，根据使用的迭代方法的不同，有不同的返回结果。

文档给出了一个初始操作的 inventor 数组，基于这个数组可以练习一下 Array 的各个方法，请打开 HTML 后在 Console 面板中查看输出结果。

## 炫酷的调试技巧

在 Console 中我们常用到的可能是 `console.log()` ，但它还有一个很炫的输出，按照表格来输出，效果如下：

```js
console.table(类名)
```

![](D:\#CODE\javascript-30day\04 - Array Cardio Day 1\console.table01.png)

## 过程指南

1. 筛选 16 世纪出生的发明家  

   ```js
   const _fifteen = inventors.filter(inventor => (inventor.year >= 1500 && inventor.year < 1600));
       console.table(_fifteen);
   ```

   [filter](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)

   ```Array.prototype.filter()``` 筛选操作：筛选出运行结果是true的元素，组成数组返回。

   

2. 展示他们的姓和名  

   ```js
   //法一
   const fullNames = inventors.map(inventor => inventor.first + ' ' + inventor.last);
   //法二
   const fullNames = inventors.map(inventor >= `${inventor.first} ${inventor.last}`);
   ```

   [map](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/map)

   ```Array.prototype.map()``` 映射操作：将数组中的每一个元素都经过callback函数处理后，返回新的元素组成的数组。

   **适用于创建包含的项与另一个数组一一对应的数组。** 

   

3. 把他们按照出生日期从大到小进行排序

   ```js
   const __ordered = inventors.sort((a, b) => (a > b) ? 1 : -1);
   console.table(__ordered);
   ```

   [sort](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)

   ```Array.prototype.sort()``` 比较操作：

   

4. 计算所有的发明家加起来一共活了多少岁

   ```js
   //法一：for 循环
       var total = 0;
       for(var i = 0; i < inventors.length; i++){
           total += inventors[i].passed - inventors[i].year;
       }
       console.log(total);
   
       //法二:
       var totalYear = inventors.reduce(function(total, inventor){
           return total + inventor.passed - inventor.year;
       }, 0);
       console.log(totalYear);
   
       //法三：
       const totalAge = inventors.reduce((total, inventor) => {   
           return  total + inventor.passed - inventor.year;
       }, 0);
       console.log(totalAge);
   ```

   [reduce](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)

   ```Array.prototype.reduce()``` 归并方法：这是一个归并数组的方法，它接受一个函数作为参数（这个函数可以理解成累加器），它会遍历数组的所有项，然后构建一个最终的返回值，这个值就是这个累加器的第一个参数。

   

5. 按照他们活了多久来进行排序

   ```js
   const oldest = inventors.sort((a, b) => {
           const last = a.passed - a.year;
           const next = b.passed - b.year;
           return (next < last) ? -1 : 1;
       });
       console.table(oldest);
   ```

   自定义排序函数，分别算出每一个发明家的年龄，按照其大小排序

   

6. 筛选出一个网页里含有某个词语的标题

   ```js
   var total = Array.from(document.querySelectorAll('.mw-category .mw-category-group ul li a'));
   var allStreet = [];  //存放所有的街道名称
   total.forEach(item => allStreet.push(item.innerText));
   allStreet.filter(item => item.includes('de'));
   //console.log(allStreet);
   //法二
   const category = document.querySelector('.mw-category');
   const links = Array.from(category.querySelectorAll('a'));
   const de = links
                   .map(link => link.textContent)
                   .filter(streetName => streetName.includes('de'));
   ```

   ```.forEach()``` & ```.filter()``` 

   

7. 按照姓氏来对发明家进行排序

   ```js
   const sortName = people.sort((a,b) => {
   	return (a.last > b.last) ? 1 : -1;
   })
   console.table(sortName);
   ```

   

8. 统计给出数组中各个物品的数量

   ```js
   const data = ['car', 'car', 'truck', 'truck', 'bike', 'walk', 'car', 'van', 'bike', 'walk', 'car', 'van', 'car', 'truck'];
   const reduce = data.reduce((obj, item) => {
   	if(!obj[item]){
   		obj[item] = 0;
   	}
   	obj[item]++;
   	return obj;
       }, {});
       console.log(reduce);
   
   ```

   ```.reduce()``` 回调函数的第一个参数用来分别存储每一类的数量，第二个参数为当前的元素，如果`obj[item]`不存在，就将其值初始化为0，否则就将改值加1，最后返回该对象，即分别存储了各个类别的数量。

   
