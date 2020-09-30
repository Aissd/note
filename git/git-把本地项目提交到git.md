### 移除掉.git文件夹（如果有的话，移除掉会删除之前的操作记录）

### 在git上新建一个仓库，复制仓库的地址

```
cd existing_folder
git init
git remote add origin https://github.com/Aissd/lunzi.git // 仓库的地址
git add .
git commit -m "Initial commit"
git pull --rebase origin master // 通过该命令进行代码合并【注：pull=fetch+merge]
git push -u origin master
```
