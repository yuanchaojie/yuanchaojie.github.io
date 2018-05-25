Tab Bar covers TableView cells 的一些解决方法：

* 设置 scrollView 的contentInset

```
UIEdgeInsets adjustForTabbarInsets = UIEdgeInsetsMake(0, 0, CGRectGetHeight(self.tabBarController.tabBar.frame), 0);
self.scrollView.contentInset = adjustForTabbarInsets;
self.scrollView.scrollIndicatorInsets = adjustForTabbarInsets;

```

通过下面三个属性设置

viewController.edgesForExtendedLayout = UIRectEdgeNone;

automaticallyAdjustsScrollViewInsets

extendedLayoutIncludesOpaqueBars