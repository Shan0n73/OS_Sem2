# JOBSHEET-10
## Studi Kasus
### Studi Kasus 10.1
Skenario: Server aplikasi terasa lambat saat banyak pengguna aktif. Administrator
perlu menentukan apakah penyebabnya adalah kekurangan memori.

Langkah 1: Periksa kondisi memori secara keseluruhan.
free-h

<img width="657" height="71" alt="Screenshot 2026-05-05 205450" src="https://github.com/user-attachments/assets/f15c3476-6beb-489d-8add-f7f1adc2ec34" />


Langkah 2: Pantau proses secara real-time.
top

<img width="1036" height="806" alt="Screenshot 2026-05-05 205722" src="https://github.com/user-attachments/assets/5098b8b6-be64-4489-ac87-3ef1313c646c" />

Di dalam top: tekan M untuk mengurutkan berdasarkan memori, tekan q
untuk keluar.

Analisis:
1. Apakah nilai available sangat kecil (misalnya di bawah 200 MB pada server
dengan RAM 2 GB)? Jika ya, server kemungkinan kekurangan memori.
> Ya, dibawah 200 mb
2. Apakah kolom used pada baris Swap lebih dari 0? Jika ya, kernel sedang
menggunakan swap, yang berarti performa menurun.
> Masih 0
3. Di tampilan top, proses apa yang memiliki %MEM terbesar? Proses tersebut
menjadi kandidat utama penyebab lambatnya server.
> proses dengan 18.8

### Studi Kasus 10.2
Skenario: Program tidak dapat membaca file konfigurasi. Penyebab umum: file
tidak ada, path salah, atau permission tidak sesuai. Kita akan mensimulasikan
kondisi ini dan mengamati pesan error yang dihasilkan.

Langkah 1: Buat direktori dan file konfigurasi contoh.
mkdir-p ~/praktikum-os/week10-memory/syscall-case
cd ~/praktikum-os/week10-memory/syscall-case
echo "PORT=8080" > app.conf
ls-l app.conf
cat app.conf

<img width="743" height="99" alt="image" src="https://github.com/user-attachments/assets/477e0813-e7bc-47fc-8524-fbc87bab8c05" />


Langkah 2: Simulasikan permission bermasalah.
chmod 000 app.conf
cat app.conf

<img width="679" height="53" alt="image" src="https://github.com/user-attachments/assets/f306559e-5edb-4e65-91e2-c18c61693d87" />


Output akan menampilkan: cat: app.conf: Permission denied. Ini terjadi
karena system call openat() gagal — kernel menolak permintaan membuka file
karena tidak ada bit izin baca (r).

Langkah 3: Kembalikan permission dan verifikasi.
chmod 644 app.conf
cat app.conf

<img width="718" height="51" alt="image" src="https://github.com/user-attachments/assets/671f00d2-49d8-426c-83ad-948c349d3b9b" />


Analisis:
1. Mengapa cat menghasilkan Permission denied setelah chmod 000? System
call apa yang gagal?
> openat(), karena ditolak oleh kernel
2. Apa perbedaan pesan error Permission denied vs No such file or directory?
Coba rm app.conf lalu cat app.conf untuk melihat perbedaannya.
> Permission denied: file ada tapi ditolak kernel; No such file or directory: File benar" tidak ditemukan/tidak ada (bisa karena rm atau belum dibuat)
3. Permission 644 berarti apa untuk owner, group, dan others?
> 6 = owner, bisa baca tulis (rw-); 4 = group, hanya bisa baca (r--); 4 = other, hanya bisa baca (r--)


## Tugas Praktikum
### Tugas 10.1 Audit Penggunaan Memori Sistem
Instruksi Umum: Kerjakan seluruh tugas pada direktori berikut.
mkdir -p ~/ praktikum - os / week10 - memory
cd ~/ praktikum - os / week10 - memory

<img width="760" height="363" alt="Screenshot 2026-05-05 213625" src="https://github.com/user-attachments/assets/3e677f0a-0c0c-4f4d-bd13-60348ba7c857" />


