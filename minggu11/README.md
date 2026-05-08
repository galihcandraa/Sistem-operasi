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

## 1.2 Access Control Lists (ACLs)
## Praktikum 11.2 — ACL
##### Langkah 1
```bash

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

