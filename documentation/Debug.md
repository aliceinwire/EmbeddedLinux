Debug
==

> Debugging is the process of finding and resolving or defects that prevent correct operation of computer software or a system. Debugging tends to be harder when various subsystems are tightly coupled, as changes in one may cause bugs to emerge in another. [Wikipedia](https://en.wikipedia.org/wiki/Debugging)

- [Ubuntu Kernel Debugging Tricks](https://wiki.ubuntu.com/Kernel/KernelDebuggingTricks)

## Kernel Configuration

```sh
    
    Kernel hacking

        -*- Kernel debugging
        [*]   Magic SysRq key
        -*-   Debug filesystem
        [*]   Detect Soft Lockups
        [ ]   Collect scheduler statistics
        [*]   Debug slab memory allocations
        [*]     Memory leak debugging
        [*]   Mutex debugging, deadlock detection
        [*]   Spinlock debugging
        [*]   Sleep-inside-spinlock checking
        [ ]   kobject debugging
        [ ]   Highmem debugging
        [ ]   Compile the kernel with debug info
```

## Kernel Integration

### Linux Debug Filesystem

> Debugfs exists as a simple way for kernel developers to make information available to user space.  Unlike /proc, which is only meant for information about a process, or sysfs, which has strict one-value-per-file rules, debugfs has no rules at all. [Wikipedia](https://en.wikipedia.org/wiki/Debugfs)

- [Linux Kernel Documentation Debugfs](https://www.kernel.org/doc/Documentation/filesystems/debugfs.txt)
- [Linux Kernel Debugfs](https://www.kernel.org/doc/Documentation/filesystems/debugfs.txt)

```sh
    root@edison:~# mount -t debugfs none /sys/kernel/debug
    mount: none is already mounted or /sys/kernel/debug busy
           none is already mounted on /tmp/temptmpfs
    root@edison:~# ls /sys/kernel/debug/
    asoc                  gpio_debug            pmu_sync_d0ix
    bdi                   hid                   pwm
    bluetooth             hsu                   regmap
    boot_params           ieee80211             regulator
    c_states_stat         ignore_add            remoteproc
    cstate_ignore_add     ignore_remove         s3_ctrl
    cstate_ignore_remove  iio                   sched_features
    debug_feature         intel_scu_oshob       soc_thermal
    disable_emmc_ipanic   kprobes               sst
    dma_buf               mce                   suspend_stats
    dri                   mid_pmu_states        tracing
    dump_cmd              mmc0                  usb
    dump_output           mmc1                  wakeup_sources
    dwc3-device.1         mmc2                  watchdog
    dynamic_debug         pmic_ccsm             x86
    emmc_ipanic           pmu_force_d0i0
    gpio                  pmu_force_d0i3
    root@edison:~# 
```

### Linux Magic System Request Key Hacks

> It is a 'magical' key combo you can hit which the kernel will respond to regardless of whatever else it is doing, unless it is completely locked up. [Documentation](https://www.kernel.org/doc/Documentation/sysrq.txt)

- [Linux Magic System Request Key Hacks](https://www.kernel.org/doc/Documentation/sysrq.txt)

### Ftrace

- [Debugging the kernel using Ftrace - Part 1](https://lwn.net/Articles/365835/)

```sh
    root@edison:~# cd /sys/kernel/debug/tracing
    root@edison:/sys/kernel/debug/tracing# cat available_tracers 
    blk function_graph wakeup_rt wakeup preemptirqsoff preemptoff irqsoff function nop
    root@edison:/sys/kernel/debug/tracing# echo function > current_tracer
    root@edison:/sys/kernel/debug/tracing# cat current_tracer
    function
```

## Applications / Libraries

### Programs

None
