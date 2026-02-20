# Laporan Jobsheet 2
Manajemen Perangkat Keras & Perintah Dasar Sistem Operasi

* Nama: Galih Candra Kirana
* NIM: 254107020078
* Kelas: TI-1G

## Praktikum 2.1: Identifikasi CPU dan Memori
Tujuan: memahami spesifikasi CPU dan kondisi memori pada server/VM.

### Langkah-langkah
1. Tampilkan informasi CPU:
```bash
lscpu
```
![informasi CPU](img/Langkah2.1-1.jpg)

2. Tampilkan ringkasan memori:
```bash
free -h
```
![ringkasan Memori](img/Langkah2.1-2.jpg) 

3. (Opsional) cek informasi hardware dari DMI/BIOS (butuh sudo): 
```bash
sudo dmidecode -t system
```
![informasi hardware](img/Langkah2.1-3.jpg) 

### Latihan 2.1
Catat: (1) jumlah CPU(s), core/thread, (2) total RAM, (3) total swap. Jelaskan perbedaan RAM vs swap dalam 2–3 kalimat.

Jawaban

* Berdasarkan hasil perintah lscpu, sistem memiliki 2 CPU(s), dengan 2 core dan 1 thread per core (total 2 logical CPU).
* Total RAM: 1.8 GiB
* Total Swap: 1.0 GiB
* Perbedaan RAM vs swap: Ram adalah penyimpanan data utama yang sangat cepat untuk menjalankan program secara langsung. Sedangkan swap berfungsi sebagai memori virtual di dalam hard drive yang baru akan aktif ketika RAM tidak lagi mampu menampung beban aplikasi yang berjalan.

## Praktikum 2.2: Identifikasi Perangkat PCI/USB dan Driver
Tujuan: mengenali perangkat PCI/USB dan melihat driver/modul yang dipakai.

### Langkah-langkah
1. Lihat daftar perangkat PCI:
```bash
lspci
```
![daftar PCI](img/Langkah2.2-1.jpg)

2. Lihat perangkat PCI beserta driver kernel yang digunakan:
```bash
lspci -nnk
```
![perangkat PCI yang digunakan](img/Langkah2.2-2.jpg) 

3. Fokus pada NIC (Ethernet) untuk mencari modul driver:
```bash
lspci - nnk | grep - A3 -i ethernet
```
![modul Driver](img/Langkah2.2-3.jpg) 

4. Lihat perangkat USB:
```bash
lsusb
```
![perangkat USB](img/Langkah2.2-4.jpg) 

5. Lihat topologi USB (tree):
```bash
lsusb -t
```
![tree topologi USB](img/Langkah2.2-5.jpg) 

### Latihan 2.2
Temukan 1 perangkat PCI (misal NIC) dan tuliskan: Vendor:Device ID (angka
heksadesimal), nama driver/modul kernel, dan deskripsi singkat fungsinya.

Jawaban

* Vendor:Device ID | 1af4:1043
* Perangkat | SCSI storage controller
* Driver/Modul Kernel	| virtio-pci
* Deskripsi Fungsi | Berfungsi sebagai pengontrol penyimpanan data virtual yang memungkinkan sistem operasi berkomunikasi dengan media penyimpanan (disk) menggunakan protokol Virtio untuk performa tinggi di lingkungan virtualisasi.

## Praktikum 2.3: Identifikasi Storage dan Filesystem
Tujuan: memahami disk/partisi dan filesystem yang terpasang

### Langkah-langkah
1. Lihat daftar disk/partisi:
```bash
lsblk -f
```
![daftar disk](img/Langkah2.3-1.jpg)

2. Tampilkan UUID dan tipe filesystem:
```bash
sudo blkid
```
![tampilan uuid](img/Langkah2.3-2.jpg) 

3. Lihat mount point untuk root filesystem:
```bash
findmnt /
```
![mount point](img/Langkah2.3-3.jpg) 

## Praktikum 2.4: Melihat Modul Aktif dan Informasinya
Tujuan: mengenal modul aktif dan keterkaitannya dengan perangkat.

### Langkah-langkah
1. Cek versi kernel:
```bash
uname -r
```
![versi kernel](img/Langkah2.4-1.jpg)

