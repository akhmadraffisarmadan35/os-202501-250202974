
# Laporan Praktikum Minggu 1
Topik: [Tuliskan judul topik, misalnya "Arsitektur Sistem Operasi dan Kernel"]

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
1. Lapisan Arsitektur Sistem Operasi
Gambar menunjukkan struktur berlapis (layered architecture) di mana sistem operasi memisahkan fungsinya menjadi beberapa lapisan — mulai dari pengguna (user) hingga perangkat keras (hardware).
2. Peran Kernel (Inti Sistem Operasi)
Kernel adalah inti dari sistem operasi yang bertanggung jawab untuk mengelola sumber daya utama komputer seperti prosesor, memori, dan perangkat I/O.
3. System Call Interface (Antarmuka Panggilan Sistem)
Bagian ini adalah jembatan antara aplikasi dan kernel. Program aplikasi tidak dapat langsung mengakses sumber daya kernel, sehingga mereka menggunakan system calls untuk meminta layanan dari sistem operasi seperti membuka file, membuat proses, atau mengakses perangkat.
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
https://photos.app.goo.gl/dSyseLLXxtV4babB9

---

## Analisis
- makna hasil percobaan: 1. Menunjukkan Hirarki Interaksi Sistem Operasi
2. Menggambarkan Peran Kernel Sebagai Pengendali Utama
3. Menggambarkan Hubungan Abstraksi Antara Software dan Hardware
- Hubungkan hasil dengan teori (fungsi kernel, system call, arsitektur OS): •Arsitektur OS memberikan kerangka struktural (lapisan-lapisan).
•Kernel menjalankan fungsi utama dalam mengatur sumber daya di lapisan inti.
•System Call Interface menjadi penghubung antara aplikasi di lapisan atas dengan kernel di lapisan inti.
- Apa perbedaan hasil di lingkungan OS berbeda (Linux vs Windows)?: •Struktur fungsional sama, tapi mekanisme internal berbeda.
•Linux lebih fleksibel dan terbuka, cocok untuk riset dan pengembangan.
•Windows lebih tertutup namun stabil, cocok untuk pengguna umum dan aplikasi bisnis.

---

## Kesimpulan
Tuliskan 2–3 poin kesimpulan dari praktikum ini.

---

## Quiz
1. [Pertanyaan 1]  
   **Jawaban:**  
2. [Pertanyaan 2]  
   **Jawaban:**  
3. [Pertanyaan 3]  
   **Jawaban:**  

---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?  memahami fungsi OS
- Bagaimana cara Anda mengatasinya?  bertanya kepada teman dan mereview materi di internet agar lebih paham

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
