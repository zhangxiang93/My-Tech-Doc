### 问题
```
warning: unable to access '/Users/zx_93/.config/git/attributes': Permission denied
```

### 原因
`config`权限问题
用户所属用户组关系

### 解决
```
 sudo chown -R 用户名:staff ~/.config
 sudo chmod 644 ~/.ssh/config
```
`staff`是组名，只读权限