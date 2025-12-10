
# Laporan Praktikum Minggu 7
Topik: concurrency-deadlock
---

## Identitas
- **Nama**  : Akhmad Raffi Sarmadan (Analisis),Ketua,Implementasi 
- **NIM**   : 250202974 
- **Kelas** :1IKRA

---

## Tujuan
Tuliskan tujuan praktikum minggu ini.  
1. Mengidentifikasi empat kondisi penyebab deadlock (*mutual exclusion, hold and wait, no preemption, circular wait*).  
2. Menjelaskan mekanisme sinkronisasi menggunakan *semaphore* atau *monitor*.  
3. Menganalisis dan memberikan solusi untuk kasus deadlock.  
4. Berkolaborasi dalam tim untuk menyusun laporan analisis.  
5. Menyajikan hasil studi kasus secara sistematis.  
---

## Dasar Teori
Di sini saya mempelajaari tentang materi Sinkronisasi Proses dan Masalah Deadlock di saat itu juga saya berlaku mencari akar masalah tersebut dengan mempraktekkan di apk bernama Visual Studio Code berbasis Python. 

---

## Langkah Praktikum
1. **Persiapan Tim**
   - Bentuk kelompok beranggotakan 3–4 orang.  
   - Tentukan ketua dan pembagian tugas (analisis, implementasi, dokumentasi).

2. **Eksperimen 1 – Simulasi Dining Philosophers (Deadlock Version)**
   - Implementasikan versi sederhana dari masalah *Dining Philosophers* tanpa mekanisme pencegahan deadlock.  
   - Contoh pseudocode:
     ```text
     while true:
       think()
       pick_left_fork()
       pick_right_fork()
       eat()
       put_left_fork()
       put_right_fork()
     ```
   - Jalankan simulasi atau analisis alur (boleh menggunakan pseudocode atau diagram alur).  
   - Identifikasi kapan dan mengapa deadlock terjadi.

 3. **Eksperimen 2 – Versi Fixed (Menggunakan Semaphore / Monitor)**
   - Modifikasi pseudocode agar deadlock tidak terjadi, misalnya:
     - Menggunakan *semaphore (mutex)* untuk mengontrol akses.
     - Membatasi jumlah filosof yang dapat makan bersamaan (max 4).  
     - Mengatur urutan pengambilan garpu (misal, filosof terakhir mengambil secara terbalik).  
   - Analisis hasil modifikasi dan buktikan bahwa deadlock telah dihindari.

4. **Eksperimen 3 – Analisis Deadlock**
   - Jelaskan empat kondisi deadlock dari versi pertama dan bagaimana kondisi tersebut dipecahkan pada versi fixed.  
   - Sajikan hasil analisis dalam tabel seperti contoh berikut:

     | Kondisi Deadlock | Terjadi di Versi Deadlock | Solusi di Versi Fixed |
     |------------------|---------------------------|------------------------|
     | Mutual Exclusion | Ya (satu garpu hanya satu proses) | Gunakan semaphore untuk kontrol akses |
     | Hold and Wait | Ya | Hindari proses menahan lebih dari satu sumber daya |
     | No Preemption | Ya | Tidak ada mekanisme pelepasan paksa |
     | Circular Wait | Ya | Ubah urutan pengambilan sumber daya |

5. **Eksperimen 4 – Dokumentasi**
   - Simpan semua diagram, screenshot simulasi, dan hasil diskusi di:
     ```
     praktikum/week7-concurrency-deadlock/screenshots/
     ```
   - Tuliskan laporan kelompok di `laporan.md` (format IMRaD singkat: *Pendahuluan, Metode, Hasil, Analisis, Diskusi*).

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
Eksperimen 1 – Simulasi Dining Philosophers (Deadlock Version)

![alt text](<screenshots/semaphore so.png>)
![alt text](<screenshots/semaphore so2.png>)

Output dan Analisis
![alt text](<screenshots/terminal so.png>)

Saya menggunakan solusi Mengatur Urutan Pengambilan Garpu (Asymmetric Solution), yang merupakan solusi paling sederhana untuk memecahkan kondisi Circular Wait.

Modifikasi Pseudocode (Asymmetric Solution)Kita membalik urutan pengambilan garpu hanya untuk satu filsuf (misalnya, filsuf terakhir, $i = N-1$):

