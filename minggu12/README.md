# LAPORAN JOBSHEET 12
## 1. Manajemen Service

* Nama  : Galih Candra Kirana
* NIM   : 254107020080
* Kelas : TI-1G

## 1.1 Pengenalan systemd

## Praktek 12.1: Amati Layanan Aktif Saat Boot
```bash
systemctl list-units --type=service --state=running
systemctl list-unit-files --type=service | head -30
systemctl status ssh
systemd-analyze blame | head -15

Output:
galihcandra@LAPTOP-QQ597UPT:~$ systemctl list-units --type=service --state=running
  UNIT                        LOAD   ACTIVE SUB     DESCRIPTION>
  console-getty.service       loaded active running Console Get>
  cron.service                loaded active running Regular bac>
  dbus.service                loaded active running D-Bus Syste>
  getty@tty1.service          loaded active running Getty on tt>
  rsyslog.service             loaded active running System Logg>
  systemd-journald.service    loaded active running Journal Ser>
  systemd-logind.service      loaded active running User Login >
  systemd-resolved.service    loaded active running Network Nam>
  systemd-timesyncd.service   loaded active running Network Tim>
  systemd-udevd.service       loaded active running Rule-based >
  unattended-upgrades.service loaded active running Unattended >
  user@1000.service           loaded active running User Manage>

Legend: LOAD   → Reflects whether the unit definition was prope>
        ACTIVE → The high-level unit activation state, i.e. gen>
        SUB    → The low-level unit activation state, values de>

12 loaded units listed.

galihcandra@LAPTOP-QQ597UPT:~$ systemctl list-unit-files --type=service | head -30
UNIT FILE                                    STATE           PRESET
apparmor.service                             enabled         enabled
apport-autoreport.service                    static          -
apport-coredump-hook@.service                static          -
apport-forward@.service                      static          -
apport.service                               enabled         enabled
apt-daily-upgrade.service                    static          -
apt-daily.service                            static          -
apt-news.service                             static          -
autovt@.service                              alias           -
cloud-config.service                         enabled         enabled
cloud-final.service                          enabled         enabled
cloud-init-hotplugd.service                  static          -
cloud-init-local.service                     enabled         enabled
cloud-init.service                           enabled         enabled
console-getty.service                        enabled-runtime disabled
console-setup.service                        enabled         enabled
container-getty@.service                     static          -
cron.service                                 enabled         enabled
cryptdisks-early.service                     masked          enabled
cryptdisks.service                           masked          enabled
dbus-org.freedesktop.hostname1.service       alias           -
dbus-org.freedesktop.locale1.service         alias           -
dbus-org.freedesktop.login1.service          alias           -
dbus-org.freedesktop.resolve1.service        alias           -
dbus-org.freedesktop.timedate1.service       alias           -
dbus-org.freedesktop.timesync1.service       alias           -
dbus.service                                 static          -
debug-shell.service                          disabled        disabled
dmesg.service                                enabled         enabled

galihcandra@LAPTOP-QQ597UPT:~$ systemd-analyze
Startup finished in 21.557s (userspace)
graphical.target reached after 21.443s in userspace.

galihcandra@LAPTOP-QQ597UPT:~$ systemd-analyze blame | head -15
32.084s apt-daily-upgrade.service
 7.405s landscape-client.service
 6.900s dev-sdd.device
 3.818s logrotate.service
 3.054s systemd-resolved.service
 2.842s e2scrub_reap.service
 2.830s snapd.seeded.service
 2.557s systemd-timesyncd.service
 2.271s snapd.service
 1.829s rsyslog.service
 1.744s systemd-udev-trigger.service
 1.636s systemd-journal-flush.service
 1.606s modprobe@drm.service
 1.600s modprobe@configfs.service
 1.592s modprobe@dm_mod.service
```

