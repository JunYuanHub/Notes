## File类  
```  
方法名称	说明
boolean canRead()	测试应用程序是否能从指定的文件中进行读取
boolean canWrite()	测试应用程序是否能写当前文件
boolean delete()	删除当前对象指定的文件
boolean exists()	测试当前 File 是否存在
String getAbsolutePath()	返回由该对象表示的文件的绝对路径名
String getName()	返回表示当前对象的文件名或路径名（如果是路径，则返回最后一级子路径名）
String getParent()	返回当前 File 对象所对应目录（最后一级子目录）的父目录名
boolean isAbsolute()	测试当前 File 对象表示的文件是否为一个绝对路径名。该方法消除了不同平台的差异，可以直接判断 file 对象是否为绝对路径。在 UNIX/Linux/BSD 等系统上，如果路径名开头是一条斜线/，则表明该 File 对象对应一个绝对路径；在 Windows 等系统上，如果路径开头是盘符，则说明它是一个绝对路径。
boolean isDirectory()	测试当前 File 对象表示的文件是否为一个路径
boolean isFile()	测试当前 File 对象表示的文件是否为一个“普通”文件
long lastModified()	返回当前 File 对象表示的文件最后修改的时间
long length()	返回当前 File 对象表示的文件长度
String[] list()	返回当前 File 对象指定的路径文件列表
String[] list(FilenameFilter)	返回当前 File 对象指定的目录中满足指定过滤器的文件列表
boolean mkdir()	创建一个目录，它的路径名由当前 File 对象指定
boolean mkdirs()	创建一个目录，它的路径名由当前 File 对象指定
boolean renameTo(File)	将当前 File 对象指定的文件更名为给定参数 File 指定的路径名
```