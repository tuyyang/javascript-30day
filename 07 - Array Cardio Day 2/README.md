# Day-07 Array Cardio 💪 指南二



## 实现效果

继续熟悉 Array 的一些基本方法，包括 `some()`、`every()`、`find()`、`splice()`、`slice()`。这篇比较简单。

文档提供了用于操作的 people 和 comments 数组，模拟的是人员信息及评论数据，基于这两个数组可以练习一下上面提及的各个方法，在 Console 面板中查看输出结果。

## 过程指南

### 一、针对 people 数组：

1. 是否有人超过 19 岁？

   ```js
   const isAdult = people.some(person => {
   	const curentYear = (new Date()).getFullYear();
   	return curentYear - person.year >= 19;
   });
   console.log({isAdult});
   ```

   

2. 是否所有人都是成年人？

   ```js
   const allAdult = people.every( person => new Date().getFullYear() - person.year >= 19);
   console.log(allAdult);
   ```

   

   ### 相关知识

   ### [some](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/some) 和  [every](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/every)

   两者的相同之处是，都接受一个函数作为参数，对数组元素都执行一次此函数，都不会改变原数组的值。不同之处在于返回条件不同：

   * `some()` 中直到某个数组元素使此函数为 `true`，就立即返回 `true`。所以可以用来判断一个数组中，是否存在某个符合条件的值。

   * `every()` 中除非所有值都使此函数为 `true`，才会返回 `true` 值，否则为 `false`。主要用处，即判断是否所有元素都符合条件。



### 二、针对 comments 数组：

1. 找到 ID 号为 823423 的评论

   ```js
   const comment = comments.find(comment => comment.id == 823423);
   console.log(comment);
   ```

   

2. 删除 ID 号为 823423 的评论
  1. 获取此 ID 对应元素在数组中所处的位置
  2. 利用位置，删除该子元素
  2. 或者拼接新的数组

  ```js
  //方法一 splice
  comments.splice(index,1);
  console.table(comments);
  //方法二   
  const newComment = [
  	...comments.slice(0,index),
  	...comments.slice(index + 1)
  ];
  console.table(newComment);
  ```

  

  ### 相关知识

  [find](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/find) 和 [fineIndex](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/findIndex)

  ```find()```  返回要找的值，若找不到返回undefined

  ```findIndex()``` 放回目标值的索引下标，若找不到返回  -1

  

  [slice](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/slice) 和 [splice](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/splice)

  相同点：参数的第一个都是指的起始位置，且都接受负数，若是负数，代表倒数第几位。

  * `slice()`：不修改原数组，按照参数复制一个新数组。

    ​				参数：复制的起点和终点索引（省略则代表到末尾），但终点索引位置的元素不包含在内。

  * `splice()`：原数组会被修改。第二个参数代表要删掉的元素个数，之后可选的参数，表示要替补被删除位置的元素。


