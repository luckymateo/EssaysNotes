****
#观察者模式
>简介

订阅——发布系统
****

* 定义：定义对象间一种一对多的依赖关系，使得每当一个对象改变状态，则所有依赖于它的对象都会得到通知并被更新。
* 使用场景 ->
	* 关联行为场景，需要注意的是，关联行为是可拆分的，而不是“组合”关系。
	* 时间多级触发场景。
	* 跨系统的消息交换场景，如消息队列、事件总线的处理机制。
	
* 简单实现
	
		/**
 		* 观察者
 		*/
		public class Coder implements Observer {

			public String name;

			public Coder(String name) {
				this.name = name;
			}

			@Override
			public void update(Observable o, Object arg) {
				System.out.println("Hi, " + name + ", DevTechFrontier更新啦，内容：" + arg);
			}

			@Override
			public String toString() {
				return "码农 ： " + name;
			}

		}
		
		/**
 		* DevTechFrontier 即开发技术前线，这个网站是被观察者角色，当它有更新时所有的观察者		（这里是程序员）都会接到相应的通知
 		*/
		public class DevTechFrontier extends Observable {

			public void postNewPublication(String content) {
				setChanged();

				notifyObservers(content);
			}	
		}
		
		public class Test {

			public static void main(String[] args) {
				DevTechFrontier frontier = new DevTechFrontier();// 被观察者

				Coder mrsimple = new Coder("mr.simple");// 观察者
				Coder coder1 = new Coder("coder-1");// 观察者
				Coder coder2 = new Coder("coder-2");// 观察者
				Coder coder3 = new Coder("coder-3");// 观察者

				frontier.addObserver(mrsimple);// 添加观察者
				frontier.addObserver(coder1);// 添加观察者
				frontier.addObserver(coder2);// 添加观察者
				frontier.addObserver(coder3);// 添加观察者

				frontier.postNewPublication("新的一期开发技术前线周报发布了");// 被观察者，发了一条新闻
			}
		}

* Android源码中的观察者模式实现

	* Adapter notifyDataSetChanged
	* RxJava

> 优点

* *观察者和被观察者之间是抽象耦合，应对业务变化；*
* *增强系统灵活性、可扩展性。*

> 缺点

* *在应用观察者模式时需要考虑一下开发侠侣和运行效率的问题，程序中包括一个被观察者，多个观察者、开发和调试等内容会比较复杂，而且在Java中消息的通知默认是顺序执行，一个观察者卡顿，会影响整体的执行效率，在这种情况下，一般考虑采用异步的方式。*

总结
****
观察者模式主要的作用就是对象解耦，将观察者与被观察者完全隔离，只依赖Observer 和 Obdervable抽象，例如，ListView 就是运用了 Adapter 和观察者模式使得它的可扩展性、灵活性非常强，而耦合度却很低，这是设计模式在Android源码中优秀运用的典范，那么为什么Android架构师们会这样设计ListView
,它们如何达到低耦合、高灵活性呢？在后续文章中会 分析：广播接收器和事件总线在观察者模式上有什么相似之处，又有什么不同 =——=。
****


