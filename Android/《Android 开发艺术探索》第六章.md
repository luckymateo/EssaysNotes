#Android的Drawable
****

* **drawable是一种图像的概念，图像或图片**
* **drawable一般通过XML来定义**
* **drawable通常被用来做View的背景**
* **Drawable是一个抽象类，它是所有Drawable对象的基类，每个Drawable对象都是它的子类，比如ShapeDrawable、BitmapDrawable ...**
* **一张图片形成的Drawable有内部宽高（getIntrinsicWidth 和 getIntrinsicHeight 去获取），但是一个颜色形成的Drawable，没有宽高的概念**

****


##Drawable的分类(drawable定义到/drawable目录下)
* BitmapDrawable

		<?xml version="1.0" encoding="utf-8"? >
 		<bitmap xmlns:android="http://schemas.android.com/apk/res/android"
    	android:src="@drawable/resource"  资源
    	android:antialias="true" 是否开启图片抗锯齿功能
    	android:dither="true" 是否开启抖动效果
    	android:filter="true" 是否开启滤镜效果
    	android:gravity="bottom"
    	android:mipMap="false" 纹理映射 一般为false，日常开发不常用
    	android:tileMode="clamp"> 平铺模式
 		</bitmap>

* ShapeDrawable

	
		<?xml version="1.0" encoding="utf-8"?>
		<shape xmlns:android="http://schemas.android.com/apk/res/android"
       		android:dither="false"
       		android:innerRadius="@dimen/activity_horizontal_margin"
       		android:innerRadiusRatio="@android:integer/status_bar_notification_info_maxnum"
       		android:shape="rectangle"
       		android:thickness="@dimen/activity_horizontal_margin"
       		android:thicknessRatio="@android:integer/status_bar_notification_info_maxnum"
       		android:tint="@color/colorAccent"
       		android:tintMode="add"
       		android:useLevel="false">
       		
       
    	<corners
        	android:bottomLeftRadius="@dimen/activity_horizontal_margin"
        	android:bottomRightRadius="@dimen/activity_horizontal_margin"
        	android:radius="@dimen/activity_horizontal_margin"
        	android:topLeftRadius="@dimen/activity_horizontal_margin"
        	android:topRightRadius="@dimen/activity_horizontal_margin"/>

    	<gradient
        	android:angle="@android:integer/status_bar_notification_info_maxnum"
        	android:centerColor="@color/colorAccent"
        	android:centerX="0"
        	android:centerY="0"
        	android:endColor="@color/colorAccent"
        	android:gradientRadius="@dimen/activity_horizontal_margin"
        	android:startColor="@color/colorAccent"
        	android:type="radial"
        	android:useLevel="false"/>


    	<padding
        	android:bottom="@dimen/activity_horizontal_margin"
        	android:left="@dimen/activity_horizontal_margin"
        	android:right="@dimen/activity_horizontal_margin"
        	android:top="@dimen/activity_horizontal_margin"/>


    	<size
        	android:width="@dimen/activity_horizontal_margin"
        	android:height="@dimen/activity_horizontal_margin"/>


    	<solid
        	android:color="@color/colorAccent"/>


    	<stroke
        	android:color="@color/colorAccent"/>

		</shape>

* LayerDrawable

		<?xml version="1.0" encoding="utf-8"?>
		<layer-list xmlns:android="http://schemas.android.com/apk/res/android"
            android:autoMirrored="true"
            android:opacity="opaque"
            android:paddingBottom="@dimen/activity_horizontal_margin"
            android:paddingEnd="@dimen/activity_horizontal_margin"
            android:paddingLeft="@dimen/activity_horizontal_margin"
            android:paddingMode="nest"
            android:paddingRight="@dimen/activity_horizontal_margin"
            android:paddingStart="@dimen/activity_horizontal_margin"
            android:paddingTop="@dimen/activity_horizontal_margin">
    	<item
        	android:id="@android:id/secondaryProgress"
        	android:width="@dimen/activity_horizontal_margin"
        	android:height="@dimen/activity_horizontal_margin"
        	android:bottom="@dimen/activity_horizontal_margin"
        	android:drawable="@drawable/checkres"
        	android:end="@dimen/activity_horizontal_margin"
        	android:gravity="bottom"
        	android:left="@dimen/activity_horizontal_margin"
        	android:right="@dimen/activity_horizontal_margin"
        	android:start="@dimen/activity_horizontal_margin"
        	android:top="@dimen/activity_horizontal_margin">
        	<shape
            	android:shape="rectangle">
            	<solid android:color="@color/colorAccent"/>
        	</shape>
    	</item>

    	.
    	.
    	.
		</layer-list>
		
* StateListDrawable
* LevelListDrawable
* TransitionDrawable
* InsetDrawable
* ScaleDrawable
* ClipDrawable

#...
不想一一列举了，在写就吐了，这种字典类型的功能，个人觉得还是随用随看比较好，不需操之过急。

