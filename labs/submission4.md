
```
~$ uptime
 14:12:47 up 1 min,  1 user,  load average: 0.09, 0.05, 0.01

aliya@LAPTOP-AA2IU80B:~$ w
 14:12:49 up 1 min,  1 user,  load average: 0.08, 0.05, 0.01
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU  WHAT
aliya    pts/1    -                14:12   40.00s  0.02s  0.02s -bash
```

```
~$ ps -eo pid,ppid,cmd,%mem,%cpu --sort=-%mem | head -n 6
    PID    PPID CMD                         %MEM %CPU
    248       1 /usr/bin/python3 /usr/share  0.2  0.0
     53       1 /usr/lib/systemd/systemd-jo  0.1  0.0
    214       1 /usr/libexec/wsl-pro-servic  0.1  0.1
      1       0 /sbin/init                   0.1  0.5
    124       1 /usr/lib/systemd/systemd-re  0.1  0.0
```
```
~$ ps -eo pid,ppid,cmd,%mem,%cpu --sort=-%cpu | head -n 6
    PID    PPID CMD                         %MEM %CPU
      1       0 /sbin/init                   0.1  0.4
    214       1 /usr/libexec/wsl-pro-servic  0.1  0.1
    112       1 /usr/lib/systemd/systemd-ud  0.0  0.0
    248       1 /usr/bin/python3 /usr/share  0.2  0.0
     53       1 /usr/lib/systemd/systemd-jo  0.1  0.0
```

```
~$ systemctl list-dependencies
default.target
○ ├─display-manager.service
○ ├─systemd-update-utmp-runlevel.service
○ ├─wslg.service
● └─multi-user.target
○   ├─apport.service
●   ├─console-setup.service
●   ├─cron.service
●   ├─dbus.service
○   ├─dmesg.service
○   ├─e2scrub_reap.service
○   ├─landscape-client.service
○   ├─networkd-dispatcher.service
●   ├─rsyslog.service
○   ├─snapd.apparmor.service
○   ├─snapd.autoimport.service
○   ├─snapd.core-fixup.service
○   ├─snapd.recovery-chooser-trigger.service
●   ├─snapd.seeded.service
○   ├─snapd.service
●   ├─systemd-ask-password-wall.path
●   ├─systemd-logind.service
○   ├─systemd-update-utmp-runlevel.service
●   ├─systemd-user-sessions.service
○   ├─ua-reboot-cmds.service
○   ├─ubuntu-advantage.service
●   ├─unattended-upgrades.service
●   ├─wsl-pro.service
●   ├─basic.target
○   │ ├─tmp.mount
●   │ ├─paths.target
○   │ │ └─apport-autoreport.path
●   │ ├─slices.target
●   │ │ ├─-.slice
●   │ │ └─system.slice
●   │ ├─sockets.target
●   │ │ ├─apport-forward.socket
●   │ │ ├─dbus.socket
●   │ │ ├─snapd.socket
●   │ │ ├─systemd-initctl.socket
●   │ │ ├─systemd-journald-dev-log.socket
●   │ │ ├─systemd-journald.socket
○   │ │ ├─systemd-pcrextend.socket
●   │ │ ├─systemd-sysext.socket
●   │ │ ├─systemd-udevd-control.socket
●   │ │ ├─systemd-udevd-kernel.socket
●   │ │ └─uuidd.socket
●   │ ├─sysinit.target
○   │ │ ├─apparmor.service
●   │ │ ├─dev-hugepages.mount
●   │ │ ├─dev-mqueue.mount
●   │ │ ├─keyboard-setup.service
●   │ │ ├─kmod-static-nodes.service
●   │ │ ├─ldconfig.service
○   │ │ ├─proc-sys-fs-binfmt_misc.automount
●   │ │ ├─setvtrgb.service
●   │ │ ├─sys-fs-fuse-connections.mount
●   │ │ ├─sys-kernel-config.mount
●   │ │ ├─sys-kernel-debug.mount
●   │ │ ├─sys-kernel-tracing.mount
●   │ │ ├─systemd-ask-password-console.path
●   │ │ ├─systemd-binfmt.service
○   │ │ ├─systemd-firstboot.service
○   │ │ ├─systemd-hwdb-update.service
●   │ │ ├─systemd-journal-catalog-update.service
●   │ │ ├─systemd-journal-flush.service
●   │ │ ├─systemd-journald.service
○   │ │ ├─systemd-machine-id-commit.service
●   │ │ ├─systemd-modules-load.service
○   │ │ ├─systemd-pcrmachine.service
○   │ │ ├─systemd-pcrphase-sysinit.service
○   │ │ ├─systemd-pcrphase.service
○   │ │ ├─systemd-pstore.service
○   │ │ ├─systemd-random-seed.service
○   │ │ ├─systemd-repart.service
●   │ │ ├─systemd-resolved.service
●   │ │ ├─systemd-sysctl.service
●   │ │ ├─systemd-sysusers.service
●   │ │ ├─systemd-timesyncd.service
●   │ │ ├─systemd-tmpfiles-setup-dev-early.service
●   │ │ ├─systemd-tmpfiles-setup-dev.service
●   │ │ ├─systemd-tmpfiles-setup.service
○   │ │ ├─systemd-tpm2-setup-early.service
○   │ │ ├─systemd-tpm2-setup.service
●   │ │ ├─systemd-udev-trigger.service
●   │ │ ├─systemd-udevd.service
●   │ │ ├─systemd-update-done.service
●   │ │ ├─systemd-update-utmp.service
●   │ │ ├─cryptsetup.target
●   │ │ ├─integritysetup.target
●   │ │ ├─local-fs.target
●   │ │ │ └─systemd-remount-fs.service
●   │ │ ├─swap.target
●   │ │ └─veritysetup.target
●   │ └─timers.target
○   │   ├─apport-autoreport.timer
●   │   ├─apt-daily-upgrade.timer
●   │   ├─apt-daily.timer
●   │   ├─dpkg-db-backup.timer
●   │   ├─e2scrub_all.timer
○   │   ├─fstrim.timer
●   │   ├─logrotate.timer
●   │   ├─man-db.timer
●   │   ├─motd-news.timer
○   │   ├─snapd.snap-repair.timer
●   │   ├─systemd-tmpfiles-clean.timer
○   │   └─ua-timer.timer
●   ├─getty.target
●   │ ├─console-getty.service
○   │ ├─getty-static.service
●   │ └─getty@tty1.service
●   └─remote-fs.target
```

