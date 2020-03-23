# git操作

## 1.基础篇

###  branck

  ```git
git branch NewImage;//创建名为newImage的分支
  ```

------

### checkout

```git
git checkout NewImages;//切换到分支NewImage
git checkout -b NewImages //创建新分支且切换到新分支
```

------

### merge

![image-20200318202833908](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20200318202833908.png)

`master` 现在指向了一个拥有两个父节点的提交记录。假如从 `master` 开始沿着箭头向上看，在到达起点的路上会经过所有的提交记录。这意味着 `master` 包含了对代码库的所有修改。


```git
git merge NewImage//将newimage分支合并到当前分支

```

------

### rabase

Rebase 实际上就是取出一系列的提交记录，“复制”它们，然后在另外一个地方逐个的放下去。== （同步开发）==

Rebase 的优势就是可以创造更线性的提交历史

```git
git rebase Image//将当前分支rebase到Image上
```

------

## 2.高级篇

### 分离HEAD

```git
git checkout 分支名
```


 HEAD 是一个对当前检出记录的符号引用 —— 也就是指向你正在其基础上进行工作的提交记录。

HEAD 总是指向当前分支上最近一次==提交记录==。	

分离的 HEAD 就是让其指向了某个具体的提交记录而不是分支名。在命令执行之前的状态如下所示：

HEAD -> master -> C1

HEAD 指向 master， master 指向 C1

------

### 相对引用（log。。。。）

```git
git log //查看提交记录
```

通过哈希值指定提交记录很不方便，所以Git引入了**相对引用**。

有两个简单用法

- 使用 `^`向上移动1个提交记录
- 使用 `~<num>` 向上移动多个提交记录，如 ~3

```git
git checkout 分支名^    //向上移动一个提交记录
```

------

### 强制修改分支位置

可以直接使用 `-f` 选项让分支指向另一个提交。

```git
git branch -f master HEAD^3  //会将 master 分支强制指向 HEAD 的第 3 级父提交。
```

------

### 撤销变更（reset，revert）

~~~

~~~

1. git reset

   ​		`git reset` 通过把分支记录回退几个提交记录来实现撤销改动。你可以将这想象成“改写历史”。`git reset` 向上移动分支，原来指向的提交记录就跟从来没有提交过一样。***对远程无效***

   ```GIT
   git reset HEAD~1  //向上移动一个记录
   ```

   

2. git revert

   ​		虽然在你的本地分支中使用 `git reset` 很方便，但是这种“改写历史”的方法对大家一起使用的远程分支是无效的哦！

   为了撤销更改并分享给别人，我们需要使用 `git revert`。

   ```git
   git revert HEAD  //向上移动一个记录
   ```

   ## 3. 自由修改提交树

   ### Git Cherry-pick

   将一些提交复制到当前所在的位置（`HEAD`）下面的话， Cherry-pick 是最直接的方式了。

   ```git
   git cherry-pick <提交号>...
   ```

   

   eg: 

   ```git
   git cherry-pick c2 c3 c4    //将c2 c3 c4复制到当前位置下
   ```

   -------

   ### 交互式 rebase

   当你知道你所需要的提交记录（并且还知道这些提交记录的哈希值）时, 用 cherry-pick 再好不过了 —— 没有比这更简单的方式了。

   但是如果你不清楚你想要的提交记录的哈希值呢? 幸好 Git 帮你想到了这一点, 我们可以利用交互式的 rebase —— 如果你想从一系列的提交记录中找到想要的记录, 这就是最好的方法了

   

   

   交互式 rebase 指的是使用带参数 `--interactive` 的 rebase 命令, 简写为 `-i`

   如果你在命令后增加了这个选项, Git 会打开一个 UI 界面并列出将要被复制到目标分支的备选提交记录，它还会显示每个提交记录的哈希值和提交说明，提交说明有助于你理解这个提交进行了哪些更改。

   在实际使用时，所谓的 UI 窗口一般会在文本编辑器 —— 如 Vim —— 中打开一个文件。 

```git
git rebase -i HEAD~4
```

