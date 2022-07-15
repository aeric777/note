# git

> 2021.11.22

---
## git initial
``` bash
# Initial a repository & connect to github.com
$ echo "# [repo_name]" >> README.md
$ git init
$ git add -all
$ git commit -m "first commit"
$ git branch -M main
$ git remote add origin git@github.com:[user_name]/[repo_name].git
$ git push -u origin main
```


## push a existing repo to github
``` bash
$ git remote add origin git@github.com:[user_name]/[repo_name].git
$ git branch -M main
$ git push -u origin main
```

## Configuration
``` bash
$ git config --global --list    # check your global configuation
```


## remote_repo
``` bash
# 可以使用ssh或https管理远程仓库
# 由于无记忆性，使用https需要每次输入密码(不推荐)
$ git remote -vv    # check status of remote repo


# change branch name
$ git branch -m [old name] [new name]
$ git fetch origin
$ git branch -u [remote]/[remote.branch] [local.branch]
#     -u, --set-upstream-to <upstream>
# change the upstream info
```


## 远程删除分支后在本地依然存在的问题
``` bash
$ git fetch -prune          # method-1
$ git remote prune origin   # method-2
```


## Removing sensitive data from a repository
    see [this page](https://docs.github.com/en/github/authenticating-to-github/removing-sensitive-data-from-a-repository) for more details.


## Forking workflow
> 参见 [Forking](https://github.com/oldratlee/translations/blob/master/git-workflows-and-tutorials/workflow-forking.md#%E9%A1%B9%E7%9B%AE%E7%BB%B4%E6%8A%A4%E8%80%85%E9%9B%86%E6%88%90%E5%BC%80%E5%8F%91%E8%80%85%E7%9A%84%E5%8A%9F%E8%83%BD)

## Pull Request workflow
> 参见 [Pull Request](https://github.com/oldratlee/translations/blob/master/git-workflows-and-tutorials/pull-request.md)