2. Tampilkan daftar modul aktif:
```bash
lsmod | head
```
![modul aktif](img/Langkah2.4-2.jpg) 

3. Pilih salah satu modul (contoh aman: loop) dan lihat detailnya:
```bash
modinfo loop
```
![modul loop](img/Langkah2.4-3.jpg) 

4. Muat modul (jika belum aktif), lalu verifikasi:
```bash
sudo modprobe loop
lsmod | grep -i loop
```
![muat modul](img/Langkah2.4-4.jpg) 

5. (Opsional) lihat pesan kernel terbaru:
```bash
dmesg -T | tail -n 20
```
![pesan kernel](img/Langkah2.4-5.jpg) 

## Praktikum 2.5: Konfigurasi Auto-load dan Blacklist
Tujuan: memahami cara membuat modul otomatis dimuat atau diblokir.

### Langkah-langkah
1. Buat file auto-load:
```bash
echo "loop" | sudo tee /etc/modules-load.d/loop.conf
```
![file auto-load](img/Langkah2.5-1.jpg)

2. Simulasikan verifikasi (tanpa reboot) dengan memastikan modul sudah aktif:
```bash
lsmod | grep -i loop
```
![simulasi verifikasi modul](img/Langkah2.5-2.jpg) 

3. (Opsional, konsep) blacklist modul:
```bash
# echo "blacklist loop" | sudo tee /etc/modprobe .d/blacklist-loop.conf
```
![modul loop](img/Langkah2.5-3.jpg) 

## Praktikum 2.6: Mengenali Block vs Character Device
Tujuan: membedakan perangkat disk vs terminal

### Langkah-langkah
1. Lihat detail salah satu disk (sesuaikan dengan perangkat Anda, misal sda)
```bash
ls -l /dev/sda
```
Berdasarkan hasil lsblk, disk utama sistem saya adalah /dev/sdd karena ter-mount pada direktori root (/).
![detail disk](img/Langkah2.6-1.jpg)

2. Lihat detail device terminal:
```bash
ls -l /dev/tty
```
![detail device terminal](img/Langkah2.6-2.jpg) 

3. Lihat disk dan partisi untuk mengaitkan dengan /dev:
```bash
lsblk
```
![disk dan partisi](img/Langkah2.6-3.jpg) 

### Latihan 2.3
Dari output ls -l, jelaskan perbedaan penanda file untuk block device dan
character device. (Hint: karakter pertama pada permission string)

Jawaban

Perbedaan penanda file block device dan character device bisa dilihat dari karakter pertama pada output ls -1. Block device dapat ditandai dengan huruf b, sedangkan character device ditandai dengan huruf c. 

## Praktikum 2.7: Melihat Informasi udev
Tujuan: melihat metadata yang dipakai udev untuk membuat device node

### Langkah-langkah
1. Cek atribut udev untuk disk:
```bash
udevadm info --query=all --name=/dev/sda | head -n 30
```
![atribut udev](img/Langkah2.7-1.jpg)

2. (Opsional) monitor event udev (jalankan, lalu colok/lepas USB pada mesin fisik):
```bash
sudo udevadm monitor
```
![monitor event udev](img/Langkah2.7-2.jpg) 

## Praktikum 2.8: Membuat Workspace Praktikum
Tujuan: membuat area kerja aman untuk semua latihan bab ini.

### Langkah-langkah
1. Buat direktori praktikum dan masuk ke dalamnya:
```bash
1 mkdir -p ~/praktikum-os/week02
2 cd ~/praktikum-os/week02
3 pwd
```
![new directory](img/Langkah2.8-1.jpg)

2. Buat beberapa file contoh:
```bash
1 touch notes.txt data.log config.txt
2 ls -lah
```
![membuat file](img/Langkah2.8-2.jpg) 

3. Isi file log contoh (simulasi):
```bash
1 echo "INFO : service started" >> data.log
2 echo "WARN : disk usage high" >> data.log
3 echo "ERROR : failed to connect" >> data.log
4 cat data.log
```
![mengisi file](img/Langkah2.8-3.jpg) 

4. Baca file dengan less:
```bash
less data.log
```
![baca file with less](img/Langkah2.8-4.jpg) 

## Praktikum 2.9: Pencarian Pola dengan grep

