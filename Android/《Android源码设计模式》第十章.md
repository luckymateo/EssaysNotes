****
#解释器模式
>简介

该模式定义了一个表达式接口，通过该接口解释一个特定的上下文。
****

* 定义：给定一个语言，定义它的文法的一种表示，并定义一个解释器，该解释器使用该表示来解释语言的句子。解释器模式设计编程语言理论知识较多，就拿上面对该模式的定义来说，
* 使用场景 ->
	* 如果某个简单的语言需要解释执行而且可以将该语言中的语句表示为一个抽象语法树时可以考虑使用解释器模式。
	* 在某些特定的领域出现不断重复的问题时，可以将该领域的问题转化为一种语法规则下的语句，然后构建解释器来解释该语句。
	
* 解释器模式

		public abstract class AbstractExpression {

			/**
		 	* 抽象的解析方法
			* 
		 	* ctx
	 	 	*/
			public abstract void interpret(Context ctx);
		}
    	
    	public class TerminalExpression extends AbstractExpression {

			@Override
			public abstract void interpret(Context ctx){
				//实现文法中与终结符有关的解释操作
			}

		}
		
		public class NonterminalExpression extends AbstractExpression {

			@Override
			public abstract void interpret(Context ctx){
				//实现文法中与非终结符有关的解释操作
			}

		}
		
		public class Context {
		}
		
		public class Client {

			public static void main(String[] args) {
				// 根据文法对特定句子构建抽象语法树后解释
			}
		}
    	
    	
    * AbstractExpression：抽象表达式
    * TerminalExpression：终结符表达式
    * NonterminalExpression：非终结符表达式
    * Context：上下文环境类
    * Client：客户类


****
总结

解释器模式优点：解释器模最大的有点事其灵活的扩展性，当我们想对文法规则进行扩展延伸时，只需要增加相应的非终结符解释器，并在都贱抽象语法树时，使用到新增的解释器对象进行具体的解释即可，非常方便。

缺点：为每一条文法都可以对应至少一个解释器，其会生成大量的类，导致后期维护困难；同时，对于过于复杂的文法，构建其抽象语法树会显得异常烦琐，甚至有可能会出现需要构建多颗语法树的情况。
****