### Tantangan
```bash
galihcandra@LAPTOP-QQ597UPT:~$ systemd-analyze blame | sort -rh | head -3
       992ms dev-hugepages.mount
       969ms sys-kernel-config.mount
       912ms systemd-sysctl.service
galihcandra@LAPTOP-QQ597UPT:~$ systemctl cat dev-hugepages.mount
# /usr/lib/systemd/system/dev-hugepages.mount
#  SPDX-License-Identifier: LGPL-2.1-or-later
#
#  This file is part of systemd.
#
#  systemd is free software; you can redistribute it and/or mod>
#  under the terms of the GNU Lesser General Public License as >
#  the Free Software Foundation; either version 2.1 of the Lice>
#  (at your option) any later version.

[Unit]
Description=Huge Pages File System
Documentation=https://docs.kernel.org/admin-guide/mm/hugetlbpag>
Documentation=https://www.freedesktop.org/wiki/Software/systemd>
DefaultDependencies=no
Before=sysinit.target
ConditionPathExists=/sys/kernel/mm/hugepages
ConditionCapability=CAP_SYS_ADMIN
ConditionVirtualization=!private-users

[Mount]
What=hugetlbfs
Where=/dev/hugepages
Type=hugetlbfs
Options=nosuid,nodev

galihcandra@LAPTOP-QQ597UPT:~$ systemctl cat sys-kernel-config.mount
# /usr/lib/systemd/system/sys-kernel-config.mount
#  SPDX-License-Identifier: LGPL-2.1-or-later
#
#  This file is part of systemd.
#
#  systemd is free software; you can redistribute it and/or mod>
#  under the terms of the GNU Lesser General Public License as >
#  the Free Software Foundation; either version 2.1 of the Lice>
#  (at your option) any later version.

[Unit]
Description=Kernel Configuration File System
Documentation=https://docs.kernel.org/filesystems/configfs.html
Documentation=https://www.freedesktop.org/wiki/Software/systemd>
DefaultDependencies=no
ConditionPathExists=/sys/kernel/config
ConditionCapability=CAP_SYS_RAWIO
Before=sysinit.target

# These dependencies are used to make certain that the module i>
# loaded. Indeed udev starts this unit when it receives an ueve>
# module but the kernel sends it too early, ie before the init(>
# is fully operational and /sys/kernel/config is created, see i>

After=modprobe@configfs.service
Requires=modprobe@configfs.service

[Mount]
What=configfs
Where=/sys/kernel/config
Type=configfs

galihcandra@LAPTOP-QQ597UPT:~$ systemctl cat systemd-sysctl.service
# /usr/lib/systemd/system/systemd-sysctl.service
#  SPDX-License-Identifier: LGPL-2.1-or-later
#
#  This file is part of systemd.
#
#  systemd is free software; you can redistribute it and/or mod>
#  under the terms of the GNU Lesser General Public License as >
#  the Free Software Foundation; either version 2.1 of the Lice>
#  (at your option) any later version.

[Unit]
Description=Apply Kernel Variables
Documentation=man:systemd-sysctl.service(8) man:sysctl.d(5)
DefaultDependencies=no
Conflicts=shutdown.target
After=systemd-modules-load.service
Before=sysinit.target shutdown.target
ConditionPathIsReadWrite=/proc/sys/net/

[Service]
Type=oneshot
RemainAfterExit=yes
ExecStart=/usr/lib/systemd/systemd-sysctl
TimeoutSec=90s
ImportCredential=sysctl.*

Penjelasan:
Nama Layanan	    Waktu Inisialisasi	Fungsi
dev-hugepages.mount	992ms	        Melakukan mount filesystem hugepages yang digunakan untuk optimasi manajemen memori besar pada Linux.
sys-kernel-config.mount	969ms	        Me-mount filesystem /sys/kernel/config untuk konfigurasi kernel secara dinamis melalui configfs.
systemd-sysctl.service	912ms	        Mengatur parameter kernel Linux dari file konfigurasi sysctl.conf saat booting sistem.
```

## 1.2 Mengelola Layanan dengan systemctl

