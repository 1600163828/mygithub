# git操作

## 1.基础篇

###  branck

  ```git
git branch NewImage;//创建名为newImage的分支
  ```

### checkout

```git
git checkout NewImages;//切换到分支NewImage
git checkout -b NewImages //创建新分支且切换到新分支
```

### merge

![image-20200318202833908](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20200318202833908.png)

`master` 现在指向了一个拥有两个父节点的提交记录。假如从 `master` 开始沿着箭头向上看，在到达起点的路上会经过所有的提交记录。这意味着 `master` 包含了对代码库的所有修改。


```git
git merge NewImage//将newimage分支合并到当前分支

```

### rabase

Rebase 实际上就是取出一系列的提交记录，“复制”它们，然后在另外一个地方逐个的放下去。== （同步开发）==

Rebase 的优势就是可以创造更线性的提交历史

```git
git rebase Image//将当前分支rebase到Image上
```




