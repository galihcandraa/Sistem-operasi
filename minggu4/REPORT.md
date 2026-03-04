# LAPORAN JOBSHEET 4
Operasi File dan Struktur Direktory

* Nama: Galih Candra Kirana
* NIM: 254107020078
* Kelas: TI-1G

## TUGAS PENDAHULUAN:
### Jawablah pertanyaan-pertanyaan di bawah ini :
1. Apa yang dimaksud perintah-perintah direktory : pwd, cd, mkdir, rmdir.
2. Apa yang dimaksud perintah-perintah manipulasi file : cp, mv dan rm (sertakan 
format yang digunakan)
3. Jelaskan perbedaan Symbolic link menggunakan hard link (direct) dan soft link (indirect).
4. Tuliskan maksud perintah-perintah : file, find, which, locate dan grep

### Jawaban
1. Penjelasan perintah-perintah directory tersebut.
   * pwd(print working directory): digunakan untuk mengecek direktori  saat ini.
   * cd (change directory): digunakan untuk mengganti direktori.
   * mkdir (make directory): digunakan untuk membuat direktori baru.
   * rmdir (remove directory): digunakan untuk menghapus direktori yang kosong.
  
2. Penjelasan perintah-perintah manipulasi file.
   * cp (copy): digunakan untuk menyalin direktori/file.
   * mv (move): digunakan untuk memindahkan direktori/file.
   * rm (remove): digunakan untuk menghapus file.
  
3. Perbedaan Symbolic link menggunakan hard link dan soft link.
   * Soft link dapat dibuat pada media disk atau partisi yang berbeda karena hanya menyimpan alamat atau path dari file asli. Sedangkan hard link terbatas pada partisi disk yang sama karena menggunakan inode yang sama dengan file aslinya.
  
4. Maksud dari perintah tersebut.
   * file: digunakan untuk mengetahui jenis atau tipe suatu file.
   * find: digunakan untuk mencari direktori atau file berdasarkan kriteria tertentu.
   * which: digunakan untuk mengetahui lokasi file executable dari suatu perintah.

