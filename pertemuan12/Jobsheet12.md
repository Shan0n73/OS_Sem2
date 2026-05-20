# JOBSHEET - 12

## Latihan
### Latihan 10.1 Audit Layanan dan Analisis Boot
Lakukan audit menyeluruh terhadap layanan yang berjalan di sistem.
1. Jalankan systemctl list-units –type=service –state=running dan catat semua layanan aktif. Pilih tiga layanan yang kamu kenal, periksa status masing-masing dengansystemctl status, dan jelaskan fungsinya.

=<img width="1070" height="514" alt="Screenshot 2026-05-20 200459" src="https://github.com/user-attachments/assets/faba0260-e3af-4284-8854-bb5b90c47b9d" />

- cron.service
berfungsi sebagai penjadwal tugas (task scheduler) otomatis di latar belakang untuk mengeksekusi perintah atau skrip pada waktu dan interval yang telah ditentukan.
- rsyslog.service
berfungsi untuk mengumpulkan, menyaring, dan mencatat segala aktivitas serta pesan log dari sistem operasi dan aplikasi ke dalam berkas teks di direktori /var/log/.
- systemd-journald.service
berfungsi untuk menangkap data log boot, kernel, serta output dari service lain, lalu menyimpannya dalam format biner yang dapat diakses via perintah.

2. Jalankan systemd-analyze blame dan identifikasi lima layanan dengan waktu inisialisasi terlama. Tampilkan hasilnya menggunakan pipeline: systemd-analyze blame | head -5.

=<img width="452" height="101" alt="Screenshot 2026-05-20 201202" src="https://github.com/user-attachments/assets/953f3282-bb65-4d73-832e-de9fe3d28d88" />

- snap.microk8s.daemon-containerd.service (1 menit 1.750 detik)
Layanan container runtime yang dipakai oleh MicroK8s untuk mengelola siklus hidup kontainer Kubernetes.

- snapd.seeded.service (46.639 detik)
Layanan yang berfungsi untuk menginisialisasi dan memasang snap paket bawaan (pre-seeded snaps) saat sistem pertama kali dinyalakan.

- snapd.service (44.867 detik)
Daemon utama penyedia layanan pengelolaan paket Snap (Snap package manager) di sistem Ubuntu.

- apport.service (18.489 detik)
Layanan yang menjadi pelapor otomatis jika terjadi kesalahan (crash report) pada sistem atau aplikasi di Ubuntu.

- grub-common.service (12.233 detik)
Layanan yang melakukan konfigurasi berkala dan pencatatan kepatuhan bootloader GRUB saat sistem dinyalakan.

3. Jalankan systemctl –failed dan dokumentasikan hasilnya. Jika ada layanan yang gagal, cari tahu penyebabnya dengan journalctl -u nama-layanan -n 30.

=<img width="420" height="70" alt="image" src="https://github.com/user-attachments/assets/5cdcce23-3629-46e1-a86c-9aae0c2a01af" />


### Latihan 10.2 Layanan Kustom dengan Restart Otomatis
Buat layanan systemd kustom yang mendemonstrasikan fitur restart otomatis.
1. Buat skrip Bash (referensi Bab 7) bernama monitor-disk.sh yang setiap 30 detik menuliskan penggunaan disk ke berkas log. Gunakan df -h dan date.

=<img width="999" height="173" alt="image" src="https://github.com/user-attachments/assets/d4e9a6e5-6c4e-4bd7-866b-2163eb17af72" />


2. Buat berkas unit /etc/systemd/system/monitor-disk.service untuk menjalankan skrip tersebut dengan konfigurasi: Restart=always, RestartSec=5s, dan berjalan sebagai pengguna kamu sendiri.

=<img width="407" height="19" alt="image" src="https://github.com/user-attachments/assets/37b07333-4220-4f79-b5cc-fac39bb6affe" />

<img width="1004" height="209" alt="image" src="https://github.com/user-attachments/assets/ae4dfb3d-e8c7-4c66-9ffc-be038236c6c3" />



3. Aktifkan dan jalankan layanan. Verifikasi dengan systemctl status dan pastikan log masuk ke journal.

=<img width="852" height="84" alt="image" src="https://github.com/user-attachments/assets/1784c4e7-9fd4-4121-b36a-0fe9da76e636" />

q<img width="1291" height="366" alt="image" src="https://github.com/user-attachments/assets/c232f29f-542d-4ce2-8fc6-3f6b0592c34f" />


4. Simulasikan crash dengan membunuh proses secara paksa (kill -9), tunggu 10 detik, dan verifikasi bahwa layanan hidup kembali secara otomatis.

=<img width="1285" height="400" alt="image" src="https://github.com/user-attachments/assets/78d3b4d1-7a49-40cc-8ab3-05f3b8858637" />

PIDnya digantikan, yang berarti telah layanan hidup kembali secara otomatis.

5. Bersihkan: nonaktifkan layanan dan hapus berkas unit setelah selesai.


### Latihan 10.3 Investigasi Log dan Keamanan SSH
Analisis log sistem dan tingkatkan keamanan konfigurasi SSH.
1. Gunakan journalctl -b -p err untuk menemukan semua error sejak boot terakhir. Simpan hasilnya ke berkas dan hitung jumlah baris dengan wc -l.



2. Lakukan tiga perubahan keamanan pada /etc/ssh/sshd_config: tambahkan PermitRootLogin no, MaxAuthTries 3, dan LoginGraceTime 30. Ikuti alur aman: backup, edit, validasi sshd-t, reload.



3. Setelah reload, verifikasi tiga hal: layanan masih berjalan (systemctl status ssh), port masih mendengarkan (ss -tlnp | grep ssh), dan konfigurasi baru terbaca (grep -E "PermitRoot|MaxAuth|GraceTime" /etc/ssh/sshd_config).



4. Kembalikan konfigurasi SSH ke kondisi semula menggunakan berkas backup.
