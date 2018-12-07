#File类
##1.创建文件/文件夹
	File(String pathname)
	File(File parent,String child)
	Flie(String parent,String child)
##2.路径
- 盘符  
	windows:/或者\\
	Linux/Unix:/
- 绝对路径与相对路径  
	/	根目录  
	./	当前目录  
	../	上一级目录  
	3.类加载路径
	4.服务器路径
	5.

##3.常用方法
###创建
	createNewFile()			创建文件
	mkdir()					创建文件夹
	mkdirs()				创建多级文件夹
	renameTo(File dest)		
	1.重命名：如果源文件与目标文件在同一目录下，重命名文件/文件夹  
	2.剪切：如果源文件与目标文件不在同一级目录下，剪贴文件，并重命名（并不能剪贴文件夹）

###删除
	delete()				删除文件/空文件夹（不能删除非空文件夹）
	deleteOnExit()			虚拟机终止时进行删除，保证程序异常时创建的临时文件也能删除

###判断
	exist()					文件/文件夹是否存在
	isFile()				是否是一个文件
	isDirectory()			是否是一个目录（即文件夹）
	isHidden()				是否是一个隐藏文件/文件夹
	isAbsolute()			输入的路径是否为绝对路径
 
###获取
	(假)getName()			获取文件/文件夹名，不包含上级目录（直接返回输入的最后/后面的值）
	(假)getPath()			获取绝对路径（直接返回输入的路径）
	上面两个方法很假，都是输出传入值，不会校验传入的路径值是否存在
	(假)getAbsolutePath()	获取绝对路径（如果输入的是绝对路径，原样输出；如果输入的是相对路径，输出 当前路径+输入的相对路径） 
	length()				获取文件的大小（字节数）,如果文件不存在返回0，如果文件夹返回0
	(假)getParent()			返回父目录（直接输出输入的文件上级目录），如果没有父路径，则返回null
	lastModified()			最后一次被修改的时间

###文件夹相关
	static File[] listRoot()	列出所有的根目录（window中就是所有系统的盘符）
	String[] list()				获取当前路径下的所有子文件名/子文件夹名（包含隐藏），对于文件这样操作会返回Null
	File[] listFiles()			获取所有文件和子目录（文件夹）
	list(FilenameFilter filter)