## LATIHAN:
1. Cobalah urutan perintah berikut :
    ```bash
    $ cd
    $ pwd
    $ ls –al
    $ cd .
    $ pwd
    $ cd ..
    $ pwd
    $ ls -al
    $ cd ..
    $ pwd
    $ ls -al
    $ cd /etc
    $ ls –al | more
    $ cat passwd
    $ cd –
    $ pwd
    ```
   output
   ```bash
   galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week04$ cd
   galihcandra@LAPTOP-QQ597UPT:~$ pwd
   /home/galihcandra
   galihcandra@LAPTOP-QQ597UPT:~$ ls -al
   total 120
   -rw-r--r--  1 root        root           17 Feb 19 07:23 -
   drwxr-x--- 13 galihcandra galihcandra  4096 Mar  4 11:14 .
   drwxr-xr-x  3 root        root         4096 Feb 11 15:19 ..
   -rw-------  1 galihcandra galihcandra 14119 Mar  4 15:15 .bash_history
   -rw-r--r--  1 galihcandra galihcandra   220 Feb 11 15:19 .bash_logout
   -rw-r--r--  1 galihcandra galihcandra  3771 Feb 11 15:19 .bashrc
   drwx------  3 galihcandra galihcandra  4096 Feb 11 19:37 .cache
   drwx------  5 galihcandra galihcandra  4096 Feb 22 09:08 .config
   drwxr-xr-x  4 galihcandra galihcandra  4096 Feb 11 21:50 .dbclient
   drwxr-xr-x  3 galihcandra galihcandra  4096 Feb 11 19:38 .dotnet
   -rw-r--r--  1 galihcandra galihcandra   156 Feb 12 15:14 .gitconfig
   drwxr-xr-x  2 galihcandra galihcandra  4096 Feb 19 05:57 .landscape
   -rw-------  1 galihcandra galihcandra    20 Mar  4 11:14 .lesshst
   drwxr-xr-x  3 galihcandra galihcandra  4096 Feb 17 15:29 .local
   -rw-rw-r--  1 galihcandra galihcandra     0 Mar  4 10:27 .motd_shown
   -rw-r--r--  1 galihcandra galihcandra   807 Feb 11 15:19 .profile
   drwxr-xr-x  2 galihcandra galihcandra  4096 Feb 11 20:11 .redhat
   -rw-r--r--  1 galihcandra galihcandra     0 Feb 11 19:11 .sudo_as_admin_successful
   drwxr-xr-x  5 galihcandra galihcandra  4096 Feb 11 19:37 .vscode-server
   drwxr-xr-x  3 galihcandra galihcandra  4096 Feb 18 11:44 Kuliah
   drwxr-xr-x  3 galihcandra galihcandra  4096 Feb 26 08:11 Latihan
   drwxr-xr-x  3 galihcandra galihcandra  4096 Feb 16 10:55 Project
   -rw-r--r--  1 root        root           17 Feb 19 07:23 conf
   -rw-r--r--  1 root        root            7 Feb 19 07:18 d
   -rw-r--r--  1 root        root            7 Feb 19 07:18 etc
   -rw-r--r--  1 root        root            7 Feb 19 07:18 load
   -rw-r--r--  1 root        root           17 Feb 19 07:23 loop
   -rw-r--r--  1 root        root           17 Feb 19 07:23 modprobe
   -rw-r--r--  1 root        root            7 Feb 19 07:18 modules
   galihcandra@LAPTOP-QQ597UPT:~$ cd .
   galihcandra@LAPTOP-QQ597UPT:~$ pwd
   /home/galihcandra
   galihcandra@LAPTOP-QQ597UPT:~$ cd ..
   galihcandra@LAPTOP-QQ597UPT:/home$ pwd
   /home
   galihcandra@LAPTOP-QQ597UPT:/home$ ls -al
   total 12
   drwxr-xr-x  3 root        root        4096 Feb 11 15:19 .
   drwxr-xr-x 32 root        root        4096 Mar  4 15:18 ..
   drwxr-x--- 13 galihcandra galihcandra 4096 Mar  4 11:14 galihcandra
   galihcandra@LAPTOP-QQ597UPT:/home$ cd ..
   galihcandra@LAPTOP-QQ597UPT:/$ pwd
   /
   galihcandra@LAPTOP-QQ597UPT:/$ ls -al
   total 2844
   drwxr-xr-x  32 root root    4096 Mar  4 15:18 .
   drwxr-xr-x  32 root root    4096 Mar  4 15:18 ..
   lrwxrwxrwx   1 root root       7 Apr 22  2024 bin -> usr/bin
   drwxr-xr-x   2 root root    4096 Feb 26  2024 bin.usr-is-merged
   drwxr-xr-x   2 root root    4096 Apr 22  2024 boot
   drwxr-xr-x  15 root root    3860 Mar  4 15:19 dev
   drwxr-xr-x  96 root root    4096 Mar  4 15:25 etc
   drwxr-xr-x   3 root root    4096 Feb 11 15:19 home
   -rwxr-xr-x   1 root root 2781568 Dec 12 08:58 init
   lrwxrwxrwx   1 root root       7 Apr 22  2024 lib -> usr/lib
   drwxr-xr-x   2 root root    4096 Apr  8  2024 lib.usr-is-merged
   lrwxrwxrwx   1 root root       9 Apr 22  2024 lib64 -> usr/lib64
   drwx------   2 root root   16384 Feb 11 15:17 lost+found
   drwxr-xr-x   2 root root    4096 Aug  5  2025 media
   drwxr-xr-x   6 root root    4096 Feb 11 15:18 mnt
   drwxr-xr-x   2 root root    4096 Aug  5  2025 opt
   dr-xr-xr-x 192 root root       0 Mar  4 15:18 proc
   drwx------   3 root root    4096 Aug  5  2025 root
   drwxr-xr-x  19 root root     560 Mar  4 15:19 run
   lrwxrwxrwx   1 root root       8 Apr 22  2024 sbin -> usr/sbin
   drwxr-xr-x   2 root root    4096 Mar 31  2024 sbin.usr-is-merged
   drwxr-xr-x   2 root root    4096 Feb 11 15:18 snap
   drwxr-xr-x   2 root root    4096 Aug  5  2025 srv
   dr-xr-xr-x  13 root root       0 Mar  4 15:18 sys
   drwxrwxrwt   8 root root    4096 Mar  4 15:20 tmp
   drwxr-xr-x  12 root root    4096 Aug  5  2025 usr
   drwxr-xr-x  13 root root    4096 Feb 11 15:18 var
   drwx------   2 root root    4096 Mar  1 13:49 wslAGnJgi
   drwx------   2 root root    4096 Feb 18 06:04 wslDhAjga
   drwx------   2 root root    4096 Mar  1 13:49 wslFhHjCB
   drwx------   2 root root    4096 Feb 18 06:04 wslNbiiha
   drwx------   2 root root    4096 Mar  1 13:49 wsldLciDB
   drwx------   2 root root    4096 Feb 18 06:04 wsldlheda
   drwx------   2 root root    4096 Feb 18 06:04 wsleHJBia
   drwx------   2 root root    4096 Feb 18 06:04 wslhjcKEK
   drwx------   2 root root    4096 Mar  1 13:49 wsllMpKoB
   drwx------   2 root root    4096 Mar  1 13:49 wsloIIinI
   galihcandra@LAPTOP-QQ597UPT:/$ cd /etc
   galihcandra@LAPTOP-QQ597UPT:/etc$ ls -al | more
   total 888
   drwxr-xr-x 96 root root       4096 Mar  4 15:25 .
   drwxr-xr-x 32 root root       4096 Mar  4 15:18 ..
   drwxr-xr-x  3 root root       4096 Feb 11 19:47 .java
   -rw-------  1 root root          0 Aug  5  2025 .pwd.lock
   -rw-r--r--  1 root root        862 Aug  5  2025 .resolv.conf.sys
   temd-resolved.bak
   -rw-r--r--  1 root root        208 Aug  5  2025 .updated
   drwxr-xr-x  2 root root       4096 Feb 20 23:05 ImageMagick-6
   drwxr-xr-x  2 root root       4096 Feb 11 19:18 PackageKit
   drwxr-xr-x  9 root root       4096 Feb 20 23:04 X11
   -rw-r--r--  1 root root       3444 Jul  6  2023 adduser.conf
   drwxr-xr-x  2 root root      12288 Mar  4 11:18 alternatives
   drwxr-xr-x  2 root root       4096 Feb 11 19:17 apparmor
   drwxr-xr-x  9 root root      12288 Feb 11 19:18 apparmor.d
   drwxr-xr-x  3 root root       4096 Aug  5  2025 apport
   drwxr-xr-x  8 root root       4096 Aug  5  2025 apt
   -rw-r--r--  1 root root       2319 Mar 31  2024 bash.bashrc
   -rw-r--r--  1 root root         45 Jan 25  2020 bash_completion
   drwxr-xr-x  2 root root       4096 Aug  5  2025 bash_completion.
   d
   -rw-r--r--  1 root root        367 Aug  2  2022 bindresvport.bla
   cklist
   drwxr-xr-x  2 root root       4096 Apr 19  2024 binfmt.d
   drwxr-xr-x  2 root root       4096 Aug  5  2025 byobu
   drwxr-xr-x  3 root root       4096 Aug  5  2025 ca-certificates
   -rw-r--r--  1 root root       6288 Aug  5  2025 ca-certificates.
   conf
   drwxr-xr-x  5 root root       4096 Feb 22 08:58 cloud
   drwxr-xr-x  2 root root       4096 Aug  5  2025 console-setup
   drwx------  2 root root       4096 Apr 19  2024 credstore
   galihcandra@LAPTOP-QQ597UPT:/etc$ cat passwd
   root:x:0:0:root:/root:/bin/bash
   daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
   bin:x:2:2:bin:/bin:/usr/sbin/nologin
   sys:x:3:3:sys:/dev:/usr/sbin/nologin
   sync:x:4:65534:sync:/bin:/bin/sync
   games:x:5:60:games:/usr/games:/usr/sbin/nologin
   man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
   lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
   mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
   news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
   uucp:x:10:10:uucp:/var/spool/uucp:/usr/sbin/nologin
   proxy:x:13:13:proxy:/bin:/usr/sbin/nologin
   www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin
   backup:x:34:34:backup:/var/backups:/usr/sbin/nologin
   list:x:38:38:Mailing List Manager:/var/list:/usr/sbin/nologin
   irc:x:39:39:ircd:/run/ircd:/usr/sbin/nologin
   _apt:x:42:65534::/nonexistent:/usr/sbin/nologin
   nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin
   systemd-network:x:998:998:systemd Network Management:/:/usr/sbin/nologin
   systemd-timesync:x:996:996:systemd Time Synchronization:/:/usr/sbin/nologin
   dhcpcd:x:100:65534:DHCP Client Daemon,,,:/usr/lib/dhcpcd:/bin/false
   messagebus:x:101:101::/nonexistent:/usr/sbin/nologin
   syslog:x:102:102::/nonexistent:/usr/sbin/nologin
   systemd-resolve:x:991:991:systemd Resolver:/:/usr/sbin/nologin
   uuidd:x:103:103::/run/uuidd:/usr/sbin/nologin
   landscape:x:104:105::/var/lib/landscape:/usr/sbin/nologin
   polkitd:x:990:990:User for polkitd:/:/usr/sbin/nologin
   galihcandra:x:1000:1000:,,,:/home/galihcandra:/bin/bash
   sshd:x:105:65534::/run/sshd:/usr/sbin/nologin
   galihcandra@LAPTOP-QQ597UPT:/etc$ cd -
   /
   galihcandra@LAPTOP-QQ597UPT:/$ pwd
   /
   ```
