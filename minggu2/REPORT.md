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