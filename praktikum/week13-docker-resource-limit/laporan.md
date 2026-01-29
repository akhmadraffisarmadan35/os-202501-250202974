
# Laporan Praktikum Minggu [X]
Topik: [Tuliskan judul topik, misalnya "Arsitektur Sistem Operasi dan Kernel"]

---

## Identitas
- **Nama**  : Akhmad Raffi Sarmadan
- **NIM**   : 250202974
- **Kelas** : 1IKRA

---

## Tujuan
1. Menulis Dockerfile sederhana untuk sebuah aplikasi/skrip.
2. Membangun image dan menjalankan container.
3. Mengamati dan menjelaskan perbedaan eksekusi container dengan dan tanpa limit resource.
4. Menjalankan container dengan pembatasan **CPU** dan **memori**.



---

## Dasar Teori
1. Containerization memungkinkan aplikasi berjalan dalam lingkungan terisolasi dengan berbagi kernel sistem operasi host, sehingga lebih ringan dan efisien dibandingkan mesin virtual.

2. Control Groups (cgroups), docker menggunakan mekanisme cgroups pada Linux untuk membatasi penggunaan resource seperti CPU dan memori pada container.

3. Resource Limiting, pembatasan CPU dan memori mencegah container menggunakan resource secara berlebihan, serta dapat menghentikan container secara otomatis ketika batas memori terlampaui (OOM Kill).

---

## Langkah Praktikum
1. **Persiapan Lingkungan**

   - Pastikan Docker terpasang dan berjalan.
   - Verifikasi:
     ```bash
     docker version
     docker ps
     ```

2. **Membuat Aplikasi/Skrip Uji**

   Buat program sederhana di folder `code/` (bahasa bebas) yang:
   - Melakukan komputasi berulang (untuk mengamati limit CPU), dan/atau
   - Mengalokasikan memori bertahap (untuk mengamati limit memori).

3. **Membuat Dockerfile**

   - Tulis `Dockerfile` untuk menjalankan program uji.
   - Build image:
     ```bash
     docker build -t week13-resource-limit .
     ```

4. **Menjalankan Container Tanpa Limit**

   - Jalankan container normal:
     ```bash
     docker run --rm week13-resource-limit
     ```
   - Catat output/hasil pengamatan.

5. **Menjalankan Container Dengan Limit Resource**

   Jalankan container dengan batasan resource (contoh):
   ```bash
   docker run --rm --cpus="0.5" --memory="256m" week13-resource-limit
   ```
   Catat perubahan perilaku program (mis. lebih lambat, error saat memori tidak cukup, dll.).

6. **Monitoring Sederhana**

   - Jalankan container (tanpa `--rm` jika perlu) dan amati penggunaan resource:
     ```bash
     docker stats
     ```
   - Ambil screenshot output eksekusi dan/atau `docker stats`.

7. **Commit & Push**

   ```bash
   git add .
   git commit -m "Minggu 13 - Docker Resource Limit"
   git push origin main
   ```

---

## Kode / Perintah

app.py
```
import time

data = []

print("Program mulai...")

try:
    while True:
        data.append("X" * 10_000_000)  # ±10MB
        print(f"Memori terpakai kira-kira: {len(data)*10} MB")
        time.sleep(1)
except MemoryError:
    print("Memory limit tercapai!")
```
dockerfile
```
FROM python:3.10-slim

WORKDIR /app

COPY app.py .

CMD ["python", "app.py"]
```
membuat dockerfile build 
```
docker build -t week13-resource-limit .
```
menjalankan container tanpa limir
``` 
docker run --rm week13-resource-limit .
```
menjalankan container dengan limit
```
docker run --rm --cpus="0.5" --memory="256m" week13-resource-limit
```

---

## Hasil Eksekusi
build container
![hasil](<screenshots/build container.png>)

container limit
![hasil](<screenshots/container limit.png>)

container tanpa limit
![hasil](<screenshots/container tanpa limit.png>)

monitoring sederhana
![hasil](<screenshots/monitoring sederhana.png>)

---

## Analisis
Pada praktikum ini dilakukan pengujian pembatasan resource container Docker dengan menjalankan program Python yang mengalokasikan memori secara berulang. Saat container dijalankan tanpa batasan resource, penggunaan memori meningkat hingga sekitar 2,3 GB dan program tetap berjalan, menunjukkan bahwa container dapat menggunakan resource host secara bebas.

Sebaliknya, ketika container dijalankan dengan batasan memori 256 MB dan CPU 0,5 core, program berhenti lebih cepat akibat keterbatasan resource. Monitoring menggunakan docker stats memperlihatkan perbedaan yang jelas pada penggunaan CPU dan memori antara container dengan dan tanpa limit. Hal ini membuktikan bahwa Docker mampu melakukan isolasi dan pembatasan resource secara efektif.

---

## Kesimpulan

1. Docker mampu mengisolasi dan mengelola penggunaan resource aplikasi di dalam container secara efektif.

2. Tanpa batasan resource, container dapat menggunakan memori besar dan berpotensi memengaruhi sistem host.

3. Pemberian batasan CPU dan memori pada container membuat aplikasi berjalan lebih terkontrol dan stabil.

---

## Quiz
1. Mengapa container perlu dibatasi CPU dan memori?

    **Jawaban:**
  Pembatasan CPU dan memori diperlukan agar satu container tidak menghabiskan seluruh resource sistem, sehingga stabilitas dan kinerja aplikasi lain tetap terjaga.
3. Apa perbedaan VM dan container dalam konteks isolasi resource?

    **Jawaban:**
  VM mengisolasi resource dengan sistem operasi terpisah di atas hypervisor, sedangkan container berbagi kernel host dan membatasi resource menggunakan mekanisme sistem operasi, sehingga container lebih ringan dibandingkan VM.
5. Apa dampak limit memori terhadap aplikasi yang boros memori?

   **Jawaban:**  Aplikasi yang boros memori akan dihentikan secara otomatis ketika melebihi batas memori yang ditentukan (OOM Kill), sehingga aplikasi dapat berhenti tiba-tiba.


---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?  
- Bagaimana cara Anda mengatasinya?  

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