## Praktek 12.2: Kelola Layanan SSH
```bash
systemctl status ssh
systemctl is-active ssh
systemctl is-enabled ssh
sudo systemctl restart ssh
systemctl status ssh
systemctl list-dependencies ssh
systemctl --failed

Output:
galihcandra@LAPTOP-QQ597UPT:~$ systemctl status ssh
○ ssh.service - OpenBSD Secure Shell server
     Loaded: loaded (/usr/lib/systemd/system/ssh.service; disab>
     Active: inactive (dead)
TriggeredBy: ● ssh.socket
       Docs: man:sshd(8)
             man:sshd_config(5)

galihcandra@LAPTOP-QQ597UPT:~$ systemctl is-active ssh
inactive

galihcandra@LAPTOP-QQ597UPT:~$ systemctl is-enabled ssh
disabled

galihcandra@LAPTOP-QQ597UPT:~$ sudo systemctl restart ssh
[sudo] password for galihcandra:

galihcandra@LAPTOP-QQ597UPT:~$ systemctl status ssh
● ssh.service - OpenBSD Secure Shell server
     Loaded: loaded (/usr/lib/systemd/system/ssh.service; disab>
     Active: active (running) since Tue 2026-05-19 22:14:12 WIB>
TriggeredBy: ● ssh.socket
       Docs: man:sshd(8)
             man:sshd_config(5)
    Process: 771 ExecStartPre=/usr/sbin/sshd -t (code=exited, s>
   Main PID: 772 (sshd)
      Tasks: 1 (limit: 2165)
     Memory: 3.9M (peak: 4.0M)
        CPU: 112ms
     CGroup: /system.slice/ssh.service
             └─772 "sshd: /usr/sbin/sshd -D [listener] 0 of 10->

May 19 22:14:12 LAPTOP-QQ597UPT systemd[1]: Starting ssh.servic>
May 19 22:14:12 LAPTOP-QQ597UPT sshd[772]: Server listening on >
May 19 22:14:12 LAPTOP-QQ597UPT sshd[772]: Server listening on >
May 19 22:14:12 LAPTOP-QQ597UPT systemd[1]: Started ssh.service>
galihcandra@LAPTOP-QQ597UPT:~$ systemctl list-dependencies ssh
ssh.service
● ├─ssh.socket
● ├─system.slice
● └─sysinit.target
○   ├─apparmor.service
●   ├─dev-hugepages.mount
●   ├─dev-mqueue.mount
●   ├─keyboard-setup.service
●   ├─kmod-static-nodes.service
○   ├─ldconfig.service
○   ├─proc-sys-fs-binfmt_misc.automount
●   ├─setvtrgb.service
●   ├─sys-fs-fuse-connections.mount
●   ├─sys-kernel-config.mount
●   ├─sys-kernel-debug.mount
●   ├─sys-kernel-tracing.mount
●   ├─systemd-ask-password-console.path
●   ├─systemd-binfmt.service
○   ├─systemd-firstboot.service
○   ├─systemd-hwdb-update.service
○   ├─systemd-journal-catalog-update.service
●   ├─systemd-journal-flush.service
●   ├─systemd-journald.service
○   ├─systemd-machine-id-commit.service
●   ├─systemd-modules-load.service
○   ├─systemd-pcrmachine.service
○   ├─systemd-pcrphase-sysinit.service
○   ├─systemd-pcrphase.service
○   ├─systemd-pstore.service
○   ├─systemd-random-seed.service
○   ├─systemd-repart.service
galihcandra@LAPTOP-QQ597UPT:~$ systemctl --failed
  UNIT LOAD ACTIVE SUB DESCRIPTION

0 loaded units listed.
```

### Tantangan
```bash
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week12/scripts$ nano daftar-layanan.txt
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week12/scripts$ nano cek-layanan.sh
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week12/scripts$ chmod +x cek-layanan.sh
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week12/scripts$ ./cek-layanan.sh
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week12/scripts$ cat laporan-layanan.log
[Tue May 19 22:19:04 WIB 2026] ssh: active
[Tue May 19 22:19:04 WIB 2026] cron: active
[Tue May 19 22:19:04 WIB 2026] rsyslog: active

Isi Script:
#!/bin/bash

while read layanan
do
    STATUS=$(systemctl is-active $layanan)

    echo "[$(date)] $layanan: $STATUS" >> laporan-layanan.log

done < daftar-layanan.txt
```

## 1.3 Membuat Berkas Unit Kustom

