## Git操做

###远程拉取项目

> http

```
//https最后不需要加.git
git clone http://61.174.54.96:12389/project/obdmanagerv2.git
```

> ssh

```
git clone git@xx.xx.xx.xx:/project/obdmanagerv2.git
```

###推送到远程仓库

```
git add .
git commit -m "***"
git push -u origin master //第一次推送
git push origin master //之后的推送
```

### 拉取更新后的项目

```
git pull
```

### git回滚分支

```
git reset --hard 分支id(不需要写全)
```

###[Git创建gitignore文件](https://www.jianshu.com/p/5eb38611b706)

> 点击链接