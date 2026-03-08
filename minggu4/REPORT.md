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

2. Lanjutkan penelusuran pohon pada sistem file menggunakan cd, ls, pwd dan cat. 
Telusuri direktory /bin, /usr/bin, /sbin, /tmp dan /boot.

   output

   /bin:
   ```bash
   galihcandra@LAPTOP-QQ597UPT:/$ cd /bin
   galihcandra@LAPTOP-QQ597UPT:/bin$ pwd
   /bin
   galihcandra@LAPTOP-QQ597UPT:/bin$ ls -al | more
   total 148864
   drwxr-xr-x  2 root root       40960 Mar  4 11:18 .
   drwxr-xr-x 12 root root        4096 Aug  5  2025 ..
   -rwxr-xr-x  1 root root       14640 Mar 31  2024 411toppm
   -rwxr-xr-x  1 root root       27008 Mar 31  2024 JxrDecApp
   -rwxr-xr-x  1 root root       28440 Mar 31  2024 JxrEncApp
   lrwxrwxrwx  1 root root           4 Feb 11  2024 NF -> col1
   lrwxrwxrwx  1 root root           1 Apr  8  2024 X11 -> .
   -rwxr-xr-x  1 root root       55744 Jun 22  2025 [
   -rwxr-xr-x  1 root root       18744 Aug 15  2025 aa-enabled
   -rwxr-xr-x  1 root root       18744 Aug 15  2025 aa-exec
   -rwxr-xr-x  1 root root       18736 Aug 15  2025 aa-features-abi
   -rwxr-xr-x  1 root root       16422 Jul  3  2025 add-apt-reposit
   ory
   -rwxr-xr-x  1 root root       14720 Sep 16 07:08 addpart
   lrwxrwxrwx  1 root root          26 Dec  3 22:01 addr2line -> x8
   6_64-linux-gnu-addr2line
   lrwxrwxrwx  1 root root          25 Mar 31  2024 animate -> /etc
   /alternatives/animate
   lrwxrwxrwx  1 root root          29 Mar 31  2024 animate-im6 ->
   /etc/alternatives/animate-im6
   -rwxr-xr-x  1 root root       14656 Mar 31  2024 animate-im6.q16
   -rwxr-xr-x  1 root root       12556 Mar 31  2024 anytopnm
   -rwxr-xr-x  1 root root        2322 Apr 18  2024 apport-bug
   -rwxr-xr-x  1 root root       13625 Jul  8  2025 apport-cli
   lrwxrwxrwx  1 root root          10 Jul  8  2025 apport-collect
   -> apport-bug
   -rwxr-xr-x  1 root root        3790 Jul  8  2025 apport-unpack
   -rwxr-xr-x  1 root root       14648 Apr  1  2024 appres
   -rwxr-xr-x  1 root root      141544 Apr  8  2024 appstreamcli
   lrwxrwxrwx  1 root root           6 Apr  8  2024 apropos -> what
   galihcandra@LAPTOP-QQ597UPT:/bin$ cat zmore
   #!/bin/sh

   # Copyright (C) 2001-2002, 2007, 2010-2022 Free Software Foundation, Inc.
   # Copyright (C) 1992, 1993 Jean-loup Gailly

   # This program is free software; you can redistribute it and/or modify
   # it under the terms of the GNU General Public License as published by
   # the Free Software Foundation; either version 3 of the License, or
   # (at your option) any later version.

   # This program is distributed in the hope that it will be useful,
   # but WITHOUT ANY WARRANTY; without even the implied warranty of
   # MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
   # GNU General Public License for more details.

   # You should have received a copy of the GNU General Public License along
   # with this program; if not, write to the Free Software Foundation, Inc.,
   # 51 Franklin Street, Fifth Floor, Boston, MA 02110-1301 USA.

   version="zmore (gzip) 1.12
   Copyright (C) 2010-2018 Free Software Foundation, Inc.
   This is free software.  You may redistribute copies of it under the terms of
   the GNU General Public License <https://www.gnu.org/licenses/gpl.html>.
   There is NO WARRANTY, to the extent permitted by law.

   Written by Jean-loup Gailly."

   usage="Usage: $0 [OPTION]... [FILE]...
   Like 'more', but operate on the uncompressed contents of any compressed FILEs.

   Report bugs to <bug-gzip@gnu.org>."

   case $1 in
   --h*) printf '%s\n' "$usage"   || exit 1; exit;;
   --v*) printf '%s\n' "$version" || exit 1; exit;;
   --) shift;;
   -?*) printf >&2 '%s\n' "$0: $1: unknown option; try '$0 --help' for help"
         exit 1;;
   esac

   if test $# = 0; then
      if test -t 0; then
         printf >&2 '%s\n' "$0: missing operands; try '$0 --help' for help"
         exit 1
      fi
      set -- -
   fi

   for FILE
   do
   test $# -lt 2 ||
      printf '::::::::::::::\n%s\n::::::::::::::\n' "$FILE" || break
   gzip -cdfq -- "$FILE"
   done 2>&1 | eval ${PAGER-more}
   ```

   /usr/bin:
   ```bash
   galihcandra@LAPTOP-QQ597UPT:~$ cd /usr/bin
   galihcandra@LAPTOP-QQ597UPT:/usr/bin$ pwd
   /usr/bin
   galihcandra@LAPTOP-QQ597UPT:/usr/bin$ ls -al | more
   total 148864
   drwxr-xr-x  2 root root       40960 Mar  4 11:18 .
   drwxr-xr-x 12 root root        4096 Aug  5  2025 ..
   -rwxr-xr-x  1 root root       14640 Mar 31  2024 411toppm
   -rwxr-xr-x  1 root root       27008 Mar 31  2024 JxrDecApp
   -rwxr-xr-x  1 root root       28440 Mar 31  2024 JxrEncApp
   lrwxrwxrwx  1 root root           4 Feb 11  2024 NF -> col1
   lrwxrwxrwx  1 root root           1 Apr  8  2024 X11 -> .
   -rwxr-xr-x  1 root root       55744 Jun 22  2025 [
   -rwxr-xr-x  1 root root       18744 Aug 15  2025 aa-enabled
   -rwxr-xr-x  1 root root       18744 Aug 15  2025 aa-exec
   -rwxr-xr-x  1 root root       18736 Aug 15  2025 aa-features-abi
   -rwxr-xr-x  1 root root       16422 Jul  3  2025 add-apt-reposit
   ory
   -rwxr-xr-x  1 root root       14720 Sep 16 07:08 addpart
   lrwxrwxrwx  1 root root          26 Dec  3 22:01 addr2line -> x8
   6_64-linux-gnu-addr2line
   lrwxrwxrwx  1 root root          25 Mar 31  2024 animate -> /etc
   /alternatives/animate
   lrwxrwxrwx  1 root root          29 Mar 31  2024 animate-im6 ->
   /etc/alternatives/animate-im6
   -rwxr-xr-x  1 root root       14656 Mar 31  2024 animate-im6.q16
   -rwxr-xr-x  1 root root       12556 Mar 31  2024 anytopnm
   -rwxr-xr-x  1 root root        2322 Apr 18  2024 apport-bug
   -rwxr-xr-x  1 root root       13625 Jul  8  2025 apport-cli
   lrwxrwxrwx  1 root root          10 Jul  8  2025 apport-collect
   -> apport-bug
   -rwxr-xr-x  1 root root        3790 Jul  8  2025 apport-unpack
   -rwxr-xr-x  1 root root       14648 Apr  1  2024 appres
   -rwxr-xr-x  1 root root      141544 Apr  8  2024 appstreamcli
   lrwxrwxrwx  1 root root           6 Apr  8  2024 apropos -> what
   galihcandra@LAPTOP-QQ597UPT:/usr/bin$ cat zcat
   #!/bin/sh
   # Uncompress files to standard output.

   # Copyright (C) 2007, 2010-2022 Free Software Foundation, Inc.

   # This program is free software; you can redistribute it and/or modify
   # it under the terms of the GNU General Public License as published by
   # the Free Software Foundation; either version 3 of the License, or
   # (at your option) any later version.

   # This program is distributed in the hope that it will be useful,
   # but WITHOUT ANY WARRANTY; without even the implied warranty of
   # MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
   # GNU General Public License for more details.

   # You should have received a copy of the GNU General Public License along
   # with this program; if not, write to the Free Software Foundation, Inc.,
   # 51 Franklin Street, Fifth Floor, Boston, MA 02110-1301 USA.

   version="zcat (gzip) 1.12
   Copyright (C) 2007, 2011-2018 Free Software Foundation, Inc.
   This is free software.  You may redistribute copies of it under the terms of
   the GNU General Public License <https://www.gnu.org/licenses/gpl.html>.
   There is NO WARRANTY, to the extent permitted by law.

   Written by Paul Eggert."

   usage="Usage: $0 [OPTION]... [FILE]...
   Uncompress FILEs to standard output.

   -f, --force       force; read compressed data even from a terminal
   -l, --list        list compressed file contents
   -q, --quiet       suppress all warnings
   -r, --recursive   operate recursively on directories
   -S, --suffix=SUF  use suffix SUF on compressed files
         --synchronous synchronous output (safer if system crashes, but slower)
   -t, --test        test compressed file integrity
   -v, --verbose     verbose mode
         --help        display this help and exit
         --version     display version information and exit

   With no FILE, or when FILE is -, read standard input.

   Report bugs to <bug-gzip@gnu.org>."

   case $1 in
   --help)    printf '%s\n' "$usage"   || exit 1; exit;;
   --version) printf '%s\n' "$version" || exit 1; exit;;
   esac

   exec gzip -cd "$@"
   ```

   /sbin:
   ```bash
   galihcandra@LAPTOP-QQ597UPT:~$ cd /sbin
   galihcandra@LAPTOP-QQ597UPT:/sbin$ pwd
   /sbin
   galihcandra@LAPTOP-QQ597UPT:/sbin$ ls -al | more
   total 14340
   drwxr-xr-x  2 root root     12288 Mar  4 11:18 .
   drwxr-xr-x 12 root root      4096 Aug  5  2025 ..
   -rwxr-xr-x  1 root root     39680 Aug 15  2025 aa-load
   -rwxr-xr-x  1 root root      3225 Aug 15  2025 aa-remove-unknown
   -rwxr-xr-x  1 root root     40000 Aug 15  2025 aa-status
   -rwxr-xr-x  1 root root       137 Apr 12  2024 aa-teardown
   -rwxr-xr-x  1 root root     14904 Apr  8  2024 accessdb
   -rwxr-xr-x  1 root root      1053 Mar 31  2024 add-shell
   -rwxr-xr-x  1 root root      3075 Jan  6 05:01 addgnupghome
   lrwxrwxrwx  1 root root         7 Jul  6  2023 addgroup -> addus
   er
   -rwxr-xr-x  1 root root     55191 Jul  6  2023 adduser
   -rwxr-xr-x  1 root root     60992 Sep 16 07:08 agetty
   -rwxr-xr-x  1 root root   1629848 Aug 15  2025 apparmor_parser
   lrwxrwxrwx  1 root root         9 Aug 15  2025 apparmor_status -
   > aa-status
   -rwxr-xr-x  1 root root      2217 Jan  6 05:01 applygnupgdefault
   s
   -rwxr-xr-x  1 root root     63088 May 28  2025 arp
   -rwxr-xr-x  1 root root     26960 Jul 10  2025 arpd
   -rwxr-xr-x  1 root root     35144 Apr 29  2024 badblocks
   -rwxr-xr-x  1 root root     27856 Oct 15  2024 biosdecode
   -rwxr-xr-x  1 root root     16351 Nov 28  2024 blkdeactivate
   -rwxr-xr-x  1 root root     22912 Sep 16 07:08 blkdiscard
   -rwxr-xr-x  1 root root     55720 Sep 16 07:08 blkid
   -rwxr-xr-x  1 root root     35200 Sep 16 07:08 blkzone
   -rwxr-xr-x  1 root root     35200 Sep 16 07:08 blockdev
   -rwxr-xr-x  1 root root    111096 Jul 10  2025 bridge
   -rwxr-xr-x  1 root root     58456 Feb 20  2025 capsh
   -rwxr-xr-x  1 root root     97008 Sep 16 07:08 cfdisk
   galihcandra@LAPTOP-QQ597UPT:/sbin$ cat ldconfig
   #!/bin/sh

   if  test $# = 0                            \
      && test x"$LDCONFIG_NOTRIGGER" = x        \
   && test x"$DPKG_MAINTSCRIPT_PACKAGE" != x    \
   && dpkg-trigger --check-supported 2>/dev/null
   then
         if dpkg-trigger --no-await ldconfig; then
            if test x"$LDCONFIG_TRIGGER_DEBUG" != x; then
               echo "ldconfig: wrapper deferring update (trigger activated)"
            fi
            exit 0
         fi
   fi

   exec /sbin/ldconfig.real "$@"
   ```

   /tmp:
   ```bash
   galihcandra@LAPTOP-QQ597UPT:~$ cd /tmp
   galihcandra@LAPTOP-QQ597UPT:/tmp$ pwd
   /tmp
   galihcandra@LAPTOP-QQ597UPT:/tmp$ ls -al | more
   total 24
   drwxrwxrwt  7 root root 4096 Mar  4 16:04 .
   drwxr-xr-x 32 root root 4096 Mar  4 15:18 ..
   drwxrwxrwx  2 root root   40 Mar  4 15:19 .X11-unix
   drwx------  2 root root 4096 Mar  4 15:19 snap-private-tmp
   drwx------  3 root root 4096 Mar  4 15:19 systemd-private-61a6ab
   bd1a95419f88be9212e6eb2298-systemd-logind.service-DKq7o8
   drwx------  3 root root 4096 Mar  4 15:19 systemd-private-61a6ab
   bd1a95419f88be9212e6eb2298-systemd-resolved.service-WYLEp3
   drwx------  3 root root 4096 Mar  4 15:19 systemd-private-61a6ab
   bd1a95419f88be9212e6eb2298-systemd-timesyncd.service-00TZgX
   galihcandra@LAPTOP-QQ597UPT:/tmp$ cat snap-private-tmp
   cat: snap-private-tmp: Permission denied   
   ```

   /boot:
   ```bash
   galihcandra@LAPTOP-QQ597UPT:~$ cd /boot
   galihcandra@LAPTOP-QQ597UPT:/boot$ pwd
   /boot
   galihcandra@LAPTOP-QQ597UPT:/boot$ ls -al | more
   total 8
   drwxr-xr-x  2 root root 4096 Apr 22  2024 .
   drwxr-xr-x 32 root root 4096 Mar  4 15:18 ..
   galihcandra@LAPTOP-QQ597UPT:/boot$ ls
   galihcandra@LAPTOP-QQ597UPT:/boot$ cat .
   cat: .: Is a directory
   ```
