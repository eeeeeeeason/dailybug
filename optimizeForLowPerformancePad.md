### 在一个1.1GHZ,6G 1333 ddr3内存中的windows平板开发所遇到问题
- QT中性能与同设备edge性能差距极大，在多帧动画，甚至表单的滚动时都有不同程度的花屏
  -  APNG,将多帧图片组合，不太方便的是18年之前的浏览器版本不兼容，资料显示webp也可以但没有尝试
- 多张全屏幕背景覆盖导致render过程缓慢
- 滚动时花屏qt中的webengine十分卡顿，当前认为是内核的优化问题，还没找到办法，
  - https://segmentfault.com/a/1190000040853792
  - https://github.com/escawn/blog/issues/5
  - https://blog.csdn.net/A3872215/article/details/98853306    qt远程连接
