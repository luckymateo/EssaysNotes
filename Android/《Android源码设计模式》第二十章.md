****
#适配器模式（推荐认真读书上原文，收获会很大）
>简介

在ListView GridView RecyclerView 使用的Adapter。。。
****

* 定义：适配器模式把一个类的接口变换成客户端所期待的另一种接口，从而使原本因接口不匹配无法连接在一起工作的两个类能够在一起工作。
* 使用场景 ->
	* 系统需要使用的现有的类，而此类的接口不符合系统的需要，即接口不兼容。
	* 想要建立一个可以重复使用的类，用于与一些彼此之间没有太大关联的一些类，包括一些可能在将来引进的类一起工作。
	* 需要一个统一的输出接口，二输入端的类型不可预知。
	
* 简单实现
	
		public interface FiveVolt {
			public int getVoly5();
		}	
		
		public class Volt220 {
			public int getVolt220() {
				return 220;
			}
		}
		
		public class VoltAdapter extends Volt220 implements FiveVolt {

			@Override
			public int getVoly5() {
				return 5;
			}

		}
		
		public class VoltAdapter2 implements FiveVolt {

			Volt220 mVolt220;

			public VoltAdapter2(Volt220 mVolt220) {
				this.mVolt220 = mVolt220;
			}

			public int getVoly200() {
				return mVolt220.getVolt220();
			}

			@Override
			public int getVoly5() {
				return 5;
			}

		}
		
		public class Test {
			public static void main(String[] args) {
				VoltAdapter adapter = new VoltAdapter();// 类适配器模式
				VoltAdapter2 adapter2 = new VoltAdapter2(new Volt220());// 对象适配器模式
				System.out.println("输出电压 ：" + adapter.getVoly5());
				System.out.println("输出电压 ：" + adapter2.getVoly5());
			}
		}

* Android源码中的适配器模式实现

	* RecyclerView
	* 适配器模式很重要

> 优点

* *更好的复用性；*
* *更好的扩展性；*

> 缺点

* *过多的使用适配器，会让西永非常凌乱，不易整体把握，例如，明明看到调用的是A接口，其实内部被适配为B接口的实现。*

