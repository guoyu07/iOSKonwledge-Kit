### git常见使用

```
http://blog.csdn.net/wirelessqa/article/details/20153689
```

1. git init
2. git add .
3. git commit -am "\#\#\#"      -------以上3步只是本地提交
   4.git remote add origin git@xx.xx.xx.xx:repos/xxx/xxx/xxx.git
   5.git push origin 本地分支:远程分支

fatal: refusing to merge unrelated histories  
解决办法：git pull origin master --allow-unrelated-histories

