UICollectionView使用

> [NSCollectionViewFlowLayout 官方文档](https://developer.apple.com/documentation/appkit/nscollectionviewflowlayout?language=objc)
> 
>[官网介绍 UICollectionView](https://developer.apple.com/documentation/uikit/uicollectionview?language=objc)



## 初始化

```
UICollectionViewFlowLayout *flowLayout = [[UICollectionViewFlowLayout alloc] init];
[flowLayout setScrollDirection:UICollectionViewScrollDirectionVertical];

//设置CollectionView的属性
 self.collectionView = [[UICollectionView alloc] initWithFrame:CGRectMake(0, 220, DeviceSize.width, DeviceSize.height - 220) collectionViewLayout:flowLayout];
 self.collectionView.backgroundColor = Color(238, 238, 238);
 self.collectionView.delegate = self;
 self.collectionView.dataSource = self;
 self.collectionView.scrollEnabled = YES;
 [self.view addSubview:self.collectionView];
 //注册Cell
[self.collectionView registerClass:[MedalCell class] forCellWithReuseIdentifier:@"cell"];
    
```

<mark>注意：</mark>

1. 初始化UICollectionView 时 要先设置 flowLayout 否则会报错提示UICollectionView: must be initialized with a non-nil layout parameter

2. UICollectionViewFlowLayoutAutomaticSize 的正确调用方法
   `layout.estimatedItemSize = UICollectionViewFlowLayoutAutomaticSize`

## UICollectionView的Delegate和DataSource

```
#pragma mark  设置CollectionView的组数
- (NSInteger)numberOfSectionsInCollectionView:(UICollectionView *)collectionView
{
    return 1;
}

#pragma mark  设置CollectionView每组所包含的个数
- (NSInteger)collectionView:(UICollectionView *)collectionView numberOfItemsInSection:(NSInteger)section
{
    return self.medals.count;
    
}

#pragma mark  设置CollectionCell的内容
- (UICollectionViewCell *)collectionView:(UICollectionView *)collectionView cellForItemAtIndexPath:(NSIndexPath *)indexPath
{
    static NSString *identify = @"cell";
    MedalCell *cell = [collectionView dequeueReusableCellWithReuseIdentifier:identify forIndexPath:indexPath];
    Medal *p = self.medals[indexPath.row];
    cell.medal = p;
    return cell;
}



#pragma mark  定义每个CollectionViewCell的大小
- (CGSize)collectionView:(UICollectionView *)collectionView layout:(UICollectionViewLayout *)collectionViewLayout sizeForItemAtIndexPath:(NSIndexPath *)indexPath
{
    return  CGSizeMake(DeviceSize.width /3,(DeviceSize.width / 3));
}



#pragma mark  定义指定的 section 的 margins
- (UIEdgeInsets)collectionView:(UICollectionView *)collectionView layout:(UICollectionViewLayout *)collectionViewLayout insetForSectionAtIndex:(NSInteger)section
{
    return UIEdgeInsetsMake(0, 0, (self.medals.count / 3 - 2) * DeviceSize.width / 3, 0);//（上、左、下、右）
}


#pragma mark  定义 Cell 之间的横向间距
- (CGFloat)collectionView:(UICollectionView *)collectionView layout:(UICollectionViewLayout *)collectionViewLayout minimumInteritemSpacingForSectionAtIndex:(NSInteger)section
{
    return 0;
}

#pragma mark  定义 Cell 之间纵向间距
- (CGFloat)collectionView:(UICollectionView *)collectionView layout:(UICollectionViewLayout*)collectionViewLayout minimumLineSpacingForSectionAtIndex:(NSInteger)section
{
    return 0;
}

#pragma mark  点击CollectionView触发事件
-(void)collectionView:(UICollectionView *)collectionView didSelectItemAtIndexPath:(NSIndexPath *)indexPath
{
    Medal *p = self.medals[indexPath.item];
    NSLog(@"---------------------");
}

#pragma mark  设置CollectionViewCell是否可以被点击
- (BOOL)collectionView:(UICollectionView *)collectionView shouldSelectItemAtIndexPath:(NSIndexPath *)indexPath
{
    return YES;
}

```
## UICollectionViewDelegateFlowLayout

Asks the delegate for the size of the header view in the specified section.
（设置header view 需要先通过此代理 设置Size 才有效）

```
- (CGSize)collectionView:(UICollectionView *)collectionView 
                  layout:(UICollectionViewLayout *)collectionViewLayout 
referenceSizeForHeaderInSection:(NSInteger)section;
```

### 相关文件推荐
***

[网格视图 UICollectionView](https://itisjoe.gitbooks.io/swiftgo/content/uikit/uicollectionview.html)
文章相关内容：

> 1. 一開始需要先設置UICollectionViewFlowLayout，用來自定義呈現的樣式，再交給建立 UICollectionView 元件時的函式使用。
2. 接著建立 UICollectionView 元件，除了要註冊 cell 之外，如果要自定義每個 section 的 header 或 footer 時，也必須註冊 header 或 footer ，以供後續重複使用。(註冊 cell 原因請參考前節說明)
3. UICollectionView 的 cell 需要自定義一個繼承自 UICollectionViewCell 的類別，用來加上需要的元件，這邊會加上一張圖片( UIImageView )及一行字( UILabel )。
4. 最後要實作委任對象需要的方法。

[SectionIndexTitles for a UICollectionView](https://stackoverflow.com/questions/13882052/sectionindextitles-for-a-uicollectionview)