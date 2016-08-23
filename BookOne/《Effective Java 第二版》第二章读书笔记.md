## 创建和销毁对象
####*❶ 静态工厂代替[构造器]*
	public static Boolean valueOf(boolean b){
		retrun b ? Boolean.True : Boolean.Flase
	}
	
> ***植入话题，说说为什么要这样做***

> * *使用起来清楚方便，方法名就代表用途*
> * *不必再每次调用的时候创建一个对象*
> 
>  ***<mark>使用预先构建好的实例缓存起来，进行重复利用，避免创建不必要的重复对象，类似于Flyweight模式</mark>***
> 
> * 可以返回原返回类型的任何子类型的对象
> * 创建参数化类型实例的时候，使用代码更加简洁
> 
> 类型堆导
  	
> 		public static <K,V> HashMap<K,V> newInstance(){
> 			new HashMap<K,V>();
> 		}
> 
> 		Map<String ,List<Boolean>> mMap = HashMap.newInstance();
> 
> 
> 静态工厂的一些弊端
> 
> * 类如果不包含公有的或者受保护的构造器，就不能被子类化
> * 他们与其他的方法实际上没有任何区别


####*❷ 遇到多个构造器参数时要考虑用[构建器]*
	重叠构造器模式：当有许多参数的时候，难以进行阅读，客户端可能会颠倒两个参数的顺序
	public class NutritionFacts{
		private final int servingSize;
		private final int servings;
		private final int calories;
		private final int fat;
		
		public NutritionFacts(int servingSize ,int servings){
			this(servingSize, servings,0);
		}
		
		public NutritionFacts(int servingSize ,int servings ,int calories){
			this(servingSize, servings, calories,0);
		}
		
		public NutritionFacts(int servingSize ,int servings ,int calories ,int fat){
			this.servingSize = servingSize;
			this.servings = servings;
			this.calories = calories
			this.fat = fat;
		}
	}
	
	JavaBean模式：构造过程被划分到了几个调用中，JavaBean对象很有可能处于不一致状态，出错都不好调试，得通过额外的努力保证线程安全
	public class NutritionFacts{
		private final int servingSize = -1;
		private final int servings = -1;
		private final int calories = 0;
		private final int fat = 0;
		
		public NutritionFacts(){
			
		}
		//Setters
		public void setServingSize(int val){ servingSize = val; }
		public void setServings(int val){ servings = val; }
		public void setCalories(int val){ calories = val; }
		public void setFat(int val){ fat = val; }
	}
	
	Builder模式 : NutritionFacts facts = new NutritionFacts.Builder(240,8).calories(100).fat(10).builder();
	
	结合了以上两种的优点
	public class NutritionFacts{
		private final int servingSize;
		private final int servings;
		private final int calories;
		private final int fat;
		
		public NutritionFacts(Builder builder){
			servingSize = builder.servingSize;
			servings = builder.servings;
			calories = builder.calories;
			fat = builder.fat;
		}
		
		public static class Builder{
			private final int servingSize = -1;
			private final int servings = -1;
			private final int calories = 0;
			private final int fat = 0;
			
			public Builder(int servingSize ,int servings){
				this.servingSize = servingSize;
				this.servings = servings;
			}
			
			public Builder calories(int val){
				calories = val;
				return this;
			}
			
			public Builder fat(int val){
				fat = val;
				return this;
			}
			
			public NutritionFacts builder(){
				return new NutritionFacts(this);
			}
		}
		
	}
	
	补充：
	public interface Builder<T>{
		public T build();
	}
	
####*❸ 用 [私有构造器] 或者 [枚举类型] 强化Singleton属性*
> 第一种
		
	public class Elvis{
		public static final Elvis INSTANCE = new Elvis();
		
		private Elvis(){ ... }
		
		public void leaveTheBuilding(){ ... }
	}
> 第二种

	public class Elvis{
		private static final Elvis INSTANCE = new Elvis();
		
		private Elvis(){ ... }
		
		public static Elvis getInstance(){ return INSTANCE; }
		
		public void leaveTheBuilding(){ ... }
	}
> 第三种：推荐

	public enum Elvis{
		INSTANCE;
		
		public void leaveTheBuilding(){ ... }
	}

####*❹ 用 [私有构造器] 强化不可实例化的能力*
	public class xxxUtil{
	
		//Suppress default constructor for noninstantiability
		private xxxUtil(){
			throw new xxxUtil();
		}
		
		public static T xxxMethod(T ...){
			return T;
		}
	}
	
####*❺ 避免创建不必要的对象*

> example
	
	public class Person {

		private final Date birthDate = new Date();

		public boolean isBabyBoomer() {
			// Unnecessary allocation of expensive object
			Calendar gmtCal = Calendar.getInstance(TimeZone.getTimeZone("GMT"));
			gmtCal.set(1946, Calendar.JANUARY, 1, 0, 0, 0);
			Date boomStart = gmtCal.getTime();
			gmtCal.set(1965, Calendar.JANUARY, 1, 0, 0, 0);
			Date boomEnd = gmtCal.getTime();
			return birthDate.compareTo(boomStart) >= 0 && birthDate.compareTo(boomEnd) < 0;
		}
	}
	
	//在被重复调用的时候，效率提升大约250倍
	public class Person {

		private final Date birthDate = new Date();

		private static final Date BOOM_START;
		private static final Date BOOM_END;

		static {
			Calendar gmtCal = Calendar.getInstance(TimeZone.getTimeZone("GMT"));
			gmtCal.set(1946, Calendar.JANUARY, 1, 0, 0, 0);
			BOOM_START = gmtCal.getTime();
			gmtCal.set(1965, Calendar.JANUARY, 1, 0, 0, 0);
			BOOM_END = gmtCal.getTime();
		}

		public boolean isBabyBoomer() {
			// Unnecessary allocation of expensive object
			return birthDate.compareTo(BOOM_START) >= 0 && birthDate.compareTo(BOOM_END) < 0;
		}
	}
	
<mark>Java 1.5之后，允许程序员将基本类型和装箱基本类型混用，称为自动装箱（优先使用基本类型）</mark>
	
	public static void mani(String[] args){
		Long sum = 0L;
		long sum = 0L;//程序执行时间从43秒减少到6.8秒，包装类型会增加JVM开销
		for (long i = 0; i < Integer.MAX_VALUE; i++) {
            sum += i;
       }
       System.out.println(sum);
	}

####*❻ 消除过期的对象引用*

android中的使用场景较少，以一个例子带过

	public class Stack{
		private Object[] elements;
		
		private int size = 0;
		
		private static final int DEFAULT_INITIAL_CAPACITY = 16;
		
		public Stack(){
			elements = new Object[DEFAULT_INITIAL_CAPACITY];
		}
		
		public void push(Object e){
			ensureCapacity();
			elements[size++] = e;
		}
		
		public Object pop(){
			if(size == 0)
				throw new EmptyStackException();
			Object result = elements[--size];
			elements[--size] = null;//优化方法
			return result;
		}
		
		private void ensureCapacity(){
			if(elements.length == size)
				elements = Arrays.copyOf(elements, 2 * size + 1);
		}
	}
	
	如果一个栈显示增长，然后在收缩，那么，从栈中弹出来的对象不会被垃圾回收，因为栈内部维护着对这些对象的过期引用（OOM）
	...
	
####*❼ 避免使用终结方法*
	后续更新，不做阐述...

	
	

	