## Praktek 12.3: Buat Layanan Sederhana dari Skrip Bash
```bash
cd ~/Kuliah/Sem\ 2/praktikum-os/

mkdir -p week12-services

cd week12-services

mkdir -p situs-demo

cat > situs-demo/index.html <<EOF
<!DOCTYPE html>
<html>
<body>
<h1>Halo dari layanan systemd kustom!</h1>
<p>Layanan ini dibuat pada praktek Bab 10.</p>
</body>
</html>
EOF

cat > jalankan-server.sh <<EOF
#!/bin/bash

DIREKTORI="\$HOME/Kuliah/Sem 2/praktikum-os/week12-services/situs-demo"
PORT=9090

echo "Memulai server di port \$PORT..."

exec python3 -m http.server \$PORT --directory "\$DIREKTORI"
EOF

chmod +x jalankan-server.sh

cat > demo-web.service <<EOF
[Unit]
Description=Demo Web Server Praktek Bab 10
After=network.target

[Service]
Type=simple
User=galihcandra
WorkingDirectory=/home/galihcandra/Kuliah/Sem 2/praktikum-os/week12-services/situs-demo
ExecStart=/usr/bin/python3 -m http.server 9090
Restart=on-failure
RestartSec=3s

[Install]
WantedBy=multi-user.target
EOF

sudo cp demo-web.service /etc/systemd/system/demo-web.service

sudo systemctl daemon-reload

sudo systemctl start demo-web

systemctl status demo-web

curl http://localhost:9090

systemctl status demo-web | grep "Main PID"

sudo kill -9 $(systemctl show demo-web --property=MainPID --value)

sleep 5

systemctl status demo-web

sudo systemctl disable --now demo-web

sudo rm /etc/systemd/system/demo-web.service

sudo systemctl daemon-reload



Output:
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os$ mkdir week12-services
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os$ cd week12-services
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week12-services$ mkdir -p situs-demo
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week12-services$ nano situs-demo/index.html
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week12-services$ nano jalankan-server.sh
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week12-services$ chmod +x jalankan-server.sh
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week12-services$ nano demo-web.service
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week12-services$ nano demo-web.service
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week12-services$ sudo cp ~/Kuliah/Sem\ 2/praktikum-os/week12-services/demo-web.service /etc/systemd/system/
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week12-services$ sudo systemctl daemon-reload
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week12-services$ sudo systemctl start demo-web
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week12-services$ systemctl status demo-web
● demo-web.service - Demo Web Server Praktek Bab 10
     Loaded: loaded (/etc/systemd/system/demo-web.service; disa>
     Active: active (running) since Tue 2026-05-19 22:42:46 WIB>
   Main PID: 1361 (python3)
      Tasks: 1 (limit: 2165)
     Memory: 9.3M (peak: 9.6M)
        CPU: 135ms
     CGroup: /system.slice/demo-web.service
             └─1361 /usr/bin/python3 -m http.server 9090

May 19 22:42:46 LAPTOP-QQ597UPT systemd[1]: Started demo-web.se>
lines 1-11/11 (END)
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week12-services$ curl http://localhost:9090
<!DOCTYPE html>
<html>
<body>
<h1>Halo dari layanan systemd kustom!</h1>
<p>Layanan ini dibuat pada praktek Bab 10.</p>
</body>
</html>
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week12-services$ systemctl status demo-web | grep "Main PID"
   Main PID: 1361 (python3)
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week12-services$ sudo kill -9 $(systemctl show demo-web --property=MainPID --value)
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week12-services$ sleep 5
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week12-services$ systemctl status demo-web
● demo-web.service - Demo Web Server Praktek Bab 10
     Loaded: loaded (/etc/systemd/system/demo-web.service; disa>
     Active: active (running) since Tue 2026-05-19 22:44:16 WIB>
   Main PID: 1373 (python3)
      Tasks: 1 (limit: 2165)
     Memory: 13.1M (peak: 13.4M)
        CPU: 367ms
     CGroup: /system.slice/demo-web.service
             └─1373 /usr/bin/python3 -m http.server 9090

May 19 22:44:16 LAPTOP-QQ597UPT systemd[1]: demo-web.service: S>
May 19 22:44:16 LAPTOP-QQ597UPT systemd[1]: Started demo-web.se>
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week12-services$ sudo systemctl disable --now demo-web
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week12-services$ sudo rm /etc/systemd/system/demo-web.service
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week12-services$ sudo systemctl daemon-reload
```

