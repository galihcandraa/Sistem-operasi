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
## Praktikum 11.3B — Group Management   

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

