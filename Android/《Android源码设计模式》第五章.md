****
#工厂方法模式
>简介

定义一个用于创建对象的接口，让子类决定实例化哪个类。
****

* 工厂实践

		public abstract class IOHandler{
			
			public abstract void add(String id, String name);
			
			public abstract void remove(String id);
		
			public abstract void update(String is, String name);
			
			public abstract String query(String id);
		
		}
		
		public FileHandler extends IOHandler{
			
			@Override
			public void add(String id, String name){
				//业务逻辑
			}
			
			@Override
			public abstract void remove(String id){
				//业务逻辑
			}
			
			@Override
			publi void update(String is, String name){
				//业务逻辑
			}
			
			@Override
			publi String query(String id){
				//业务逻辑
			}
		}
		
		public void IOFactory{
		
			public static <T extends IOHandler> T getIOHandler(Class<T> clz){
			
				IOHandler handler = null;
				try{
					handler =  (IOHandler)Class.forName(clz.getName()).newInstance();
				}catch(Exception e){
					e.printStackTrace();
				}
				return (T) handler;
			}
		
		}
		
* 总结
	
	每次为工厂添加新的产品时就要编写一个新的产品类，同时还要引入抽象层，必然导致类结构复杂化，所以在使用时需权衡利弊。

