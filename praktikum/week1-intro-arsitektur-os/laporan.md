
# Laporan Praktikum Minggu 1
Topik: [Tuliskan judul topik, misalnya "Arsitektur Sistem Operasi dan Kernel"]

---

## Identitas
- **Nama**  : Akhmad Raffi Sarmadan
- **NIM**   : 250202974
- **Kelas** : 1IKRA

---

## Tujuan
Percobaan ini bertujuan untuk memvisualisasikan dan memahami cara kerja sistem operasi dalam menghubungkan pengguna, aplikasi, dan perangkat keras melalui struktur berlapis yang diatur oleh kernel dan system call interface.

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
1. Sistem operasi memiliki arsitektur berlapis (layered architecture) yang mengatur hubungan antara pengguna, aplikasi, sistem operasi, dan perangkat keras agar sistem berjalan secara terstruktur dan efisien.

2. Kernel merupakan inti dari sistem operasi yang berperan penting dalam mengelola sumber daya komputer, termasuk proses, memori, sistem berkas, dan perangkat I/O. Tanpa kernel, sistem operasi tidak dapat berfungsi.

3. System Call Interface berfungsi sebagai jembatan antara program aplikasi dan kernel. Melalui system call, aplikasi dapat meminta layanan dari sistem operasi tanpa harus mengakses perangkat keras secara langsung.

---

## Quiz
1. Sebutkan tiga fungsi utama sistem operasi!
   Jawaban: Manajemen Proses (Process Management)
Mengatur pembuatan, penjadwalan, dan penghentian proses agar CPU dapat digunakan secara efisien.

Manajemen Memori (Memory Management)
Mengatur penggunaan memori utama (RAM), termasuk alokasi dan pembebasan ruang memori untuk proses yang sedang berjalan.

Manajemen Input/Output dan Sistem Berkas (I/O & File System Management)
Mengontrol akses ke perangkat keras (seperti disk, printer, keyboard) dan mengatur penyimpanan serta pengambilan data pada sistem berkas.

2. Jelaskan perbedaan antara kernel mode dan user mode!
   Jawaban: Kernel mode digunakan oleh sistem operasi untuk mengontrol perangkat keras, sedangkan user mode digunakan oleh program aplikasi dengan hak terbatas agar sistem tetap aman.
   
3. Sebutkan contoh OS dengan arsitektur monolithic dan microkernel!
   Jawaban: Monolithic Kernel:
Semua fungsi utama sistem operasi dijalankan dalam satu ruang kernel sehingga kinerjanya cepat, tapi rentan terhadap kesalahan sistem.
Contohnya: Linux, Unix, MS-DOS.

Microkernel:
Hanya fungsi inti yang ada di kernel, sedangkan layanan lain dijalankan di user space agar lebih stabil dan mudah dikembangkan.
Contohnya: Minix, QNX, Mach (macOS, iOS).

---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?  memahami fungsi OS
- Bagaimana cara Anda mengatasinya?  bertanya kepada teman dan mereview materi di internet agar lebih paham

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
