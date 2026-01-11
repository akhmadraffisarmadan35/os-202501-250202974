 
# Laporan Praktikum Minggu 10
Topik: page-replacement

---

## Identitas
- **Nama**  : Akhmad Raffi Sarmadan
- **NIM**   : 250202974 
- **Kelas** : 1IKRA

---

## Tujuan
- Tuliskan tujuan praktikum minggu ini.  
Tujuan dari percobaan algoritma Page Replacement FIFO (First-In First-Out) dan LRU (Least Recently Used) adalah untuk memahami cara kerja masing-masing algoritma dalam mengelola memori utama, khususnya dalam menentukan halaman yang harus digantikan ketika terjadi kekurangan frame. Selain itu, percobaan ini bertujuan untuk membandingkan kinerja kedua algoritma berdasarkan jumlah page fault yang dihasilkan, sehingga dapat diketahui algoritma mana yang lebih efisien dalam mempertahankan halaman yang sering digunakan dan meminimalkan terjadinya page fault.
---

## Dasar Teori
1. Algoritma FIFO (First-In First-Out)

FIFO merupakan algoritma page replacement yang mengganti halaman berdasarkan urutan kedatangan. Halaman yang pertama kali masuk ke memori akan menjadi halaman pertama yang digantikan. Algoritma ini sederhana, namun tidak mempertimbangkan frekuensi atau pola akses halaman, sehingga dapat menghasilkan page fault yang lebih banyak.

2. Algoritma LRU (Least Recently Used)
LRU adalah algoritma page replacement yang mengganti halaman yang paling lama tidak digunakan. Algoritma ini bekerja berdasarkan prinsip locality of reference, yaitu kecenderungan proses untuk mengakses kembali halaman yang baru saja digunakan. Oleh karena itu, LRU umumnya lebih efisien dibandingkan FIFO dalam mengurangi jumlah page fault.
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
```python
# Dataset dan jumlah frame
pages = [7, 0, 1, 2, 0, 3, 0, 4, 2, 3, 0, 3, 2]
frame_size = 3

frames = []
queue_index = 0
page_fault = 0

print(f"Dataset Loaded: {pages}")
print(f"Jumlah Frame  : {frame_size}\n")

print("=" * 50)
print(" SIMULASI FIFO (First-In First-Out)")
print("=" * 50)
print("| No | Page | Status | Isi Frame (Memori) |")
print("-" * 50)

for i, page in enumerate(pages, start=1):
    if page in frames:
        status = "HIT"
    else:
        status = "MISS"
        page_fault += 1

        if len(frames) < frame_size:
            frames.append(page)
        else:
            frames[queue_index] = page
            queue_index = (queue_index + 1) % frame_size

    # Menampilkan frame dengan tanda '-' jika belum penuh
    display_frames = frames + ['-'] * (frame_size - len(frames))
    frame_str = " ".join(map(str, display_frames))

    print(f"| {i:2} | {page:4} | {status:6} | [ {frame_str} ] |")

print("-" * 50)
print(f"Total Page Fault FIFO: {page_fault}")




pages = [7, 0, 1, 2, 0, 3, 0, 4, 2, 3, 0, 3, 2]
frame_size = 3

stack = []
page_fault = 0

print("=" * 55)
print(" SIMULASI LRU (Least Recently Used)")
print("=" * 55)
print("| No | Page | Status | Isi Frame (Stack Visual) |")
print("-" * 55)

for i, page in enumerate(pages, start=1):
    if page in stack:
        status = "HIT"
        stack.remove(page)
        stack.append(page)
    else:
        status = "MISS"
        page_fault += 1

        if len(stack) < frame_size:
            stack.append(page)
        else:
            stack.pop(0)   # hapus yang paling lama digunakan
            stack.append(page)

    # Tampilan frame
    display_stack = stack + ['-'] * (frame_size - len(stack))
    stack_view = " ".join(map(str, display_stack))

    print(f"| {i:2} | {page:4} | {status:6} | [ {stack_view} ] |")

print("-" * 55)
print(f"Total Page Fault LRU : {page_fault}")


```

---

## Hasil Eksekusi
Sertakan screenshot hasil percobaan atau diagram:
![alt text](<screenshots/FIFO.png>)
![alt text](<screenshots/LRU.png>)
## Tabel Perbandingan Algoritma

| Algoritma | Jumlah Page Fault | Keterangan |
|-----------|:-----------------:|------------|
| FIFO (First-In First-Out) | 10 | Membuang halaman berdasarkan waktu masuk tanpa mempertimbangkan frekuensi akses. |
| LRU (Least Recently Used) | 9 | Mempertahankan halaman yang baru saja digunakan untuk meminimalkan terjadinya page fault. |



---

## Analisis

1. Makna Hasil Percobaan
Hasil percobaan menunjukkan bahwa algoritma LRU menghasilkan page fault lebih sedikit (9) dibandingkan FIFO (10). Hal ini membuktikan bahwa LRU lebih efisien karena mempertahankan halaman yang masih sering digunakan, sedangkan FIFO hanya mempertimbangkan urutan masuk halaman.

2. Keterkaitan dengan Teori Sistem Operasi
Algoritma FIFO dan LRU merupakan bagian dari manajemen memori kernel. Ketika terjadi page fault, kernel melalui system call memuat halaman dari disk ke memori utama. LRU lebih optimal karena sesuai dengan prinsip locality of reference, sehingga dapat mengurangi frekuensi page fault.

3. Perbedaan pada Lingkungan OS (Linux vs Windows)
Pada praktiknya, hasil dapat berbeda antara Linux dan Windows. Linux menggunakan pendekatan LRU approximation, sedangkan Windows menerapkan working set model. Perbedaan kebijakan kernel dan arsitektur manajemen memori ini memengaruhi efisiensi page replacement di masing-masing sistem operasi.

---

## Kesimpulan
1. Algoritma LRU lebih efisien dibandingkan FIFO karena menghasilkan jumlah page fault yang lebih sedikit, sehingga lebih optimal dalam pengelolaan memori.

2. Perbedaan hasil terjadi karena LRU mempertimbangkan riwayat penggunaan halaman, sedangkan FIFO hanya berdasarkan urutan masuk tanpa memperhatikan pola akses.

3. Implementasi algoritma page replacement sangat bergantung pada kebijakan kernel sistem operasi, sehingga hasil nyata dapat berbeda antara sistem operasi seperti Linux dan Windows.
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
