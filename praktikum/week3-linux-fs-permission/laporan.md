
# Laporan Praktikum Minggu 3
Topik: linux-fs-permission

---

## Identitas
- **Nama**  : Akhmad Raffi Sarmadan
- **NIM**   : 250202974 
- **Kelas** :1IKRA
---

## Tujuan
Tuliskan tujuan praktikum minggu ini.  
Contoh:  
> Mahasiswa mampu menjelaskan fungsi utama sistem operasi dan peran kernel serta system call.

---

## Dasar Teori
Tuliskan ringkasan teori (3–5 poin) yang mendasari percobaan.

---

## Langkah Praktikum
1. Langkah-langkah yang dilakukan.  
2. Perintah yang dijalankan.  
3. File dan kode yang dibuat.  
4. Commit message yang digunakan.

---

## Kode / Perintah
Tuliskan potongan kode atau perintah utama:
```bash
uname -a
lsmod | head
dmesg | head
```

---

## Hasil Eksekusi
Sertakan screenshot hasil percobaan atau diagram:
![Screenshot hasil](screenshots/example.png)

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
