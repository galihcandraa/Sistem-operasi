# LAPORAN JOBSHEET 9
Pemrograman Bash

* Nama: Galih Candra Kirana
* NIM: 254107020080
* Kelas: TI-1G

## Praktikum 7.1 Script Pertama: Laporan Sistem
![](img/Praktikum-9.1.1.jpg)

### Latihan 9.1
Modifikasi laporan-sistem.sh agar menyimpan output ke file
laporan-YYYY-MM-DD.txt sekaligus menampilkannya di terminal. Petunjuk:
gunakan tee yang sudah dipelajari di bab sebelumnya.

Jawaban
![](img/Latihan-9.1.1.jpg)

Script:
```bash
#!/bin/bash
# Script: laporan-sistem.sh

file="laporan-$(date +%Y-%m-%d).txt"

{
echo "================================"
echo "LAPORAN SISTEM"
echo "================================"
echo "Tanggal : $(date '+%A, %d %B %Y')"
echo "Jam : $(date '+%H:%M:%S')"
echo "Hostname : $(hostname)"
echo "User : $(whoami)"
echo "CPU core : $(nproc)"
echo "RAM bebas : $(free -h | awk '/^Mem/ {print $4}')"
echo " Disk / : $(df -h / | awk 'NR==2 {print $5}')
terpakai "
echo "================================"
} | tee "$file"
```


## Praktikum 7.2 Script Info Sistem dengan Argumen

## Praktikum 7.3 Script Grading dan Menu Interaktif

## Praktikum 7.4 Library Fungsi Validasi

##  7.5 Script Backup dengan Opsi

## Praktikum 7.6 Debugging Script

## Tugas Praktikum