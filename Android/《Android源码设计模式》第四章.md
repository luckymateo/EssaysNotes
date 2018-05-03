****
#原型模式
>简介

原型模式是一个创建型的模式。原型二字表明了该模板应该有一个样板实例。
****

* 定义：用原型实例指定创建对象的种类，并通过拷贝这些原型创建新的对象。
* 使用场景 ->
	* 类初始化需要消化非常多的资源，这个资源包括数据。硬件等，通过原型拷贝避免这些消耗。
	* 通过new产生一个对象需要非常繁琐的数据准备或访问权限，这时可以使用原型模式。
	* 一个对象需要提供给其他对象访问，而且各个调用者可能都需要修改其值时，可以考虑使用原型模式拷贝多个对象供调用者使用，即保护性拷贝。
	
* 深拷贝和浅拷贝

		@Override
    	protected WordDocument clone(){
        	try {
            	WordDocument doc = (WordDocument) super.clone();
            	doc.mText = this.mText;
            	doc.mImages = this.mImages; --> 浅拷贝
            	return doc;
        	} catch (CloneNotSupportedException e) {
        	}
        	return null;
    	}
    	
    	@Override
    	protected WordDocument clone(){
        	try {
            	WordDocument doc = (WordDocument) super.clone();
            	doc.mText = this.mText;
            	doc.mImages = (ArrayList<String>) this.mImages.clone();--> 深拷贝
            	return doc;
        	} catch (CloneNotSupportedException e) {
        	}
        	return null;
    	}
    * 区别：深拷贝为保护性拷贝，即使被拷贝内容被改变，也不会影响原型。浅拷贝反之。
* 原型模式本质上就是对象拷贝

> 优点

*原型模式是在内存中二进制流的拷贝，要比直接new一个对象性能好很多，特别是要在一个循环体内产生大量的对象时，原型模式可以更好地体现其优点。*

> 缺点

*这既是它的优点又是它的缺点，直接在内存中拷贝，构造函数是不会执行的，在实际开发当中应该注意这个潜在的问题。优点就是减少了约束，缺点也是减少了约束，需要大家在实际应用时考虑。*

****
通过实现Cloneable接口的原型模式在调用clone函数构造实例时并不一定比通过new操作速度快，只有当通过new构造对象较为耗时或者说成本较高时，通过clone方法才能够获得效率上的提升。因此，在使用Cloneable时需要考虑构建对象的成本以及做一些效率上的测试。当然，实现原型模式不一定非要实现Cloneable接口，也有其他的实现方式。
	
	其他方式，类似于Android 中Intent的clone方法
	
	@Override
    public Object clone() {
        return new Intent(this); --> new 开销的成本
    }

使用clone和new需要根据构造对象的成本来决定
****

###本节问题
****

![](http://img.blog.csdn.net/20160316125730134)

[为什么String类型的变量，在浅拷贝下也修改了，但原型并未改变呢？](http://blog.csdn.net/jonstank2013/article/details/50904467)

String类型是一个值类型

String指向的对象是一个不可变的对象，String类型的每次变化其实都是创建一个新的对象，之后再将引用指向这个新的对象而已。之前的那个对象其实还是存在的，只是我们不指向它了。 
如果将String mText更改为StringBuffer mText, setText方法更改为append(text)的话结果就一样了。


