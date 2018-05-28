---
layout: post
title: 拯救最后一个cell(UICollectionViewCell、UITableViewCell)
date:  2018-04-22 11:36:38 +0800
tags:  iOS开发
---

> 这篇文章主要是尝试找出cell 被遮挡的一些场景、以及引起的原因


### contentInsetAdjustmentBehavior
###### 定义如何适应 ScrollView的contentInset
***

#### 声明：

```	
@property(nonatomic) UIScrollViewContentInsetAdjustmentBehavior contentInsetAdjustmentBehavior API_AVAILABLE(ios(11.0),tvos(11.0));
// ScrollView iOS 11.0 之后的属性 默认值是 UIScrollViewContentInsetAdjustmentAutomatic

```
	

### edgesForExtendedLayout 
*** 

#### 声明：

```
@property(nonatomic,assign) UIRectEdge edgesForExtendedLayout NS_AVAILABLE_IOS(7_0); // Defaults to UIRectEdgeAll
// UIViewController iOS 7.0 之后的属性 默认值是 UIRectEdgeAll
```



#### 属性描述
	
Instead of this property, use the safe area of your view to determine which parts of your interface are occluded by other content. For more information, see the safeAreaLayoutGuide and safeAreaInsets properties of UIView.
	
In iOS 10 and earlier, use this property to report which edges of your view controller extend underneath navigation bars or other system-provided views. The default value of this property is UIRectEdgeAll, and it is recommended that you do not change that value.
	
If you remove an edge value from this property, the system does not lay out your content underneath other bars on that same edge. In addition, the system provides a default background so that translucent bars have an appropriate appearance. The window’s root view controller does not react to this property.
	
iOS 11.0+ 的增加了safeAreaLayoutGuide、safeAreaInsets 属性来指定 view 的那个部分不被遮挡
	
iOS 10和更早的版本 可以通过枚举UIRectEdge 指定 view的哪些edges 在 系统提供的bars（navigation bar，status bar, search bar, navigation bar, toolbar, or tab bar）下面
	
window’s root view controller 不受 这个属性影响

	
#### 注意：
<mark>不合适的界面布局可能会导致 页面内容显示凌乱<mark>

例如（UINavigationController.rootVC -- UISplitViewController -- view controller）

* edgesForExtendedLayout 无效
* 如果 父子控制器同时设置edgesForExtendedLayout = UIRectEdgeNone 会导致 viewController 多减去一个tab bar的高度
* 父子控制器设置其中一个 edgesForExtendedLayout = UIRectEdgeNone 显示正常

<em> 扩展阅读 <em>

> 布局错误原因：
> 
[SVC is expected to be root, with the exception of being placed under a TBC, so no, not allowed as child of a nav controller](https://forums.developer.apple.com/thread/68664#198748)

> [View Controller Catalog for iOS](https://developer.apple.com/library/content/documentation/WindowsViews/Conceptual/ViewControllerCatalog/Chapters/SplitViewControllers.html)

> [human-interface-guidelines](https://developer.apple.com/ios/human-interface-guidelines/views/split-views/)


### automaticallyAdjustsScrollViewInsets
***

#### 声明：

	@property(nonatomic,assign) BOOL automaticallyAdjustsScrollViewInsets API_DEPRECATED("Use UIScrollView's contentInsetAdjustmentBehavior instead", ios(7.0,11.0),tvos(7.0,11.0)); // Defaults to YES
	// UIViewController 的属性 ios(7.0,11.0)  默认 YES
#### 属性描述


The default value of this property is YES, which lets container view controllers know that they should adjust the scroll view insets of this view controller’s view to account for screen areas consumed by a status bar, search bar, navigation bar, toolbar, or tab bar. Set this property to NO if your view controller implementation manages its own scroll view inset adjustments.

如果设置属性为YES viewController 将会 考虑系统的bars 计算scroll view insets 


### extendedLayoutIncludesOpaqueBars
*** 

#### 声明：
	@property(nonatomic, assign) BOOL extendedLayoutIncludesOpaqueBars;
	// UIViewController 的属性 ios(7.0,11.0)  默认 NO
	
#### 属性描述
如果Bars是不透明的，view不会被延伸到Bars，除非extendedLayoutIncludesOpaqueBars = YES;
注意：Bars are translucent by default in iOS 7.0

### 相关推荐
***
[iOS 11.0 下adjustContentInset属性的计算方式](https://www.jianshu.com/p/efbc8619d56b)

代码强制 设置 scrollView contentInset方法：

```
// 设置 scrollView 的contentInset
UIEdgeInsets adjustForTabbarInsets = UIEdgeInsetsMake(0, 0, CGRectGetHeight(self.tabBarController.tabBar.frame), 0);
self.scrollView.contentInset = adjustForTabbarInsets;
self.scrollView.scrollIndicatorInsets = adjustForTabbarInsets;

```