# Lab 5 — Virtualization & System Analysis

## Task 1 — VirtualBox Installation
### Host operating system
Windows 11 Pro 24H2 (сборка 26100.1150)

### VirtualBox version number
Version 7.0.18 r162988 (Qt5.15.2)

### Any installation issues encountered
При установке проблем не возникло. Установка прошла штатно, после завершения компьютер не требовал перезагрузки.

## Task 2 — Ubuntu VM and System Analysis

```
lscpuA
rchitecture:             x86_64 
 CPU op-mode(s):         32-bit, 64-bit 
 Address sizes:          46 bits physical, 48 bits virtual 
 Byte Order:             Little EndianC
PU(s):                   6 
 On-line CPU(s) list:    0-5V
endor ID:                GenuineIntel 
 Model name:             Intel(R) Core(TM) Ultra 5 125H 
   CPU family:           6 
   Model:                170 
   Thread(s) per core:   1 
   Core(s) per socket:   6 
   Socket(s):            1 
   Stepping:             4 
   BogoMIPS:             5990.39 
   Flags:                fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxs 
                         r sse sse2 ht syscall nx rdtscp lm constant_tsc rep_good nopl xtopology nonstop_tsc cpu 
                         id tsc_known_freq pni pclmulqdq ssse3 fma cx16 pcid sse4_1 sse4_2 movbe popcnt aes xsav 
                         e avx f16c rdrand hypervisor lahf_lm abm 3dnowprefetch ibrs_enhanced fsgsbase bmi1 avx2 
                          bmi2 invpcid rdseed adx clflushopt sha_ni arat md_clear flush_l1d arch_capabilitiesV
irtualization features:   
 Hypervisor vendor:      KVM 
 Virtualization type:    fullC
aches (sum of all):       
 L1d:                    192 KiB (6 instances) 
 L1i:                    384 KiB (6 instances) 
 L2:                     12 MiB (6 instances) 
 L3:                     108 MiB (6 instances)N
UMA:                      
 NUMA node(s):           1 
 NUMA node0 CPU(s):      0-5V
ulnerabilities:           
 Gather data sampling:   Not affected 
 Ghostwrite:             Not affected 
 Itlb multihit:          Not affected 
 L1tf:                   Not affected 
 Mds:                    Not affected 
 Meltdown:               Not affected 
 Mmio stale data:        Not affected 
 Reg file data sampling: Not affected 
 Retbleed:               Mitigation; Enhanced IBRS 
 Spec rstack overflow:   Not affected 
 Spec store bypass:      Vulnerable 
 Spectre v1:             Mitigation; usercopy/swapgs barriers and __user pointer sanitization 
 Spectre v2:             Mitigation; Enhanced / Automatic IBRS; PBRSB-eIBRS SW sequence; BHI SW loop, KVM SW loo 
                         p 
 Srbds:                  Not affected 
 Tsx async abort:        Not affected
```


``` free -h — использование оперативной памяти
free -h
               total        used        free      shared  buff/cache   available
Mem:           3.8Gi       1.7Gi       698Mi        56Mi       1.5Gi       2.2Gi
Swap:             0B          0B          0B
```

``` ip addr, ip link, ip route — сетевые интерфейсы и маршрутизация
ip addr
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute 
       valid_lft forever preferred_lft forever
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:d3:da:08 brd ff:ff:ff:ff:ff:ff
    inet 10.0.2.15/24 brd 10.0.2.255 scope global dynamic noprefixroute enp0s3
       valid_lft 85372sec preferred_lft 85372sec
    inet6 fd17:625c:f037:2:3206:c028:aae8:5b4a/64 scope global temporary dynamic 
       valid_lft 86146sec preferred_lft 14146sec
    inet6 fd17:625c:f037:2:ad1e:99b0:1de4:dd73/64 scope global dynamic mngtmpaddr noprefixroute 
       valid_lft 86146sec preferred_lft 14146sec
    inet6 fe80::d664:4a34:b1d4:31ea/64 scope link noprefixroute 
       valid_lft forever preferred_lft forever
user@user-pc:~$ ip link
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN mode DEFAULT group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP mode DEFAULT group default qlen 1000
    link/ether 08:00:27:d3:da:08 brd ff:ff:ff:ff:ff:ff
user@user-pc:~$ ip route
default via 10.0.2.2 dev enp0s3 proto dhcp src 10.0.2.15 metric 100 
10.0.2.0/24 dev enp0s3 proto kernel scope link src 10.0.2.15 metric 100
```


``` df -h и du -sh * — использование дискового пространства
df -h
Filesystem      Size  Used Avail Use% Mounted on
tmpfs           392M  1.3M  391M   1% /run
/dev/sda1        30G   23G  5.4G  81% /
tmpfs           2.0G     0  2.0G   0% /dev/shm
tmpfs           5.0M  8.0K  5.0M   1% /run/lock
tmpfs           392M  132K  392M   1% /run/user/1000
user@user-pc:~$ du -sh *
190M    basics-graphics-music
40K     Desktop
4.0K    Documents
43M     Downloads
```

``` uname -a — информация о ядре и системе
uname -a
Linux user-pc 6.14.0-27-generic #27~24.04.1-Ubuntu SMP PREEMPT_DYNAMIC Tue Jul 22 17:38:49 UTC 2 x86_64 x86_64 x86_64 GNU/Linux
```

``` systemd-detect-virt — определение типа виртуализации
systemd-detect-virt
oracle
```

