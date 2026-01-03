 
# Laporan Praktikum Minggu 10
Topik: page-replacement

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

   Gunakan *reference string* berikut sebagai contoh:
   ```
   7, 0, 1, 2, 0, 3, 0, 4, 2, 3, 0, 3, 2
   ```
   Jumlah frame memori: **3 frame**.

2. **Implementasi FIFO**

   - Simulasikan penggantian halaman menggunakan algoritma FIFO.
   - Catat setiap *page hit* dan *page fault*.
   - Hitung total *page fault*.

3. **Implementasi LRU**

   - Simulasikan penggantian halaman menggunakan algoritma LRU.
   - Catat setiap *page hit* dan *page fault*.
   - Hitung total *page fault*.

4. **Eksekusi & Validasi**

   - Jalankan program untuk FIFO dan LRU.
   - Pastikan hasil simulasi logis dan konsisten.
   - Simpan screenshot hasil eksekusi.

5. **Analisis Perbandingan**

   Buat tabel perbandingan seperti berikut:

   | Algoritma | Jumlah Page Fault | Keterangan |
   |:--|:--:|:--|
   | FIFO | ... | ... |
   | LRU | ... | ... |


   - Jelaskan mengapa jumlah *page fault* bisa berbeda.
   - Analisis algoritma mana yang lebih efisien dan alasannya.

6. **Commit & Push**

   ```bash
   git add .
   git commit -m "Minggu 10 - Page Replacement FIFO & LRU"
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
1. Apa perbedaan utama FIFO dan LRU?

FIFO (First In First Out) mengganti halaman yang pertama kali masuk ke memori tanpa memperhatikan seberapa sering atau baru halaman tersebut digunakan. Sementara itu, LRU (Least Recently Used) mengganti halaman yang paling lama tidak digunakan berdasarkan riwayat akses. Perbedaan utamanya terletak pada kriteria penggantian halaman, yaitu urutan masuk pada FIFO dan waktu penggunaan terakhir pada LRU.

2. Mengapa FIFO dapat menghasilkan Belady’s Anomaly?

FIFO dapat menghasilkan Belady’s Anomaly karena algoritma ini tidak mempertimbangkan pola akses halaman. Penambahan jumlah frame memori justru dapat menyebabkan peningkatan page fault, karena halaman yang sering dibutuhkan bisa terhapus hanya karena masuk lebih awal ke memori, meskipun masih sering digunakan.

3. Mengapa LRU umumnya menghasilkan performa lebih baik dibanding FIFO?

LRU umumnya menghasilkan performa lebih baik karena algoritma ini mempertimbangkan prinsip locality of reference, yaitu halaman yang baru digunakan kemungkinan besar akan digunakan kembali dalam waktu dekat. Dengan mempertahankan halaman yang sering atau baru diakses, LRU mampu mengurangi jumlah page fault dibandingkan FIFO.

---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?  
- Bagaimana cara Anda mengatasinya?  

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
