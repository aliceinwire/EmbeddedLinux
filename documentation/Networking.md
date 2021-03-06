# Networking

- [Intel® Edison Connecting to a Network](https://software.intel.com/en-us/connecting-to-a-network-intel-edison-board)
- [Intel® Edison Static IP Address](http://pagealh.com/2015/09/12/getting-started-with-edison-static-ip-address/)

## Applications / Libraries

### Programs

#### Misc

```sh
    root@edison:~# systemctl start connman
    root@edison:~# systemctl start wpa_supplicant
    root@edison:~# connmanctl
    connmanctl> enable_wifi
    connmanctl> scan_wifi
    connmanctl> agent_on
    connmanctl> connect ...
```

```sh
    root@edison:~# vi /lib/systemd/system/sshd.socket
    [Unit]
    Conflicts=sshd.service
    
    [Socket]
    ExecStartPre=/bin/mkdir -p /var/run/sshd
    ListenStream=22
    # restrict access to wired access for security reasons
    # comment this line to remove restriction
    BindToDevice=usb0
    Accept=yes

    [Install]
    WantedBy=sockets.target
```

## Controller Area Network

- [1](https://communities.intel.com/message/294647#294647)
- [2](https://www.sparkfun.com/products/13262)
- [3](https://store.digilentinc.com/?NavPath=2,892,942&Prod=CHIPKIT-NETWORK-SHIELD)
