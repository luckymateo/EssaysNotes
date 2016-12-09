****
#享元模式
>简介

享元模式是对象池的一种实现，它的英文名称叫做FlyWeight，代表轻量级的意思，享元模式用来尽可能减少内存使用量，它适合用于可能存在大量重复对象的场景，来缓存可共享的对象，达到对象共享，避免创建过多对象的效果，这样依赖就可以替身性能、避免内存移除等。。。
****

* 定义：使用共享对象可有效地支持大量的细粒度的对象。
* 使用场景 ->
	* 系统中存在大量的相似对象。
	* 细粒度的对象都具备较接近的外部状态，而且内部状态与环境无关，也就是说对象没有特定身份。
	* 需要缓冲池的场景。
	
* 简单实现
	
		public interface Ticket {
			void showTicketInfo(String bunk);
		}			
		
		public class TrainTicket implements Ticket {

			public String from;// 始发地
			public String to;// 目的地
			public String bunk;// 铺位
			public int price;

			public TrainTicket(String from, String to) {
				this.from = from;
				this.to = to;
			}

			@Override
			public void showTicketInfo(String bunk) {
				price = new Random().nextInt(300);
				System.out.println("购买从" + from + "到" + to + "的" + bunk + "火车票" + ",价格：" + price);
			}

		}	
		
		public class TicketFactory {

			static Map<String, Ticket> sTicketMap = new ConcurrentHashMap<>();

			public static Ticket getTicket(String from, String to) {
				String key = from + "-" + to;
				if (sTicketMap.containsKey(key)) {
					System.out.println("使用缓存 ==>" + key);
					return sTicketMap.get(key);
				} else {
					System.out.println("创建对象 ==>" + key);
					Ticket ticket = new TrainTicket(from, to);
					sTicketMap.put(key, ticket);
					return ticket;
				}
			}
		}
		
		public class Client {
			public static void main(String[] args) {
				Ticket ticket01 = TicketFactory.getTicket("北京", "青岛");
				ticket01.showTicketInfo("上铺");
				Ticket ticket02 = TicketFactory.getTicket("北京", "青岛");
				ticket02.showTicketInfo("下铺");
				Ticket ticket03 = TicketFactory.getTicket("北京", "青岛");
				ticket03.showTicketInfo("坐票");
			}
		}

* 源码中的享元模式实现

	* String中的常量池
	* Handle Message MessageQueue Looper


总结
****
享元模式实现比较简单，但是它的作用在某些场景确实机器重要的。它可以打打减少应用程序创建的对象，降低程序内存的占用，增强程序的性能，但它同时也提高了系统的复杂性，需要分离出外部状态和内部状态，而且外部状态具有固话特性，不应该随内部状态改变而改变，否则导致系统的逻辑混乱。
	
* 享元模式的优点在于大幅度降低内存中对象的数量。但是，他做到这一点所付出的代价也很高。
	* 享元模式使得系统更加复杂。为了使对象可以共享，需要将一些状态外部化，这使得程序的逻辑复杂化。
	* 享元模式将享元对象的状态外部化，而读取外部状态使得运行时间稍微变长。

****


