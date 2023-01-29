# github使用

## github 上传

```
1.初始化文件夹
git init
2.设置远端地址
git remot add origin https://github.com/JfyhDcm/PaperReading.git
3.将文件保存在本地分支上
git add .
4.查看信息
git status
5.查看远端信息
git remote -v
6.配置config
git config --global user.name "JfyhDcm"
git config --global user.email "wei836439982@sina.com"
7.为当前branch添加commit
git commit -m "this is your commit"
8.git推送远端
git pull origin master


9.git同步到本地
	相当于两步操作，第一步先将远端同步到本地的远端副本，再将副本同步到本地分支
9.1 git fetch orgin master
git branch 查看当前所在分支
* master
9.2 git merge orgin/master

```