3. Telusuri direktory /dev. Identifikasi perangkat yang tersedia. Identifikasi tty (termninal) Anda (ketik who am i); siapa pemilih tty Anda (gunakan ls –l).

   output
   ```bash
   galihcandra@LAPTOP-QQ597UPT:/$ cd /dev
   galihcandra@LAPTOP-QQ597UPT:/dev$ ls 
   autofs           hvc2          loop6       ram11   sdc       tty13  tty3   tty46  tty62        vcs2   vcsu6
   block            hvc3          loop7       ram12   sdd       tty14  tty30  tty47  tty63        vcs3   vfio
   bsg              hvc4          mapper      ram13   sg0       tty15  tty31  tty48  tty7         vcs4   vga_arbiter
   btrfs-control    hvc5          mcelog      ram14   sg1       tty16  tty32  tty49  tty8         vcs5   vhost-net
   char             hvc6          mem         ram15   sg2       tty17  tty33  tty5   tty9         vcs6   vhost-vsock
   console          hvc7          mptctl      ram2    sg3       tty18  tty34  tty50  ttyS0        vcsa   virtio-ports
   core             hwrng         mqueue      ram3    shm       tty19  tty35  tty51  ttyS1        vcsa1  vport0p0
   cpu_dma_latency  initctl       net         ram4    snapshot  tty2   tty36  tty52  ttyS2        vcsa2  vport0p1
   cuse             kmsg          null        ram5    snd       tty20  tty37  tty53  ttyS3        vcsa3  vport0p2
   disk             kvm           nvram       ram6    stderr    tty21  tty38  tty54  ttyS4        vcsa4  vsock
   dxg              log           ppp         ram7    stdin     tty22  tty39  tty55  ttyS5        vcsa5  zero
   fd               loop-control  ptmx        ram8    stdout    tty23  tty4   tty56  ttyS6        vcsa6
   full             loop0         ptp0        ram9    tty       tty24  tty40  tty57  ttyS7        vcsu
   fuse             loop1         ptp_hyperv  random  tty0      tty25  tty41  tty58  uinput       vcsu1
   hpet             loop2         pts         rtc     tty1      tty26  tty42  tty59  urandom      vcsu2
   hugepages        loop3         ram0        rtc0    tty10     tty27  tty43  tty6   userfaultfd  vcsu3
   hvc0             loop4         ram1        sda     tty11     tty28  tty44  tty60  vcs          vcsu4
   hvc1             loop5         ram10       sdb     tty12     tty29  tty45  tty61  vcs1         vcsu5
   galihcandra@LAPTOP-QQ597UPT:/dev$ who am i
   galihcandra@LAPTOP-QQ597UPT:/dev$ whoami
   galihcandra
   galihcandra@LAPTOP-QQ597UPT:/dev$ tty
   /dev/pts/5
   galihcandra@LAPTOP-QQ597UPT:/dev$ ls -l /dev/pts/5
   crw--w---- 1 galihcandra tty 136, 5 Mar  8 10:55 /dev/pts/5
   ```

