以下转自：http://derien.me/使用sfntly中的sfnttool-jar提取中文字体/

         对于一个web前端来说，制作一个移动端的H5页面是很简单的，但是对于多样的动画效果、累赘的N多图片以及外部字体的优化问题，就远没有制作那么简单了。这里说一下我对字体文件太大的解决方法。

我们这里使用google的sfntly中的sfnttool.jar对字体文件进行指定文字的提取，以达到字体文件压缩的目的。

先来看一下sfnttool.jar的选项：



java -jar sfnttool.jar -h

Subset [-?|-h|-help] [-b] [-s string] fontfile outfile

Prototype font subsetter

-?,-help        print this help information

-s,-string       String to subset

-b,-bench        Benchmark (run 10000 iterations)

-h,-hints        Strip hints

-w,-woff         Output WOFF format

-e,-eot  Output EOT format

-x,-mtx  Enable Microtype Express compression for EOT format

输入的命令行：

$ java -jar sfnttool.jar -s ‘要进行提取的文案‘ 提取前的文件名.ttf 提取后的文件名.ttf
在使用之前，需要配置的事宜如下：

1.jdk，至少1.6+以上版本，记得配置环境变量；

2.ant，java的build工具，[点此下载](http://ant.apache.org/bindownload.cgi)，下载后解压记得配置到环境变量中，这样在项目的cmd中，直接输入ant即可进行java项目的build；

具体build方案：

在cmd中切换到sfntly代码的java目录，然后输入ant就开始build了。build完成后，sfnttool.jar在项目目录的java\dist\tools\sfnttool文件夹下 。

 

P.S. 只要将要进行文字提取的字体包放在与snfttool.jar文件同级目录下，运行命令行即可在该目录下生成提取后的字体包，简单快捷。

不过，这种方式仅支持使用固定文案的部分，还请各位亲们看好再行实践。

 

这里提供两个版本的下载：

【[sfntly原版（未ant版）](http://pan.baidu.com/s/1mg4GTLm)】

【[sfntly安装版（ant版）](http://pan.baidu.com/s/1eQEw6Ds)】


# What is sfntly?

sfntly is pronounced "esfontlee".

sfntly is a Java and C++ library for using, editing, and creating sfnt container based fonts (e.g. OpenType, TrueType). This library was initially created by Google's Font Team and the C++ port was done by the Chrome team. It has been made open source.

The basic features of sfntly are the reading, editing, and writing of an sfnt container font. Fonts that use an sfnt container include OpenType, TrueType, AAT/GX, and Graphite. sfntly isn't itself a tool that is usable by an end user - it is a library that allows software developers to build tools that manipulate fonts in ways that haven't been easily accessible to most developers. The sfntly library is available in Java with a partial C++ port. However, we have included some font tools that are built on top of sfntly: a font subsetter, font dumper, a font linter, some compression utilities.

The uses of sfntly are really anything that you can think of that involves reading and/or editing fonts. Right now, the Java version is the core library used to power Google's Web Fonts project. There it is used for all font manipulation - to read font data, to pull apart fonts, and to then reassemble them before they are streamed out to a user. Portions of the font that are not needed - specific glyph ranges or features - are stripped using sfntly to minimize the size of the streamed font. The C++ port is used somewhat similarly within Chrome to subset fonts for insertion into a PDF for viewing or printing. Though the features stripped in the font are different in Chrome than in Web Fonts because the end use is different.

Using sfntly you can read and extract any of the tables in a font. The tables are the individual data structures within the font for each of the features and functionality: glyph outlines, character maps, kerning, meta data, etc. If you look over the OpenType and TrueType specs, you will see a number of categories of tables. sfntly currently supports all of the required tables, the TrueType outline tables, bitmap glyph tables, and a couple of the other miscellaneous tables. This level of support provides for many of the needs developers have related to the informational reading of font data. It also covers a lot of the editing needs.

To get started with sfntly: clone the repository and follow the quickstart.txt guide in the Java directory

have fun

Stuart Gill - sfntly Architect and Lead Developer
