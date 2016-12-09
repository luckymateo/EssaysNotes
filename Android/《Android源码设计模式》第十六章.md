****
#访问者模式
>简介

访问者模式是一种将数据操作与数据结构分离的设计模式，它也是最复杂的一个，大多数情况下，你并不需要使用访问者模式，但是当你一旦需要使用它时，那你就是真正的需要它了。。。哈哈哈


>基本思想

* 拥有一个accept方法用来注入访问者
* 拥有一个visit方法，对访问对象结构元素作出不同处理

****

* 定义：封装一些作用于某种数据结构中的各元素的操作，它可以在不改变这个数据结构的前提下定义作用于这些元素的新的操作。
* 使用场景 ->
	* 对象结构比较稳定，但经常需要在此对象结构上定义新的操作。
	* 需要对一个对象结构中的对象进行很多不同的并且不相关的操作，二需要避免这些操作“污染”这些对象的类，也不希望在增加新操作时修改这些类。
	
* Demo实现
	
		public abstract class Staff {
			public String name;
			// 员工KPI
			public int kpi;

			public Staff(String name) {
				this.name = name;
				kpi = new Random().nextInt(10);
			}

			public abstract void accept(Visitor visitor);

		}
		
		public interface Visitor {

			public void visit(Engineer engineer);

			public void visit(Manager manager);
		}
		
		public class Manager extends Staff{
	
			private int products;

			public Manager(String name) {
				super(name);
				products = new Random().nextInt(10);
			}

			@Override
			public void accept(Visitor visitor) {
				visitor.visit(this);
			}
	
			public int getProducts(){
				return products;
			}

		}
		
		public class Engineer extends Staff {

			public Engineer(String name) {
				super(name);
			}

			@Override
			public void accept(Visitor visitor) {
				visitor.visit(this);
			}

			public int getCodeLines() {
				return new Random().nextInt(10 * 10000);
			}

		}
		
		public class BusinessReport {
			List<Staff> mStaffs = new ArrayList<>();

			public BusinessReport() {
				mStaffs.add(new Manager("王经理"));
				mStaffs.add(new Engineer("工程师- 小李"));
				mStaffs.add(new Engineer("工程师- 小王"));
				mStaffs.add(new Engineer("工程师- 小明"));
				mStaffs.add(new Engineer("工程师- 小马"));
			}

			public void showReport(Visitor visitor) {
				for (Staff staff : mStaffs) {
					staff.accept(visitor);
				}
			}

		}
		
		public class ReportUtil {
			public void visit(Staff staff) {
				if (staff instanceof Manager) {
					Manager manager = (Manager) staff;
					System.out.println("经理 ：" + manager.name + ",KPI :" + manager.kpi + ",新产品数量： " + manager.getProducts());
				} else {
					Engineer engineer = (Engineer) staff;
					System.out.println("工程师 ： " + engineer.name + ",KPI :" + engineer.kpi);
				}
			}
		}
		
		public class CEOVisitor implements Visitor {

			@Override
			public void visit(Engineer engineer) {
				System.out.println("工程师 ：" + engineer.name + ", KPI :" + engineer.kpi);
			}

			@Override
			public void visit(Manager manager) {
				System.out.println("经理 ：" + manager.name + ", KPI :" + manager.kpi + ",新产品数量：" + manager.getProducts());
			}

		}
		
		public class CTOVisitor implements Visitor {

			@Override
			public void visit(Engineer engineer) {
				System.out.println("工程师 ：" + engineer.name + ", 代码函数 :" + 		engineer.getCodeLines());
			}

			@Override
			public void visit(Manager manager) {
				System.out.println("经理 ：" + manager.name + ",产品数量：" + manager.getProducts());
			}

		}
		
		public class Client {

			public static void main(String[] args) {
				BusinessReport report = new BusinessReport();
				System.out.println("=============给CEO看的报表=============");
				report.showReport(new CEOVisitor());
				System.out.println("=============给CTO看的报表=============");
				report.showReport(new CTOVisitor());
			}

		}



* Android源码中的访问者模式实现

	* Butterknife 、Dagger 、Retrofit 等都基于APT （编译注解）
	* 使用基类 Element 去实现注解

> 优点

* *各角色职责分离，符合单一职责原则；*
* *具有优秀的扩展性；*
* *使得数据结构和作用于结构上的操作解耦，使得操作集合可以独立变化；*
* *灵活性。*

> 缺点

* *具体元素对访问者公布细节，违反了迪米特原则。*
* *具体元素变更时导致修改成本大。*
* *违反了依赖倒置原则，为了到达“区别对待”而依赖了具体类，没有依赖抽象。*