1. Cari baris yang mengandung ERROR pada data.log:
```bash
grep "ERROR" data.log
```
![baris error](img/Langkah2.9-1.jpg)

2. Cari tanpa memperhatikan huruf besar/kecil:
```bash
grep -i "error" data.log
```
![baris error ignore case](img/Langkah2.9-2.jpg) 

3. Tampilkan nomor baris:
```bash
grep -n "WARN" data.log
```
![tampil with no baris](img/Langkah2.9-3.jpg) 

4. Tampilkan baris yang tidak cocok (invert match):
```bash
grep -v "INFO" data.log
```
![invert match](img/Langkah2.9-4.jpg) 

### Latihan 2.4
Gunakan grep untuk menampilkan hanya baris yang mengandung INFO atau
WARN dari data.log. (Hint: gunakan grep -E dengan pola alternatif)

Jawaban

![menampilkan info / warn](img/Latihan2.4.jpg) 

## Praktikum 2.10: Substitusi dengan sed (Aman di File Latihan)

1. Siapkan file konfigurasi latihan:
```bash
1 cat > config.txt << 'EOF'
2 PORT=8080
3 MODE=dev
4 SERVICE_NAME=myserver
5 EOF
6 cat config.txt
```
![menyiapkan file config](img/Langkah2.10-1.jpg)

2. Ganti dev menjadi prod (tanpa mengubah file asli):
```bash
sed 's/MODE=dev/MODE=prod/' config.txt
```
![dev jadi prod](img/Langkah2.10-2.jpg) 

3. Terapkan perubahan langsung ke file (-i):
```bash
1 sed -i 's/MODE=dev/MODE=prod/' config.txt
2 cat config.txt
```
![menerapkan langsung ke file](img/Langkah2.10-3.jpg) 

4. Ganti semua kemunculan kata (g untuk global), contoh ubah myserver menjadi node:
```bash
1 sed -i 's/myserver/node/g' config.txt
2 cat config.txt
```
![mengubah myserver menjadi node](img/Langkah2.10-4.jpg) 

## Praktikum 2.11: Ekstraksi Kolom dengan awk

1. Lihat output df -h:
```bash
df -h
```
![output df -h](img/Langkah2.11-1.jpg)

2. Ambil kolom filesystem dan persentase pemakaian:
```bash
df -h | awk 'NR==1 {print $1 , $5 , $6} NR>1 {print $1, $5, $6}'
```
![ambil kolom filesystem](img/Langkah2.11-2.jpg) 

3. Filter hanya yang pemakaian disk di atas 80%:
```bash
df -h | awk 'NR==1 || ($5+0) > 80 {print $1 , $5 , $6}'
```
![filter > 80%](img/Langkah2.11-3.jpg) 

## Praktikum 2.12: Melihat Proses dengan ps

1. Tampilkan semua proses (format BSD):
```bash
ps aux | head
```
![tampil semua proses](img/Langkah2.12-1.jpg)

2. Cari proses tertentu (misal sshd):
```bash
ps aux | grep -i sshd
```
![mencari proses tertentu](img/Langkah2.12-2.jpg) 

## Praktikum 2.13: Monitoring Real-time dengan top

1. Jalankan top:
```bash
top
```
![menjalankan top](img/Langkah2.13-1.jpg)

2. Amati nilai load average, pemakaian CPU, dan proses teratas. Tekan q untukkeluar
```bash
ps aux | grep -i sshd
```
![q untuk keluar dari top](img/Langkah2.13-2.jpg) 

## Praktikum 2.14: Menghentikan Proses dengan kill

1. Jalankan proses dummy di background:
```bash
sleep 300 &
```
![menjalankan proses dummy](img/Langkah2.14-1.jpg)

2. Cari PID proses sleep:
```bash
ps aux | grep -E "sleep 300" | grep -v grep
```
![PID proses sleep](img/Langkah2.14-2.jpg) 

3. Hentikan dengan SIGTERM:
```bash
kill < PID_ANDA >
```
![menghentikan proses](img/Langkah2.14-3.jpg) 

4. Verifikasi proses berhenti:
```bash
ps aux | grep -E "sleep 300" | grep -v grep
```
![memverifikasi proses berhenti](img/Langkah2.14-4.jpg) 
