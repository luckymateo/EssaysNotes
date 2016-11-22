****
#责任链模式
>简介

责任链模式，是行为设计模式之一。
****

* 定义：使对个对象都有机会处理请求，从而避免了请求的发送者和接受者之间的耦合关系。将这些对象练成一条链，并沿着这条链传递该请求，直到有对象处理它为止。
* 使用场景 ->
	* 多个对象可以处理同一请求，但具体由哪个对象处理则在运行时动态决定。
	* 在请求处理者不明确的情况下向多个对象中的一个提交一个请求。
	* 需要动态指定一组对象处理请求。
	
* 责任链模式

		public abstract class Handler {
			protected Handler successor;

			/**
		 	* 请求条件
	 	 	* 
	 	 	* @param condition
	 	 	*/
			public abstract void handleRequest(String condition);
		}
    	
    	public class ConcreteHandler1 extends Handler {

			@Override
			public void handleRequest(String condition) {
				if (condition.equals("ConcreteHandler1")) {
					System.out.println("ConcreteHandler1 handled");
				} else {
					successor.handleRequest(condition);
				}
			}

		}
		
		public class ConcreteHandler2 extends Handler {

			@Override
			public void handleRequest(String condition) {
				if (condition.equals("ConcreteHandler2")) {
					System.out.println("ConcreteHandler2 handled");
				} else {
					successor.handleRequest(condition);
				}
			}

		}
		
		public class Client {

			public static void main(String[] args) {
				// 构造一个ConcreteHandler1 对象
				ConcreteHandler1 handler1 = new ConcreteHandler1();
				// 构造一个ConcreteHandler2 对象
				ConcreteHandler2 handler2 = new ConcreteHandler2();
				// 设置handler1的下一个节点
				handler1.successor = handler2;
				// 设置handler2的下一个节点
				handler2.successor = handler1;
				// 处理请求
				handler1.handleRequest("ConcreteHandler2");
			}
		}
    	
    	
    * Handler：抽象处理者角色，声明一个请求处理的方法，并在其中保持一个对下一个处理节点Handler对象的引用。
    * ConcreteHandler：具体处理者角色，对请求进行处理，如果不能处理则将该请求转发给下一个节点上的处理对象。


****
总结

责任链模式优点：对请求者和处理者关系解耦，提高代码灵活性。

缺点：对链中请求处理者的遍历，如果处理者太多那么遍历必定影响性能，特别是在一些递归调用中
****



