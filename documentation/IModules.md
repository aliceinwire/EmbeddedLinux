# Modules

> In computing, a loadable kernel module (or LKM) is an object file that contains code to extend the running kernel, or so-called base kernel, of an operating system. LKMs are typically used to add support for new hardware (as device drivers) and/or filesystems, or for adding system calls. [Wikipedia](https://en.wikipedia.org/wiki/Loadable_kernel_module)

# Project: Hello World Kernel Module Automatic Startup

```sh
root@edison:~# cd kernelmodule
root@edison:~/kernelmodule# make clean
root@edison:~/kernelmodule# ls
Makefile  helloworld.c
```

```sh
root@edison:~/kernelmodule# make
make -C /lib/modules/3.10.17-poky-edison+/build M=/home/root/kernelmodule modules
make[1]: Entering directory '/home/root/usr/src/linux-headers-3.10.17-poky-edison'
  CC [M]  /home/root/kernelmodule/helloworld.o
  Building modules, stage 2.
  MODPOST 1 modules
  CC      /home/root/kernelmodule/helloworld.mod.o
  LD [M]  /home/root/kernelmodule/helloworld.ko
make[1]: Leaving directory '/home/root/usr/src/linux-headers-3.10.17-poky-edison'
root@edison:~/kernelmodule# 
```

```sh
root@edison:~/kernelmodule# cp helloworld.ko /lib/modules/3.10.17-poky-edison+/kernel/drivers/
```

```sh
root@edison:~/kernelmodule# ls /usr/lib/modules-load.d/
root@edison:~/kernelmodule# 
```

```sh
root@edison:~/kernelmodule# echo helloworld > /usr/lib/modules-load.d/helloworld
root@edison:~/kernelmodule# depmod -a
```

# Release v3.5 Yocto Default Loaded Kernel Modules

```sh
root@edison:~# lsmod
Module                  Size  Used by
usb_f_acm              14335  1                                                 
u_serial               18582  6 usb_f_acm                                       
g_multi                70924  0                                                 
libcomposite           39238  2 usb_f_acm,g_multi                               
bcm_bt_lpm             13708  0                                                 
bcm4334x              587105  0       
```

# Release v3.0 Yocto Default Loaded Kernel Modules

```sh
root@edison:~# lsmod
Module                  Size  Used by
usb_f_acm              14335  1                                                 
u_serial               18582  6 usb_f_acm                                       
g_multi                70924  0                                                 
libcomposite           39238  2 usb_f_acm,g_multi                               
bcm_bt_lpm             13708  0                                                 
bcm4334x              587105  0       
```

# Release v2.1 Yocto Default Loaded Kernel Modules

```sh
    root@edison:~# lsmod
    Module                  Size  Used by
    usb_f_acm              14335  1 
    u_serial               18582  6 usb_f_acm
    g_multi                70924  0 
    libcomposite           39245  2 usb_f_acm,g_multi
    bcm_bt_lpm             13708  0 
    bcm4334x              587105  0 
```

# Search for the name of the default loaded kernel modules

```sh
root@edison:~# modinfo iwlwifi
filename:       /lib/modules/3.10.17-poky-edison+/extra/bcm4334x.ko
license:        GPL v2
alias:          sdio:c*v02D0dA94D*
depends:
vermagic:       3.10.17-poky-edison+ SMP preempt mod_unload ATOM
parm:           dhd_doflow:uint
parm:           dhd_dpcpoll:uint
parm:           clockoverride:SDIO card clock override (int)
parm:           sd_msglevel:uint
parm:           sd_power:uint
parm:           sd_clock:uint
parm:           sd_divisor:uint
parm:           sd_sdmode:uint
parm:           sd_hiok:uint
parm:           sd_f2_blocksize:int
parm:           info_string:string
parm:           op_mode:int
parm:           dhd_msg_level:int
parm:           dhd_arp_enable:uint
```

```sh
    root@edison:~# nano searchm.sh
```

```sh
    for mod in `cat /proc/modules | cut -d " " -f 1`
    do
        desc=`modinfo -d $mod`
        printf "%-20s $desc\n" "$mod:"
    done
```

Output

```sh
    root@edison:~# sh searchm.sh
    usb_f_acm:
    u_serial:
    g_multi:             Multifunction Composite Gadget
    libcomposite:
    bcm_bt_lpm:          bcm43xx_bluetooth
    bcm4334x:
```

# Search for a specific kernel module loaded or compiled

```sh
    root@edison:~/IntelEdison/examples# find /lib/modules/* -name 'uvc'
    /lib/modules/3.10.17-yocto-standard/kernel/drivers/media/usb/uvc
    root@edison:~/IntelEdison/examples# opkg install kernel-module-uvcvideo
    Package kernel-module-uvcvideo (3.10.17-r0) installed in root is up to date.
    root@edison:~/IntelEdison/examples# lsmod | grep uvc
    root@edison:~/IntelEdison/examples# find /lib/modules/* -name 'snd'
    root@edison:~/IntelEdison/examples# find /lib/modules/* -name 'audio'
    root@edison:~/IntelEdison/examples# find /lib/modules/* -name 'alsa'
    root@edison:~/IntelEdison/examples# find /lib/modules/* -name ''
```

# Intel Edison Linux Kernel all modules

## Release v3.5 Yocto 

```sh
root@edison:~# find /lib/modules/* -name '*'                                    
/lib/modules/3.10.98-poky-edison+                                               
/lib/modules/3.10.98-poky-edison+/modules.dep                                   
/lib/modules/3.10.98-poky-edison+/modules.alias                                 
/lib/modules/3.10.98-poky-edison+/modules.symbols                               
/lib/modules/3.10.98-poky-edison+/modules.dep.bin                               
/lib/modules/3.10.98-poky-edison+/modules.builtin.bin                           
/lib/modules/3.10.98-poky-edison+/modules.builtin                               
/lib/modules/3.10.98-poky-edison+/modules.softdep                               
/lib/modules/3.10.98-poky-edison+/modules.devname                               
/lib/modules/3.10.98-poky-edison+/modules.symbols.bin                           
/lib/modules/3.10.98-poky-edison+/kernel                                        
/lib/modules/3.10.98-poky-edison+/kernel/net                                    
/lib/modules/3.10.98-poky-edison+/kernel/net/mac80211                           
/lib/modules/3.10.98-poky-edison+/kernel/net/mac80211/mac80211.ko               
/lib/modules/3.10.98-poky-edison+/kernel/arch                                   
/lib/modules/3.10.98-poky-edison+/kernel/arch/x86                               
/lib/modules/3.10.98-poky-edison+/kernel/arch/x86/kernel                        
/lib/modules/3.10.98-poky-edison+/kernel/arch/x86/kernel/test_nx.ko             
/lib/modules/3.10.98-poky-edison+/kernel/drivers                                
/lib/modules/3.10.98-poky-edison+/kernel/drivers/net                            
/lib/modules/3.10.98-poky-edison+/kernel/drivers/net/usb                        
/lib/modules/3.10.98-poky-edison+/kernel/drivers/net/usb/rtl8150.ko             
/lib/modules/3.10.98-poky-edison+/kernel/drivers/net/usb/r8152.ko               
/lib/modules/3.10.98-poky-edison+/kernel/drivers/usb                            
/lib/modules/3.10.98-poky-edison+/kernel/drivers/usb/gadget                     
/lib/modules/3.10.98-poky-edison+/kernel/drivers/usb/gadget/u_serial.ko         
/lib/modules/3.10.98-poky-edison+/kernel/drivers/usb/gadget/libcomposite.ko     
/lib/modules/3.10.98-poky-edison+/kernel/drivers/usb/gadget/g_multi.ko          
/lib/modules/3.10.98-poky-edison+/kernel/drivers/usb/gadget/usb_f_acm.ko        
/lib/modules/3.10.98-poky-edison+/kernel/drivers/usb/serial                     
/lib/modules/3.10.98-poky-edison+/kernel/drivers/usb/serial/cp210x.ko           
/lib/modules/3.10.98-poky-edison+/kernel/drivers/usb/serial/ftdi_sio.ko         
/lib/modules/3.10.98-poky-edison+/kernel/drivers/staging                        
/lib/modules/3.10.98-poky-edison+/kernel/drivers/staging/iio                    
/lib/modules/3.10.98-poky-edison+/kernel/drivers/staging/iio/trigger            
/lib/modules/3.10.98-poky-edison+/kernel/drivers/staging/iio/trigger/iio-trig-so
/lib/modules/3.10.98-poky-edison+/kernel/drivers/misc                           
/lib/modules/3.10.98-poky-edison+/kernel/drivers/misc/bcm-lpm                   
/lib/modules/3.10.98-poky-edison+/kernel/drivers/misc/bcm-lpm/bcm_bt_lpm.ko     
/lib/modules/3.10.98-poky-edison+/kernel/drivers/media                          
/lib/modules/3.10.98-poky-edison+/kernel/drivers/media/v4l2-core                
/lib/modules/3.10.98-poky-edison+/kernel/drivers/media/v4l2-core/videobuf2-coreo
/lib/modules/3.10.98-poky-edison+/kernel/drivers/media/v4l2-core/videobuf2-vmalo
/lib/modules/3.10.98-poky-edison+/kernel/drivers/media/v4l2-core/videobuf2-memoo
/lib/modules/3.10.98-poky-edison+/kernel/drivers/media/usb                      
/lib/modules/3.10.98-poky-edison+/kernel/drivers/media/usb/uvc                  
/lib/modules/3.10.98-poky-edison+/kernel/drivers/media/usb/uvc/uvcvideo.ko      
/lib/modules/3.10.98-poky-edison+/kernel/drivers/media/usb/gspca                
/lib/modules/3.10.98-poky-edison+/kernel/drivers/media/usb/gspca/gspca_ov534_9.o
/lib/modules/3.10.98-poky-edison+/kernel/drivers/media/usb/gspca/gspca_ov534.ko 
/lib/modules/3.10.98-poky-edison+/kernel/drivers/media/usb/gspca/gspca_main.ko  
/lib/modules/3.10.98-poky-edison+/extra                                         
/lib/modules/3.10.98-poky-edison+/extra/bcm4334x.ko                             
/lib/modules/3.10.98-poky-edison+/modules.alias.bin                             
/lib/modules/3.10.98-poky-edison+/modules.order                                 
root@edison:~# 
```

## Release v3.0 Yocto 

```sh
    root@edison:~/IntelEdison/examples# find /lib/modules/* -name '*'
    /lib/modules/3.10.17-yocto-standard
    /lib/modules/3.10.17-yocto-standard/modules.devname
    /lib/modules/3.10.17-yocto-standard/modules.dep
    /lib/modules/3.10.17-yocto-standard/modules.alias.bin
    /lib/modules/3.10.17-yocto-standard/modules.builtin.bin
    /lib/modules/3.10.17-yocto-standard/modules.order
    /lib/modules/3.10.17-yocto-standard/modules.softdep
    /lib/modules/3.10.17-yocto-standard/extra
    /lib/modules/3.10.17-yocto-standard/extra/bcm4334x.ko
    /lib/modules/3.10.17-yocto-standard/modules.symbols
    /lib/modules/3.10.17-yocto-standard/modules.builtin
    /lib/modules/3.10.17-yocto-standard/modules.dep.bin
    /lib/modules/3.10.17-yocto-standard/modules.alias
    /lib/modules/3.10.17-yocto-standard/kernel
    /lib/modules/3.10.17-yocto-standard/kernel/net
    /lib/modules/3.10.17-yocto-standard/kernel/net/netfilter
    /lib/modules/3.10.17-yocto-standard/kernel/net/netfilter/xt_state.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/netfilter/xt_length.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/netfilter/xt_NETMAP.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/netfilter/nf_conntrack.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/netfilter/nf_conntrack_broadcast.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/netfilter/xt_connbytes.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/netfilter/nf_conntrack_proto_sctp.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/netfilter/nfnetlink_queue.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/netfilter/nf_nat_ftp.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/netfilter/xt_policy.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/netfilter/xt_helper.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/netfilter/xt_CT.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/netfilter/xt_ecn.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/netfilter/nf_conntrack_proto_gre.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/netfilter/nf_conntrack_irc.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/netfilter/xt_NFQUEUE.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/netfilter/xt_string.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/netfilter/xt_limit.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/netfilter/nf_conntrack_netbios_ns.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/netfilter/xt_realm.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/netfilter/xt_CLASSIFY.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/netfilter/xt_connmark.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/netfilter/xt_connlimit.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/netfilter/nf_conntrack_sip.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/netfilter/nf_conntrack_ftp.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/netfilter/xt_TRACE.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/netfilter/nf_nat.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/netfilter/nf_conntrack_sane.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/netfilter/xt_tcpmss.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/netfilter/nf_conntrack_h323.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/netfilter/xt_mac.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/netfilter/xt_esp.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/netfilter/nf_conntrack_amanda.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/netfilter/xt_pkttype.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/netfilter/xt_multiport.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/netfilter/nf_nat_proto_udplite.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/netfilter/nfnetlink_log.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/netfilter/nfnetlink.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/netfilter/xt_dscp.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/netfilter/nf_conntrack_proto_udplite.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/netfilter/xt_NFLOG.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/netfilter/nf_conntrack_tftp.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/netfilter/xt_cluster.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/netfilter/nf_tproxy_core.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/netfilter/xt_dccp.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/netfilter/xt_TCPMSS.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/netfilter/nf_nat_sip.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/netfilter/nf_conntrack_pptp.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/netfilter/nf_conntrack_netlink.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/netfilter/xt_sctp.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/netfilter/nf_nat_tftp.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/netfilter/xt_DSCP.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/netfilter/xt_socket.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/netfilter/nf_nat_proto_sctp.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/netfilter/xt_u32.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/netfilter/nf_nat_amanda.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/netfilter/xt_statistic.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/netfilter/xt_quota.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/netfilter/xt_comment.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/netfilter/xt_hashlimit.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/netfilter/xt_REDIRECT.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/netfilter/nf_nat_irc.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/netfilter/xt_nat.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/netfilter/xt_conntrack.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/mac80211
    /lib/modules/3.10.17-yocto-standard/kernel/net/mac80211/mac80211.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/ipv6
    /lib/modules/3.10.17-yocto-standard/kernel/net/ipv6/netfilter
    /lib/modules/3.10.17-yocto-standard/kernel/net/ipv6/netfilter/nf_defrag_ipv6.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/ipv4
    /lib/modules/3.10.17-yocto-standard/kernel/net/ipv4/netfilter
    /lib/modules/3.10.17-yocto-standard/kernel/net/ipv4/netfilter/nf_nat_pptp.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/ipv4/netfilter/arp_tables.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/ipv4/netfilter/nf_nat_h323.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/ipv4/netfilter/arptable_filter.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/ipv4/netfilter/ipt_ah.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/ipv4/netfilter/nf_defrag_ipv4.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/ipv4/netfilter/iptable_filter.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/ipv4/netfilter/iptable_nat.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/ipv4/netfilter/ip_tables.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/ipv4/netfilter/iptable_raw.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/ipv4/netfilter/ipt_CLUSTERIP.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/ipv4/netfilter/nf_conntrack_ipv4.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/ipv4/netfilter/ipt_ULOG.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/ipv4/netfilter/nf_nat_proto_gre.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/ipv4/netfilter/arpt_mangle.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/ipv4/netfilter/ipt_REJECT.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/ipv4/netfilter/ipt_MASQUERADE.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/ipv4/netfilter/iptable_mangle.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/ipv4/netfilter/nf_nat_ipv4.ko
    /lib/modules/3.10.17-yocto-standard/kernel/net/ipv4/netfilter/ipt_ECN.ko
    /lib/modules/3.10.17-yocto-standard/kernel/drivers
    /lib/modules/3.10.17-yocto-standard/kernel/drivers/media
    /lib/modules/3.10.17-yocto-standard/kernel/drivers/media/v4l2-core
    /lib/modules/3.10.17-yocto-standard/kernel/drivers/media/v4l2-core/videobuf2-vmalloc.ko
    /lib/modules/3.10.17-yocto-standard/kernel/drivers/media/v4l2-core/videobuf2-memops.ko
    /lib/modules/3.10.17-yocto-standard/kernel/drivers/media/v4l2-core/videobuf2-core.ko
    /lib/modules/3.10.17-yocto-standard/kernel/drivers/media/usb
    /lib/modules/3.10.17-yocto-standard/kernel/drivers/media/usb/uvc
    /lib/modules/3.10.17-yocto-standard/kernel/drivers/media/usb/uvc/uvcvideo.ko
    /lib/modules/3.10.17-yocto-standard/kernel/drivers/media/usb/gspca
    /lib/modules/3.10.17-yocto-standard/kernel/drivers/media/usb/gspca/gspca_main.ko
    /lib/modules/3.10.17-yocto-standard/kernel/drivers/staging
    /lib/modules/3.10.17-yocto-standard/kernel/drivers/staging/iio
    /lib/modules/3.10.17-yocto-standard/kernel/drivers/staging/iio/trigger
    /lib/modules/3.10.17-yocto-standard/kernel/drivers/staging/iio/trigger/iio-trig-sysfs.ko
    /lib/modules/3.10.17-yocto-standard/kernel/drivers/usb
    /lib/modules/3.10.17-yocto-standard/kernel/drivers/usb/serial
    /lib/modules/3.10.17-yocto-standard/kernel/drivers/usb/serial/cp210x.ko
    /lib/modules/3.10.17-yocto-standard/kernel/drivers/usb/gadget
    /lib/modules/3.10.17-yocto-standard/kernel/drivers/usb/gadget/usb_f_acm.ko
    /lib/modules/3.10.17-yocto-standard/kernel/drivers/usb/gadget/u_serial.ko
    /lib/modules/3.10.17-yocto-standard/kernel/drivers/usb/gadget/g_multi.ko
    /lib/modules/3.10.17-yocto-standard/kernel/drivers/usb/gadget/libcomposite.ko
    /lib/modules/3.10.17-yocto-standard/kernel/drivers/misc
    /lib/modules/3.10.17-yocto-standard/kernel/drivers/misc/bcm-lpm
    /lib/modules/3.10.17-yocto-standard/kernel/drivers/misc/bcm-lpm/bcm_bt_lpm.ko
    /lib/modules/3.10.17-yocto-standard/kernel/lib
    /lib/modules/3.10.17-yocto-standard/kernel/lib/ts_kmp.ko
    /lib/modules/3.10.17-yocto-standard/kernel/lib/ts_fsm.ko
    /lib/modules/3.10.17-yocto-standard/kernel/lib/ts_bm.ko
    /lib/modules/3.10.17-yocto-standard/kernel/fs
    /lib/modules/3.10.17-yocto-standard/kernel/fs/aufs
    /lib/modules/3.10.17-yocto-standard/kernel/fs/aufs/aufs.ko
    /lib/modules/3.10.17-yocto-standard/kernel/arch
    /lib/modules/3.10.17-yocto-standard/kernel/arch/x86
    /lib/modules/3.10.17-yocto-standard/kernel/arch/x86/kernel
    /lib/modules/3.10.17-yocto-standard/kernel/arch/x86/kernel/test_nx.ko
    /lib/modules/3.10.17-yocto-standard/modules.symbols.bin
```