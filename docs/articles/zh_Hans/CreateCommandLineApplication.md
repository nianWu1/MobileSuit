# 创建命令行应用程序

通常命令行应用程序应接受一个 **string[] args** 参数，并返回一个整数。

我们假设您已经阅读了[快速入门](./GetStarted.md)。

## 添加客户端类

在项目中添加一个名为 ***CliClient*** 的类。它继承自类 ***HitRefresh.MobileSuit.ObjectModel.CommandLineApplication*** 。

然后，覆盖 ***int SuitStartUp(string[] args)*** 。当 args.Length>0 且 args 作为一个命令无法由 MobileSuit 解析时，将调用此方法。

## 添加成员和属性

就像对待 ***QuickStartClient*** 一样。

## 修改应用程序的主方法

在主方法中

``` csharp
public static int Main(String[] args){
    ...
}
```

在最后一行添加以下代码：

``` csharp
return Suit.GetBuilder().Build<QuickStartClient>().Run(args);
```

## 检查 QuickStartClient.cs 的代码

它可能如下所示：

``` csharp
using HitRefresh.MobileSuit;

namespace HitRefresh.MobileSuitDemo
{
    [SuitInfo("Demo")]
    public class CliClient : MobileSuit.ObjectModel.CommandLineApplication
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
        public override int SuitStartUp(string[] args)
        {
            IO.WriteLine(args[0]);
            return 0;
        }
    }
}



```

## 运行并测试您的应用程序

构建您的应用程序。在终端中运行它，使用类似以下的 shell 命令：

``` shell
demo hello
demo foo
demo bye bar
```

看看会发生什么！