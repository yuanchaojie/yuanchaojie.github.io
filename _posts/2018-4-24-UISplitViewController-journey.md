
---
layout: post
title:  "UISplitViewController 使用"
---

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

## bugs

### displayModeButtonItem 

**navigationItem.leftBarButtonItem=splitViewController.displayModeButtonItem不执行**

伪代码 如下：（MyIntentionLibraryController 为 splitViewController 的DetailViewController）


@interface CJCollectionViewController : UICollectionViewController


@interface MyIntentionLibraryController :CJCollectionViewController

@implementation CJCollectionViewController


```

- (instancetype)init{
    return [self initWithObject:nil];
}
- (instancetype)initWithObject:(id)object{
	UICollectionViewFlowLayout* flowLayout = [[UICollectionViewFlowLayout alloc]init];
	flowLayout.itemSize = CGSizeMake(50, 50);
	[flowLayout setScrollDirection:UICollectionViewScrollDirectionVertical];
	self = [super initWithCollectionViewLayout:flowLayout];
	if (self) {
	    self.object = object;
	    self.collectionView.backgroundColor = [UIColor whiteColor];
	}
	return self;
}

@end


```

@implementation MyIntentionLibraryController

```

-(void)viewDidLoad {
    self.navigationItem.leftBarButtonItem =self.splitViewController.displayModeButtonItem;(不起作用、没有展现出displayModeButton)
}
```

问题解决过程：

刚开始不确定 splitViewController 是否支持在UICollectionViewController 设置displayModeButtonItem 于是做了一下尝试

1. 更换继承关系`@interface MyIntentionLibraryController :UIViewController` 设置displayModeButtonItem 有效
2. 更换继承关系`@interface MyIntentionLibraryController : UICollectionViewController ` 设置displayModeButtonItem 有效

在 MyIntentionLibraryController中po self.navigationController 竟然为nil
发现在init方法中 写了这个方法self.collectionView.backgroundColor = [UIColor whiteColor];导致viewDidLoad 提前执行......  
去掉 设置color的方法  displayModeButtonItem 出现了～～













