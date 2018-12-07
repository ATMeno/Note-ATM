#IO流
- 关闭资源原则：先开后关
#字节流
##一.输入字节流 InputStream
###1.文件输入字节流 FileInputStream
	read()
	read(byte[] b)
###2.缓冲输入字节流 BufferedInputStream 提高读取文件效率
	凡是缓冲流都没有读写数据的能力  

	BufferedInputStream(InputStream in)  
	(具体看源码)close()						实际关闭的就是in,即调用in.close()
	
##二.输出字节流 OutputStream
###1.文件输出字节流 FileOutputStream
	new FileOutputStream(File file)					如果不存在该文件，则会先创建再写入；如果存在该文件，则会覆写该文件数据
	new FileOutputStream(File file,boolean append)	是否追加数据
	（坑）write(int b)								虽然接受的参数是一个int类型数据，但实际只会把数据的低八位写入，其余24位丢弃
###2.缓冲输出字节流 BufferedOutputStream 提高读取文件效率
	(具体看源码)close()		实际关闭的就是in,即调用in.close()
	flush()					调用flush()才能将数据写入硬盘
	调用flush()或者close()或者缓冲数组满了才会从内存写入到硬盘上

#字符流   
- 字符流 = 字节流 + 编码（解码）
##三.输入字符流  Reader
###1.文件输入字符流 FileReader

###2.缓冲输入字符流 BufferedReader
	readLine()			一行一行读

##四.输出字符流	Writer
- **内部维护了一个1KB的char[]数组)，所以写入需要flush或close或者数组满**
###1.文件输出字符流 FileWriter
	new FileWriter(File file)		如果没有文件，则会创建，如果有，则不会

###2.缓冲输出字符流
	newLine()			调用本系统的回车换行
