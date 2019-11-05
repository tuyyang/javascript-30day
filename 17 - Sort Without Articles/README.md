# Day-17 数组的去前缀排序



## 实现效果
初始文件中提供了一个无序列表元素，去除元素前面的 a / an / the 后进行排序。

## 基本思路
1.基本的编程任务有两个要点，即**排序**和**展示**;<br>
2.数组排序部分最外层即为`Array.sort(arr)`函数，内层实现具体排序规则;<br>
3.展示部分即将排列好的新数组拼接成带有标签的HTML元素，然后一次性插入到列表中。

## 过程指南

```js
//去除前缀
const delPreFix = item => item.replace(/^(The|A|An)\s{1}/,'');

//数组排序
const sortedBands = bands.sort((a,b) => delPreFix(a) > delPreFix(b) ? 1 : -1);

//展示至HTML页面
document.querySelector('#bands').innerHTML = `<li>` + sortedBands.join('</li><li>') + `</li>`;
```

