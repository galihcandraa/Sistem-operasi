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
![](img/Praktikum-9.2.1.jpg)

### Latihan 9.2
Buat script kalkulator.sh yang menerima tiga argumen: <angka1> <operator> <angka2> dengan operator +, -, *, atau /. Contoh:
./kalkulator.sh 20 + 5 menghasilkan 25. Gunakan case untuk memilih operasi, dan validasi jika argumen tidak lengkap.

![](img/Latihan-9.2.1.jpg)

Script:
```bash
#!/bin/bash
# Penggunaan : ./kalkulator.sh [angka1] [operator] [angka2]

ANGKA1=${1}
OPERATOR=${2}
ANGKA2=${3}

# Validasi jumlah argumen
if [ $# -ne 3 ]; then
     echo "Usage: $0 <angka1> <operator> <angka2>"
     echo "Contoh: $0 20 + 5"
     exit 1
fi

case $OPERATOR in
     +)
        HASIL=$((ANGKA1 + ANGKA2))
        ;;
     -)
        HASIL=$((ANGKA1 - ANGKA2))
        ;;
     \*)
        HASIL=$((ANGKA1 * ANGKA2))
        ;;
     /)
        if [ "$ANGKA2" -eq 0 ]; then
          echo "Error: pembagian dengan nol tidak diperbolehkan"
          exit 1
        fi
        HASIL=$((ANGKA1 / ANGKA2))
        ;;
     *)
        echo "Operator tidak valid. Gunakan +, -, *, atau /"
        exit 1
        ;;
esac

echo "Hasil: $HASIL"
```

## Praktikum 7.3 Script Grading dan Menu Interaktif

## Praktikum 7.4 Library Fungsi Validasi

##  7.5 Script Backup dengan Opsi

## Praktikum 7.6 Debugging Script

## Tugas Praktikum