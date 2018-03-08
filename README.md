# GeoMap 开发规范

文档规定GeoMap开发规范，包括[文件组织](#jump)、程序注释、命名规则、数据类型（包含类）、函数及语句、UI规范、资源规范。

## 一、<span id="jump">文件组织</span> ##
**1. 组织目录**

![](http://192.168.100.118/kodexplorer/index.php?user/public_link&fid=be8c-AtTby5UyHj16HEfJUwFJxLpl64mJI_uFNhqYF3ReeNmnkSbcB2CTepbpxC5WFPsJ_hIZMbBVtrxNRU3ydsNxrpyq-besLCDrrb7is5FtZbxbjgAK_8cHHR51Ub6hO-b9IAkOms6DT6kh9gaFbU979l9Db63tzCM4Uy8Ttdb&file_name=/folder.png)

（1）`data`：数据文件夹，存放系统各种数据文件，包括系统配置数据等；

（2）`debugx64/releasex64`：编译目录文件夹，包含依赖的第三方lib和编译生成的库；该文件夹下包含plugins文件夹，用于存储插件；

（3）`i18n`：国际化文件夹，存放语言包；

（4）`include`：第三方头文件存放文件夹，包括GeoMap输出的公用头文件（qtport的存储在"include\kernel\qt"下，GeoMap其他存储在"include\app"下）；

（5）`kernel`：内核文件夹，随时获取最新的，保持和内核版本一致（注意：获取最新后，需要运行CopyFromKernel.bat批处理文件）；

（6）`resources`：系统资源文件夹，存放图片及图标等资源文件，图片存于"工程名\images"，图标存于"工程名\icons"；

（7）`src`：系统源码文件夹，包含app（主应用程序源码）、qtport（qt和内核交互中间件源码）、plugins（系统各插件源码）；

（8）`tests`：单元测试文件夹，包含app（主应用程序单元测试源码）、qtport（qt和内核交互中间件单元测试源码）、plugins（系统各插件单元测试源码）；

（9）`CopyFromKernel.bat`：增量批拷贝命名文件，用于将kernel文件夹下的获取的最新内核库和头文件拷贝到编译目录下（文件第一行，根据各自环境自行调整）。

**2. 工程创建**：

（1）必须使用QtCreator进行工程文件的创建（创建完成后，可基于VisualStudio2015打开编辑或直接用QtCreator编辑均可，须保证二者均能编译通过）;

（2）.pro工程文件设置输出和依赖的lib和头文件必须和组织目录中要求的文件夹内容保持一致；

（3）.pro工程文件目录必须是相对目录，且多级目录必须用“/”。

**3. 文件规范**：

（1）所有的文件命名必须小写,比如gsapp.h;

（2）每个.h头文件，必须加#define进行保护，命名格式:<FILE>_H_，比如：

``` C++
#ifndef GSAPP_H
#define GSAPP_H
... 
#endif // GSAPP_H
```
（3）代码文件(.h，.cpp)的存储格式都采用UTF8的签名模式。

## 二、程序注释 ##

（1）所有的文件头、类、枚举、结构体、全局变量、函数必须加注释；

（2）C++标准注释原则：`基于doxygen的C++注释`；

（3）详细注释说明如下：

**文件头**
``` C++
/*!
* \file gsapp.h
* \brief 概述 
* 
*详细概述 
* 
* \author 作者 
* \version 版本号
* \date 日期 
*/
```	
**类注释**
``` C++
/// \brief 类简要说明
class IconManager
```
**函数注释**
``` C++
/// \brief 函数简要说明
/// \param painter 参数1
/// \param option 参数2
/// \return 返回说明
bool paint(QPainter *painter,
		const QStyleOptionGraphicsItem *option);
```
**变量及枚举**
``` C++
int m_a;     ///< 成员变量1m_a说明
double m_b; ///< 成员变量2m_b说明

/// \brief 成员变量m_c简要说明
///
/// 成员变量m_c的详细说明，这里可以对变量进行
///详细的说明和描述，具体方法和函数的标注是一样的
float m_c;

/// \brief xxx枚举变量的简要说明
enum{
    em_1,///< 枚举值1的说明
    em_2,///< 枚举值2的说明
    em_3 ///< 枚举值3的说明
};
```
## 三、命名规则 ##
**1. 通用命名规则**

函数命名、变量命名、文件命名应具有描述性，不要过度缩写，类型和变量应该是名词，函数名可以用“命令性”动词，尽可能给出描述性名称。类型和变量名一般为名词：如dArea;函数名通常是指令性的，如 openFile()。
*文件和类命名均以"qgs"开头，基础框架相关的均以“gs"开头。*

**2. 文件命名规则**

文件名要全部小写，不要使用破折号-、下划线_,如ribboncontrolhook.h;定义类时文件名一般成对出现,如gsapp.h、gsapp.cpp。

**3. 类型命名**

类型命名每个单词以大写字母开头，不包含下划线，所有类型命名——类、结构体、类型定义（typedef）、枚举，均使用相同约定,比如：

``` C++
struct DataStruct
{
    QString strName;
    int     nYear;
    double  dSalary;
    QDate   birthday;
};

typedef QList<DataStruct*> DataStore;

class GsEvent
{
public:
    //Todo
protected:
    //Todo
private:
    LstDataStore m_Data;
	//Todo
	};
```
**4. 变量命名**

变量名一律首字母小写,基础数据类型前面加上缩写，自定义类型不加缩写前缀：strFullFilePath,。
常用变量缩写:

整形 
``` C++
int nErrCnt = 0;
```
浮点型 
``` C++
double dArea = 0;
```
字符型 
``` C++
QString strName;
```
一般指针 
``` C++
T* pData = NULL;
```
智能指针 
``` C++
QSharedPointer<T> spObject;
```
常用容器:
``` C++
QList<QSharedPointer<MyObject>> lstObject;
QVector<int> vecData;
QMap<int, QString> mapKeyMatch;    
QMap<int, QString>::Iterator itBegin = mapKeyMatch.begin();
```
类的成员变量以m_开始：m_MainConfig
全局变量以g_开始：g_Library。

**5. 常量命名**

全局常量和宏命名全部大写，并以下划线 '_' 分隔单词，如：

``` C++
const long GEOCRS_ID = 3344;
```
**6. 函数命名**

函数名以小写字母开头，每个单词首字母大写，没有下划线，如openFile（）。

## 四、数据类型 ##
**1. 常用类型**

常见的操作必须使用Qt自带的类型，如果使用第三方库必须申请，常见的数据类型如下：

``` C++
QChar
QString
QPoint
QSize
QRect
QFont
QTextCodec
QByteArray
QVariant
QDate
QDateTime
QDir
QFile
QFileInfo
QDataStream
QTextStream
QList
QMap
QImage
QIcon
QPixmap
QBitmap
QPicture
QLibrary
QMovie
QPalette
```
**2. 类**

（1）构造函数不处理业务逻辑，尽量简化；

（2）单参数构造函数使用C++关键字explicit；

（3）所有的基类后缀必须以"Base"结尾，比如：

``` C++
class HumanBase
{
public:
    enum humanSex
    {
        enumMan = 0,
        enumWoman,
    };

    HumanBase();
    ~HumanBase();
    void putName(QString strName){m_strName = strName;}
    QString getName(){ return m_strName; }
protected:
    QString m_strName;
    int     m_nYear;
    humanSex enumSex;
};

class Man:public HumanBase
{
    public:
};

class Women:public HumanBase
{
   public:
};
```
（4）数据成员私有化，提供相关的存取函数（set,get)；

（5）在类中使用特定的声明次序：public在protected之前，protected在private之前，成员函数在数据成员（变量）前；

（6）可变静态类的成员名称应该以小写字母 ‘s’ 开头，但常量静态类成员名称应该全部大写：

``` C++
sRefCounter
DEFAULT_QUEUE_SIZE
```
## 五、函数及语句 ##
**1. 函数规则**

（1）定义函数时，参数顺序为：输入参数在前，输出参数在后，比如：

``` C++
void sum(int nInputA, int nInputB, int& nValue);
```
（2）返回类型和函数名在同一行，合适的话，参数也放在同一行；

（3）函数形参表中，所有引用必须是const：

``` C++
void foo(const string &in, string *out); 
```
**2. 语句规则**

（1）推荐只使用Qt中的两种智能指针，QSharedPointer, QScopedPointer,无论是一般指针，还是智能指针，在实际使用前，必须判断是否为空;

>QScopedPointer仅作用在其作用域内，无法作为容器内成员，无法拷贝复制给其它对象。
QSharedPointer则共享同一内存，在所有引用计数置空的时候，才进行真正的对象销毁。原则上，如果对引用计数器不太了解的情况下，不要进行手动的对象清空。

``` C++
//单一作用域时，或者需要保证对象唯一性时，推荐使用QScopedPointer。
void dosomething()
{
	QSharedPointer<MyObject> spObject(new MyObject);
	If(spObject)
		spObject->func();
}
void dosomething(const QSharedPointer<MyObject>& spObject);
//在容器内，或子类继承、多态等，用QSharedPointer
QList<QSharedPointer<MyObject>> lstObject;
	
    QSharedPointer<ParentObject> spBase;
    
//todo
…
    QSharedPointer<ChildObject> spChild(new MyChild);

spBase = static_cast<QSharedPointer< ParentObject > >(spChild);
if(spBase) spBase->dosomething();
```
（2）在任何可以使用的情况下都要使用const。

>在声明的变量或参数前加上关键字const用于指明变量值不可修改（如const int foo），为类中的函数加上const限定表明该函数不会修改类成员变量的状态（如class Foo { int bar(char c) const; };）

（3）Qt信号和槽，使用Qt5中的新样式，避免使用 Qt 自动连接的槽；

（4）将常量放在比较判断语句的前面；

例如，使用
``` C++
0 == value
```
（5）宏文件统一定义，需区分哪些地方使用和内核一致的宏，哪些作为QMAP的宏，比如日志，操作系统定义等等，比如，export宏使用GS_API，内核的宏如下：

```C++
#pragma once
#define UTILITY_NS namespace GeoStar{namespace Utility{
#define UTILITY_ENDNS }}
#define UTILITY_NAME GeoStar::Utility

#define KERNEL_NS namespace GeoStar{namespace Kernel{
#define KERNEL_ENDNS }}
#define KERNEL_NAME GeoStar::Kernel

#define GLOBE_NS namespace GeoStar{namespace Kernel{namespace Globe{
#define GLOBE_ENDNS }}}
#define GLOBE_NAME GeoStar::Kernel::Globe

#define GLOBE_UI_NS namespace GeoStar{namespace Globe{namespace UI{
#define GLOBE_UI_ENDNS }}}
#define GLOBE_UI_NAME GeoStar::Globe::UI

#ifndef GS_API
#if defined(GEOSTAR_DLL)
    #if defined(_WIN32)
        #if GEOSTAR_IMPLEMENTATION
            #define GS_API __declspec(dllexport)
        #else
            #define GS_API __declspec(dllimport)
        #endif
    #else
        #define GS_API __attribute__((visibility("default")))
    #endif
#else
    #define GS_API
#endif
#endif


#ifdef _MSC_VER
#pragma warning(disable : 4018)

#pragma warning(disable : 4100)
#pragma warning(disable : 4101)
#pragma warning(disable : 4189)
#pragma warning(disable : 4192)

#pragma warning(disable : 4238)
#pragma warning(disable : 4239)
#pragma warning(disable : 4244)
#pragma warning(disable : 4245)
#pragma warning(disable : 4251)
#pragma warning(disable : 4267)


#pragma warning(disable : 4305)
#pragma warning(disable : 4311)
#pragma warning(disable : 4389)

#pragma warning(disable : 4482)
#pragma warning(disable : 4635) 
#pragma warning(disable : 4701)

#pragma warning(disable : 4800)
#pragma warning(disable : 4996)

#endif

#include <stdio.h>
#include <memory>


#ifdef _WIN32

#ifdef _WIN64
#define INT3264_MAX _I64_MAX
#else //_WIN64
#define INT3264_MAX INT_MAX
#endif //_WIN64

#else //WIN32
#include "limits.h"
#ifdef _LP64
#define INT3264_MAX LONG_LONG_MAX
#else //_LP64
#define INT3264_MAX INT_MAX
#endif //_LP64
 
#endif
```
（6）不允许引用windows的任何api。

## 六、UI规范 ##
（1）UI均采用.ui后缀，基于QGIS3.0源码，基于QGIS的UI进行修改；

（2）UI的文字控件都使用英文占位（英文都从qgis上找对应的内容，找不到的讨论确认），然后通过国际化的手段翻译成中文；

（3）UI控件及其子控件命名规则，以m开头，以控件类型简称结尾，中间根据控件作用命名，如下：

```C++
<widget class="QMenu" name="mRecentProjectsMenu">
<widget class="QDialog" name="mQgsAboutDialog">
<widget class="QComboBox" name="mTypeBox"/>
<widget class="QLineEdit" name="mNameEdit"/>
<widget class="QRadioButton" name="mTabButton">
<widget class="QGroupBox" name="mAttributesGroupBox">
<widget class="QPushButton" name="mColumnDownPushButton">
<widget class="QTableView" name="mColumnsTableView">
```
## 七、资源规范 ##
（1）所有的图标都是用QGIS相对应的图标;
（2）图片采用png格式。
