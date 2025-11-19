
# Laporan Praktikum Minggu 6
Topik: scheduling-rr-priorty

---

## Identitas
- **Nama**  : Akhmad Raffi Sarmadan
- **NIM**   : 250202974
- **Kelas** : 1IKRA

---

## Tujuan
1. Mahasiswa mampu menghitung waiting time dan turnaround time pada algoritma RR dan Priority.

2. Mahasiswa mampu menyusun tabel hasil perhitungan dengan benar dan sistematis.

3. Mahasiswa mampu membandingkan performa algoritma RR dan Priority.

---

## Dasar Teori
1. Penjadwalan CPU adalah proses pemilihan proses dari ready queue (antrian siap) untuk dieksekusi oleh CPU. Tujuannya adalah untuk memaksimalkan utilitas CPU dan meminimalkan waktu tunggu.

2. Round Robin (RR) adalah algoritma yang dirancang khusus untuk sistem time-sharing. RR bersifat preemptive, artinya ia tidak menunggu proses selesai. Setiap proses mendapat jatah waktu CPU yang disebut time quantum (q), biasanya antara 10-100 milidetik. Jika proses belum selesai dalam satu quantum, ia akan dihentikan sementara (preempted) dan dipindahkan ke akhir antrian 'ready' untuk menunggu giliran berikutnya. Ini memastikan semua proses mendapatkan respons dalam interval waktu yang terdefinisi.

3. Priority Scheduling adalah algoritma yang dirancang untuk mengalokasikan CPU ke proses dengan prioritas tertinggi. Prioritas dapat ditentukan secara internal (misalnya, batas memori, rasio I/O) atau eksternal (misalnya, kepentingan komersial, kebijakan). Algoritma ini bisa bersifat preemptive (proses baru berprioritas tinggi bisa langsung merebut CPU) atau non-preemptive (proses baru menunggu CPU dilepaskan). Kelemahan utamanya adalah potensi starvation, di mana proses berprioritas rendah mungkin tidak akan pernah dieksekusi..

---

## Langkah Praktikum

1. **Siapkan Data Proses**
   Gunakan contoh data berikut (boleh dimodifikasi sesuai kebutuhan):
   | Proses | Burst Time | Arrival Time | Priority |
   |:--:|:--:|:--:|:--:|
   | P1 | 5 | 0 | 2 |
   | P2 | 3 | 1 | 1 |
   | P3 | 8 | 2 | 4 |
   | P4 | 6 | 3 | 3 |

2. **Eksperimen 1 – Round Robin (RR)**
   - Gunakan *time quantum (q)* = 3.  
   - Hitung *waiting time* dan *turnaround time* untuk tiap proses.  
   - Simulasikan eksekusi menggunakan Gantt Chart (manual atau spreadsheet).  
     ```
     | P1 | P2 | P3 | P4 | P1 | P3 | ...
     0    3    6    9   12   15   18  ...
     ```
   - Catat sisa *burst time* tiap putaran.

3. **Eksperimen 2 – Priority Scheduling (Non-Preemptive)**
   - Urutkan proses berdasarkan nilai prioritas (angka kecil = prioritas tinggi).  
   - Lakukan perhitungan manual untuk:
     ```
     WT[i] = waktu mulai eksekusi - Arrival[i]
     TAT[i] = WT[i] + Burst[i]
     ```
   - Buat tabel perbandingan hasil RR dan Priority.

4. **Eksperimen 3 – Analisis Variasi Time Quantum (Opsional)**
   - Ubah *quantum* menjadi 2 dan 5.  
   - Amati perubahan nilai rata-rata *waiting time* dan *turnaround time*.  
   - Buat tabel perbandingan efek *quantum*.

5. **Eksperimen 4 – Dokumentasi**
   - Simpan semua hasil tabel dan screenshot ke:
     ```
     praktikum/week6-scheduling-rr-priority/screenshots/
     ```
   - Buat tabel perbandingan seperti berikut:

     | Algoritma | Avg Waiting Time | Avg Turnaround Time | Kelebihan | Kekurangan |
     |------------|------------------|----------------------|------------|-------------|
     | RR | ... | ... | Adil terhadap semua proses | Tidak efisien jika quantum tidak tepat |
     | Priority | ... | ... | Efisien untuk proses penting | Potensi *starvation* pada prioritas rendah |

6. **Commit & Push**
   ```bash
   git add .
   git commit -m "Minggu 6 - CPU Scheduling RR & Priority"
   git push origin main
   ```
---

