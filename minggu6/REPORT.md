# LAPORAN JOBSHEET 6
Manajemen Proses

* Nama: Galih Candra Kirana
* NIM: 254107020080
* Kelas: TI-1G

## Praktikum 6.1 — Melihat Proses dan Thread
![](img/Praktikum-6.1.1.jpg)
![](img/Praktikum-6.1.2.jpg)
### Latihan 6.1
Jalankan ps aux dan amati outputnya:
1. Berapa total proses yang berjalan? Proses apa yang memiliki PID
terkecil?
2. Jalankan pstree -p dan temukan proses bash Anda. Proses apa yang
menjadi induk (PPID) dari bash tersebut?
3. Bandingkan output ps aux dan ps aux -L. Apa perbedaan yang Anda
lihat?

![](img/Latihan-6.1.jpg)

Jawaban:
1. Total proses yang berjalan adalah 41 proses, dan PID terkecil adalah 1, yaitu proses /sbin/init.
1. Proses bash memiliki induk (PPID) yaitu login dan Relay, tergantung dari proses bash yang diamati.
2. ps aux menampilkan proses saja, sedangkan ps aux -L menampilkan proses beserta thread, sehingga satu proses bisa muncul lebih dari satu baris.

## Praktikum 6.2 — Mengamati Siklus Hidup Proses
![](img/Praktikum-6.2.1.jpg)

### Latihan 6.2
1. Jalankan sleep 120 & dan amati kolom STAT pada ps aux. Kondisi
apa yang ditampilkan? Mengapa proses sleep berada di kondisi tersebut?
2. Jalankan beberapa perintah yang berhasil dan yang gagal, lalu catat exit
code masing-masing. Pola apa yang Anda temukan?

![](img/Latihan-6.2.jpg)
Jawaban:

1. Kondisi yang ditampilkan pada kolom STAT adalah S (sleeping).
Hal ini karena proses sleep sedang menunggu waktu (delay) tanpa melakukan aktivitas CPU, sehingga berada dalam kondisi tidur
2. Pola yang saya temukan adalah kode 0 jika berhasil, dan kode selain 0 jika tidak berhasil.
