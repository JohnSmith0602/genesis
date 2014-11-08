title: 學會使用$PATH
date: 2014-11-08 01:34:02
tags:

categories:
- 計算機

---

源文：[The $PATH to Enlightenment](http://alistapart.com/article/the-path-to-enlightenment)

命令行（The Command Line）在流行文化中被描述成專屬於電腦黑客和極客的神奇工具，但它在現實生活中使用起來並沒有那麼「酷」，只是一些非常簡單的工具集合而已。它出生於1970年代的貝爾實驗室，主要被寄望於完成一些簡單的任務。其實只要掌握了幾個基本概念，就可以玩轉命令行。**路徑**，就是這幾個基本概念中的一個。


####一個重要的變量：$PATH

$PATH，美元符前綴+全大寫字母，表示UNIX中的一個環境變量。$PATH指定了計算機運行可執行文件時的查找/加載路徑。

- 查看所有環境變量的方法：
```bash
$ env
```

- 查看$PATH的值（多個加載路徑間用冒號隔開）：
```bash
$ echo $PATH
/usr/local/heroku/bin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin
```

```bash
$ echo $PATH | tr ':' '\n'
/usr/local/heroku/bin
/usr/local/bin
/usr/bin
/bin
/usr/sbin
/sbin
```

- 修改$PATH值：一次性的話，在命令行中修改；一勞永逸的話，在*~/.bash-profile*文件中修改。
```bash
$ export PATH=Hallo $PATH
```

####多版本的二進制文件

在UNIX中，可執行程序是二進制文件。UNIX中有多個存儲二進制文件的文件夾，在*/etc/paths*中可以查看這些文件夾的地址。由於paths文件中是有序地選擇加載地址，所以文件中的第一個文件夾地址就是加載二進制文件的默認路徑。
```bash
$ cat /etc/paths
/usr/local/bin
/usr/bin
/bin
/usr/sbin
/sbin
```

- 查看二進制文件默認被執行版本的路徑：
```bash
$ which git
/usr/local/bin/git
```

- 查看二進制文件所有版本的路徑（第一個即爲默認被執行版本的路徑）：
```bash
$ which -a git
/usr/local/bin/git
/usr/bin/git
```

####修改路徑

當存在同一個可執行程序的多個版本時，我們可以通過修改路徑的方式確定默認執行哪個版本的二進制文件。修改路徑的方式主要有：

- 調整*/etc/paths*中路徑的先後順序。
這個方法雖然可以達到目的，但絕對不要使用。因爲*/etc*文件夾中的配置會影響到整個系統，它不應該被某一個用戶去修改。對它的改動也很可能會導致一些其它的問題。

- 在用戶自己環境下的.bash_profile文件中修改$PATH的值：
```bash
$ sudo vim ~/.bash_profile
export PATH=/user/local/bin:$PATH
```
這樣你就可以按需選擇默認執行的二進制文件的版本。如果你又不再想使用自己安裝的版本，刪掉即可，執行時系統會自動地找到系統提供的版本。

####管理PATH
很多應用會在安裝時修改你的.bash_profile文件。一個臃腫的$PATH配置會造成加載shell的速度變慢，所以你可以定期查看你的$PATH，確認其中的配置都是有意義的；如果有可以優化的地方，通過修改*~/.bash_profile*文件進行修改。

