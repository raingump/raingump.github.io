---
title: SF Symbols
date: 2022-08-21 23:09:45
tags:
---

# SF Symbols

## 1. 什么是 SF Symbols

SF Symbols 拥有超过 3,300 个符号，是一个图标库，旨在与 Apple 平台的系统字体 San Francisco 无缝集成。符号有九种重量和三种比例，并自动与文本标签对齐。它们可以在矢量图形编辑工具中导出和编辑，以创建具有共享设计特征和辅助功能的自定义符号。SF Symbols 3 具有 600 多个新符号、增强的颜色自定义、新的检查器以及对自定义符号的改进支持。

<!--more-->

## 2. 为什么要有 SF Symbols？

<img src="https://raingump-image-bucket.oss-cn-shenzhen.aliyuncs.com/iShot_2022-05-16_14.56.42.png" alt="iShot_2022-05-16_14.56.42" style="zoom:50%;" />

如上图，一般 APP 从视觉元素上可以简单分为三大类：

- 图片
- UI 元素
- 文字

可以看到 UI 元素是占据了相当大的一部分展示比重的，起到了引导、展示和交互等重要作用。

而在 SF Symbols 诞生以前，当 APP 进入到设计阶段，通常视觉设计师主导以及产品经理协助，共同来完成对 UI 元素的设计，这可能会带来几个问题：

1. 当 APP 受众足够广，APP 用户覆盖了不同的国籍、种族、年龄或文化时，会给 UI 元素的设计带来很大挑战，因为 APP 使用者的习惯很可能相差很大，没有足够通用的设计语言，很多用户在使用的时候可能会感到困惑
2. 承载 APP 的系统发生了变化，而 APP 的 UI 元素设计没有，比如：iOS 13 的深色模式新特性，UI 元素也应该有两套
3. UI 元素可能会给开发带来不便，当使用传统的 UI 元素混排文字的时候，开发可能需要手动计算 UI 元素的大小，来进行与文字的底线或者底端对齐
4. UI 元素可能无法做到与字体相协调，比如：在同一页面，字体如果同时存在细体和粗体的情况，后面如果跟着相同的 UI 元素，就会显得不太协调
5. 常规的图片导入，会因为缩放而失去清晰度

……



所以，SF Symbols 诞生了，完美的解决了上述的问题：

1. SF Symbols 3 为特定语言和书写系统提供了许多变体，包括拉丁语、阿拉伯语、希伯来语、印地语、泰语、中文、日语和韩语。当设备语言发生变化时，特定于语言和脚本的变体会自动适应，如下图。

   <img src="https://raingump-image-bucket.oss-cn-shenzhen.aliyuncs.com/localized_2x.png" alt="localized_2x" style="zoom:50%;" />

2. 自带了浅色、深色模式

3. 在开发的 API 层面上提供了便利

4. 要浏览可用的符号图像，请可以从 [Apple Design Resources](https://developer.apple.com/design/resources/) 下载使用 SF Symbols 应用程序

5. 符号有九种重量和三种比例

6. 可以创建自己的符号，要创建自定义符号，首先导出想要的设计相似的符号，然后使用 Sketch 或 Illustrator 等矢量编辑工具对其进行修改。在您的应用程序中使用结果，就像使用原始符号文件一样

7. 矢量图不会因为缩放而失去清晰度

……



## 3. 如何使用 SF Symbols？

*建议配合附件 [Demo](https://github.com/raingump/SF-Symbols-Demo) 阅读*

初始化一个ImageView，图片的名称可以从上面下载的 SF Symbols 应用程序中查看。

```swift
// 初始化一个 UIImageView，并指定使用 systemName
let imageView = UIImageView.init(image: UIImage(systemName: "thermometer.sun.fill"))
```



根据字体的大小，设定 Image 的大小

```swift
let font = UIFont.systemFont(ofSize: 30)
// 根据 font 设定
let image = UIImage(systemName: "thermometer.sun.fill")?.applyingSymbolConfiguration(.init(font: font))
```



根据磅数的大小，设定 Image 的大小

```swift
// 设定磅数
imageView.preferredSymbolConfiguration = UIImage.SymbolConfiguration(weight: .regular)
```



根据比例的大小，设定 Image 的大小

```swift
// 设定比例
imageView.preferredSymbolConfiguration = UIImage.SymbolConfiguration(scale: .medium)
```



已经设定了 UIImage.SymbolConfiguration 的情况下，更新 config，然后重新作用在图片上

```swift
var config = imageView.preferredSymbolConfiguration
let weight: UIImage.SymbolWeight = UIImage.SymbolWeight(rawValue: value) ?? .medium

// 修改磅数
config = config?.applying(UIImage.SymbolConfiguration.init(weight: weight))
imageView.preferredSymbolConfiguration = config

```

如 Demo 截图所示，左图是 `utralLight`，右图是 `black`：

<img src="https://raingump-image-bucket.oss-cn-shenzhen.aliyuncs.com/IMG_2964.JPEG" alt="IMG_2964" style="zoom: 25%;" />



设定 SF Symbol 的 Image 颜色样式

```swift
// 默认单色
let imageView1 = createImageView(config: UIImage.SymbolConfiguration(weight: .ultraLight))

// 分层
let imageView2 = createImageView(config: UIImage.SymbolConfiguration.init(hierarchicalColor: .systemBlue).applying(UIImage.SymbolConfiguration(weight: .light)))

// 调色盘
let imageView3 = createImageView(config: UIImage.SymbolConfiguration.init(paletteColors: [.systemTeal, .red, .brown]).applying(UIImage.SymbolConfiguration(weight: .black)))

// 默认多色
let imageView4 = createImageView(config: UIImage.SymbolConfiguration.preferringMulticolor().applying(UIImage.SymbolConfiguration(weight: .black)))

```

单张图片色彩修改如 Demo 截图所示：

<img src="https://raingump-image-bucket.oss-cn-shenzhen.aliyuncs.com/Simulator Screen Shot - iPhone 13 - 2022-08-02 at 19.04.10.png" alt="Simulator Screen Shot - iPhone 13 - 2022-08-02 at 19.04.10" style="zoom: 25%;" />



修改本地化语言之后，不需要修改代码，即可支持本地化 SF Symbols：

<img src="https://raingump-image-bucket.oss-cn-shenzhen.aliyuncs.com/IMG_2965.JPEG" alt="IMG_2965" style="zoom: 25%;" />





**SF Symbols 那么强大，那所有机型都支持吗？**

- iOS 13 及更高版本
- watchOS 6 及更高版本
- macOS 11 及更高版本
- tvOS 13 及更高版本

很遗憾并不是的。SF Symbols 只支持 iOS 13 以上的机型，那么 iOS 13 以下的机型如何使用呢？可以使用 SF Symbols 应用程序导出图标的 SVG 版本，然后使用一些图形工具将它们转换为可以导入工程的 PNG 图标。



## 4. 总结

SF Symbols 4 已经在 beta 阶段，使用 SF Symbols 可以最大程度的获得苹果的最新特性支持，无论是匹配文本控件、深浅色模式显示效果、本地化支持、包体缩减和Swift UI支持等方面都有显著获益。



Demo地址：https://github.com/raingump/SF-Symbols-Demo
