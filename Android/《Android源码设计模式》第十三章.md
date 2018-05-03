****
#备忘录模式
>简介

备忘录模式是一种行为模式，该模式用于保存对象当前状态，并且在之后可以再次恢复到此状态。。。
****

* 定义：在不破坏封闭的前提下，捕获一个对象的内部状态，并在该对象之外保存这个状态，这样。以后就可将该对象恢复到原先保存的状态。
* 使用场景 ->
	* 需要保存一个对象在某一个时刻的状态或部分状态。
	* 如果用一个接口来让其他对象得到这些状态，将会暴露对象的实现细节并破坏对象的封装性，一个对象不希望外界直接访问其内部状态，通过中间对象可以直接访问其内部状态。
	
* 简单实现
	
		public class CallOfDuty {
			private int mCheckpoint = 1;
			private int mLiftValue = 100;
			private String mWeapon = "沙漠之鹰";

			public void play() {
				System.out.println("玩游戏：" + String.format("第%d关", mCheckpoint) + "奋战杀敌中");
				mLiftValue -= 10;
				System.out.println("进度升级啦");
				mCheckpoint++;
				System.out.println("到达" + String.format("第%d关", mCheckpoint));
			}

			public void quit() {
				System.out.println("---------------------");
				System.out.println("退出前的游戏属性 ：" + this.toString());
				System.out.println("退出游戏");
				System.out.println("---------------------");
			}

			public Memoto createMemoto() {
				Memoto memoto = new Memoto();
				memoto.mCheckpoint = mCheckpoint;
				memoto.mLiftValue = mLiftValue;
				memoto.mWeapon = mWeapon;
				return memoto;
			}

			public void restore(Memoto memoto) {
				this.mCheckpoint = memoto.mCheckpoint;
				this.mLiftValue = memoto.mLiftValue;
				this.mWeapon = memoto.mWeapon;
				System.out.println("恢复后的游戏属性 ：" + this.toString());
			}

			@Override
			public String toString() {
				return "CallOfDuty [mCheckpoint=" + mCheckpoint + ", mLiftValue=" + mLiftValue + ",mWeapon" + mWeapon + "]";
			}
		}
		
		public class Memoto {
			public int mCheckpoint;
			public int mLiftValue;
			public String mWeapon;

			@Override
			public String toString() {
				return "Memoto [mCheckpoint=" + mCheckpoint + ", mLiftValue=" + mLiftValue + ",mWeapon" + mWeapon + "]";
			}
		}
		
		public class Caretaker {
			Memoto mMemoto;

			public void archive(Memoto memoto) {
				this.mMemoto = memoto;
			}

			public Memoto getMemoto() {
				return mMemoto;
			}
		}
		
		public class Client {

			public static void main(String[] args) {
				CallOfDuty game = new CallOfDuty();
				game.play();

				Caretaker caretaker = new Caretaker();

				caretaker.archive(game.createMemoto());
				game.quit();

				CallOfDuty newGame = new CallOfDuty();
				newGame.restore(caretaker.getMemoto());
			}

		}


> 优点

* *给用户提供了一种可以恢复状态的机制，可以使用户能够比较方便地回到某个历史的状态；*
* *实现了信息的封装，使得用户不需要关心状态的保存细节*

> 缺点

* *消耗资源，如果累的成员变量过多，势必会占用比较大的资源，而且每一次保存都会消耗一定的内存。*

总结
****
备忘录模式是在不破坏封装的条件下，通过备忘录对象存储另外一个对象内部状态的快照，在将来合适的时候把这个对象还原到存储起来的状态。
****


