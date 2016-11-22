****
#状态模式
>简介

状态模式的行为是由状态决定的，不同的状态下有不同的行为。
****

* 定义：当一个对象的内在状态改变时允许改变其行为，这个对象看起来像是改变了其类
* 使用场景 ->
	* 一个对象的行为取决于它的状态，并且它必须在运行时根据状态改变它的行为。
	* 代码中包含大量与对象状态有关的条件语句。
	
* 状态模式的简单实例

		public interface TState{
			public void a();
			public void b();
			public void c();
			public void d();
		}    	
    	
    	public A implements TState{
    		
    		@Override
    		public void a(){
    		}
    		...
    	}
    	
    	public B implements TState{
    		
    		@Override
    		public void a(){
    		}
    		...
    	}
    	
    	public C implements TState{
    		
    		@Override
    		public void a(){
    		}
    		...
    	}
    	
    	public interface Controller{
    		public void A();
    		public void B();
			public void C();
    	}
    	
    	public StatusClass implements Controller{
    		
    		TState mTState;
    		
    		public setTState(TState state){
    			mTState = state;
    		}
    		
    		@Override
    		public void A(){
    			setTState(new A());
    		}
    		
    		@Override
    		public void B(){
    			setTState(new B());
    		}
    		
    		@Override
    		public void C(){
    			setTState(new C());
    		}
    		
    		public void a(){
    			mTState.a();
    		}
    		
    		public void b(){
    			mTState.b();
    		}
    		
    		public void c(){
    			mTState.c();
    		}
    		
    		public void d(){
    			mTState.d();
    		}
    	
    	}
    	
    	public class Client {
    	
    		public static void main(String[] args){
    			StatusClass status = new StatusClass();
    			
    			status.A(); //A状态
    			//status.B(); //B状态
    			//status.C(); //C状态
    			
    			//切换状态后执行不一样的功能
    			status.a();
    			status.b();
    			status.c();
    			status.d();
    		}
    	
    	}
    	
 

总结
****
状态模式的关键点在于不同的状态下对于同一行为有不同的响应，这其实就是一个将if-else用 [多态]()来实现的一个具体示例。

在if-else 或者 switch-case 形式下根据不同的状态进行判断，这种实现使得逻辑耦合在一起，易于出错，通过状态模式能够很好的消除这类“丑陋”的逻辑处理。
****

> 优点

*State 模式将所有与一个特定的状态相关的行为都放入一个状态对象中，它提供了一个更好的方法来组织与特定状态相关的代码，将烦琐的状态转换成结构清晰的状态类族，在避免代码膨胀的同时也保证了可扩展性与可维护性。*

> 缺点

*状态模式的使用必然会增加系统类和对象的个数。*