### Tantangan
```bash
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week12-services$ sudo nano /etc/systemd/system/demo-web.service
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week12-services$ sudo systemctl daemon-reload
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week12-services$ sudo systemctl enable --now demo-web
Created symlink /etc/systemd/system/multi-user.target.wants/demo-web.service → /etc/systemd/system/demo-web.service.
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week12-services$ systemctl status demo-web
● demo-web.service - Demo Web Server Praktek Bab 10
     Loaded: loaded (/etc/systemd/system/demo-web.service; enab>
     Active: active (running) since Tue 2026-05-19 22:49:39 WIB>
   Main PID: 1533 (python3)
      Tasks: 1 (limit: 2165)
     Memory: 13.2M (peak: 13.4M)
        CPU: 409ms
     CGroup: /system.slice/demo-web.service
             └─1533 /usr/bin/python3 -m http.server 9091

May 19 22:49:39 LAPTOP-QQ597UPT systemd[1]: Started demo-web.se>
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week12-services$ ss -tlnp | grep 9091
LISTEN 0      5             0.0.0.0:9091      0.0.0.0:*    users:(("python3",pid=1533,fd=3))
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week12-services$ curl http://localhost:9091
<!DOCTYPE html>
<html>
<body>
<h1>Halo dari layanan systemd kustom!</h1>
<p>Layanan ini dibuat pada praktek Bab 10.</p>
</body>
</html>
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week12-services$ systemctl status demo-web | grep "Main PID"
   Main PID: 1533 (python3)
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week12-services$ sudo kill -9 $(systemctl show demo-web --property=MainPID --value)
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week12-services$ sleep 5
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week12-services$ systemctl status demo-web
● demo-web.service - Demo Web Server Praktek Bab 10
     Loaded: loaded (/etc/systemd/system/demo-web.service; enab>
     Active: active (running) since Tue 2026-05-19 22:50:44 WIB>
   Main PID: 1548 (python3)
      Tasks: 1 (limit: 2165)
     Memory: 1.2M (peak: 1.2M)
        CPU: 156ms
     CGroup: /system.slice/demo-web.service
             └─1548 /usr/bin/python3 -m http.server 9091

May 19 22:50:44 LAPTOP-QQ597UPT systemd[1]: demo-web.service: S>
May 19 22:50:44 LAPTOP-QQ597UPT systemd[1]: Started demo-web.se>
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week12-services$ sleep 6
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week12-services$ systemctl status demo-web
● demo-web.service - Demo Web Server Praktek Bab 10
     Loaded: loaded (/etc/systemd/system/demo-web.service; enab>
     Active: active (running) since Tue 2026-05-19 22:50:44 WIB>
   Main PID: 1548 (python3)
      Tasks: 1 (limit: 2165)
     Memory: 13.1M (peak: 13.5M)
        CPU: 446ms
     CGroup: /system.slice/demo-web.service
             └─1548 /usr/bin/python3 -m http.server 9091

May 19 22:50:44 LAPTOP-QQ597UPT systemd[1]: demo-web.service: S>
May 19 22:50:44 LAPTOP-QQ597UPT systemd[1]: Started demo-web.se>
lines 1-12/12 (END)

Isi script modifikasi:
[Unit]
Description=Demo Web Server Praktek Bab 10
After=network.target

[Service]
Type=simple
User=galihcandra
WorkingDirectory=/home/galihcandra/Kuliah/Sem 2/praktikum-os/week12-services/situs-demo

Environment="PORT=9091"

ExecStart=/usr/bin/python3 -m http.server ${PORT}

Restart=on-failure
RestartSec=10s

[Install]
WantedBy=multi-user.target


Perbedaan perilaku dibanding versi sebelumnya terdapat pada waktu restart yang awalnya 3 sec menjadi 10 sec, dan perubahan enviroment port yang awalnya 9090 menjadi 9091.
```

## 1.4 Logging dengan journalctl

