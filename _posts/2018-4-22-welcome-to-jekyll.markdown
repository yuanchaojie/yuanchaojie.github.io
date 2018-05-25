---
layout: post
title:  "Welcome to Jekyll!"
date:   2018-04-22 11:36:38 +0800

---

## 自定义 jekyll site

* 在配置（_config.yml）文件中 修改title、email、description 等信息

## 安装jekyll-paginate plugin 运行 Bundler install 提示消息如下
> The dependency tzinfo-data (>= 0) will be unused by any of the platforms Bundler is installing for. Bundler is installing for ruby but the dependency is only for x86-mingw32, x86-mswin32, x64-mingw32, java. To add those platforms to the bundle, run `bundle lock --add-platform x86-mingw32 x86-mswin32 x64-mingw32 java`.

首先 这是个警告 不是个错误 可以忽略~
产生警告的原因 Gemfile 包含这个命令

> gem "tzinfo-data", platforms: [:mingw, :mswin, :x64_mingw, :jruby]


消除这条消息的三个方法 [参考这里](https://github.com/tzinfo/tzinfo-data/issues/12)
> If you want to get rid of the message you can do one of the following:
> 
> 1. Remove the platforms option from the gem 'tzinfo-data' line in the Gemfile (and run bundle update). This will cause tzinfo to use tzinfo-data as its data source on all platforms instead of using the system time zone data.
> 
2. Remove the gem 'tzinfo-data' line from the Gemfile. This will cause tzinfo to always try and use the system time zone data. A TZInfo::DataSourceNotFound exception will be raised if you try and run your app on Windows.
3. Run bundle lock --add-platform mingw, mswin, x64_mingw, jruby to add mingw, mswin, x64_mingw, and jruby to the list of platforms Bundler will include in the bundle.

> Each of these options would need to be carried out for each Rails application you create.

## 记录安装错误：

* 翻页功能（Pagination）  只有设置在html 文件中 才有效  [详情](https://jekyllrb.com/docs/pagination/)
* 在jekyll site 上使用评论功能的[方法](https://disqus.com/admin/install/platforms/jekyll/)
* [Liquid 语法介绍](https://shopify.github.io/liquid/basics/introduction/)




#### 以下部分文档jekyll自带的说明部分
***

* 编辑完重启服务器

> You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. You can rebuild the site in many different ways, but the most common way is to run `jekyll serve`, which launches a web server and auto-regenerates your site when a file is updated.


* 自己写的blog需要按照 “YYYY-MM-DD-name-of-post.ext ” 格式放在_posts下

> To add new posts, simply add a file in the `_posts` directory that follows the convention `YYYY-MM-DD-name-of-post.ext` and includes the necessary front matter. Take a look at the source for this post to get an idea about how it works.

Jekyll also offers powerful support for code snippets:


{% highlight ruby %}
def print_hi(name)
  puts "Hi, #{name}"
end
print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
{% endhighlight %}


Check out the [Jekyll docs][jekyll-docs] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll Talk][jekyll-talk].

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/

#### 参考文档：
[GitHubHelp](https://help.github.com/articles/using-jekyll-as-a-static-site-generator-with-github-pages/)
 
[jekyll Configuration](https://jekyllrb.com/docs/configuration/)
 
[GitHub Pages](https://pages.github.com/)