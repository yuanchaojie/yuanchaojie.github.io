### UISplitViewController

相关文章记录：
***

[在 iPhone 6+使用UISplitViewController 图文简单讲解](http://nshipster.cn/uisplitviewcontroller/)
文章内容:

1. 视频呈现效果
2. displayModeButtonItem的作用
3. collapseSecondaryViewController 代理方法的使用
`
func splitViewController(splitViewController: UISplitViewController, collapseSecondaryViewController secondaryViewController: UIViewController!, ontoPrimaryViewController primaryViewController: UIViewController!) -> Bool {
        return collapseDetailViewController
    }
`

[UISplitViewController 官方说明文档](https://developer.apple.com/documentation/uikit/uisplitviewcontroller?language=objc)文章内容:

关于UISplitViewController的用法、使用场景、展现模式、以及相关API

[Change the Width of Master View in Split View Controller](https://useyourloaf.com/blog/change-the-width-of-master-view-in-split-view-controller/)
文中有实例代码 WorldFacts