## Praktek 12.4: Filter dan Analisis Log Layanan
```bash
journalctl -u ssh --since "1 hour ago" --no-pager
journalctl -b -p err --no-pager
journalctl -u ssh -f
ssh localhost // terminal 2
journalctl -u ssh --since today --no-pager > log-ssh-hari-ini.txt
wc -l log-ssh-hari-ini.txt
grep -i "error\|failed" log-ssh-hari-ini.txt | head -20

Output:
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week12-services$ journalctl -u ssh --since "1 hour ago" --no-pager
May 19 22:14:12 LAPTOP-QQ597UPT systemd[1]: Starting ssh.service - OpenBSD Secure Shell server...
May 19 22:14:12 LAPTOP-QQ597UPT sshd[772]: Server listening on 0.0.0.0 port 22.
May 19 22:14:12 LAPTOP-QQ597UPT sshd[772]: Server listening on :: port 22.
May 19 22:14:12 LAPTOP-QQ597UPT systemd[1]: Started ssh.service - OpenBSD Secure Shell server.
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week12-services$ journalctl -b -p err --no-pager | head -n 5
May 19 20:25:53 LAPTOP-QQ597UPT kernel: PCI: Fatal: No config space access function found
May 19 20:25:53 LAPTOP-QQ597UPT unknown: WSL (175) ERROR: CheckConnection: getaddrinfo() failed: -5
May 19 20:25:53 LAPTOP-QQ597UPT kernel: misc dxg: dxgk: dxgkio_is_feature_enabled: Ioctl failed: -22
May 19 20:25:53 LAPTOP-QQ597UPT kernel: misc dxg: dxgk: dxgkio_query_adapter_info: Ioctl failed: -22
May 19 20:25:53 LAPTOP-QQ597UPT kernel: misc dxg: dxgk: dxgkio_query_adapter_info: Ioctl failed: -22
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week12-services$ journalctl -u ssh -f
May 19 22:14:12 LAPTOP-QQ597UPT systemd[1]: Starting ssh.service - OpenBSD Secure Shell server...
May 19 22:14:12 LAPTOP-QQ597UPT sshd[772]: Server listening on 0.0.0.0 port 22.
May 19 22:14:12 LAPTOP-QQ597UPT sshd[772]: Server listening on :: port 22.
May 19 22:14:12 LAPTOP-QQ597UPT systemd[1]: Started ssh.service - OpenBSD Secure Shell server.

Terminal 2:
galihcandra@LAPTOP-QQ597UPT:~$ ssh localhost
The authenticity of host 'localhost (127.0.0.1)' can't be established.
ED25519 key fingerprint is SHA256:/UAZ6xPLVvdbL/0WGN5yttUMBijQZHsEJfbDh4HgN1U.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added 'localhost' (ED25519) to the list of known hosts.
galihcandra@localhost's password:

Terminal 1:
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week12-services$ journalctl -u ssh -f
May 19 22:14:12 LAPTOP-QQ597UPT systemd[1]: Starting ssh.service - OpenBSD Secure Shell server...
May 19 22:14:12 LAPTOP-QQ597UPT sshd[772]: Server listening on 0.0.0.0 port 22.
May 19 22:14:12 LAPTOP-QQ597UPT sshd[772]: Server listening on :: port 22.
May 19 22:14:12 LAPTOP-QQ597UPT systemd[1]: Started ssh.service - OpenBSD Secure Shell server.
May 19 23:02:26 LAPTOP-QQ597UPT sshd[1669]: Accepted password for galihcandra from 127.0.0.1 port 59476 ssh2
May 19 23:02:26 LAPTOP-QQ597UPT sshd[1669]: pam_unix(sshd:session): session opened for user galihcandra(uid=1000) by galihcandra(uid=0)
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week12-services$ journalctl -u ssh --since today --no-pager > log-ssh-hari-ini.txt
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week12-services$ wc -l log-ssh-hari-ini.txt
6 log-ssh-hari-ini.txt
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week12-services$ grep -i "error\|failed" log-ssh-hari-ini.txt | head -20
```

### Tantangan
```bash
Perintah lengkap:
journalctl -u ssh -p err --since "24 hours ago" --no-pager > error-ssh-24jam.txt
wc -l error-ssh-24jam.txt
sort error-ssh-24jam.txt | uniq -c | sort -rn | head -10

Output:
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week12-services$ journalctl -u ssh -p err --since "24 hours ago" --no-pager > error-ssh-24jam.txt
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week12-services$ wc -l error-ssh-24jam.txt
1 error-ssh-24jam.txt
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week12-services$ sort error-ssh-24jam.txt | uniq -c | sort -rn | head -10
      1 -- No entries --
```

## 1.5 Konfigurasi Layanan Jaringan