chmod +x ~/praktikum-os/week10-memory/memory-audit.sh
cd ~/praktikum-os/week10-memory
bash memory-audit.sh

<img width="655" height="502" alt="image" src="https://github.com/user-attachments/assets/9e152f7c-faaa-46d1-8ef5-c08da0e8b975" />


Analisis
1. Hitung persentase memori tersedia (available / total × 100%). Apakah
sistem dalam kondisi normal?
= Sekitar ~51%-an.
2. Mengapa buff/cache tidak dihitung sebagai memori yang terpakai dari sudut
pandang ketersediaan untuk aplikasi?
= buff/cache terhitung sebagai memori yang digunakan oleh kernel untuk mempercepat akses data (seperti membaca file dari disk).
   Karena bersifat Reclaimable (Dapat Diambil Kembali). Juga untuk Optimalisasi RAM dan Perspektif Aplikasi.


3. Dari /proc/meminfo, apakah SwapTotal lebih besar dari 0? Berapa nilai SwapFree?
= SwapTotal tidak lebih besar dari 0 dan untuk nilai SwapFree adalah 0 kb


### Tugas 10.2 Identifikasi Proses dengan Memori Tertinggi
Instruksi: Simpan daftar 10 proses pengguna memori terbesar ke file.
ps aux -- sort = -% mem | head -n 10 > top - memory - process . txt
cat top - memory - process . txt

-

Analisis
1. Proses apa di urutan pertama? Catat nilai %MEM dan RSS.
=
2. Konversikan RSS ke MB (bagi 1024). Apakah wajar?
= 
3. Jumlahkan %MEM dari 5 proses teratas. Berapa persen RAM yang mereka
gunakan bersama?
= 



### Tugas 10.3 Membuat dan Memverifikasi Swap File
Instruksi: Buat swap file khusus tugas sebesar 256 MB dan verifikasi.
sudo fallocate -l 256M /swapfile-tugas-week10
sudo chmod 600 /swapfile-tugas-week10
sudo mkswap /swapfile-tugas-week10
sudo swapon /swapfile-tugas-week10

-

Analisis
1. Identifikasi kolom NAME, TYPE, SIZE, dan USED pada output swapon –show.
=

2. Apakah nilai total pada baris Swap di free -h bertambah 256 MB?
= 

3. Mengapa permission 600 penting? Apa risiko jika diatur ke 644?
=



### Tugas 10.4 Analisis System Call dengan strace
Instruksi: Analisis system call yang dipanggil perintah ls.
strace -c ls 2 > strace - summary . txt
strace ls / etc 2 > strace - ls - etc . txt
cat strace - summary . txt

-

Analisis
1. Sebutkan minimal 5 system call dari strace-summary.txt beserta fungsi singkatnya.
= 

2. System call mana yang paling sering dipanggil? Mengapa?
= 
3. Apakah ada errors lebih dari 0? Apakah program tetap berjalan normal
meskipun ada kegagalan tersebut?
= 

### Tugas 10.5 Studi Kasus Diagnosa Server Lambat
Skenario: Server terasa lambat. Buat script diagnosa yang menggabungkan semua
pemeriksaan dari bab ini menggunakan fungsi Bash.
nano ~/praktikum-os/week10-memory/diagnosa-server.sh

-

bash monitor - memori . sh

-

Analisis
1. Jelaskan peran masing-masing fungsi: cek_memori, cek_swap, cek_proses,
cek_paging, dan ringkasan. Mengapa diagnosa dipecah menjadi fungsi
terpisah?
=
2. Berdasarkan bagian RINGKASAN, apakah kondisi sistem normal atau kritis?
Jelaskan berdasarkan nilai threshold yang digunakan script.
=
3. Mengapa script menggunakan tee "$LAPORAN" bukan redirection biasa >
"$LAPORAN"? Apa keuntungannya?
= 
4. Dari output cek_paging, apakah ada aktivitas si atau so? Jika ada, apa
implikasinya terhadap performa server?
= 
