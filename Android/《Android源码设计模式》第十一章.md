****
#命令模式
>简介

命令模式是行为设计模式之一，命令模式会将一系列的方法调用封装，只用只需调用一个方法执行，那么所有这些被封装的方法就会被挨个执行调用。。。
****

* 定义：将一个请求封装成一个对象，从而让用户使用不用的请求把客户端参数化；对请求排队或者记录请求日志，以及支持可撤销的操作。
* 使用场景 ->
	* 命令模式是回调机制的一个面向对象的替代品。
	* 在不用的时刻指定、排列和执行请求。
	* 需要支持取消操作。
	* 支持修改日志功能，这样当系统奔溃时，这些修改可以被重做一遍。
	* 需要支持事务操作。
	
* 通用模式代码
	
		/**
 		* 接受者类
 		*/
		public class Receiver {

			public void action() {
				System.out.println("执行具体操作");
			}
		}	
		
		/**
 		* 抽象命令接口
 		*/
		public interface Command {
			/**
	 		* 执行具体操作命令
	 		*/
			void execute();
		}
		
		/**
		 * 具体命令类
 		*/
		public class ConcreteCommand implements Command {

			private Receiver receiver;

			public ConcreteCommand(Receiver receiver) {
				this.receiver = receiver;
			}

			@Override
			public void execute() {
				receiver.action();
			}

		}
		
		/**
 		* 请求者类
 		*/
		public class Invoker {

			private Command command;

			public Invoker(Command command) {
				this.command = command;
			}

			public void action() {
				// 调用具体命令对象的相关方法，执行具体命令
				command.execute();
			}
		}
		
		/**
 		* 客户类
 		*/
		public class Client {

			public static void main(String[] args) {
				// 构造一个接收者对象
				Receiver receiver = new Receiver();

				// 根据接收者对象构造一个命令对象
				Command command = new ConcreteCommand(receiver);

				// 根据具体的对象构造请求对象
				Invoker invoker = new Invoker(command);

				// 执行请求方法
				invoker.action();
			}
		}

> 优点

* *可以毫不夸张地说，可以在任何地方应用命令模式*
* *弱耦合、更灵活的扩展性、更好的扩展性*

> 缺点

* *几乎是所有设计模式的通病，就是类的膨胀，大量衍生类的创建。*


