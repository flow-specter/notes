# git

## 常用命令

1. 添加

`git add .`

2. 上传

`git commit -m 'XXX'`

3. push到远程仓库

`git push -u origin master`或者`git push -u origin main`



## ignoring files

https://docs.github.com/en/free-pro-team@latest/github/using-git/ignoring-files

有C++、cmake的模板之类的。

**2020.10.9 14:53:** 有效。

- **语法：**

https://www.jianshu.com/p/ea6341224e89

## vs2019中的git





# 报错及解决

1. src refspec master does not match any. error: failed to push some refs to...

   答: 以为是什么文件为空之类的问题，实际上是`master`已经不叫``master`了，叫`main`了。。。改名了，所以在`push`的时候，应该是：

   `git push -u main`而不是`git push -u master`。
   
2. fatal: refusing to merge unrelated histories
   `git pull origin master --allow-unrelated-histories`