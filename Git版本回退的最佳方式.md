Git版本回退的最佳方式
====
使用git开发的过程中，存在误提交的时候怎么办呢？不用慌张，强大的git提供了两种版本回退的方式，可以让你恢复提交之前的内容：

方式一：reset（不推荐）
----
通过reset的方式，把head指针指向之前的某次提交，reset之后，后面的版本就找不到了
![图片](https://img2018.cnblogs.com/blog/1114289/201901/1114289-20190104171721230-1366009529.png)

操作步骤如下：

1.在gitlab上找到要恢复的版本号，如：
<br>
`139dcfaa558e3276b30b6b2e5cbbb9c00bbdca96 `

2.在客户端执行如下命令（执行前，先将本地代码切换到对应分支）
<br>
`git reset --hard 139dcfaa558e3276b30b6b2e5cbbb9c00bbdca96`

3.强制push到对应的远程分支（如提交到develop分支）
<br>
`git push -f -u origin develop`

方式二：revert（推荐）
----
这种方式不会把版本往前回退，而是生成一个新的版本。所以，你只需要让别人更新一下代码就可以了，你之前操作的提交记录也会被保留下来
![图片](https://img2018.cnblogs.com/blog/1114289/201901/1114289-20190104172250618-1810657676.png)

操作步骤如下：

1.找到你误提交之前的版本号，如：
<br>
`139dcfaa558e3276b30b6b2e5cbbb9c00bbdca96 `

2.git revert -n 版本号
<br>
`git revert --n 139dcfaa558e3276b30b6b2e5cbbb9c00bbdca96`

3.提交
<br>
`git commit -m "版本回退"`

4.推送到远程
<br>
`git push <远程主机名> <本地分支名>:<远程分支名>`
<br>
`如：git push origin dev:dev`