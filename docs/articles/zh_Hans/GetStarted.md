# 快速入门

HitRefresh.MobileSuit 是一个强大的工具，可以快速构建 .NET Core 控制台应用程序。

在本文中，我将介绍如何构建一个基本的 MobileSuit 应用程序。

## 创建项目

首先，在你的 IDE 中创建一个新的应用程序。

然后，通过 NuGet 向项目添加[HitRefresh.MobileSuit](https://www.nuget.org/packages/HitRefresh.MobileSuit/) 。

## 编写 MobileSuit 客户端类

### 创建类

向项目添加一个名为*** QuickStartClient*** 的类。它继承自类 ***HitRefresh.MobileSuit.ObjectModel.SuitClient***。

### 为类添加自定义标记

使用参数 "Demo" 添加 *HitRefresh.MobileSuit.SuitInfoAttribute*。

### 添加第一条指令

向类 ***Client*** 添加一个名为 ***Hello*** 的方法。它没有参数，也没有返回值。

方法的内容可以是任意的，你可以使用 *IO.WriteLine* 和 *IO.ReadLine* 代替 *Console.WriteLine* 和 *Console.ReadLine*。

### 向第一条指令添加说明和别名

向方法添加以下自定义标记：

1. 使用参数 "hello command." 添加 _HitRefresh.MobileSuit.SuitInfoAttribute_。
2. 使用参数 "H" 添加 _HitRefresh.MobileSuit.SuitAliasAttribute_。

### 添加另一条指令

向类 ***Client*** 添加一个名为 ***Bye*** 的方法。它有一个字符串参数，名为 *name*。它返回一个 *string*。

方法的内容可以是任意的，你可以使用 _IO.WriteLine_ 和 _IO.ReadLin_ 代替 *Console.WriteLine* 和 *Console.ReadLine*。

### 此外

如果你不希望某些公共方法出现在 Mobile Suit 中，为其添加 ***SuitIgnore*** 属性。

## 修改应用程序的主方法

在主方法中

``` csharp
public static void Main(String[] args){
    ...
}
```

添加以下代码：

``` csharp
Suit.GetBuilder().Build<QuickStartClient>().Run();
```

## 检查 QuickStartClient.cs 的代码

它可能如下所示：

``` csharp
using HitRefresh.MobileSuit;
using HitRefresh.MobileSuit.ObjectModel;

namespace HitRefresh.MobileSuitDemo
{
    [SuitInfo("Demo")]
    public class QuickStartClient : SuitClient
    {

        [SuitAlias("H")]
        [SuitInfo("hello command.")]
        public void Hello()
        {
            IO.WriteLine("Hello! MobileSuit!");
        }



        public string Bye(string name)
        {
            IO.WriteLine($"Bye! {name}");
            return "bye";
        }
    }
}


```

## 运行并测试你的应用程序

构建并运行你的应用程序。

在控制台中，你可以输入：

1. **Help** 查看 **MobileSuit** 的帮助

2. **List** 或 **ls** 查看当前客户端可用的所有指令

3. **Hello** 或 **h** 运行 *QuickStartClient.Hello()**

4. ***Bye** ***name*** 运行 *QuickStartClient.Bye(* ***name*** *)**

5. ***Exit** 退出程序

Mobile Suit 中的命令可以在多行中输入，当行的最后一个字符是 *%* 时。
可以在行格式 "^\s*#" 中添加注释。

例如：

```text
 #comment
he%
llo
```

等价于

```text
hello
```

构建这样一个应用程序的过程非常简单，你只需要编写一个类。

要让你的应用程序接受 string[] args，参见 [创建命令行应用程序](./CreateCommandLineApplication.md)