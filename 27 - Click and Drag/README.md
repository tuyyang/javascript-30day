# Day-27 Click And Drag #



## 实现效果 ##

鼠标点击并能进行拖曳的效果。

## 过程指南 ##

1. 监听鼠标按下、移动、离开事件，为其添加或移除`active`类名

   ```js
   slider.addEventListener('mousedown', (e) => {
       isDown = true;
       slider.classList.add('active');
       startX = e.pageX - slider.offsetLeft;
       scrollLeft = slider.scrollLeft;
   });
   
   slider.addEventListener('mouseup', () => {
       isDown = false;
       slider.classList.remove('active');
   });
   
   slider.addEventListener('mouseleave', () => {
       isDown = false;
       slider.classList.remove('active');
   });
   
   slider.addEventListener('mousemove', (e) => {
       if(!isDown) return;
       e.preventDefault(); //阻止默认事件
       const x = e.pageX - slider.offsetLeft;
       const walk = (x - startX) * 3;
       slider.scrollLeft = scrollLeft - walk;
   });
   ```

2. 使用`mousedown`和`mousemove`事件配合，实现鼠标点击拖曳效果

   * 鼠标当前点相对于容器左边的水平距离：`x = e.pageX - slider.offsetLeft`
     * `e.pageX`：当前点相对于浏览器左边框的距离
     * `slider.offsetLeft`：当前容器相对于浏览器左边框的距离
   * 鼠标点击拖曳的距离：`walk = (x - startX) * 3`
     * `startX`：鼠标滑动时的位置
   * 鼠标当前点相对于容器在水平方向上的滚动距离：`scrollLeft = slider.scrollLeft`
   * 动态更新容器的水平滚动距离：`slider.scrollLeft = scrollLeft - walk`