# LAPORAN JOBSHEET 3
Dasar Input/Output (I/O)

* Nama: Galih Candra Kirana
* NIM: 254107020078
* Kelas: TI-1G

## Latihan 3.1
Buatlah script yang:

1. Menampilkan daftar 10 file terbesar di direktori /var/log/
2. Menyimpan hasilnya ke file large-logs.txt
3. Menampilkan output juga di terminal menggunakan tee
4. Menangani error dengan redirect ke error.log

## Jawaban

### script
```bash
LOG_OUTPUT="large-logs.txt"
ERROR_LOG="error.log"
echo "=== 10 File Terbesar di /var/log ===" | tee "$LOG_OUTPUT"
find /var/log -type f -exec ls -lh {} + 2>>"$ERROR_LOG" \
| sort -k5 -hr \
| head -10 \
| tee -a "$LOG_OUTPUT"
```

### output
```bash
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week03$ nano largest.sh
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week03$ chmod +x largest.sh
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week03$ ./largest.sh
=== 10 File Terbesar di /var/log ===
-rw-r-----+ 1 root      systemd-journal 8.0M Feb 27 16:45 /var/log/journal/7242c56d5fe44227a6a5d64387f01001/system.journal
-rw-r-----+ 1 root      systemd-journal 8.0M Feb 27 16:33 /var/log/journal/7242c56d5fe44227a6a5d64387f01001/user-1000.journal
-rw-r-----+ 1 root      systemd-journal 8.0M Feb 27 16:29 /var/log/journal/7242c56d5fe44227a6a5d64387f01001/system@e3a0d81fad994ceca8c310a1a84b0adf-00000000000071e2-00064bca97abde41.journal
-rw-r-----+ 1 root      systemd-journal 8.0M Feb 27 16:09 /var/log/journal/7242c56d5fe44227a6a5d64387f01001/system@e3a0d81fad994ceca8c310a1a84b0adf-00000000000071cc-00064bca8077a2bc.journal
-rw-r-----+ 1 root      systemd-journal 8.0M Feb 27 16:02 /var/log/journal/7242c56d5fe44227a6a5d64387f01001/system@e3a0d81fad994ceca8c310a1a84b0adf-00000000000071ac-00064bca5764d21f.journal
-rw-r-----+ 1 root      systemd-journal 8.0M Feb 27 15:55 /var/log/journal/7242c56d5fe44227a6a5d64387f01001/system@e3a0d81fad994ceca8c310a1a84b0adf-000000000000716b-00064bc785c623b4.journal
-rw-r-----+ 1 root      systemd-journal 8.0M Feb 27 12:29 /var/log/journal/7242c56d5fe44227a6a5d64387f01001/system@e3a0d81fad994ceca8c310a1a84b0adf-0000000000007160-00064bc5f216702d.journal
-rw-r-----+ 1 root      systemd-journal 8.0M Feb 27 10:36 /var/log/journal/7242c56d5fe44227a6a5d64387f01001/system@e3a0d81fad994ceca8c310a1a84b0adf-000000000000711c-00064bc56c4ad48e.journal
-rw-r-----+ 1 root      systemd-journal 8.0M Feb 27 09:59 /var/log/journal/7242c56d5fe44227a6a5d64387f01001/system@e3a0d81fad994ceca8c310a1a84b0adf-0000000000007103-00064bc555589a17.journal
-rw-r-----+ 1 root      systemd-journal 8.0M Feb 27 09:52 /var/log/journal/7242c56d5fe44227a6a5d64387f01001/system@e3a0d81fad994ceca8c310a1a84b0adf-00000000000070bf-00064bc46ba1ff19.journal
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week03$ ls
config.txt  error.log  large-logs.txt  largest.sh
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week03$ cat large-logs.txt
=== 10 File Terbesar di /var/log ===
-rw-r-----+ 1 root      systemd-journal 8.0M Feb 27 16:45 /var/log/journal/7242c56d5fe44227a6a5d64387f01001/system.journal
-rw-r-----+ 1 root      systemd-journal 8.0M Feb 27 16:33 /var/log/journal/7242c56d5fe44227a6a5d64387f01001/user-1000.journal
-rw-r-----+ 1 root      systemd-journal 8.0M Feb 27 16:29 /var/log/journal/7242c56d5fe44227a6a5d64387f01001/system@e3a0d81fad994ceca8c310a1a84b0adf-00000000000071e2-00064bca97abde41.journal
-rw-r-----+ 1 root      systemd-journal 8.0M Feb 27 16:09 /var/log/journal/7242c56d5fe44227a6a5d64387f01001/system@e3a0d81fad994ceca8c310a1a84b0adf-00000000000071cc-00064bca8077a2bc.journal
-rw-r-----+ 1 root      systemd-journal 8.0M Feb 27 16:02 /var/log/journal/7242c56d5fe44227a6a5d64387f01001/system@e3a0d81fad994ceca8c310a1a84b0adf-00000000000071ac-00064bca5764d21f.journal
-rw-r-----+ 1 root      systemd-journal 8.0M Feb 27 15:55 /var/log/journal/7242c56d5fe44227a6a5d64387f01001/system@e3a0d81fad994ceca8c310a1a84b0adf-000000000000716b-00064bc785c623b4.journal
-rw-r-----+ 1 root      systemd-journal 8.0M Feb 27 12:29 /var/log/journal/7242c56d5fe44227a6a5d64387f01001/system@e3a0d81fad994ceca8c310a1a84b0adf-0000000000007160-00064bc5f216702d.journal
-rw-r-----+ 1 root      systemd-journal 8.0M Feb 27 10:36 /var/log/journal/7242c56d5fe44227a6a5d64387f01001/system@e3a0d81fad994ceca8c310a1a84b0adf-000000000000711c-00064bc56c4ad48e.journal
-rw-r-----+ 1 root      systemd-journal 8.0M Feb 27 09:59 /var/log/journal/7242c56d5fe44227a6a5d64387f01001/system@e3a0d81fad994ceca8c310a1a84b0adf-0000000000007103-00064bc555589a17.journal
-rw-r-----+ 1 root      systemd-journal 8.0M Feb 27 09:52 /var/log/journal/7242c56d5fe44227a6a5d64387f01001/system@e3a0d81fad994ceca8c310a1a84b0adf-00000000000070bf-00064bc46ba1ff19.journal
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week03$ cat error.log
find: ‘/var/log/private’: Permission denied
```

## Latihan 3.2
Buat pipeline yang:
1. Membaca /etc/passwd
2. Mengekstrak username (kolom pertama)
3. Mengurutkan alfabetis
4. Menyimpan ke file sorted-users.txt
Hint: Gunakan cut, sort, dan operator redirect.

## Jawaban

### pipeline
```bash
cut -d: -f1 /etc/passwd | sort > sorted-users.txt
```

### output
```bash
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week03$ cut -d: -f1 /etc/passwd | sort > sorted-users.txt
galihcandra@LAPTOP-QQ597UPT:~/Kuliah/Sem 2/praktikum-os/week03$ cat sorted-users.txt
_apt
backup
bin
daemon
dhcpcd
galihcandra
games
irc
landscape
list
lp
mail
man
messagebus
news
nobody
polkitd
proxy
root
sshd
sync
sys
syslog
systemd-network
systemd-resolve
systemd-timesync
uucp
uuidd
www-data
```

