# User management

> 2021.11.22

## Related files
- `/etc/passwd`
``` bash
# 用户名:口令(加密后的用户口令):用户标识号:组标识号:注释性描述:主目录:登录Shell
```
- `/etc/shadow`
``` bash
# 对安全性要求较高的Linux系统都把加密后的口令字分离出来，单独存放在`/etc/shadow`文件中.
```

- `/etc/group`
``` bash
# 包含root、admin、sudo、vboxsf等
# 组名:口令:组标识号:组内用户列表
```

## 用户 & 组
在 Linux 操作系统系统中，一个用户是可以**同时存在多个不同的用户组**的，但是享有的用户组权限，只有**同时拥有一个**，一般是 默认组。针对不能用户组之间的切换，可以使用 `newgrp` 命令。


## 相关指令
``` bash
# add user
$ useradd + [option] + [username]
# option:
# -c comment        # 指定一段注释性描述。
# -d directory      # 目录:指定用户主目录，如果此目录不存在，则同时使用-m选项，可以创建主目录。
# -m                # create the user's home directory
# -g  group         # 用户组 指定用户所属的用户组。
# -G                # 用户组，用户组 指定用户所属的附加组。
# -s  shell         # Shell文件 指定用户的登录Shell。
# -u  user          # 用户号:指定用户的用户号，如果同时有-o选项，则可以重复使用其他用户的标识号。
# example:
$ useradd -c "Using by ljf as a normal user" -d /home/eric eric


# change password
passwd + [username]     # (root can change any users's password in this way )
passwd -d [username]    # specify this user has no password


# eliminate user
userdel [username]
# option:
# -r eliminate user_file


# add user to specific group
$ sudo usermod  -a -G [group] [user]
```