WHILE TRUE:
    // ... (Thinking & Hungry states remain the same) ...

    IF i == (N - 1): // The last philosopher (e.g., Philosopher 4)
        // 1. Acquire RIGHT Fork first
        ACQUIRE Forks[(i + 1) MOD N] 
        // 2. Acquire LEFT Fork second
        ACQUIRE Forks[i]
    ELSE:
        // Standard: Acquire LEFT Fork first, then RIGHT
        ACQUIRE Forks[i] 
        ACQUIRE Forks[(i + 1) MOD N] 

    // ... (Eating & Release states remain the same) ...
END WHILE

Identifikasi Deadlock
Kapan Terjadi Deadlock? Deadlock terjadi ketika semua 5 filsuf berhasil melewati langkah 3 (ACQUIRE Forks[i]) hampir secara bersamaan.

Mengapa Terjadi Deadlock? Setiap filsuf sekarang memegang satu garpu (garpu kiri mereka) dan mencoba mendapatkan garpu kedua (garpu kanan) yang sedang dipegang oleh tetangga di sebelah kanannya. Ini menciptakan Ketergantungan Melingkar (Circular Wait). Tidak ada filsuf yang mau melepaskan garpu yang sudah dipegang (Hold and Wait), sehingga tidak ada yang bisa makan.

Analisis Hasil Modifikasi
Buktinya Deadlock Dihindari:

1.Jika semua filsuf (0, 1, 2, 3) berhasil mengambil garpu kiri mereka, Philosopher 4 akan memegang garpu kanan (Fork 0) terlebih dahulu.

2.Ketika Philosopher 4 mencoba mengambil garpu kiri (Fork 4), dia mungkin harus menunggu Philosopher 3 melepaskannya.

3.Namun, karena Philosopher 4 memegang Fork 0, Philosopher 0 tidak akan bisa menyelesaikan langkah pengambilannya (karena butuh Fork 1 yang dipegang oleh P1, dan Fork 0 yang sekarang dipegang oleh P4).

4.Pada akhirnya, Philosopher 4 akan mendapatkan garpu 4 dan mulai makan. Setelah Philosopher 4 selesai, dia akan melepaskan Fork 0 dan Fork 4.

5.Pelepasan Fork 0 akan memecahkan ketergantungan dan memungkinkan Philosopher 0 (atau P3) untuk melanjutkan, dan seterusnya.

Solusi Asimetris ini memecahkan kondisi Ketergantungan Melingkar karena tidak semua filsuf mengikuti pola melingkar yang sama dalam pengambilan sumber daya.

Analisis Deadlock

| Kondisi Deadlock  | Terjadi di Versi Deadlock (Naïve) | Solusi di Versi Fixed (Asymmetric) |
|-------------------|-----------------------------------|-------------------------------------|
| **1. Mutual Exclusion** | Ya. Semaphore `Semaphore(1)` memastikan satu garpu hanya bisa dipegang satu filsuf. | Tetap ada. Kondisi ini memang wajib; solusi tidak menghilangkannya, hanya bekerja mengatasinya. |
| **2. Hold and Wait** | Ya. Filsuf memegang garpu kiri sambil menunggu garpu kanan. | Diatasi. Meskipun masih memegang satu garpu, risiko deadlock menurun karena ada filsuf yang mengambil garpu dengan urutan berbeda sehingga memberi peluang progress. |
| **3. No Preemption** | Ya. Garpu tidak dapat direbut paksa; hanya dilepas sukarela. | Tetap ada. Karena garpu adalah sumber daya fisik, tidak bisa dipaksa lepas. Solusi bekerja di sekitar kondisi ini. |
| **4. Circular Wait** | Ya. Semua filsuf mengambil garpu dengan urutan yang sama (Kiri → Kanan), membentuk siklus tunggu. | Dipecahkan. Satu filsuf (misal P4) mengambil garpu dengan urutan terbalik (Kanan → Kiri), memutus rantai tunggu melingkar. |

---

## Analisis
1. Analisis versi *Dining Philosophers* yang menyebabkan deadlock dan versi fixed yang bebas deadlock.  

Analisis Perbandingan Versi Deadlock vs. Fixed
Versi Deadlock (Naïve) gagal karena menciptakan kondisi Ketergantungan Melingkar (Circular Wait). Versi Fixed (Asimetris) memecahkan kondisi ini dengan mengubah urutan pengambilan sumber daya untuk satu proses.

