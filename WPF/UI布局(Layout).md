#UI布局(Layout)

###布局元素：
- Grid:网格。可以自定义行和列并通过行列的数量、行高和列宽来调整控件的布局。近似于HTML的Table。
- StackPanel:栈式面板。可将包含的元素在竖直或水平方向上排成一条直线，当移除一个元素后，后面的元素会自动向前移动以填充空缺。
- Canvas:内部元素可以使用以像素为单位的绝对坐标进行定位。
- DockPanel:泊靠式面板。内部元素可以选择泊靠方向。
- WrapPanel:自动拆行面板。内部元素在排满一行后能够自动折行。

###静态布局和动态布局
- 静态布局：在XMAL中进行布局
- 动态布局：在C#代码中进行布局


##1.Grid
###特点：
- 可以定义任意数量的行和列，非常灵活
- 行的高度和列的宽度可以使用绝对数值，相对比例或者自动调整的方式进行精确设定，并可设定最大和最小值
- 内部元素可以设置自己的所在的行和列，还可以设置自己纵向跨几行、横向跨几行
- 可以设置Children元素的对齐方向
###适用场景：
- UI布局的大框架设计
- 大量UI元素需要成行或者成列对齐的情况
- UI整体尺寸改变时，元素需要保持固有的高度和宽度比例
- UI后期可能有较大的变更或者扩展
###如何选用单位：
px:屏幕  
cm:打印  
in:打印  
![](https://i.imgur.com/9VOGVM5.png)
###取值：
- 绝对值(固定值)：double数值加单位后缀（例：40px,12cm）
- 比例值：double数值加"*"(例：30*)
- 自动值：字符串Auto
###实现可拖拽的分隔栏
- 使用Grid和GridSplitter(GridSplitter会改变Grid的初始设置的行高和列宽)   

		<GridSplitter Grid.Row="1" Grid.Column="1"  
			VerticalAlignment="Stretch"  
			HorizontalAlignment="Center"  
			Width="5"  
			Background="Gray"  
			ShowsPreview="True"></GridSplitter>
##2.StackPanel
###适用场景：
- 同类元素需要紧凑排列（如制作菜单或者列表）
- 移除其中的元素后能够自动补缺的布局或者动画

##3.Canvas
###适用场景:
- 一经设计基本不会在改变的小型布局（如图标）
- 艺术性比较强的布局
- 需要大量使用横纵坐标进行绝对定点的布局
- 依赖横纵坐标的动画

##4.DockPanel
![](https://i.imgur.com/6PVROhG.png)

##5.WrapPanel
WrapPanel是流式布局，在流延伸方向上，会尽可能多的排列控件，排不下的控件将会新起一行或一列
![](https://i.imgur.com/iTWlR0t.png)