# LAPORAN JOBSHEET 11
Manajemen File & User/Group

* Nama: Galih Candra Kirana
* NIM: 254107020080
* Kelas: TI-1G

## 1.1 Sistem Kontrol Akses (Permissions)
## Praktikum 11.1 — Permissions
##### Langkah : Membuat direktori kerja dan file uji
```bash
mkdir ~/lab-permissions && cd ~/lab-permissions
echo "data rahasia" > secret.txt
echo '#!/bin/bash' > myscript.sh
echo 'echo Hello' >> myscript.sh
ls -la

Output:
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11$ mkdir lab-permissions && cd lab-permissions
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11/lab-permissions$ echo "data rahasia" > secret.txt
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11/lab-permissions$ echo '#!/bin/bash' > myscript.sh
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11/lab-permissions$ echo 'echo Hello' >> myscript.sh
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11/lab-permissions$ ls -la
total 16
drwxr-xr-x  2 galihcandra galihcandra 4096 May  8 21:48 .
drwxr-xr-x 13 galihcandra galihcandra 4096 May  8 21:45 ..
-rw-r--r--  1 galihcandra galihcandra   23 May  8 21:48 myscript.sh
-rw-r--r--  1 galihcandra galihcandra   13 May  8 21:46 secret.txt
```

##### Langkah 2: Membuat secret.txt menjadi privat
```bash
chmod 600 secret.txt
ls -l secret.txt

Output: 
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11/lab-permissions$ chmod 600 secret.txt
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11/lab-permissions$ ls -l secret.txt
-rw------- 1 galihcandra galihcandra 13 May  8 21:46 secret.txt
```

##### Langkah 3: Membuat script dapat dijalankan
```bash
chmod 755 myscript.sh
ls -l myscript.sh
./myscript.sh

Output:
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11/lab-permissions$ chmod 755 myscript.sh
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11/lab-permissions$ ls -l myscript.sh
-rwxr-xr-x 1 galihcandra galihcandra 23 May  8 21:48 myscript.sh
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11/lab-permissions$ ./myscript.sh
Hello
```

##### Langkah 4: Membuat direktori dengan SGID
```bash
mkdir shared-dir
chmod g+s shared-dir
ls -ld shared-dir

Output:
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11/lab-permissions$ mkdir shared-dir
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11/lab-permissions$ chmod g+s shared-dir
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11/lab-permissions$ ls -ld shared-dir
drwxr-sr-x 2 galihcandra galihcandra 4096 May  8 22:05 shared-dir
```

##### Langkah 5: Menguji efek umask
```bash
umask
umask 027
touch testfile-027
ls -l testfile-027

Output:
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11/lab-permissions$ umask 027
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11/lab-permissions$ touch testfile-027
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11/lab-permissions$ ls -l testfile-027
-rw-r----- 1 galihcandra galihcandra 0 May  8 22:11 testfile-027
```

#### Analisis
1. Mengapa secret.txt tidak dapat dibaca oleh group dan others setelah chmod 600?
2. Apa perbedaan arti 600 dan 755 terhadap file yang diuji?
3. Setelah umask 027, permission apa yang dihasilkan untuk file baru, dan mengapa bukan 777?

##### Jawaban:
1. secret.txt tidak dapat dibaca oleh group dan other karena permission telah diubah ke 600.
Jadi, user = 6 (r,w) group = 0 (-) other (-).
2. Perbedaanya terletak pada izin aksesnya. 
    * 600: owner bisa read dan write, lainnya tidak bisa apa-apa.  
    * 755: owner bisa read, write, dan execute. group bisa read, execute. other bisa read, execute.
3. Permission yang dihasilkan adalah 640 yaitu owner(r,w), group (r) other(-). Bukan 777 karena permission awal yaitu 666 - 027 = 640

#### Tantangan
Ubah owner atau group salah satu file uji ke akun atau group lain yang tersedia di sistem, kemudian jelaskan
perubahan output ls -l sebelum dan sesudahnya.

