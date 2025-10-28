
# Laporan Praktikum Minggu 3
Topik: linux-fs-permission

---

## Identitas
- **Nama**  : Akhmad Raffi Sarmadan
- **NIM**   : 250202974 
- **Kelas** :1IKRA
---

## Tujuan
-Mengenal direktori kerja dan sistem file Linux
-Menggunakan perintah dasar seperti pwd, ls, dan cd untuk menavigasi sistem file.
---

## Dasar Teori
1. Abraham Silberschatz, Peter Baer Galvin, Greg Gagne — Operating System Concepts (2018)
Buku ini menjelaskan bahwa sistem operasi mengatur sumber daya komputer, termasuk manajemen file. Setiap file memiliki atribut dan hak akses yang diatur untuk menjaga keamanan data. Mekanisme seperti access control menentukan siapa yang dapat membaca, menulis, atau mengeksekusi file.
➡️ Relevansi: Konsep ini diterapkan saat menggunakan chmod dan chown untuk mengatur izin dan kepemilikan file.
2. Andrew S. Tanenbaum, Herbert Bos — Modern Operating Systems (2015)
Tanenbaum menekankan bahwa file system menyediakan struktur penyimpanan dan kontrol akses melalui permission bits (r, w, x) bagi owner, group, dan others. Hanya pengguna dengan hak superuser (root) yang dapat mengubah kepemilikan file.
➡️ Relevansi: Terlihat saat file diubah menjadi milik root dengan perintah sudo chown root.
3. Linux Manual Pages (man chmod, man chown, man ls)
Manual Linux menjelaskan fungsi perintah:
ls menampilkan atribut file,
chmod mengubah izin akses,
chown mengubah kepemilikan file.
➡️ Relevansi: Menjadi panduan utama penggunaan perintah dalam praktikum.
4. OSTEP — Operating Systems: Three Easy Pieces (2018)
OSTEP membahas sistem operasi sebagai pengelola virtualization, concurrency, dan persistence. Dalam konteks file system, dijelaskan pentingnya proteksi dan keamanan data melalui mekanisme izin dan kepemilikan file.
➡️ Relevansi: Menjelaskan dasar teoretis bagaimana sistem operasi mengatur akses file melalui kernel.
---

## Langkah Praktikum
1. Langkah-langkah yang dilakukan.  
2. Perintah yang dijalankan.
 jawab: pwd
ls -l
cd /tmp
ls -a
cat /etc/passwd | head -n 5
echo "Hello <NAME><NIM>" > percobaan.txt
ls -l percobaan.txt
chmod 600 percobaan.txt
ls -l percobaan.txt
sudo chown root percobaan.txt
ls -l percobaan.txt 
4. File dan kode yang dibuat.
 jawab: praktikum/week3-linux-fs-permission/screenshots/  
6. Commit message yang digunakan.
 jawab: git add .
git commit -m "Minggu 3 - Linux File System & Permission"
git push origin main
---

## Kode / Perintah
Tuliskan potongan kode atau perintah utama:
```bash
pwd
ls -l
cd /tmp
ls -a
cat /etc/passwd | head -n 5
echo "Hello <NAME><NIM>" > percobaan.txt
ls -l percobaan.txt
chmod 600 percobaan.txt
ls -l percobaan.txt
sudo chown root percobaan.txt
ls -l percobaan.txt
```

---

## Hasil Eksekusi
![alt text](screensots/
---

## Analisis
- Jelaskan makna hasil percobaan.  
- Hubungkan hasil dengan teori (fungsi kernel, system call, arsitektur OS).  
- Apa perbedaan hasil di lingkungan OS berbeda (Linux vs Windows)?  

---

## Kesimpulan
Tuliskan 2–3 poin kesimpulan dari praktikum ini.

---

## Quiz
1. Apa fungsi dari perintah chmod? 
   Jawaban: chmod (change mode) digunakan untuk mengubah hak akses (permission) pada file atau direktori di sistem operasi berbasis Unix/Linux
Hak akses yang bisa diubah adalah:
r (read) → hak untuk membaca isi file / melihat isi direktori
w (write) → hak untuk menulis atau mengubah file / menambah dan menghapus isi direktori
x (execute) → hak untuk menjalankan file (jika file executable atau script) / masuk ke dalam direktori
2. apa arti dari kode permissionrwxr-xr--? 
   Jawaban: Pemilik (owner) → rwx → dapat membaca, menulis, dan menjalankan.
Grup (group) → r-x → dapat membaca dan menjalankan, tapi tidak menulis.
Lainnya (others) → r-- → hanya dapat membaca  
3. Jelaskan perbedaan antara chown dan chmod 
   Jawaban:  chmod → mengatur apa yang boleh dilakukan oleh siapa.
chown → mengatur siapa yang memiliki file atau direktori tersebut.

---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?  
- Bagaimana cara Anda mengatasinya?  

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
