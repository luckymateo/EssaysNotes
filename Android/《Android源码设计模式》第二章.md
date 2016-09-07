##单例模式

####确保某一个类只有一个实例，而且自行实例化并向整个系统提供这个系统。

* 构造函数不对外公开，一般为private；
* 通过一个静态方法或者枚举返回单例类对象；
* 确保单例类的对象有且只有一个，尤其是在多线程环境下；
* 确保单例类对象在反序列化时不会重新构建对象。

> 饿汉式单例
	
	public class XXX{
		private static final XXX mX = new XXX();
		
		private XXX(){
		}
		
		public static XXX getXXX(){
			return mX;
		}
	}
	
> 懒汉模式

	public class XXX{
		private stati XXX mX;
		
		private XXX(){
		}
		
		public static synchronized XXX getXXX(){
			if(mX == null){
				mX = new XXX();
			}
			return mX;
		}
	}
	
	缺点：第一次加载时需要及时进行实例化，反应稍慢，最大问题是每次调用getXXX()都进行同步，造成不必要的同步开销

> Double Check Lock （DCL）实现单例

	public class XXX{
		private static XXX mX = null;
		
		private XXX(){
		}
		
		public static XXX getXXX(){
			if(mX == null){
				synchronized(XXX.class){
					if(mX == null){
						mX = new XXX();
					}
				}
			}
			return mX;
		}
	}
	
* 1、给XXX的实例分配内存；
* 2、调用XXX（）的构造函数，初始化成员字段；（此时mX还是空）
* 3、将mX对象指向分配的内存空间（此时mX 就不是null了）

****
由于Java编译器允许处理器乱序执行。。Java1.5之前的JMM（Java Memory Model，Java内存模型）中Cache、寄存器 到 主存储回写顺序的规定，上面的2、3是无法保证顺序的。。

JDK1.5后 官方调整了JVM，具体化了 volatile 关键字，只需要定义为：
	
	private volatile static XXX mX = null;
就可保证mX对象每次都是从主内存中读取，来完成DCL单例模式，but volatile 或多或少影响到性能

DCL优点：资源利用率高，第一次执行getInstance时单例对象才会被实例化，效率高。

DCL缺点：第一次加载时反应稍慢，也由于Java内存模型的原因偶尔会失败。

> 静态内部类单例模式

	public class Singleton{
		
		private Singleton(){
		}
		
		public static Singleton get Singleton(){
			return Singleton Holder.sInstance;
		}
		
		private static class Singleton Holder{
			private static final Singleton sInstance = new Singleton();
		}
	}
	
> 枚举单例

	public enum SingletonEnum{
		INSTANCE;
		
		public void doSomething(){
			System.out.printnln("do sth");
		}
	}
	
> 使用容器实现单例模式

	public class SingletonManager{
		
		private static Map<String,Object> objMap = new HashMap<>();
		
		private SingletonManager(){}
		
		public static void registerService(){
			if(!objMap.containKey(key)){
				objMap.put(key ,instance);
			}
		}
		
		public static Object getService(String key){
			return objMap.get(Key);
		}
	
	}
	
	在程序开始时，将多种单例类注入到一个统一的管理类中，在使用时根据key获取对象对应类型的对象。
	这种方式使得我们可以管理多种类型的单例，并且在使用时可以通过统一的接口进行获取操作，降低了用
	户的使用成本，也隐藏了具体实现，降低了耦合度。