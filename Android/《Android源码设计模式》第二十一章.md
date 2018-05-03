****
#装饰模式
>简介

装饰着模式也称为包装模式，结构性设计模式之一，其使用一种对客户端透明的方式来动态地扩展对象的功能，同时它也是继承关系的一种替代方案之一。。。
****

* 定义：动态地给一个对象添加一些额外的职责。就增加功能来说，装饰模式相比生成子类更为灵活。
* 使用场景 ->
	* 需要透明且动态地扩展类的功能时。
	
* 简单实现
	
		public abstract class Component {
			public abstract void operate();
		}

		
		public class ConcreteComponent extends Component {

			@Override
			public void operate() {
				// 具体逻辑随意写
				System.out.println("111111111111");
			}		

		}
		
		public class ConcreteDecoratorA extends Decorator {

			public ConcreteDecoratorA(Component component) {
				super(component);
			}

			@Override
			public void operate() {
				super.operate();
				operateA();
				operateB();
			}

			public void operateA() {
				// 装饰方法逻辑
				System.out.println("ConcreteDecoratorA.operateA()");
			}

			public void operateB() {
				// 装饰方法逻辑
				System.out.println("ConcreteDecoratorA.operateB()");
			}

		}
		
		public class ConcreteDecoratorB extends Decorator {

			public ConcreteDecoratorB(Component component) {
				super(component);
			}

			@Override
			public void operate() {
				super.operate();
				operateA();
				operateB();
			}

			public void operateA() {
				// 装饰方法逻辑
				System.out.println("ConcreteDecoratorB.operateA()");
			}

			public void operateB() {
				// 装饰方法逻辑
				System.out.println("ConcreteDecoratorB.operateB()");
			}

		}
		
		public abstract class Decorator extends Component {

			private Component component;

			public Decorator(Component component) {
				super();
				this.component = component;
			}
	
			@Override
			public void operate() {
				component.operate();
			}

		}
		
		public class Client {
			public static void main(String[] args) {
				Component component = new ConcreteComponent();
				Decorator decoratorA = new ConcreteDecoratorA(component);
				decoratorA.operate();
				Decorator decoratorB = new ConcreteDecoratorB(component);
				decoratorB.operate();
			}
		}


* Android源码中的装饰者模式实现

	* Context ContextImpl COntextThemeWrapper ContextWrapper


总结
****
装饰模式和代理模式有点类似，有时甚至容易混淆，倒不是说会把代理当成装饰，而常常回事将装饰看做代理，装饰模式应该为所装饰的对象增强功能；代理模式对代理的对象施加控制，但不对对象本身的功能进行增强。
****