| Kondisi Deadlock   | Terjadi di Versi Deadlock (Naïve) | Solusi di Versi Fixed (Asymmetric) |
|--------------------|------------------------------------|-------------------------------------|
| **Mutual Exclusion** | Ya. Setiap garpu adalah sumber daya eksklusif (Semaphore = 1). | Tetap Ada. (Diperlukan agar garpu tidak digunakan bersamaan). |
| **Hold and Wait** | Ya. Filsuf memegang garpu kiri sambil menunggu garpu kanan. | Diatasi. Risiko diminimalisasi karena simetri dipecahkan, memastikan kemajuan minimal satu proses. |
| **No Preemption** | Ya. Garpu tidak dapat direbut paksa. | Tetap Ada. (Dipertahankan, karena garpu tidak bisa direbut). |
| **Circular Wait** | Ya. Semua P mengambil Kiri → Kanan, menciptakan rantai tunggu P0 → P1 → ... → P0. | Dipecahkan. Satu filsuf (P4) mengambil Kanan → Kiri, mematahkan rantai tunggu dan menjamin minimal satu garpu akan dilepaskan. |

2. Dokumentasikan hasil diskusi kelompok ke dalam `laporan.md`.  

3. Sertakan diagram atau screenshot hasil simulasi/pseudocode.   

- Diagram dan Pseudocode Alur KritisBerikut adalah diagram alur (visualisasi) dan perbandingan pseudocode yang menunjukkan perbedaan pada bagian paling kritis dari algoritma: pengambilan garpu.

A. Visualisasi MasalahDiagram berikut menunjukkan pengaturan meja dan garpu, di mana setiap Filsuf ($P$) membutuhkan dua garpu ($F$) dari total $N$ sumber daya untuk dapat makan.

B. Pseudocode Alur Kritis1.

1.Versi Deadlock (Naïve)Semua filsuf mengikuti aturan yang sama. Deadlock terjadi di baris kedua ACQUIRE.

| Langkah | Kode / Penjelasan |
|--------|--------------------|
| **Status Awal** | `STATUS = "Hungry"` |
| **1. Ambil Garpu Kiri** | `ACQUIRE Forks[i]` |
| **2. Ambil Garpu Kanan** | `ACQUIRE Forks[(i + 1) MOD N]` <br> *Akan ter-block jika semua filsuf sudah memegang garpu kiri* |
| **Status Setelah Sukses** | `STATUS = "Eating"` |
| **Release** | `// ... Release ...` |

2. Versi Fixed (Deadlock-Free - Asymmetric)

Dengan membalik urutan pengambilan garpu untuk filsuf terakhir (misalnya P4, di mana $i = N-1$), kita memecahkan kondisi Circular Wait.

| Langkah | Kode / Penjelasan |
|--------|--------------------|
| **Status Awal** | `STATUS = "Hungry"` |
| **Cek Filsuf Terakhir** | `IF i == (N - 1)` |
| **Jika Filsuf Terakhir** | Ambil garpu **kanan dulu**:<br>`ACQUIRE Forks[(i + 1) MOD N]`<br>lalu garpu **kiri**:<br>`ACQUIRE Forks[i]` |
| **Jika Bukan Filsuf Terakhir** | Ambil garpu **kiri dulu**:<br>`ACQUIRE Forks[i]`<br>lalu garpu **kanan**:<br>`ACQUIRE Forks[(i + 1) MOD N]` |
| **Status Setelah Sukses** | `STATUS = "Eating"` |
| **Release** | `// ... Release ...` |

5. Laporkan temuan penyebab deadlock dan solusi pencegahannya.  

---

## Kesimpulan
1.Penyebab Deadlock adalah Simetri Perilaku:Deadlock terjadi karena semua proses (thread) mencoba mengambil sumber daya (garpu) dalam urutan yang sama (Kiri $\rightarrow$ Kanan). Hal ini menciptakan Ketergantungan Melingkar (Circular Wait) yang melibatkan semua filsuf, memenuhi semua syarat Deadlock secara simultan.

2.Solusi Inti adalah Memecahkan Ketergantungan Melingkar:Deadlock dihindari bukan dengan menghindari Hold and Wait atau Mutual Exclusion, melainkan dengan mematahkan kondisi Circular Wait. Ini dicapai dengan memperkenalkan asimetri dalam aturan pengambilan sumber daya (misalnya, membuat satu filsuf mengambil garpu dalam urutan terbalik: Kanan $\rightarrow$ Kiri), sehingga menjamin bahwa rantai tunggu melingkar tidak akan terbentuk dan program dapat berlanjut.