#####
```bash
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11/lab-permissions$ ls -l secret.txt
-rw------- 1 galihcandra galihcandra 13 May  8 21:46 secret.txt
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11/lab-permissions$ sudo chgrp sudo secret.txt
[sudo] password for galihcandra:
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11/lab-permissions$ ls -l secret.txt
-rw------- 1 galihcandra sudo 13 May  8 21:46 secret.txt
```

## 1.2 Access Control Lists (ACLs)
## Praktikum 11.2 — ACL
##### Langkah 1: Menyiapkan file uji ACL
```bash
mkdir ~/lab-acl && cd ~/lab-acl
echo "Data penting" > confidential.txt
chmod 640 confidential.txt
ls -l confidential.txt
getfacl confidential.txt

Output:
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11$ mkdir lab-acl && cd lab-acl
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11/lab-acl$ echo "Data Penting" > confidental.txt
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11/lab-acl$ chmod 640 confidental.txt
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11/lab-acl$ ls -l confidental.txt
-rw-r----- 1 galihcandra galihcandra 13 May  9 14:50 confidental.txt
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11/lab-acl$ getfacl confidental.txt
# file: confidental.txt
# owner: galihcandra
# group: galihcandra
user::rw-
group::r--
other::---
```

##### Langkah 2: Menambahkan ACL untuk satu user
```bash
setfacl -m u:userA:r confidential.txt
ls -l confidential.txt
getfacl confidential.txt

Output:
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11/lab-acl$ setfacl -m u:userA:r confidental.txt
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11/lab-acl$ ls -l confidental.txt
-rw-r-----+ 1 galihcandra galihcandra 13 May  9 14:50 confidental.txt
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11/lab-acl$ getfacl confidental.txt
# file: confidental.txt
# owner: galihcandra
# group: galihcandra
user::rw-
user:userA:r--
group::r--
mask::r--
other::---
```

##### Langkah 3: Default ACL pada direktori
```bash
mkdir shared
setfacl -d -m u:userA:rwx shared
setfacl -d -m u:userB:r-x shared
getfacl shared

touch shared/inherited.txt
getfacl shared/inherited.txt

Output:
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11/lab-acl$ mkdir shared
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11/lab-acl$ setfacl -d -m u:userA:rwx shared
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11/lab-acl$ setfacl -d -m u:userB:r-x shared
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11/lab-acl$ getfacl shared/
# file: shared/
# owner: galihcandra
# group: galihcandra
user::rwx
group::r-x
other::r-x
default:user::rwx
default:user:userA:rwx
default:user:userB:r-x
default:group::r-x
default:mask::rwx
default:other::r-x

galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11/lab-acl$ touch shared/inherited.txt
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11/lab-acl$ getfacl shared/inherited.txt
# file: shared/inherited.txt
# owner: galihcandra
# group: galihcandra
user::rw-
user:userA:rwx                  #effective:rw-
user:userB:r-x                  #effective:r--
group::r-x                      #effective:r--
mask::rw-
other::r--
```

#### Analisis
1. Mengapa getfacl confidential.txt awalnya tidak menampilkan user tertentu?
2. Setelah setfacl -m u:userA:r confidential.txt, apa perbedaan output ls -l dan getfacl?
3. Mengapa file inherited.txt mewarisi ACL dari direktori shared?

##### Jawaban:
1. Karena file tersebut awalnya tidak memiliki ACL tambahan.
dengan permission Unix biasa: owner, group, dan others.
2. Perbedaan utamanya, jika ls -l itu hanya menampilkan informasi secara singkat, sedangkan getfacl outputnya lebih spesifik.
3. Karena dir shared memiliki default ACL, sehingga setiap file/dir baru akan mewarisi ACL tersebut.

#### Tantangan
Tambahkan satu ACL lagi agar group readonly-group hanya dapat membaca confidential.txt. Setelah
itu, hapus ACL untuk userA dan verifikasi hasil akhirnya dengan getfacl.

```bash
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11/lab-acl$ setfacl -m g:readonly-group:r confidental.txt
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11/lab-acl$ setfacl -x u:userA confidental.txt
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11/lab-acl$ getfacl confidental.txt
# file: confidental.txt
# owner: galihcandra
# group: galihcandra
user::rw-
group::r--
group:readonly-group:r--
mask::r--
other::---
```