## Praktek 12.5: Konfigurasi SSH Server
```bash

```

## 1.6 Rangkuman
Dalam bab ini, kamu telah mempelajari:
• Evolusi init system: Linux berevolusi dari SysV init berbasis skrip berurutan, melalui Upstart berbasis event, ke systemd modern yang menjalankan layanan secara paralel dengan manajemen
dependensi eksplisit.
• Tipe unit systemd: .service untuk proses latar belakang, .socket untuk endpoint jaringan,
.timer untuk tugas terjadwal, .target untuk pengelompokan.
• systemctl runtime: start, stop, restart, reload, dan status untuk mengontrol layanan
yang sedang berjalan; enable/disable untuk auto-start saat boot; mask/unmask untuk blokir
total.
• Berkas unit kustom: struktur [Unit], [Service], [Install]; field penting seperti ExecStart,
Restart=on-failure, RestartSec, User; selalu jalankan daemon-reload setelah mengubah berkas unit.
• journalctl: filter log per unit (-u), per waktu (–since), per prioritas (-p), mode follow (-f),
dan ekspor ke berkas dengan –no-pager.
• Konfigurasi SSH: berkas konfigurasi di /etc/ssh/sshd_config; alur aman ubah konfigurasi:
backup, edit, validasi dengan sshd -t, lalu reload; verifikasi port aktif dengan ss -tlnp.

## 1.7 Latihan

### Latihan 12.1 Audit Layanan dan Analisis Boot
Lakukan audit menyeluruh terhadap layanan yang berjalan di sistem.
1. Jalankan systemctl list-units –type=service –state=running dan catat semua
layanan aktif. Pilih tiga layanan yang kamu kenal, periksa status masing-masing dengan
systemctl status, dan jelaskan fungsinya.
2. Jalankan systemd-analyze blame dan identifikasi lima layanan dengan waktu inisialisasi
terlama. Tampilkan hasilnya menggunakan pipeline: systemd-analyze blame | head -5.
3. Jalankan systemctl –failed dan dokumentasikan hasilnya. Jika ada layanan yang gagal, cari
tahu penyebabnya dengan journalctl -u nama-layanan -n 30.

Jawaban:
```bash

```

### Latihan 12.2 Layanan Kustom dengan Restart Otomatis
Buat layanan systemd kustom yang mendemonstrasikan fitur restart otomatis.
1. Buat skrip Bash (referensi Bab 7) bernama monitor-disk.sh yang setiap 30 detik menuliskan
penggunaan disk ke berkas log. Gunakan df -h dan date.
2. Buat berkas unit /etc/systemd/system/monitor-disk.service untuk menjalankan skrip
tersebut dengan konfigurasi: Restart=always, RestartSec=5s, dan berjalan sebagai pengguna kamu sendiri.
3. Aktifkan dan jalankan layanan. Verifikasi dengan systemctl status dan pastikan log masuk
ke journal.
4. Simulasikan crash dengan membunuh proses secara paksa (kill -9), tunggu 10 detik, dan
verifikasi bahwa layanan hidup kembali secara otomatis.
5. Bersihkan: nonaktifkan layanan dan hapus berkas unit setelah selesai.

Jawaban:
```bash

```

### Latihan 12.3 Investigasi Log dan Keamanan SSH
Analisis log sistem dan tingkatkan keamanan konfigurasi SSH.
1. Gunakan journalctl -b -p err untuk menemukan semua error sejak boot terakhir. Simpan
hasilnya ke berkas dan hitung jumlah baris dengan wc -l.
2. Lakukan tiga perubahan keamanan pada /etc/ssh/sshd_config: tambahkan PermitRootLogin
no, MaxAuthTries 3, dan LoginGraceTime 30. Ikuti alur aman: backup, edit, validasi sshd
-t, reload.
3. Setelah reload, verifikasi tiga hal: layanan masih berjalan (systemctl status ssh), port
masih mendengarkan (ss -tlnp | grep ssh), dan konfigurasi baru terbaca (grep -E
"PermitRoot|MaxAuth|GraceTime" /etc/ssh/sshd_config).
4. Kembalikan konfigurasi SSH ke kondisi semula menggunakan berkas backup.

Jawaban:
```bash

```