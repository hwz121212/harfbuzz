GNU libiconv-1.15和libintl-0.19.8.1，VS2017工程和 Makefile.mak 命令行编译文件

CSDN-tags： libiconv1.15 libintl 0.19.8.1 VS2017 SDK17134.12

声明：

最新版，修正了relocatable.c文件中GetModuleFileName函数的问题。在ANSI下，等同于：GetModuleFileNameA；Unicode下等同于：GetModuleFileNameW，如果你的程序出错，请检查。

代码为本人良心制作，虽然花费了一定的时间和精力，但不保证完全没有错误。如果您下载并使用了本代码，将其包含在您发布的应用中，给您带来了经济上，心理上，生活上的损失，本人不负有责任。

所有代码都基于官网进行修改，iconv的代码来源于libiconv-1.15的lib目录，intl的代码来源于gettext-runtime的intl目录。

intl需要iconv的支持，如果想单独编译不需要iconv的intl，
请自行修改intl目录下的config.h文件，

/* Define if you have the iconv() function and it works. */
#define HAVE_ICONV 1

/* Define to 1 if you have the <iconv.h> header file. */
#define HAVE_ICONV_H 1

为：

/* Define if you have the iconv() function and it works. */
/* #undef HAVE_ICONV */

/* Define to 1 if you have the <iconv.h> header file. */
/* #undef HAVE_ICONV_H */

并修改VS工程中预处理器定义，删掉/DDEPENDS_ON_LIBICONV=1

VS的工程为VS2017的工程文件，使用VC141工具集，SDK10.0.17134.12，如果没有2017，也可以用Makefile.mak文件来编译。
或者你自己降低版本，我最初使用的最低版本是VC140_xp，SDK8.1，也就是VS2015默认安装的兼容xp工具集，VS2015以下版本未测试。

nmake /f Makefile.mak [DLL<=1>] [DEBUG<=1>]

指定 DLL=1   编译dll版本，默认是lib版本，libiconv.lib , libintl.lib。
指定 DEBUG=1 编译debug版本，默认是release版本。

同理，如果intl不需要iconv，请修改上面的配置文件选项，并，
删掉Makefile.mak中/DDEPENDS_ON_LIBICONV=1

配置文件的制作，参考了以下几处，修改的大概原则是，能定义的全定义了，就这样：

https://github.com/kahrl/gettext-msvc
这个地址提供了libiconv和libintl的VS工程和配置文件。

https://github.com/winlibs
为编译PHP而修改的libiconv和libintl源码。

附带的Cygwin目录中的工具
libiconv官方的制作文档，用cygwin配合VC，生成的配置文件。

一大堆的宏和函数搞得我头晕脑涨。所以配置文件如果有错误，也在所难免，所有修改的文件，如config.h，iconv.h,libintl.h都附带了原始文件。

如:

配置文件       原始文件      DLL原始文件               LIB原始文件
config.h       config.h.in
iconv.h                      iconv.h.build.in          iconv.h.in
localcharset.h               localcharset.h.build.in   localcharset.h.in

libintl.h   libgnuintl.in.h

欢迎同学们下载测试。有问题可以给我发邮件travel981cn@139.com