---

## Quiz
1.Sebutkan empat kondisi utama penyebab deadlock.

Deadlock adalah situasi di mana serangkaian proses terhenti karena setiap proses menunggu sumber daya (resource) yang sedang dipegang oleh proses lain. Menurut Coffman Conditions, deadlock hanya akan terjadi jika keempat kondisi berikut terpenuhi secara bersamaan:

1.Mutual Exclusion (Saling Mengunci): Setidaknya ada satu sumber daya yang bersifat non-sharable (tidak dapat dibagi). Artinya, hanya satu proses yang dapat menggunakan sumber daya tersebut pada satu waktu.

2.Hold and Wait (Genggam dan Tunggu): Sebuah proses sedang memegang setidaknya satu sumber daya dan sedang menunggu untuk mendapatkan sumber daya tambahan yang saat ini sedang dipegang oleh proses lain.

3.No Preemption (Tidak Ada Preemption): Sumber daya tidak dapat diambil paksa dari proses yang memegangnya. Sumber daya hanya dapat dilepaskan secara sukarela oleh proses itu sendiri setelah tugasnya selesai.

4.Circular Wait (Menunggu Melingkar): Terdapat rantai proses (P1, P2, ..., Pn) di mana P1 menunggu sumber daya yang dipegang P2, P2 menunggu P3, dan seterusnya 
hingga Pn menunggu sumber daya yang dipegang kembali oleh P1.

2. Mengapa sinkronisasi diperlukan dalam sistem operasi?


Sinkronisasi proses mutlak diperlukan dalam sistem operasi, terutama pada sistem multiprogramming atau multithreading, karena alasan berikut:

Mencegah Race Condition: Ini adalah kondisi paling kritis. Race condition terjadi ketika beberapa proses mengakses dan memanipulasi data yang sama secara bersamaan. Tanpa sinkronisasi, hasil akhirnya bergantung pada urutan eksekusi yang tidak terprediksi, menyebabkan data menjadi korup atau tidak konsisten.

Menjaga Konsistensi Data: Sinkronisasi memastikan bahwa ketika satu proses sedang menulis data ke variabel bersama (shared variable), proses lain tidak boleh membaca atau menulis ke variabel yang sama sampai proses pertama selesai.

Mengatur Urutan Eksekusi: Dalam beberapa kasus, proses B mungkin membutuhkan hasil output dari proses A sebelum bisa berjalan. Sinkronisasi memastikan proses B "menunggu" hingga A selesai.

Analogi: Bayangkan dua orang mencoba menarik uang dari rekening bank yang sama pada detik yang persis sama di ATM berbeda. Tanpa sinkronisasi (penguncian database), saldo bisa menjadi negatif atau transaksi ganda bisa terjadi. 

3.Jelaskan perbedaan antara *semaphore* dan *monitor*.

| Fitur             | Semaphore                                                                 | Monitor                                                                                   |
|-------------------|---------------------------------------------------------------------------|-------------------------------------------------------------------------------------------|
| Definisi          | Variabel integer yang digunakan untuk memberi sinyal antar proses.        | Tipe data abstrak (ADT) atau modul tingkat tinggi yang mengenkapsulasi data dan prosedur. |
| Tingkat Abstraksi | Low-level: Lebih dekat ke mesin/bahasa assembly atau C.                   | High-level: Fitur bahasa pemrograman (seperti `synchronized` di Java).                    |
| Mekanisme         | Menggunakan operasi atomik `Wait()` (P) dan `Signal()` (V).               | Menggunakan prosedur di dalam monitor; mutual exclusion diatur otomatis oleh monitor.      |
| Fleksibilitas     | Sangat fleksibel tapi rawan error. Jika programmer lupa memanggil `Signal()`, deadlock mudah terjadi. | Lebih kaku tapi lebih aman dan mudah dikelola karena penanganan dilakukan oleh compiler/bahasa. |
| Kepemilikan       | Tidak ada konsep kepemilikan; proses manapun bisa melakukan signal.       | Hanya proses yang berada dalam monitor yang memiliki akses.                                |

---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini? di saat kode saya masukkan tersebut adaa erorr yang tidak dapat menjalankan di terminal  
- Bagaimana cara Anda mengatasinya?memperbaiki kode yang menjadi akar masalah tersebut dan memperbaiki kode tersebut meskipun saya mengerjakan agak kewalahan dengan kode tersebut


---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
