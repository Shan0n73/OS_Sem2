# JOBSHEET - 9

## LATIHAN
### Latihan 9.1
Modifikasi laporan-sistem.sh agar menyimpan output ke file laporan-YYYY-MM-DD.txt sekaligus menampilkannya di terminal. Petunjuk:
gunakan tee yang sudah dipelajari di bab sebelumnya.
<img width="1284" height="414" alt="Screenshot 2026-04-28 174333" src="https://github.com/user-attachments/assets/a7fff279-f231-44d0-a310-78e8bece84ca" />

<img width="875" height="468" alt="Screenshot 2026-04-28 174752" src="https://github.com/user-attachments/assets/2c172dbd-7d84-469b-a52f-321007960447" />



### Latihan 9.2
Buat script kalkulator.sh yang menerima tiga argumen: <angka1>
<operator> <angka2> dengan operator +, -, *, atau /. Contoh:
./kalkulator.sh 20 + 5 menghasilkan 25. Gunakan case untuk memilih
operasi, dan validasi jika argumen tidak lengkap.
<img width="873" height="773" alt="Screenshot 2026-04-28 181914" src="https://github.com/user-attachments/assets/02dae825-659c-4960-b89b-7b00814ed55f" />

<img width="462" height="43" alt="Screenshot 2026-04-28 182019" src="https://github.com/user-attachments/assets/fc8a3c68-4947-4f25-8223-1586c8b0f61e" />


### Latihan 9.3
Tambahkan ke script grading-batch.sh sebuah ringkasan di bagian bawah yang menampilkan: jumlah mahasiswa per grade (A, B, C, D, E) menggunakan
perulangan for kedua yang mengiterasi array MAHASISWA
<img width="805" height="571" alt="Screenshot 2026-04-28 204446" src="https://github.com/user-attachments/assets/4c4f1f7c-4fae-4322-836f-10f015c23036" />

<img width="372" height="233" alt="Screenshot 2026-04-28 204411" src="https://github.com/user-attachments/assets/7a546c6a-588d-47e2-9a63-9e2e9f31fa6e" />



### Latihan 9.4
Tambahkan fungsi konfirmasi() ke lib-validasi.sh. Fungsi ini menampilkan pertanyaan, membaca input Y/N dari user, mengembalikan
0 jika Y dan 1 jika N. Buat script demo yang memanggil fungsi ini sebelum menghapus sebuah file.
Terakhir, kita masuk ke Latihan 9.4. Di sini kita akan belajar membuat Library Script (file yang berisi kumpulan fungsi) dan cara memanggil fungsi tersebut dari script lain.
<img width="1017" height="311" alt="image" src="https://github.com/user-attachments/assets/3aaa2415-a90d-4e20-9e29-e81985d936ca" />
<img width="1014" height="237" alt="Screenshot 2026-04-28 211124" src="https://github.com/user-attachments/assets/8fb6e4e1-b4ab-4e3a-81c7-77da195bd9e6" />

<img width="538" height="133" alt="image" src="https://github.com/user-attachments/assets/e5b0955b-dca6-4e83-97b1-166042213576" />



### Latihan 9.5
Script debug-latihan.sh tidak menangani direktori yang tidak ada. Perbaiki
dengan menambahkan:
• set -e di baris kedua
• Pengecekan -d "$DIREKTORI" sebelum memanggil du
• Pesan error yang informatif jika direktori tidak ditemukan
Uji dengan direktori yang tidak ada.
<img width="1014" height="758" alt="image" src="https://github.com/user-attachments/assets/252dc147-c9da-4714-8297-cfdbe5fdbf10" />

<img width="627" height="94" alt="Screenshot 2026-04-28 213920" src="https://github.com/user-attachments/assets/fa904c4a-27c4-4dc4-bd3b-b1752a43b6d9" />



## PRAKTIKUM
### Tugas 1 Script Absensi Kelas
Konteks: instruktur mencatat kehadiran mahasiswa dari command line.
1. Buat script absensi.sh yang:
• Menerima argumen nama mahasiswa dan status (hadir/izin/alpha)
• Menyimpan entri ke absensi-YYYY-MM-DD.txt dengan format [HH:MM]
NAMA - STATUS
• Opsi -r: tampilkan rekapitulasi (jumlah per status)
• Opsi -h: tampilkan bantuan
2. Rekam minimal 5 entri dan tampilkan rekapitulasinya.
Konsep wajib: variabel, parameter posisional, getopts, if, for, fungsi, dan
redirection ke file.
<img width="1019" height="760" alt="image" src="https://github.com/user-attachments/assets/6dfd2872-5b6f-4b40-ac55-f32d615204c4" />
<img width="1017" height="119" alt="image" src="https://github.com/user-attachments/assets/84b5cee1-1e60-4da5-bf62-be81365d1a47" />

<img width="1017" height="258" alt="image" src="https://github.com/user-attachments/assets/d23154fa-a3ca-45fc-a6ed-a64d0236611d" />


### Tugas 2 Script Health Check Sistem
Konteks: administrator membuat pemeriksaan kondisi server sebelum maintenance.
1. Buat script healthcheck.sh menggunakan template profesional dari bagian
Best Practices.
2. Script menampilkan: tanggal/waktu, hostname, uptime, penggunaan CPU,
memori, dan disk untuk setiap filesystem yang terpasang.
3. Jika penggunaan disk mana pun melebihi 80%, tampilkan peringatan.
4. Simpan hasil ke healthcheck-YYYY-MM-DD.log dan tampilkan ke terminal
sekaligus menggunakan tee.
5. Opsi -t <persen> mengubah batas peringatan disk (default 80).
Konsep wajib: set -euo pipefail, trap, getopts, fungsi dengan local,
for, if, dan tee.
<img width="1015" height="757" alt="image" src="https://github.com/user-attachments/assets/f9292f32-ed0b-425b-8f20-8d53b82021f4" />
<img width="1017" height="74" alt="image" src="https://github.com/user-attachments/assets/5c157812-d4b8-4c7d-9fe2-c4b3571d4cc5" />


<img width="1015" height="566" alt="Screenshot 2026-04-28 232040" src="https://github.com/user-attachments/assets/b10d45f4-250f-4f06-893f-019620998be7" />


<img width="1018" height="17" alt="Screenshot 2026-04-28 232349" src="https://github.com/user-attachments/assets/87959f9e-b046-4d80-8814-1bdcaf088d9c" />


<img width="1017" height="738" alt="Screenshot 2026-04-28 232428" src="https://github.com/user-attachments/assets/99f13843-d5ca-448c-a991-2318c8ad7d3d" />




