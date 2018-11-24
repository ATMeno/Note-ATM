#GOF23设计模式

##序
###创建型模式（用来构建对象）
	-单例模式、工厂模式、抽象工厂模式、建造者模式、原型模式
###结构型模式
	-适配器模式、桥接模式、装饰模式、组合模式、外观模式、享元模式、代理模式
###行为型模式
	-模板方法模式、命令模式、迭代器模式、观察者模式、中介者模式、备忘录模式、解释器模式、状态模式、策略模式、责任链模式、访问者模式

##1.单例模式
###核心作用：
	-保证一个类只有一个实例，并且提供一个访问该实例的全局访问点（方法）。

###常见应用场景：
	-Windows的Task Manager(任务管理器)
	-Windows的Recycle Bin(回收站)
	-应用程序的日志应用
	-数据库连接池的设计
	-操作系统的文件操作系统
	-Servlet编程中的Application是一个单例，每个Servlet也是单例
	-Spring中，每个Bean默认就是单例，这样做的有优点是Spring容器可以管理
	-Srping MVC中，控制器对象也是单例

###五个常见实现方法

####主要：懒汉式，饿汉式
####其他：双重检测锁式，静态内部类式，枚举单例
####需要注意的方面：线程安全，调用效率，是否延迟加载
#####懒汉式（线程安全，调用效率高。但是，不能延时加载）
	/**
	* @Description 单例模式---饿汉式
	*             类初始化时，立即加载,线程安全，调用效率高
	* @Author ATMeno
	* @Date 2018-11-20 12:31
	*/
	public class SingleDemo1 {
	//类初始时，立即加载这个对象到加载类中，天然是线程安全的
    private static SingleDemo1 instance = new SingleDemo1();

    private SingleDemo1(){
    }

    public static SingleDemo1 getSingleDemo1(){
        return instance;
    }
#####饿汉式（线程安全，调用效率不高。能够延时加载）
	/**
	 * @Description lazy load 延迟加载
	 *              资源利用率高  每次调用getInstance都要同步，并发效率低
	 * @Author:MAOTY
	 * @Date:2018-11-20 13:54
	 */
	public class SingleDemo2 {
	    private static SingleDemo2 instance;
	
		private SingletonDemo2(){
		
		    }
	    public static synchronized SingleDemo2 getInstance(){
	        if(instance == null){
	            instance = new SingleDemo2();
	        }
	        return instance;
	    }
	}

#####双重检测锁式（不建议使用）
	**问题：由于编译器优化原因和JVM底层内部模型原因，偶尔会出现问题，不建议使用**
	
	这个模式将同步内容下放到if内部，提高了执行的效率，不必每次获取对象时都进行同步，只有第一次同步创建了以后就没必要了。
	
	/**
	 * @Description 双重检测锁式 不建议使用
	 * @Author:MAOTY
	 * @Date:2018-11-20 14:13
	 */
	public class SingletonDemo3 {
	    private static SingletonDemo3 instance;
	
	    private SingletonDemo3(){
	
	    }
	
	    public static SingletonDemo3 getInstance(){
	        if (instance == null){
	            SingletonDemo3 sc;
	            synchronized (SingletonDemo3.class){
	                sc = instance;
	                if(sc == null){
	                    synchronized (SingletonDemo3.class){
	                        if(sc == null){
	                            sc = new SingletonDemo3();
	                        }
	                    }
	                }
	            }
	        }
	        return  instance;
	    }
	}
		

#####静态内部类式（线程安全，调用效率高，实现了延时加载）
	外部类没有static属性，则不会像饿汉式那样立即加载对象。
	只有真正调用getInstance()，才会加载静态内部类，加载类是线程安全的。instance是static final类型，保证了内存中只有一个实例存在，而且只能被赋值一次，从而保证了线程安全。
	兼备了并发效高效调用和延迟加载的优势。

	/**
	 * @Description 静态内部类
	 * @Author:MAOTY
	 * @Date:2018-11-20 14:28
	 */
	public class SingletonDemo4 {
	    private static class SingletonClassInsatnce {
	        private static final SingletonDemo4 instance = new SingletonDemo4();	
	    }

        public static SingletonDemo4 getInstance() {
            return SingletonClassInsatnce.instance;
        }
	
	    private SingletonDemo4(){
	    }
	}	

#####枚举单例（线程安全，效率较高，不能延时加载，并且可以天然防止反射和反序列化）
枚举元素本身就是单例模式

	/**
	 * @Description 枚举实现
	 * @Author:MAOTY
	 * @Date:2018-11-20 14:49
	 */
	public enum SingletonDemo5 {
	    INSTANCE;
	
	    public void SingletonOperation(){
	
	    }
	}
####如何选用？
-单例对象占用资源少，不需要延时加载  
　　　　**枚举式**	>	饿汉式  
-单例对象占用资源大，需要延时加载   
　　　　**静态内部类**		>	懒汉式	


####效率对比		
| 模式 | 耗时
| ------ | ------ | 
| 懒汉式 | 636ms |
| 静态内部类式 | 28ms √|
| 饿汉式 | 22ms |
| 枚举式 | 32ms √|
| 双重检查锁式 | 65ms |



##2.简单工厂模式
###面向对象设计的基本原则（6大原则）
- OCP(开闭原则)：对扩展开放，对修改关闭。
- DIP(依赖倒转原则)：针对接口编程，而不是针对实现编程。
- LoD(迪米特法则)：只与你直接的朋友通信，而避免和陌生人通信。
###工厂模式：
实现了创建者和调用者的分离。

###应用场景
	-JDK中Calendar的getInstance方法  
	-JDBC中Connection对象的获取  
	-Hibernate中的SessionFactory创建Session  
	-spring中IOC容器创建管理bean对象  
	-XML解析时的DocumentBuilderFactory创建解析器对象  
	-反射中Class对象的newInstance() 
###详细分类：		
####1.简单/静态工厂模式(最简单，最常用，但违反了开闭原则)  
######用来生产同一等级结构中的任意产品（对于增加新的产品，需要修改已有代码）
####2.工厂方法模式
######用来生产同一等级结构中的固定产品（支持增加任意产品）  
####3.抽象工厂模式(针对产品族)
######用来生产不同产品族的全部产品（对于增加新的产品，无能为力；支持增加产品族） 


###1.简单/静态工厂模式
最简单，最常用  


###2.工厂方法模式
--为了避免简单工厂模式的缺点，不满足开闭原则。  
--工厂方法模式和简单工厂模式最大的不同在于，简单工厂模式只有一个（对于一个项目或者一个独立模块而言）工厂类，而工厂方法模式有一组实现了相同接口的工厂类。  

|  | 简单工厂模式  |  工厂方法模式  
| ------ | :-: | :-: | 
| 结构复杂度 | √ |	  	
| 代码复杂度 | √ |  
| 客户端编程难度 | √ |  
| 管理上的难度 | √ |   
####综上：根据设计理论，工厂方法模式；实际上，一般采用简单工厂模式。	

###3.抽象工厂模式
--抽象工厂模式是工厂方法模式的升级版本，在有多个业务品种、业务分类时，通过抽象工厂模式产生需要的对象是一种非常好的解决方式。  

##总结
	-简单工厂模式  
	　　虽然某种程度不符合设计模式，但实际使用最多。  
	-工厂方法模式    
	　　不修改已有类的前提下，通过增加新的工厂类实现扩展。  
	-抽象工厂模式   
	　　只可以增加产品族！不可以增加产品。　　

 

##3.工厂方法模式

##4.抽象工厂模式

##5.建造者模式  
- ###场景：  
	我们需要构造一个复杂的产品，这个复杂产品的创建，有这样一个问题需要处理：装配这些组件是不是有个步骤问题？
	实际开发中，我们所需要的对象构建时，也非常复杂，有很多步骤需要处理时。
  
- ###构造模式的本质  
	-分离了对象子组件的单独构造(由Builder来负责)和装配(由Director负责)。从而可以构造出复杂的对象。这个模式适用于:某个对象的构造过程复杂的情况下使用。  
	-由于实现了构建和装配的解耦，不同的构建器，相同的装配，也可以做出不同的对象；相同的构建器，不同的装配顺序也可以做出不同的对象。也就是实现了构建算法、装配算法的解耦，实现了更好的复用。

###应用场景
	-StringBuider类的append方法
	-SQL的PreparedStatement
	-JDOM中，DOMBuilder、SAXBuilder

##6.原型模式

##7.适配器模式

##8.代理模式

##9.桥接模式

##10.组合模式

##11.装饰模式

##12.外观模式

##13.享元模式

##14.责任链模式

##15.迭代器模式

##16.中介者模式

##17.命令模式

##18.解释器模式

##19.策略模式

##20.模板方法模式

##21.状态模式

##22.观察者模式

##23.备忘录模式