## Kode / Perintah
Tuliskan potongan kode atau perintah utama:
```bash
Waiting Time (WT) = Turnaround Time - Burst Time
(Untuk RR, WT adalah Total Waktu Tunggu selama proses dieksekusi)
Turnaround Time (TAT) = Finish Time - Arrival Time
Average Waiting Time (AWT) = Total Waiting Time / Jumlah Proses
Average Turnaround Time (ATAT) = Total Turnaround Time / Jumlah Proses
```

---

## Hasil Eksekusi
![alt text](<screenshots/rr-priorty.png>)

**Eksperimen 1 – Round Robin (RR)**
 Hasil Perhitungan 
 | Proses | Burst Time | Arrival Time | Finish Time P1 | Finish Time P2 | Finish Time P3 | TAT (FT - AT) | WT (TAT - BT) |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| P1 | 5 | 0 | 3 (sisa 2) | 14 (selesai) | - | 14 - 0 = 14 | 14 - 5 = 9 |
| P2 | 3 | 1 | 6 (selesai) | - | - | 6 - 1 = 5 | 5 - 3 = 2 |
| P3 | 8 | 2 | 9 (sisa 5) | 17 (sisa 2) | 22 (selesai ) | 22 - 2 = 20 | 20 - 8 = 12 |
| P4 | 6 | 3 | 12 (sisa 3) | 20 (selesai ) | - | 20 - 3 = 17 | 17 - 6 = 11 |

Simulasi eksekusi menggunakan Gantt Chart

```
   | P1 | P2 | P3 | P4 | P1 | P3 | P4 | P3 |
   0    3    6    9   12   14   17   20   22
```

**Eksperimen 2 – Priority Scheduling (Non-Preemptive)**
Hasil Perhitungan

| Proses | Arrival Time | Burst Time | Priority | Start | Finish Time (Start - BT) | WT (Start - AT) | TAT (WT + BT)
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| P1 | 0 | 5 | 2 | 0 | 0 + 5 = 5 | 0 - 0 = 0 | 0 + 5 = 5 |
| P2 | 1 | 3 | 1 | 5 | 5 + 3 = 8 | 5 - 1 = 4 | 4 + 3 = 7 |
| P4 | 3 | 6 | 3 | 8 | 8 + 6 = 14 | 8 - 3 = 5 | 5 + 6 = 11 |
| P3 | 2 | 8 | 4 | 14 | 14 + 8 = 22 | 14 - 2 = 12 | 12 + 8 = 20 |

Simulasi eksekusi menggunakan Gantt Chart

```
   | P1 | P2 | P3 | P4 |
   0    5    8    14   22
```

**Eksperimen 3 – Variasi Time Quantum**
![alt text](<screenshots/variasi time quantum.png>)

Time Quantum = 2

Hasil Perhitungan

| Proses | Burst Time | Arrival Time | Finish Time P1 | Finish Time P2 | Finish Time P3 | Finish Time P4 |TAT (FT - AT) | WT (TAT - BT) |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| P1 | 5 | 0 | 2 (sisa 3) | 10 (sisa 1) | 16 (selesai) | - | 16 - 0 = 16 | 16 - 5 = 11 |
| P2 | 3 | 1 | 4 (sisa 1) | 11 (selesai) | - | - | 11 - 1 = 10 | 10 - 3 = 7 |
| P3 | 8 | 2 | 6 (sisa 6) | 13 (sisa 4) | 18 (sisa 2) | 22 (selesai) | 22 - 2 = 20 | 20 - 8 = 12 |
| P4 | 6 | 3 | 8 (sisa 4) | 15 (sisa2) | 20 (selesai) | - | 20 - 3 = 17 | 17 - 6 = 11 |

Simulasi eksekusi menggunakan Gantt Chart

```
   | P1 | P2 | P3 | P4 | P1 | P2 | P3 | P4 | P1 | P3 | P4 | P3 |
   0    2    4    6    8   10   11   13   15   16   18    20   22
```

- Time Quantum = 5

Hasil Perhitungan

| Proses | Burst Time | Arrival Time | Finish Time P1 | Finish Time P2 |TAT (FT - AT) | WT (TAT - BT) |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | 
| P1 | 5 | 0 | 5 (selesai) | - | 5 - 0 = 5 | 5 - 5 = 0 |
| P2 | 3 | 1 | 8 (selesai) | - | 8 - 1 = 7 | 7 - 3 = 4 |
| P3 | 8 | 2 | 13 (sisa 3) | 21 (selesai) | 21 - 2 = 19 | 19 - 8 = 11 |
| P4 | 6 | 3 | 18 (sisa 1) | 22 (selesai) | 22 - 3 = 19 | 19 - 6 = 13 |

Simulasi eksekusi menggunakan Gantt Chart

```
   | P1 | P2 | P3 | P4 | P3 | P4 |
   0    5    8   13   18   21   22   
```

- Tabel Perbandingan Efek Quantum

