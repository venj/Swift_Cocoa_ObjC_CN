# 迁移到Swift

## 把你的Objective-C代码迁移到Swift

*迁移*为你提供了一个重新回顾Objective-C应用的机会，让你可以用Swift一点点地替换应用的各部分，从而改进架构、业务逻辑和性能。直接、增量式的迁移一个应用的方法就是使用前面学到的技术--互操作性和混合编程。混合编程功能能让你自由选择哪些功能和特性用Swift来实现，哪些部分依然使用Objective-C。而互操作性则能使这些新特性无缝整合回Objective-C代码。使用这两种技术来探索Swift的强大性能，并把它应用到你的Objective-C应用中，而无需用Swift完全重写整个应用。

### 让Objective-C代码为迁移做好准备

在你开始迁移你的代码之前，需要确保你的Objective-C代码能与Swift代码有良好的兼容性。这意味着你需要清理你的Objective-C代码，并把它现代化。你的现存代码需要遵循现代的编码实践，使之能方便地与Swift无缝交互。在开始迁移之前，请先参阅“Adopting Modern Objective-C”文档，快速查看这些编码实践。

### 迁移过程

最有效的把代码迁移至Swift的方法是逐文件替换--也就是每次替换一个类。因为你不能在Objective-C中继承Swift的类，因此最好先从应用中选择一个没有任何子类的类开始迁移。你需要用一个`.swift`文件替代类的`.h`和`.m`文件。类的接口和实现都直接保存在单个Swift文件中。你不需要创建头文件；Xcode会在你需要参考的时候为你自动生成头文件。

#### 开始之前

- ✓ 通过菜单和对话框：File > New > File > (iOS, watchOS, tvOS, 或OS X) > Source > Swift 为对应的Objective-C的`.m`和`.h`文件创建一个Swift类。你可以使用与Objective-C类同样的名字，或使用一个不同的名字。类的前缀在Swift中是可选的。
- ✓ 导入合适的系统框架。
- ✓ 如果你需要在同一个编译目标下的Swift文件中访问Objective-C代码，请在桥接头文件中进行头文件导入。你可以参阅[从同一个应用编译目标中导入代码](./3_混合编程.markdown#从同一个应用编译目标中导入代码)部分获取相关指导。
- ✓ 要让你的Swift类在Objective-C中可用，请让它继承自某个Objective-C类。把类用`@objc(<#name#>)`标记，让这个类在Objective-C使用时用一个特定的名字，其中`<#name#>`是Objective-C代码访问Swift类时使用的名字。要了解更多关于`@objc`的信息，请参阅[Swift类型的兼容性](./2_互操作性.markdown#swift类型的兼容性)部分。

#### 迁移过程中

- ✓ 通过让你的Swift类派生自Objective-C的类，或遵守Objective-C的协议等方式，使之具备Objective-C的行为。要了解更多信息，请参阅[编写具备Objective-C行为的Swift类](./2_互操作性.markdown#编写具备objective-c行为的swift类)。
- ✓ 当你使用Objective-C的API时，你需要了解Swift如何转译Objective-C的语言特性。要了解更多信息，请参阅[与Objective-C API交互](./2_互操作性.markdown#与objective-c-api交互)。
- ✓ 当你编写使用Cocoa框架的Swift代码时，请记住某些类型是被桥接的，这意味着你可以在某些使用Objective-C类型的地方用相应的Swift类型代替。要了解更多信息，请参阅[使用Cocoa数据类型](./2_互操作性.markdown#使用cocoa数据类型)。
- ✓ 在你把Cocoa设计模式应用到Swift代码中的时候，请参考[使用Cocoa设计模式](./2_互操作性.markdown#使用cocoa设计模式)，了解关于如何转译常见的设计模式的信息。
- ✓ 要了解把Objective-C的属性转译到Swift中的注意事项，请阅读“Swift编程语言（Swift 2.1版）”的“属性”章节。
- ✓ 使用`@objc(<#name#>)`注解可以在需要的时候，为属性和方法向Objective-C暴露特殊的名字。例如，你可以把一个名为`enabled`的属性，暴露给Objective-C时使用名为`isEnabled`的访问方法，你可以这样写：

``` swift
var enabled: Bool {
	@objc(isEnabled) get {
		//...
	}
}
```

- ✓ Objective-C用（`-`）标记实例方法，用（`+`）标记类方法，在Swift中分别用`func`和和`class func`表示。
- ✓ 把简单的宏声明为全局常量，把复杂的宏改为用函数实现。

#### 收尾工作

- ✓ 参考[从同一个应用编译目标中导入代码](./3_混合编程.markdown#从同一个应用编译目标中导入代码)中的描述，更新Objective-C代码中的导入语句（改为#import "ProductModuleName-Swift.h"）。
- ✓ 从编译目标中取消选择原来的Objective-C的`.m`文件的复选框，把它从编译目标中移除。不要立刻删除`.m`和`.h`文件；你可能需要用它们来进行问题诊断。
- ✓ 如果你的Swift类使用了一个不同的类名，你需要更新你的代码，用Swift的类名替换Objective-C的类名。

### 问题诊断和注意事项

尽管每一个迁移过程都会因为你的已有代码的不同而不同，不过还是有一些通用的步骤和工具能帮助你在迁移代码的过程中进行问题诊断：

- 请记住，你不能在Objective-C中创建Swift类的子类。因此，在你的应用中，不能包含你要迁移的类的Objective-C子类。
- 一旦你把一个类迁移到了Swift，你必须把相应的`.m`文件从编译目标中移除，以避免在编译时产生重复的符号错误。
- Swift类要在Objective-C中访问和使用，这个类必须派生自Objective-C的类，或使用了`@objc`标记。
- 当你把Swift代码用于Objective-C中时，请记住Objective-C不能转译某些Swift特有的特性。要了解哪些特性不可用，请参考[在Swift中使用Objective-C](./3_混合编程.markdown#在swift中使用objective-c)。
- Command-点击一个Swift类名，可以查看它的生成的头文件（generated header）。
- Option-点击一个符号，可以查看它的基本信息，例如，类型、参数以及文档注释。

[< 3. 混合编程](./3_混合编程.markdown) | [目录](./0_目录.markdown)