# Ip configuration ???

# file in /etc/netplan
``` bash
# example
# This file is generated from information provided by
# the datasource.  Changes to it will not persist across an instance.
# To disable cloud-init's network configuration capabilities, write a file
# /etc/cloud/cloud.cfg.d/99-disable-network-config.cfg with the following:
# network: {config: disabled}
network:
  version: 2
  renderer: networkd      #指定后端采用systemd-networkd或者Network Manager，可不填写则默认使用systemd-workd
  ethernets:
    eth0:
      dhcp4: true  # open dhcp4 ???
      match:
        macaddress: 00:16:3e:16:a0:11  # MAC address
      nameservers:
        addresses: [114.114.114.114,8.8.8.8,8.8.4.4]  #DNS服务器地址，多个DNS服务器地址需要用英文逗号分隔开
      set-name: eth0
```

# after configuration
``` bash
sudo netplan --debug apply
ip a
```