4. Telusuri directory /proc. Tampilkan isi file interrupts, devices,cpuinfo, meminfo dan uptime menggunakan perintah cat. Dapatkah Anda melihat mengapa directory /proc disebut pseudo -filesystem yang memungkinkan akses ke struktur data kernel ? 

   Jawaban:

   Direktori /proc disebut pseudo filesystem karena:
   1. File di dalamnya tidak benar-benar tersimpan di disk.
   2. Isinya dibuat secara dinamis oleh kernel saat diakses.
   3. Digunakan untuk melihat dan mengakses informasi internal kernel dan proses.
   4. Berfungsi sebagai interface antara kernel dan user space.
   
   ```bash
   galihcandra@LAPTOP-QQ597UPT:/$ cd /proc
   galihcandra@LAPTOP-QQ597UPT:/proc$ ls
   1     164   2    379  800        devices        iomem        kpageflags     net           swaps          vmstat
   104   165   215  515  acpi       diskstats      ioports      latency_stats  pagetypeinfo  sys            zoneinfo
   1252  1855  217  528  buddyinfo  dma            irq          loadavg        partitions    sysrq-trigger
   1253  1878  222  557  bus        driver         kallsyms     locks          pressure      sysvipc
   1254  193   234  56   cgroups    dynamic_debug  kcore        meminfo        schedstat     thread-self
   1261  194   238  574  cmdline    execdomains    key-users    misc           scsi          timer_list
   1262  195   241  622  config.gz  fb             keys         modules        self          tty
   1263  196   259  7    consoles   filesystems    kmsg         mounts         slabinfo      uptime
   127   197   337  798  cpuinfo    fs             kpagecgroup  mpt            softirqs      version
   1567  198   341  799  crypto     interrupts     kpagecount   mtrr           stat          vmallocinfo
   galihcandra@LAPTOP-QQ597UPT:/proc$ cat interrupts
            CPU0       CPU1
   8:          0          0   IO-APIC   8-edge      rtc0
   9:          1          0   IO-APIC   9-fasteoi   acpi
   24:          0          1  Hyper-V PCIe MSI 2938026065920-edge      virtio0-config
   25:       1146          0  Hyper-V PCIe MSI 2938026065921-edge      virtio0-virtqueues
   26:          1          0  Hyper-V PCIe MSI 6801751801856-edge      virtio1-config
   27:          0          1  Hyper-V PCIe MSI 6801751801857-edge      virtio1-hiprio
   28:         10          0  Hyper-V PCIe MSI 6801751801858-edge      virtio1-requests.0
   NMI:          0          0   Non-maskable interrupts
   LOC:          0          0   Local timer interrupts
   SPU:          0          0   Spurious interrupts
   PMI:          0          0   Performance monitoring interrupts
   IWI:          0          0   IRQ work interrupts
   RTR:          0          0   APIC ICR read retries
   RES:       1339       1369   Rescheduling interrupts
   CAL:      29816      38207   Function call interrupts
   TLB:          0          0   TLB shootdowns
   TRM:          0          0   Thermal event interrupts
   THR:          0          0   Threshold APIC interrupts
   DFR:          0          0   Deferred Error APIC interrupts
   MCE:          0          0   Machine check exceptions
   MCP:          7          7   Machine check polls
   HYP:      26775       2010   Hypervisor callback interrupts
   HRE:          0          0   Hyper-V reenlightenment interrupts
   HVS:     106482     101490   Hyper-V stimer0 interrupts
   ERR:          0
   MIS:          0
   PIN:          0          0   Posted-interrupt notification event
   NPI:          0          0   Nested posted-interrupt event
   PIW:          0          0   Posted-interrupt wakeup event
   galihcandra@LAPTOP-QQ597UPT:/proc$ cat devices
   Character devices:
   1 mem
   4 /dev/vc/0
   4 tty
   4 ttyS
   5 /dev/tty
   5 /dev/console
   5 /dev/ptmx
   7 vcs
   10 misc
   13 input
   21 sg
   29 fb
   108 ppp
   128 ptm
   136 pts
   226 drm
   229 hvc
   241 intel_mid_scu
   242 nvme-generic
   243 nvme
   244 virtio-portsdev
   245 bsg
   246 watchdog
   247 ptp
   248 pps
   249 rtc
   250 dax
   251 dimmctl
   252 ndctl
   253 tpm
   254 gpiochip

   Block devices:
   1 ramdisk
   7 loop
   8 sd
   11 sr
   65 sd
   66 sd
   67 sd
   68 sd
   69 sd
   70 sd
   71 sd
   128 sd
   129 sd
   130 sd
   131 sd
   132 sd
   133 sd
   134 sd
   135 sd
   254 device-mapper
   259 blkext
   galihcandra@LAPTOP-QQ597UPT:/proc$ cat cpuinfo
   processor       : 0
   vendor_id       : GenuineIntel
   cpu family      : 6
   model           : 122
   model name      : Intel(R) Celeron(R) N4020 CPU @ 1.10GHz
   stepping        : 8
   microcode       : 0xffffffff
   cpu MHz         : 1094.399
   cache size      : 4096 KB
   physical id     : 0
   siblings        : 2
   core id         : 0
   cpu cores       : 2
   apicid          : 0
   initial apicid  : 0
   fpu             : yes
   fpu_exception   : yes
   cpuid level     : 24
   wp              : yes
   flags           : fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ss ht syscall nx pdpe1gb rdtscp lm constant_tsc arch_perfmon rep_good nopl xtopology tsc_reliable nonstop_tsc cpuid tsc_known_freq pni pclmulqdq vmx ssse3 cx16 pdcm sse4_1 sse4_2 x2apic movbe popcnt tsc_deadline_timer aes xsave rdrand hypervisor lahf_lm 3dnowprefetch ssbd ibrs ibpb stibp ibrs_enhanced tpr_shadow ept vpid ept_ad fsgsbase tsc_adjust smep erms rdseed smap clflushopt sha_ni xsaveopt xsavec xgetbv1 xsaves vnmi umip rdpid md_clear arch_capabilities
   vmx flags       : vnmi invvpid ept_x_only ept_ad ept_1gb tsc_offset vtpr ept vpid unrestricted_guest ept_mode_based_exec tsc_scaling
   bugs            : spectre_v1 spectre_v2 spec_store_bypass retbleed rfds bhi
   bogomips        : 2188.79
   clflush size    : 64
   cache_alignment : 64
   address sizes   : 39 bits physical, 48 bits virtual
   power management:

   processor       : 1
   vendor_id       : GenuineIntel
   cpu family      : 6
   model           : 122
   model name      : Intel(R) Celeron(R) N4020 CPU @ 1.10GHz
   stepping        : 8
   microcode       : 0xffffffff
   cpu MHz         : 1094.399
   cache size      : 4096 KB
   physical id     : 0
   siblings        : 2
   core id         : 1
   cpu cores       : 2
   apicid          : 1
   initial apicid  : 1
   fpu             : yes
   fpu_exception   : yes
   cpuid level     : 24
   wp              : yes
   flags           : fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ss ht syscall nx pdpe1gb rdtscp lm constant_tsc arch_perfmon rep_good nopl xtopology tsc_reliable nonstop_tsc cpuid tsc_known_freq pni pclmulqdq vmx ssse3 cx16 pdcm sse4_1 sse4_2 x2apic movbe popcnt tsc_deadline_timer aes xsave rdrand hypervisor lahf_lm 3dnowprefetch ssbd ibrs ibpb stibp ibrs_enhanced tpr_shadow ept vpid ept_ad fsgsbase tsc_adjust smep erms rdseed smap clflushopt sha_ni xsaveopt xsavec xgetbv1 xsaves vnmi umip rdpid md_clear arch_capabilities
   vmx flags       : vnmi invvpid ept_x_only ept_ad ept_1gb tsc_offset vtpr ept vpid unrestricted_guest ept_mode_based_exec tsc_scaling
   bugs            : spectre_v1 spectre_v2 spec_store_bypass retbleed rfds bhi
   bogomips        : 2188.79
   clflush size    : 64
   cache_alignment : 64
   address sizes   : 39 bits physical, 48 bits virtual
   power management:

   galihcandra@LAPTOP-QQ597UPT:/proc$ cat meminfo
   MemTotal:        1858304 kB
   MemFree:          652740 kB
   MemAvailable:    1182164 kB
   Buffers:           10068 kB
   Cached:           571132 kB
   SwapCached:            0 kB
   Active:           132592 kB
   Inactive:         791176 kB
   Active(anon):       2700 kB
   Inactive(anon):   343344 kB
   Active(file):     129892 kB
   Inactive(file):   447832 kB
   Unevictable:           0 kB
   Mlocked:               0 kB
   SwapTotal:       1048576 kB
   SwapFree:        1048576 kB
   Dirty:                16 kB
   Writeback:             0 kB
   AnonPages:        342580 kB
   Mapped:           137232 kB
   Shmem:              3468 kB
   KReclaimable:      27560 kB
   Slab:              62668 kB
   SReclaimable:      27560 kB
   SUnreclaim:        35108 kB
   KernelStack:        3792 kB
   PageTables:        10216 kB
   SecPageTables:         0 kB
   NFS_Unstable:          0 kB
   Bounce:                0 kB
   WritebackTmp:          0 kB
   CommitLimit:     1977728 kB
   Committed_AS:    1010672 kB
   VmallocTotal:   34359738367 kB
   VmallocUsed:       29120 kB
   VmallocChunk:          0 kB
   Percpu:              840 kB
   HardwareCorrupted:     0 kB
   AnonHugePages:         0 kB
   ShmemHugePages:        0 kB
   ShmemPmdMapped:        0 kB
   FileHugePages:         0 kB
   FilePmdMapped:         0 kB
   Unaccepted:            0 kB
   HugePages_Total:       0
   HugePages_Free:        0
   HugePages_Rsvd:        0
   HugePages_Surp:        0
   Hugepagesize:       2048 kB
   Hugetlb:               0 kB
   DirectMap4k:       62464 kB
   DirectMap2M:     1941504 kB
   DirectMap1G:     8388608 kB
   galihcandra@LAPTOP-QQ597UPT:/proc$ cat uptime
   2089.96 3315.88
   ```