```
 who -a
           system boot  2026-02-25 14:11
           run-level 5  2026-02-25 14:11
LOGIN      console      2026-02-25 14:11               223 id=cons
LOGIN      tty1         2026-02-25 14:11               234 id=tty1
aliya    - pts/1        2026-02-25 14:12 00:20         572
```

```
$ last -n 5
reboot   system boot  6.6.87.2-microso Wed Feb 25 14:11   still running

wtmp begins Wed Feb 25 14:11:29 2026
```

```
 free -h
               total        used        free      shared  buff/cache   available
Mem:           7.5Gi       509Mi       7.0Gi       3.6Mi       147Mi       7.0Gi
Swap:          2.0Gi          0B       2.0Gi
```

```
$ cat /proc/meminfo | grep -e MemTotal -e SwapTotal -e MemAvailable
MemTotal:        7880368 kB
MemAvailable:    7358292 kB
SwapTotal:       2097152 kB
```

Процесс с PID 248 (/usr/bin/python3 /usr/share/...) является наибольшим потребителем оперативной памяти, занимая 0.2% от общего объёма RAM.

### Task 2

```
 traceroute github.com
traceroute to github.com (140.82.121.3), 30 hops max, 60 byte packets
 1  LAPTOP-AA2IU80B.mshome.net (172.28.128.1)  0.804 ms  0.771 ms  0.760 ms
 2  192.168.43.1 (192.168.43.1)  6.799 ms  6.785 ms  6.774 ms
 3  * * *
 4  172.16.1.206 (172.16.1.206)  39.887 ms  32.846 ms  48.007 ms
 5  pgag-cr03-eth-trunk52.100.nnov.mts-internet.net (212.188.61.85)  41.802 ms  41.791 ms  41.334 ms
 6  bek-cr01-be5.nnov.mts-internet.net (195.34.59.98)  65.638 ms  63.030 ms  64.056 ms
 7  * * mag9-cr02-be3.52.msk.mts-internet.net (212.188.28.169)  54.643 ms
 8  a433-cr06-eth-trunk15.msk.mts-internet.net (212.188.28.102)  57.926 ms  62.171 ms  61.753 ms
 9  mmon-cr02-eth-trunk1.spb.mts-internet.net (212.188.2.53)  74.597 ms  75.207 ms  80.139 ms
10  radio-cr01-ae9.0.hel.mts-internet.net (212.188.29.23)  76.125 ms radio-cr01-ae3.0.hel.mts-internet.net (212.188.29.109)  59.269 ms  50.431 ms
11  de-cix2.fra.github.com (80.81.196.80)  98.484 ms  82.767 ms  80.328 ms
```

