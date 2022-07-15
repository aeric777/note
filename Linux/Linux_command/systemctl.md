## system_command

### systemctl

``` bash
$ systemctl start   [service]   # 启动
$ systemctl stop    [service]   # 停止
$ systemctl restart [service]   # 重启
$ systemctl status  [service]   # 查看状态

$ systemctl enable  [service]       # 开机自启
$ systemctl disable [service]       # 停止开机自启
$ systemctl is-enabled [service]    # 查看是否开机自启


$ sudo systemctl status		        # 层级查看所有运行中的服务状态
$ systemctl --failed			    # 列出启动失败的服务列表
$ systemctl list-unit-files | grep enabled	# 列出所有开机启动的服务

```