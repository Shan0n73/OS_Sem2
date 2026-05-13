# JOBSHEET - 11

## Latihan
### Latihan 9.A — Audit dan Kolaborasi
1. Temukan file SUID aktif dengan find / -perm -4000 -type f 2>/dev/null, lalu jelaskan
tiga file yang Anda kenali beserta alasannya.

<img width="1120" height="582" alt="image" src="https://github.com/user-attachments/assets/54660615-be00-499e-8132-a7c1bd030b6d" />

- /usr/bin/passwd -> File ini memiliki bit SUID agar pengguna biasa dapat mengubah password mereka sendiri. Saat dijalankan, program ini membutuhkan akses tulis ke file /etc/shadow yang hanya dimiliki oleh root.
- /usr/bin/sudo -> SUID memungkinkan pengguna yang terdaftar di sudoers untuk menjalankan perintah dengan hak akses root.
- /usr/bin/mount -> Digunakan untuk memasang (mount) sistem berkas atau perangkat (misal USB drive ataupun ISO) ke dalam hirarki direktori Linux. Teknisnya, operasi memerlukan hak akses root agar berinteraksi langsung dengan kernel dan perangkat keras, sehingga bit SUID di-pin agar user biasa bisa melakukan mount pada titik-titik tertentu yang telah diizinkan.


2. Cari direktori world-writable dan tentukan mana yang valid dan mana yang berisiko.

<img width="1170" height="342" alt="image" src="https://github.com/user-attachments/assets/fec8857e-1826-43e1-9c02-75096a03e5d0" />

- Valid : Direktori /tmp dan /var/tmp. Karena arena digunakan untuk menyimpan file sementara oleh berbagai pengguna dan proses, namun biasanya dilindungi dengan "Sticky Bit" agar pengguna tidak bisa menghapus file milik orang lain.
- Berisiko : Direktori /var/crash. Karena jika direktori ini dapat ditulis oleh semua orang tanpa "Sticky Bit", penyerang bisa memanipulasi laporan kerusakan (crash reports) untuk menyembunyikan jejak aktivitas mereka atau mencoba melakukan eksploitasi lokal.


3. Rancang konfigurasi permission standar dan ACL untuk direktori proyek /srv/webapp/ agar
group webapp-team dapat menulis, user deploy hanya membaca, dan file baru selalu mewarisi
group proyek.

<img width="1169" height="483" alt="image" src="https://github.com/user-attachments/assets/18d8a026-8e7c-4c30-9b3c-48bd68638896" />

<img width="671" height="242" alt="image" src="https://github.com/user-attachments/assets/16e65d17-3a3c-4f70-ac55-ec60a0b3aad5" />


<img width="1171" height="337" alt="image" src="https://github.com/user-attachments/assets/e7905660-9392-414a-b8d7-0eec5a47f605" />



###  Latihan 9.B — Kebijakan Akun dan Quota
Tuliskan langkah untuk membuat user intern, menambahkannya ke group labgroup, memaksa pergantian password tiap 45 hari (warning 7 hari), memberi izin sudo hanya untuk systemctl status, dan menetapkan quota ruang serta inode sederhana pada /home/.




