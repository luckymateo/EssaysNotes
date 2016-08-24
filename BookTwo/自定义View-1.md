##自定义View基础-坐标系

> 一、坐标系

`>` 屏幕坐标系和数学坐标系的区别

![](http://ww2.sinaimg.cn/large/005Xtdi2jw1f1qygzfvhoj308c0dwglr.jpg)

`>` 手机屏幕的坐标系

![](http://ww1.sinaimg.cn/large/005Xtdi2jw1f1qyhbqvihj308c0dwjrh.jpg)
![](http://ww3.sinaimg.cn/large/005Xtdi2jw1f1qyhjy7h8j308c0dwq32.jpg)

> 二、View的坐标系

*注意：View的坐标系统是相对于父控件而言的.*

	getTop();       //获取子View左上角距父View顶部的距离
	getLeft();      //获取子View左上角距父View左侧的距离
	getBottom();    //获取子View右下角距父View顶部的距离
	getRight();     //获取子View右下角距父View左侧的距离
如下图所示：

![](http://ww2.sinaimg.cn/large/005Xtdi2gw1f1qzqwvkkbj308c0dwgm9.jpg)

> 三、MotionEvent中 get 和 getRaw 的区别

	event.getX();       //触摸点相对于其所在组件坐标系的坐标
	event.getY();

	event.getRawX();    //触摸点相对于屏幕默认坐标系的坐标
	event.getRawY();
如下图所示：

![](http://ww1.sinaimg.cn/large/005Xtdi2jw1f1r2bdlqhbj308c0dwwew.jpg)

> 四、核心要点

* 1	**在数学中常见的坐标系与屏幕默认坐标系的差别**
* 2	**View的坐标系是相对于父控件而言的**
* 3	**MotionEvent中get和getRaw的区别**