## 1.3 Manajemen User dan Group
## Praktikum 11.3A — Membuat dan Mengelola User
```bash
# buat dua user
sudo useradd -m -s /bin/bash userA
sudo useradd -m -s /bin/bash userB
sudo passwd userA
sudo passwd userB

# verifikasi
id userA
getent passwd userA

# modifikasi shell userA
sudo usermod -s /bin/zsh userA
getent passwd userA

# lock dan unlock userB
sudo usermod -L userB
sudo passwd -S userB
sudo usermod -U userB
sudo passwd -S userB

Output:
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11/lab-acl$ sudo useradd -m -s /bin/bash userA
useradd: user 'userA' already exists
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11/lab-acl$ sudo useradd -m -s /bin/bash userB
useradd: user 'userB' already exists
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11/lab-acl$ sudo passwd userA
New password:
Retype new password:
passwd: password updated successfully
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11/lab-acl$ sudo passwd userB
New password:
Retype new password:
passwd: password updated successfully
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11/lab-acl$ id userA
uid=1001(userA) gid=1001(userA) groups=1001(userA)
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11/lab-acl$ getent passwd userA
userA:x:1001:1001::/home/userA:/bin/sh
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11/lab-acl$ sudo usermod -s /bin/zsh userA
usermod: Warning: missing or non-executable shell '/bin/zsh'
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11/lab-acl$ getent passwd userA
userA:x:1001:1001::/home/userA:/bin/zsh
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11/lab-acl$  sudo usermod -L userB
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11/lab-acl$ sudo passwd -S userB
userB L 2026-05-09 0 99999 7 -1
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11/lab-acl$ sudo usermod -U userB
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11/lab-acl$ sudo passwd -S userB
userB P 2026-05-09 0 99999 7 -1
```

#### Pertanyaan
1. Apa perbedaan output id userA sebelum dan sesudah menambah group?
2. Bagaimana status passwd -S userB berubah saat akun di-lock?

##### Jawaban
1. Maksud dari soalnya mungkin perbedaan saat menggunakan getent passwd, yang dimana hanya berubah di shell login.
2. Perubahan status saat di lock(-L) yaitu ada keterangan L (Locked) di samping nama user.

## Praktikum 11.3B — Group Management  
```bash
# buat dua group
sudo groupadd labgroup
sudo groupadd readonly-group

# tambahkan userA ke kedua group
sudo usermod -aG labgroup,readonly-group userA

# tambahkan userB hanya ke readonly-group
sudo usermod -aG readonly-group userB

# verifikasi
id userA
id userB
getent group labgroup
getent group readonly-group

Output:
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11/lab-acl$ cd ..
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11$ sudo groupadd labgroup
[sudo] password for galihcandra:
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11$ sudo groupadd readonly-group
groupadd: group 'readonly-group' already exists
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11$ sudo usermod -aG labgroup,readonly-group userA
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11$ sudo usermod -aG readonly-group userB
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11$ id userA
uid=1001(userA) gid=1001(userA) groups=1001(userA),1003(readonly-group),1004(labgroup)
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11$ id userB
uid=1002(userB) gid=1002(userB) groups=1002(userB),1003(readonly-group)
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11$ getent group labgroup
labgroup:x:1004:userA
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11$ getent group readonly-group
readonly-group:x:1003:userA,userB
```

#### Pertanyaan:
1. Apa yang ditampilkan id userA vs groups userA?
2. Mengapa -a pada usermod -aG penting?

##### Jawaban:
1. Yang ditampilkan userA yaitu informasi lengkap dari user tersebut, sedangkan yang ditampilkan groups userA yaitu hanya menampilkan group yang diikuti oleh userA.
2. Karena fungsi -a pada command tersebut berfungsi sebagai append agar tidak menimpa group sebelumnya.

