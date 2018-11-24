Data Binding  
Dependency Property  
Data Template  

----------

###0.类实现INotifyPropertyChanged接口并在set方法中激发PropertyChanged事件。
txtAge.SetBinding(TextBox.TextProperty, new Binding("Name") { Source = stu = new Student() });
###1.把控件作为Binding源与Binding标记扩展
txtSilder.SetBinding(TextBox.TextProperty, new Binding("Value") { ElementName = "slider1" });
###2.控制Binding的方向及数据更新
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
###1.没有Source的Binding——使用DataContext作为Binding源
	自动沿着UI树寻找每个节点是否有Path属性  
####使用场景：
- 当UI上的多个控件都使用Binding关注同一个对象时，不妨使用DataContext
- 当作为Source的对象不能直接被访问时
###2.使用集合对象作为列表控件的ItemsSource