| Time Quantum | Rata-rata Waiting Time (WT) | Rata-rata Turnaround Time (TAT) | Efek |
| :--- | :--- | :--- | :--- |
|Quantum Kecil (q = 2) | Lebih besar (10,25) | Lebih besar (15,75) | Proses sering berganti sehingga sistem lebih responsif, tetapi waktu tunggu (WT) dan turnaround time (TAT) menjadi lebih besar akibat banyaknya context switch. |
|Quantum Besar (q = 5) | Lebih kecil (7,00) | Lebih kecil (12,50) | Proses berganti lebih jarang sehingga efisiensi meningkat dan WT serta TAT lebih kecil, namun sistem menjadi kurang responsif seperti FCFS. |

---

**Eksperimen 4 – Perbandingan Round Robin (RR) dan Priority Scheduling**

   | Algoritma | Avg Waiting Time | Avg Turnaround Time | Kelebihan | Kekurangan |
   |------------|------------------|----------------------|------------|-------------|
   | RR | 8,5 | 14 | Adil terhadap semua proses | Tidak efisien jika quantum tidak tepat |
   | Priority | 5,25 | 10,75 | Efisien untuk proses penting | Potensi *starvation* pada prioritas rendah |
   
---

## Analisis
- Pada percobaan Round Robin, setiap proses mendapat giliran secara bergantian sehingga sistem lebih adil, tetapi waktu tunggu dan turnaround-nya lebih besar karena sering terjadi pergantian konteks.

- Sementara pada Priority Scheduling, proses dengan prioritas tertinggi dieksekusi lebih dulu sehingga waktu tunggu dan turnaround rata-ratanya lebih kecil. Namun, proses berprioritas rendah bisa menunggu lama jika banyak proses prioritas tinggi, yang dapat menyebabkan starvation.

- Ketika time quantum kecil (q = 2), sistem menjadi lebih responsif, tetapi terlalu sering melakukan context switch sehingga efisiensinya menurun. Sebaliknya, jika time quantum besar (q = 5), efisiensi meningkat dan waktu rata-rata menurun, tetapi responsivitas terhadap proses baru menjadi lebih lambat
---

## Kesimpulan
1. Algoritma Priority Scheduling menawarkan throughput dan efisiensi rata-rata (AWT 5.25) yang superior dibandingkan Round Robin, namun keunggulannya diimbangi oleh risiko starvation yang signifikan terhadap proses berprioritas rendah.

2. Algoritma Round Robin menjamin keadilan (fairness) dan responsivitas yang lebih baik, memastikan setiap proses mendapatkan alokasi CPU tanpa penundaan indefinit, meskipun dengan mengorbankan efisiensi rata-rata. 

3. Kinerja algoritma Round Robin sangat bergantung pada pemilihan time quantum. Nilai quantum yang tidak tepat—baik terlampau kecil (q=2) maupun terlampau besar (q=5)—akan menurunkan performa sistem, baik melalui peningkatan overhead komputasi ataupun hilangnya jaminan responsivitas.

---

## Quiz
1. Apa perbedaan utama antara Round Robin dan Priority Scheduling ?

Jawaban:

Round Robin adalah algoritma preemptive yang mengambil keputusan berdasarkan kuantum waktu (time quantum), ia fokus pada keadilan dan pembagian waktu yang merata. Priority Scheduling mengambil keputusan berdasarkan nilai prioritas proses, ia fokus pada penyelesaian tugas-tugas yang dianggap lebih penting terlebih dahulu, dan bisa bersifat preemptive maupun non-preemptive.

2. Apa pengaruh besar/kecilnya time quantum terhadap performa sistem (pada RR) ?

Jawaban:

Ukuran kuantum waktu sangat krusial. Jika time quantum terlalu besar, performa RR akan mendekati FCFS (First Come First Served), karena setiap proses kemungkinan besar akan selesai sebelum kuantumnya habis. Jika time quantum terlalu kecil, overhead akibat context switching (proses menyimpan status dan memuat status proses baru) akan menjadi sangat tinggi, sehingga CPU lebih banyak menghabiskan waktu untuk berganti proses daripada untuk bekerja (eksekusi), yang menurunkan efisiensi sistem secara drastis.

3. Mengapa algoritma Priority dapat menyebabkan starvation ?

Jawaban:

- Starvation dapat terjadi jika sistem terus-menerus menerima aliran proses-proses baru dengan prioritas tinggi. Akibatnya, proses-proses yang sudah lama menunggu di antrian tetapi memiliki prioritas rendah mungkin tidak akan pernah mendapat giliran untuk dieksekusi oleh CPU, karena mereka selalu kalah oleh proses-proses baru yang lebih penting.
---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?  
- Bagaimana cara Anda mengatasinya?  

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
