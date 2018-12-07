###1.绑定语法（XAML中，C#代码中）
###2.绑定的Path
###3.绑定的Source
###4.控制Binding数据流向和数据更新时间
###5.数据转换与校验
###6.其他关键词
Data Binding  
Dependency Property  
Data Template  

----------
##基础
###1.类实现INotifyPropertyChanged接口并在set方法中激发PropertyChanged事件。
txtAge.SetBinding(TextBox.TextProperty, new Binding("Name") { Source = stu = new Student() });
###2.把控件作为Binding源与Binding标记扩展
txtSilder.SetBinding(TextBox.TextProperty, new Binding("Value") { ElementName = "slider1" });
###3.控制Binding的方向及数据更新
①控制数据流向的属性是Mode，它的类型是BindingMode枚举  
②控制何时更新的属性是UpdateSourceTrigger,它的类型是UpdateSourceTrigger枚举  
③NotifyOnSourceUpdated、NotifyOnTargetUpdated两个bool类型，当源或目标更新后Binding会激发相应的SourceUpdated事件和TargetUpdated事件，实际工作中，可以监听这两个事件来找出有哪些数据或者控件被更新了  

----------
##为Binding指定路径(Path)
###1.Binding的路径（Path）
Source传对象，ElementName传控件名（x:Name）  
绑定集合用法
###2."没有Path"的Binding
Binding源本身就是数据且不需要Path来指明	
string myString="AAA"
txt1.SetBinding(TextBox.TextProperty,new Binding(".") { Source = myString });

----------
##为Binding指定源（Source）
- 1.实现INotifyPropertyChanged接口，通过在属性的set语句中激发PropertyChanged事件来通知Binding数据已被更新
- 2.把集合指定为Source。一般把集合作为ItemControl派生类的数据源，把控件的ItemSource属性使用Binding关联到一个集合对象上
- 3.把ADO.NET数据对象指定为Source：包括DataTable和DataView等对象。
- 4.XMLDataProvider把XML数据指定为Source
- 5.把依赖对象（Dependengcy Object）指定为Source
- 6.把容器的DataContext指定为Source。知道从哪个属性获取数据，但不确定从哪个对象时使用
- 7.通过ElementName指定Source
- 8.通过Binding的RelativeSource属性相对地指定Source：当控件需要关注自己的、自己的容器的或者自己内部元素的某个值时使用
- 9.把ObjectDataProvider对象指定为Source:当数据源的数据不是通过属性而是通过方法暴露给外界的时候，可以使用这两种对象来包装数据源再把它们指定为Source
- 10.把使用LINQ检索得到的数据对象作为Binding的源

###1.没有Source的Binding——使用DataContext作为Binding源
	自动沿着UI树寻找每个节点是否有Path属性  
![](https://i.imgur.com/VWIIWKg.png)
####使用场景：
- 当UI上的多个控件都使用Binding关注同一个对象时，不妨使用DataContext
- 当作为Source的对象不能直接被访问的时候（详见P98）
###2.使用集合对象作为列表控件的ItemsSource
	列表控件派生自ItemControl,也就继承了ItemsSource属性。ItemsSource属性可以接收IEnumerable实现的值（如数组，List<T>)