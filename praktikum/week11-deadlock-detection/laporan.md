
# Laporan Praktikum Minggu 11
Topik: deadlock-detection

---

## Identitas
- **Nama**  : Akhmad Raffi Sarmadan 
- **NIM**   : 250202974
- **Kelas** : 1IKRA

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
1. **Menyiapkan Dataset**

   Gunakan dataset sederhana yang berisi:
   - Daftar proses  
   - Resource Allocation  
   - Resource Request / Need

   Contoh tabel:

   | Proses | Allocation | Request |
   |:--:|:--:|:--:|
   | P1 | R1 | R2 |
   | P2 | R2 | R3 |
   | P3 | R3 | R1 |

2. **Implementasi Algoritma Deteksi Deadlock**

   Program minimal harus:
   - Membaca data proses dan resource.  
   - Menentukan apakah sistem berada dalam kondisi deadlock.  
   - Menampilkan proses mana saja yang terlibat deadlock.

3. **Eksekusi & Validasi**

   - Jalankan program dengan dataset uji.  
   - Validasi hasil deteksi dengan analisis manual/logis.  
   - Simpan hasil eksekusi dalam bentuk screenshot.

4. **Analisis Hasil**

   - Sajikan hasil deteksi dalam tabel (proses deadlock / tidak).  
   - Jelaskan mengapa deadlock terjadi atau tidak terjadi.  
   - Kaitkan hasil dengan teori deadlock (empat kondisi).

5. **Commit & Push**

   ```bash
   git add .
   git commit -m "Minggu 11 - Deadlock Detection"
   git push origin main
   ```


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
1. Apa perbedaan antara deadlock prevention, avoidance, dan detection?

Deadlock prevention bertujuan mencegah deadlock sejak awal dengan menghilangkan salah satu dari empat kondisi deadlock, misalnya dengan membatasi penggunaan resource. Deadlock avoidance berusaha menghindari deadlock dengan memeriksa keadaan sistem sebelum mengalokasikan resource, seperti pada algoritma Banker. Sementara itu, deadlock detection mengizinkan deadlock terjadi, tetapi sistem secara berkala melakukan pemeriksaan untuk mendeteksi deadlock dan kemudian melakukan pemulihan.

2. Mengapa deteksi deadlock tetap diperlukan dalam sistem operasi?

Deteksi deadlock tetap diperlukan karena tidak semua sistem dapat menerapkan prevention atau avoidance secara efisien. Pada sistem dengan banyak proses dan resource yang dinamis, lebih realistis untuk mengizinkan deadlock terjadi dan kemudian mendeteksinya daripada membatasi penggunaan resource secara ketat atau melakukan pemeriksaan kompleks sebelum setiap alokasi.

3. Apa kelebihan dan kekurangan pendekatan deteksi deadlock?

Kelebihan pendekatan deteksi deadlock adalah fleksibilitas yang tinggi karena sistem tidak perlu membatasi alokasi resource sejak awal. Namun, kekurangannya adalah adanya overhead tambahan untuk melakukan proses deteksi serta risiko terganggunya proses ketika sistem harus melakukan pemulihan, seperti menghentikan atau menggulir ulang proses.  

---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?  
- Bagaimana cara Anda mengatasinya?  

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
