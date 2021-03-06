# C and C++ 跨平台编译


autoscan
```bash
autoscan扫描源代码目录生成configure.scan文件
将configure.scan改名为configure.ac,并编辑修改内,去掉无关的
```

aclocal
```bash
aclocal根据configure.in文件的内容,自动生成aclocal.m4文件
```

autoconf
autoreconf -vfi
```bash
autoconf 是 用来生成自动配置软件源代码脚本（configure）的 工具.configure脚本能独立于autoconf运行，且在运行过程中,不需要用户的干预.
```

automake --add-missing
```bash
使用automake --add-missing来产生Makefile.in
--add-missing:add missing standard files to package
```

./configure (软件源代码脚本)
```bash
生成Makefile,用于自动编译和链接
```

make
```bash
使用Makefile编译代码
```

----

命令解释 <a href="https://www.laruence.com/2009/11/18/1154.html">链接地址</a>
```bash
1. autoscan
　　autoscan是用来扫描源代码目录生成configure.scan文件的 .autoscan
可以用目录名做为参数,但如果你不使用参数的 话,那么autoscan将认为使用的是当前目录.
autoscan将扫描你所指定目录中的 源文件,并创建configure.scan文件.
2. configure.scan
　　configure.scan包含了系统配置的 基本选项,里面都是 一些宏定义.我们需要将它改名为
configure.in
3. aclocal
　　aclocal是 一个perl 脚本程序.aclocal根据configure.in文件的 内容
,自动生成aclocal.m4文件.aclocal的 定义是 ："aclocal - create aclocal.m4 by scanning configure.ac".
4. autoconf
　　autoconf是 用来产生configure文件的 .configure是 一个脚本,它能设置
源程序来适应各种不同的操作系统平台,并且根据不同的 系统来产生合适的 Makefile,从而可以使
你的源代码能在不同的操作系统平台上被编译出来.
　　configure.in文件的 内容是 一些宏,这些宏经过autoconf 处理后会变成检查系统
特性.环境变量.软件必须的 参数的 shell脚本.configure.in文件中的 宏的 顺序并没
有规定,但是 你必须在 所有宏的 最前面和最后面分别加上AC_INIT宏和AC_OUTPUT宏.
　　在 configure.ini中：
　　#号表示注释,这个宏后面的 内容将被忽略.
　　AC_INIT(FILE)
　　这个宏用来检查源代码所在 的 路径.
AM_INIT_AUTOMAKE(PACKAGE, VERSION)
　　 这个宏是 必须的 ,它描述了我们将要生成的 软件包的 名字及其版本号：PACKAGE是软件包
的名字,VERSION是 版本号.当你使用make dist命令时,它会给你生成一个类似
helloworld-1.0.tar.gz的 软件发行包,其中就有对应的 软件包的 名字和版本号.
AC_PROG_CC
　　这个宏将检查系统所用的 C编译器.
AC_OUTPUT(FILE)
　　这个宏是 我们要输出的 Makefile的 名字.
　　我们在 使用automake时,实际上还需要用到其他的 一些宏,但我们可以用aclocal 来帮
我们自动产生.执行aclocal后我们会得到aclocal.m4文件.
　　产生了configure.in和aclocal.m4 两个宏文件后,我们就可以使用autocon
f来产生configure文件了.
5. Makefile.am
　　Makefile.am是 用来生成Makefile.in的 ,需要你手工书写.Makefile.
am中定义了一些内容：
AUTOMAKE_OPTIONS
　　这个是 automake的 选项.在 执行automake时,它会检查目录下是 否存在 标准
GNU软件包中应具备的各种文件,例如AUTHORS.ChangeLog.NEWS等文件.
我们将其设置成foreign时,automake会改用一般软件包的 标准来检查.
bin_PROGRAMS
　　这个是 指定我们所要产生的 可执行文件的 文件名.如果你要产生多个可执行文件,
那么在各个名字间用空格隔开.
helloworld_SOURCES
　　这个是 指定产生"helloworld"时所需要的 源代码.如果它用到了多个源文件,
那么请使用空格符号将它们隔开.比如需要helloworld.h,helloworld.c那么请写成:
helloworld_SOURCES= helloworld.h helloworld.c.
　　如果你在 bin_PROGRAMS定义了多个可执行文件,则对应每个可执行文件都要定义相对的
filename_SOURCES.
6. automake
　　我们使用automake --add-missing来产生Makefile.in.
　　选项--add-missing的 定义是 "add missing standard files
 to package",它会让automake加入一个标准的 软件包所必须的 一些文件.
　　我们用automake产生出来的 Makefile.in文件是 符合GNU Makefile惯例
的 ,接下来我们只要执行configure这个shell 脚本就可以产生合适的 Makefile 文
件了.
7. Makefile
　　在 符合GNU Makefiel惯例的 Makefile中,包含了一些基本的 预先定义的 操作：
make
　　根据Makefile编译源代码,连接,生成目标文件,可执行文件.
make clean
　　清除上次的 make命令所产生的 object文件（后缀为".o"的 文件）及可执行文件.
make install
　　将编译成功的 可执行文件安装到系统目录中,一般为/usr/local/bin目录.
make dist
　　产生发布软件包文件（即distribution package）.这个命令将会将可执行文件及相关
文件打包成一个tar.gz压缩的 文件用来作为发布软件的 软件包.
　　它会在 当前目录下生成一个名字类似"PACKAGE-VERSION.tar.gz"的 文件.PA
CKAGE和VERSION,是 我们在 configure.in中定义的 AM_INIT_AUTOM
AKE(PACKAGE, VERSION).
make distcheck
　　生成发布软件包并对其进行测试检查,以确定发布包的正确性.
```