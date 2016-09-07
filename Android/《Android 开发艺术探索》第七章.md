#Android动画深入分析
****

* View动画
* 帧动画
* 属性动画

****

##View动画,一般放到/anim,目录
* **View的四种变换对应着Animation的四个子类：**
> TranslateAnimation
> 
> ScaleAnimation
> 
> RotateAnimation
> 
> AlphaAnimation

		<?xml version="1.0" encoding="utf-8"?>
		<set xmlns:android="http://schemas.android.com/apk/res/android"
     		android:Interpolator="@anim/scaleanim" ❶插值器
     		android:shareInterpolator="true"> ❷表示集合中的动画是否和集合共享同一个插值器
    		<alpha/>
    		<scale/>
    		<rotate/>
    		<translate/>
		</set>

	*❶：表示动画集合所采用的插值器，插值器影响动画的速度，比如非匀速动画就需要通过插值器来控制动画的播放过程*

	*❷：表示集合中的动画是否和集合共享同一个插值器，如果集合不指定插值器，那么子动画就需要单独指定所需的插值器或者使用默认值*

	代码中的使用

	`Button mButton = (Button)findViewById(R.id.button);`
	`Animation animation = AnimationUtils.loadAnimation(this,R.anim.animation_test);`
	`mButton.startAnimation(animation);`

	自定义View动画

	`主要是矩阵变换的过程，数学上的概念，不再详述`，很多时候采用Camera来简化矩阵变化的过程


* **View动画的特殊使用场景**

	* LayoutAnimation
	
		作用于ViewGroup,为ViewGroup指定一个动画，这样当它的子元素出厂时都会具有这种动画效果。这种效果常常被用在ListView，它每个item都以一定的动画形式出现。
	
			<?xml version="1.0" encoding="utf-8"?>
			<layoutAnimation xmlns:android="http://schemas.android.com/apk/res/android"
                 android:animation="@anim/alphaanim"  为子元素指定具体的入场动画
                 android:animationOrder="random" ❶子元素动画的顺序（normal、reverse和random）
                 android:delay="0.5" 开始动画的时间延迟
                 android:interpolator="@anim/scaleanim">
			</layoutAnimation>

		*❶：normal：表示顺序显示，排在前面的子元素先开始播放入场动画； reverse：表示逆向显示，排后面的先显示；random：随机入场*

	* 使用方法
		
			通过xml
		
			<xxxViewGroup
				android:layoutAnimation="@anim/anim_layout"
			/>
			
			通过代码
			
			Animation animation = AnimationUtils.loadAnimation(this,R.anim.anim_litem);
			LayoutAnimationController controller = new LayoutAnimationController(animation);
			controller.setDelay(0.5f);
			controller.setOrder(LayoutAnimationController.ORDER_NORMAL);
			listView.setLayoutAnimation(controller);
			

* **Activity的切换效果**

	overridePendingTransition(R.anim.enter_anim ,R.anim.exit_anim);
	overridePendingTransition这个方法必须位于startActivity 或者finish的后面，否则动画效果不起作用
	
##帧动画
顺序播放一组预先定义好的图片，类似于播放电影。注意小心OOM。。

##属性动画 --本小节很重要

身体不适...  额/(ㄒoㄒ)/~~ 