```
 dig github.com

; <<>> DiG 9.18.39-0ubuntu0.24.04.2-Ubuntu <<>> github.com
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 410
;; flags: qr rd ra ad; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 0

;; QUESTION SECTION:
;github.com.                    IN      A

;; ANSWER SECTION:
github.com.             528     IN      A       140.82.121.3

;; Query time: 66 msec
;; SERVER: 10.255.255.254#53(10.255.255.254) (UDP)
;; WHEN: Wed Feb 25 14:48:09 MSK 2026
;; MSG SIZE  rcvd: 44
```

```
 sudo timeout 10 tcpdump -c 5 -i any 'port 53' -nn
tcpdump: data link type LINUX_SLL2
tcpdump: verbose output suppressed, use -v[v]... for full protocol decode
listening on any, link-type LINUX_SLL2 (Linux cooked v2), snapshot length 262144 bytes

0 packets captured
0 packets received by filter
0 packets dropped by kernel
```

```
~$ dig -x 8.8.4.4

; <<>> DiG 9.18.39-0ubuntu0.24.04.2-Ubuntu <<>> -x 8.8.4.4
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 31243
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
;; QUESTION SECTION:
;4.4.8.8.in-addr.arpa.          IN      PTR

;; ANSWER SECTION:
4.4.8.8.in-addr.arpa.   17674   IN      PTR     dns.google.

;; Query time: 77 msec
;; SERVER: 10.255.255.254#53(10.255.255.254) (UDP)
;; WHEN: Wed Feb 25 14:49:34 MSK 2026
;; MSG SIZE  rcvd: 73
```

```
 dig -x 1.1.2.2

; <<>> DiG 9.18.39-0ubuntu0.24.04.2-Ubuntu <<>> -x 1.1.2.2
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NXDOMAIN, id: 20736
;; flags: qr rd ra ad; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
;; QUESTION SECTION:
;2.2.1.1.in-addr.arpa.          IN      PTR

;; AUTHORITY SECTION:
1.in-addr.arpa.         3600    IN      SOA     ns.apnic.net. read-txt-record-of-zone-first-dns-admin.apnic.net. 23597 7200 1800 604800 3600

;; Query time: 654 msec
;; SERVER: 10.255.255.254#53(10.255.255.254) (UDP)
;; WHEN: Wed Feb 25 14:50:08 MSK 2026
;; MSG SIZE  rcvd: 137
```

### Insights on network paths discovered
Трафик идёт через локальный шлюз WSL (172.28.128.1), затем через точку доступа 192.168.43.1.

На третьем хопе все пакеты потеряны (* * *) – это может быть узлом, не отвечающим на ICMP-запросы (обычная практика для защиты от сканирования).

Конечный хоп – 140.82.121.3 (github.com) достигается за 11 шагов.

Задержки постепенно возрастают от 0.8 мс до ~80 мс, что соответствует географическому удалению и транзиту через магистральные маршрутизаторы.
Последний хоп перед github.com (80.81.196.80) принадлежит сети GitHub, что указывает на прямое пиринговое подключение через DE-CIX.


### Analysis of DNS query/response patterns 

DNS-запрос типа A для github.com был отправлен на локальный рекурсивный сервер 10.255.255.254 (порт 53).

Ответ пришёл со статусом NOERROR, флагами qr, rd, ra и ad 

В ответе содержится одна запись A: 140.82.121.3 с TTL 528 секунд.

Время отклика составило 66 мс, что говорит о быстрой работе резолвера.

Отсутствуют авторитетные и дополнительные записи – это типично для простого A-запроса.

Полученный IP-адрес полностью совпадает с тем, который показала трассировка, подтверждая корректность разрешения имени.

### Comparison of reverse lookup results
Для адреса 8.8.4.4 успешно выполнен обратный запрос: получена PTR-запись dns.google. Это ожидаемо, так как адрес принадлежит публичным DNS-серверам Google, которые имеют правильно настроенные обратные зоны.

Для адреса 1.1.2.2 запрос вернул статус NXDOMAIN – PTR-запись отсутствует. В авторитетной секции указан SOA для зоны 1.in-addr.arpa, управляемой APNIC. Это означает, что обратная зона делегирована, но конкретная запись для 1.1.2.2 не настроена.

Время ответа для 1.1.2.2 значительно выше (654 мс против 77 мс) из-за необходимости обращения к авторитетным серверам APNIC и отсутствия кэширования.

