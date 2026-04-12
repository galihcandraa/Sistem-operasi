# LAPORAN JOBSHEET 7
Bash Shell dan Shell Basic

* Nama: Galih Candra Kirana
* NIM: 254107020080
* Kelas: TI-1G

## Praktikum 6.1 — Mengenali Bash dan Menyiapkan Workspace
![](img/Praktikum-7.1.1.jpg)
![](img/Praktikum-7.1.2.jpg)

# Praktikum 6.2 — Membuat Ringkasan Sesi Terminal
![](img/Praktikum-7.2.1.jpg)

## Praktikum 6.3 — Menambahkan Konfigurasi Aman pada .bashrc
![](img/Praktikum-7.3.1.jpg)

## Praktikum 6.4 — Menyiapkan .bash_profile untuk Shell Login
![](img/Praktikum-7.4.1.jpg)

## Praktikum 6.5 — Membedakan Variabel Shell dan Environment Variable
![](img/Praktikum-7.5.1.jpg)

## Praktikum 6.6 — Menambahkan Direktori Script Pribadi ke PATH
![](img/Praktikum-7.6.1.jpg)

## Praktikum 6.7 — Membuat Alias Produktivitas Dasar
![](img/Praktikum-7.7.1.jpg)
![](img/Praktikum-7.7.2.jpg)

## Praktikum 6.8 — Membuat Fungsi Backup Konfigurasi
![](img/Praktikum-7.8.1.jpg)

## Praktikum 6.9 — Menggunakan Completion Dasar dan Melihat History
![](img/Praktikum-7.9.1.jpg)

## Praktikum 6.10 — Menelusuri Perintah Diagnostik dengan History
![](img/Praktikum-7.10.1.jpg)
![](img/Praktikum-7.10.2.jpg)

## Praktikum 6.11 — Mencoba Wildcard Dasar
![](img/Praktikum-7.11.1.jpg)

## Praktikum 6.12 — Mengarsipkan Banyak Log Sekaligus
![](img/Praktikum-7.12.1.jpg)

## Praktikum 6.13 — Membedakan Single Quote, Double Quote, dan Escape
![](img/Praktikum-7.13.1.jpg)

## Praktikum 6.14 — Menangani File dengan Nama Sulit secara aman
![](img/Praktikum-7.14.1.jpg)

## Tugas Praktikum

### Tugas Praktikum 1 — Toolkit Bash Administrtor Pribadi 
![](img/Tugas-7.1.1.jpg)

Output toolkit-bash-report.txt:
```bash
galihcandra@LAPTOP-QQ597UPT:~$ cat praktikum-os/week07-bash/toolkit-bash-report.txt
=== TOOLKIT REPORT ===
/home/galihcandra/praktikum-os/week07-bash/bin:/home/galihcandra/praktikum-os/week07-bash/bin:/home/galihcandra/praktikum-os/week07-bash/bin:/home/galihcandra/praktikum-os/week07-bash/bin:/home/galihcandra/praktikum-os/week07-bash/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/usr/lib/wsl/lib:/mnt/c/Program Files/WindowsApps/MicrosoftCorporationII.WindowsSubsystemForLinux_2.6.3.0_x64__8wekyb3d8bbwe:/mnt/c/Program Files/Python310/Scripts/:/mnt/c/Program Files/Python310/:/mnt/c/WINDOWS/system32:/mnt/c/WINDOWS:/mnt/c/WINDOWS/System32/Wbem:/mnt/c/WINDOWS/System32/WindowsPowerShell/v1.0/:/mnt/c/WINDOWS/System32/OpenSSH/:/mnt/c/Program Files/Git/cmd:/mnt/d/jdk-24.0.1/bin:/mnt/d/nodejs/:/mnt/c/Users/USER/AppData/Local/Microsoft/WindowsApps:/mnt/c/Users/USER/AppData/Local/Programs/Microsoft VS Code/bin:/mnt/c/Users/USER/AppData/Local/Microsoft/WindowsApps:/mnt/d/laragon/bin/php/php-8.1.10-Win32-vs16-x64:/mnt/c/Users/USER/AppData/Roaming/npm:/snap/bin
ll is aliased to `ls -lah --color=auto'
backup_simple is a function
backup_simple ()
{
    cp -- "$1" "$HOME/praktikum-os/week07-bash/backup/$(basename "$1").bak"
}
```

### Tugas Praktikum 2 — Audit File Konfigurasi dan Logging Aman
![](img/Tugas-7.2.1.jpg)
![](img/Tugas-7.2.2.jpg)

Analisis hasil audit:
* Ditemukan 157 file konfigurasi (.conf) di direktori /etc.
* Menunjukkan konfigurasi sistem tersebar di beberapa lokasi.
* Terdapat beberapa error akses (permission denied) yang tidak mempengaruhi hasil utama karena sudah dipisahkan.
* Pemisahan stdout dan stderr membuat hasil audit lebih akurat dan mudah dianalisis.

### Tugas Praktikum 3 — Mini Health Check Harian Server
![](img/Tugas-7.3.1.jpg)

Penjelasan tiap bagian script:
* #!/usr/bin/env bash → menentukan interpreter Bash
* LOG=... → menyimpan nama & lokasi file log
* { ... } → mengelompokkan semua perintah jadi satu output
* echo "=== HEALTH CHECK ===" → judul output
* date → waktu saat ini
* hostname → nama komputer
* whoami → user aktif
* $0 → nama script/shell
* uptime -p → lama sistem berjalan
* free -h → penggunaan RAM
* df -h / → penggunaan disk
* * tail -n 10 ~/.bash_history → 10 command terakhir 
* tee "$LOG" → tampilkan output + simpan ke file

### Tugas Praktikum 4 — Penanganan File dengan Nama Kompleks dan Arsip Aman
![](img/Tugas-7.4.1.jpg)

Daftar File awal:
```bash
galihcandra@LAPTOP-QQ597UPT:~/praktikum-os/week07-bash$ ls
''$'\n''login-audit.log'   bin           diag-history.txt             riwayat-arsip.txt
 backup                                  sample-app.conf
'backup [mingguan].conf'      healthcheck-2026-04-12.log   toolkit-bash-report.txt
 backup-arsip.tar.gz         login-audit.log
```

Daftar file hasil backup:
```bash
galihcandra@LAPTOP-QQ597UPT:~/praktikum-os/week07-bash$ ls backup
'backup [mingguan].conf'      'file satu.txt'
 backup-mingguan-server.conf   sample-app.conf.2026-04-12-143140.bak
```

Refleksi pentingnya quoting di Bash:
* Penanganan file dengan nama kompleks (spasi, simbol) memerlukan penggunaan quote (" ") atau escape (\) agar tidak terjadi error.
* Wildcard (*, ?, [ ]) sangat membantu dalam mengelola banyak file sekaligus, tetapi harus digunakan dengan hati-hati.
* Praktik preview menggunakan echo sebelum eksekusi penting untuk menghindari kesalahan fatal (misalnya salah hapus file).
* Penggunaan -- pada command seperti cp membantu mencegah kesalahan interpretasi nama file sebagai opsi.
* Pengarsipan dengan tar memudahkan pengelolaan dan penyimpanan banyak file dalam satu file terkompresi.