## Praktikum 11.3C — Password Aging Policy 
```bash
# set aging policy untuk userA
sudo chage -M 60 -W 7 -m 1 userA
sudo chage -l userA

# paksa userA ganti password saat login pertama
sudo chage -d 0 userA

# kunci password userB
sudo passwd -l userB
sudo passwd -S userB

# unlock kembali
sudo passwd -u userB
sudo passwd -S userB

Output:
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11$ sudo chage -M 60 -W 7 -m 1 userA
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11$ sudo chage -l userA
Last password change                                    : May 09, 2026
Password expires                                        : Jul 08, 2026
Password inactive                                       : never
Account expires                                         : never
Minimum number of days between password change          : 1
Maximum number of days between password change          : 60
Number of days of warning before password expires       : 7
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11$ sudo chage -d 0 userA
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11$ sudo passwd -l userB
passwd: password changed.
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11$ sudo passwd -S userB
userB L 2026-05-09 0 99999 7 -1
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11$ sudo passwd -u userB
passwd: password changed.
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11$ sudo passwd -S userB
userB P 2026-05-09 0 99999 7 -1
```

#### Pertanyaan:
1. Apa arti nilai yang ditampilkan chage -l userA?
2. Bagaimana cara membuktikan userB terkunci dari output passwd -S?
3. Kapan sebaiknya menggunakan chage -d 0 vs passwd -e?

##### Jawaban:
1. Yang ditampilkan adalah informasi lengkap tentang perubahan password.
2. Pada outputnya terdapat simbol L di samping nama user.
3. Ketika ingin memaksa melakukan pergantian password pada login berikutnya.

#### Tantangan
Buat user bernama intern yang:
• memiliki shell /bin/bash;
• menjadi anggota labgroup;
• dipaksa ganti password pada login pertama;
• password expired setelah 45 hari dengan warning 7 hari sebelumnya.

##### Jawaban:
```bash
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11$ sudo useradd -m -s /bin/bash intern
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11$ sudo usermod -aG labgroup intern
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11$ id intern
uid=1003(intern) gid=1005(intern) groups=1005(intern),1004(labgroup)
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11$ sudo chage -d 0 intern
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11$ sudo chage -M 45 -W 7 intern
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week11$ sudo chage -l intern
Last password change                                    : password must be changed
Password expires                                        : password must be changed
Password inactive                                       : password must be changed
Account expires                                         : never
Minimum number of days between password change          : 0
Maximum number of days between password change          : 45
Number of days of warning before password expires       : 7
```

## 1.4 Konfigurasi sudo dan su
## Praktikum 11.4 — Konfigurasi sudo

## 1.5 Disk Quota
## Praktikum 11.5 — Disk Quota

## 1.6 Rangkuman
```bash
Bab ini membahas lima kelompok konsep inti:
Permissions owner, group, others; izin rwx; chmod, chown, chgrp; special bits; dan umask.
ACL perluasan permission Unix untuk kebutuhan akses granular per-user atau per-group, termasuk default ACL
direktori dan mask.
User/Group identitas pengguna disimpan di /etc/passwd, /etc/shadow, dan /etc/group; dikelola dengan keluarga perintah useradd, usermod, userdel, groupadd, dan gpasswd.
sudo dan su sudo adalah mekanisme delegasi hak administratif yang lebih aman dan lebih dapat diaudit
dibanding su.
Disk Quota pembatasan blok dan inode melalui soft limit, hard limit, grace period, serta perintah seperti
edquota, setquota, dan repquota.
```
  
## 1.7 Latihan

### Latihan Latihan 11.A — Audit dan Kolaborasi
1. Temukan file SUID aktif dengan find / -perm -4000 -type f 2>/dev/null, lalu jelaskan
tiga file yang Anda kenali beserta alasannya.
2. Cari direktori world-writable dan tentukan mana yang valid dan mana yang berisiko.
3. Rancang konfigurasi permission standar dan ACL untuk direktori proyek /srv/webapp/ agar
group webapp-team dapat menulis, user deploy hanya membaca, dan file baru selalu mewarisi
group proyek

### Latihan Latihan 11.B — Kebijakan Akun dan Quota
Tuliskan langkah untuk membuat user intern, menambahkannya ke group labgroup, memaksa pergantian password tiap 45 hari (warning 7 hari), memberi izin sudo hanya untuk systemctl status, dan
menetapkan quota ruang serta inode sederhana pada /home/.

