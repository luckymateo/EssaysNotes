****
#策略模式
>简介

在软件开发中常常遇到这样的情况：实现某一个功能可以有多种算法或者策略，我们根据实际情况选择不同的算法或者策略来完成该功能。。。
****

* 定义：策略模式定义了一系列的算法，并将每一个算法封装起来，而且使他们还可以相互替换。策略模式让算法独立于使用它的客户而独立变化。
* 使用场景 ->
	* 针对同一类型问题的多种处理方式，仅仅是具体行为有差别时。
	* 需要安全地封装多种同一类型的操作时。
	* 出现同一抽象类有多个子类，而又需要使用if-else 或者 switch-case 来选择具体子类时。
	
* 简单实现
	
		public interface CalculateStrategy{
			int calculatePrice(int km);//按距离算价格
		}	
		
		//公交车价格计算策略
		public class BusStrategy implements CalculateStrategy{
		
			@Override
			public int calculatePrice(int km){
				。。。
				retrun price;
			}
		}
		
		···
		
		main(){
			private statis final int BUS = 1;
			private statis final int SUBWAY = 2;
			private statis final int TAXI = 3;
			
			int calulatePrice(int km, int type){
				if(type == BUS){
					return busPrice(km);
				} else if(type == SUBWAY){
					return subwayPrice(km);
				}else if(type == TAXI){
					return taxiPrice(km);
				}
				return 0;
			}
		}

* Android源码中的策略模式实现

	* 时间插值器
	* 属性动画

> 优点

* *结构清晰明了、使用简单直观；*
* *耦合度相对而言较低，扩展方便；*
* *操作封装也更为彻底，数据更为安全。*

> 缺点

* *随着策略的增加，子类也会变得繁多。*

总结
****
策略模式主要用来分离算法，在相同的行为抽象下有不同的具体实现策略。这个模式很好地演示了开闭原则，也就是定义抽象，注入不同的实现，从而达到很好的可扩展性。
****


