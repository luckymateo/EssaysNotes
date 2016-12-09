****
#代理模式
>简介

代理模式也称为委托模式。。。结构性设计模式
****

* 定义：为其他对象提供一种代理以控制对这个对象的访问。
* 使用场景 ->
	* 当无法或不想直接访问某个对象或访问某个对象存在困难时可以通过一个代理对象来间接访问，为了保证客户端使用的透明性，委托对象与代理对象需要实现相同的接口。
	
* 通用代码模式
	
		/**
 		* 抽象主题
 		*/
		public abstract class Subject {
			public abstract void visit();
		}	
		
		//真是场景
		public class RealSubject extends Subject{

			@Override
			public void visit() {
				System.out.println("real subject！");
			}

		}
		
		//被委托类 或者代理类
		public class ProxySubject extends Subject {

			RealSubject mSubject;

			public ProxySubject(RealSubject mSubject) {
				super();
				this.mSubject = mSubject;
			}

			@Override
			public void visit() {
				mSubject.visit();
			}

		}
		
		public class Client {

			public static void main(String[] args) {
				RealSubject real = new RealSubject();

				ProxySubject proxy = new ProxySubject(real);// 中间代理层

				proxy.visit();
			}

		}



* 代理模式的简单实现

		/**
 		* 诉讼类接口
 		*/
		public interface ILawsuit {
			void submit();// 提交申请

			void burden();// 进行举证

			void defend();// 开始辩护

			void finish();// 诉讼完成
		}
		
		
		/**
 		* 具体诉讼人，小明
 		*/
		public class XiaoMin implements ILawsuit {

			@Override
			public void submit() { // 提交申请
				// 老板欠小民工资 小民只好申请仲裁
				System.out.println("老板拖欠工资！特此申请仲裁！");
			}

			@Override
			public void burden() { // 举证
				// 小民证据充足，不怕被告赢
				System.out.println("这是合同书和过去一年的银行卡工资流水！");
			}

			@Override
			public void defend() { // 辩护
				// 铁证如山，辩护也没什么好说的
				System.out.println("证据确凿！不需要再说什么了！");
			}

			@Override
			public void finish() { // 诉讼结束
				// 结果也是肯定的，必赢
				System.out.println("诉讼成功！判决老板七日内结算工资！");
			}

		}
		
		
		/**
 		* 代理律师
 		*/
		public class Lawyer implements ILawsuit {

			private ILawsuit mILawsuit;

			public Lawyer(ILawsuit mILawsuit) {
				this.mILawsuit = mILawsuit;
			}

			@Override
			public void submit() {
				mILawsuit.submit();
			}

			@Override
			public void burden() {
				mILawsuit.burden();
			}

			@Override
			public void defend() {
				mILawsuit.defend();
			}

			@Override
			public void finish() {
				mILawsuit.finish();
			}

		}
		
		public class Client {

			public static void main(String[] args) {
				ILawsuit xiaomin = new XiaoMin();//当事人

				ILawsuit lawyer = new Lawyer(xiaomin);//代理律师

				// 由律师发起 仲裁流程
				lawyer.submit();
				lawyer.burden();
				lawyer.defend();
				lawyer.finish();
			}
		}

* Android源码中的代理模式实现

	* ActivityManagerProxy代理类，具体代理的是 ActivityManagerNative 的子类ActivityManagerService。。
	* Android中的Binder跨进程通信机制与AIDL



