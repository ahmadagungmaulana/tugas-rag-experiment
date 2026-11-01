# RAG Parameter Exploration

## Informasi Eksperimen

**Nama PDF:**
Makalah_CISC_vs_RISC.pdf

**Jumlah halaman PDF:**
2 Halaman

**Isi / topik PDF secara singkat:**
Analisis perbandingan antara arsitektur mikroprosesor CISC (seperti x86 Intel/AMD) dan RISC (seperti ARM) berdasarkan kompleksitas instruksi, cara akses memori, penggunaan daya, dan kecocokannya untuk PC vs perangkat portabel (smartphone).

---

# Pertanyaan Pengujian

## Pertanyaan 1
Apa perbedaan utama antara arsitektur CISC dan RISC dalam hal akses operasi memori?

## Pertanyaan 2
Mengapa arsitektur RISC (ARM) lebih dominan digunakan pada perangkat portabel seperti smartphone dibandingkan CISC (x86)?

---

# Baseline Configuration

Konfigurasi awal sebelum eksperimen dimulai:

```text
Temperature: 0.2
TOP_K: 4
Chunk Size: 100
Chunk Overlap: 20
Embedding Model: BAAI/bge-small-en-v1.5
LLM Model: openai/gpt-oss-120b
```

---

# Experiment 1 - Temperature

## Temperature = 0.0

### Actual Output
**Question 1:**
Perbedaan utama yang dijelaskan dalam dokumen adalah bahwa arsitektur CISC (x86 Intel) mengizinkan instruksi aritmatika/logika (ALU) untuk mengakses memori (RAM) secara langsung, sehingga mengurangi ketergantungan pada register internal CPU, meskipun dapat menimbulkan bottleneck pada bus alamat dan data【Source: Makalah_CISC_vs_RISC.pdf | Page: 1】.

Dokumen tidak memuat informasi tentang cara arsitektur RISC menangani akses memori, sehingga perbandingan lengkap tidak dapat diberikan.

**Question 2:**
Arsitektur RISC (ARM) lebih dominan pada perangkat portabel karena :
Sirkuit yang lebih sederhana – Unit kendali pada RISC menggunakan struktur instruksi yang seragam, sehingga logikanya jauh lebih ringan dibandingkan CISC.
Konsumsi daya yang sangat rendah – Penyederhanaan ini menghasilkan efisiensi daya dan termal yang tinggi, sangat penting untuk perangkat yang bergantung pada baterai.
Dirancang untuk menghemat baterai dan mengeksekusi perintah cepat, sehingga cocok untuk smartphone dan perangkat elektronik kecil.

### Observation
Jawaban AI sangat kaku dan konsisten mengikuti teks di dokumen secara pas. Kalimatnya berbentuk *bullet points* tapi tanpa tanda baca peluru yang rapi, terkesan lugas apa adanya.

---

## Temperature = 0.2

### Actual Output
**Question 1:**
Perbedaan utama yang dijelaskan dalam dokumen adalah bahwa pada arsitektur CISC (x86 Intel) instruksi aritmatika/logika (ALU) dapat mengakses memori (RAM) secara langsung, sehingga mengurangi ketergantungan pada register internal CPU namun dapat menimbulkan bottleneck pada bus alamat dan data (Von Neumann Bottleneck) [Makalah_CISC_vs_RISC.pdf, hal 1].

Dokumen tidak memuat informasi tentang cara arsitektur RISC mengakses memori, sehingga perbandingan lengkap tidak dapat diberikan.

**Question 2:**
Arsitektur RISC (ARM) lebih cocok untuk perangkat portabel karena :

- Unit kendali yang sederhana – Instruksi yang seragam membuat rangkaian kontrol lebih ringan, sehingga konsumsi daya sangat rendah dan panas yang dihasilkan minimal【Makalah_CISC_vs_RISC.pdf | Page: 2】.

- Fokus pada efisiensi baterai – RISC dirancang untuk menghemat daya baterai sekaligus mengeksekusi perintah dengan cepat, sehingga ideal untuk smartphone dan perangkat elektronik kecil【Makalah_CISC_vs_RISC.pdf | Page: 2】.

Sebaliknya, arsitektur CISC (x86) dioptimalkan untuk beban kerja berat dan performa tinggi pada sistem yang selalu terhubung listrik (PC, server), sehingga kurang efisien untuk penggunaan baterai terbatas.

### Observation
Jawaban masih sangat terstruktur tapi mulai ada sedikit perbaikan *formatting* (pakai strip/bullet). Fakta intinya tetap sama dengan temp 0.0.

---

## Temperature = 0.8

### Actual Output
**Question 1:**
Perbedaan utama yang dicatat dalam dokumen adalah bahwa pada arsitektur CISC (misalnya x86 Intel) instruksi aritmetika/logika (ALU) dapat mengakses memori (RAM) secara langsung, sehingga ketergantungan pada register internal berkurang, namun hal ini dapat menimbulkan bottleneck pada bus alamat‑data (Von Neumann Bottleneck)【Source: Makalah_CISC_vs_RISC.pdf | Page: 1】.

Dokumen tidak memuat penjelasan mengenai cara arsitektur RISC mengakses memori, sehingga perbandingan lengkap tidak dapat diberikan dari sumber yang tersedia.

**Question 2:**
RISC‑based ARM dipilih untuk perangkat portabel karena unit kendalinya jauh lebih sederhana (instruksi seragam) sehingga rangkaian logiknya lebih ringan. Penyederhanaan ini memberikan konsumsi daya yang sangat efisien dan efisiensi termal yang tinggi, yang penting untuk menghemat baterai pada smartphone serta memungkinkan perangkat kecil tetap tetap dingin. Oleh karena itu ARM “dikhususkan untuk menghemat daya baterai dan menjalankan perintah secara cepat”, sementara x86 (CISC) lebih cocok untuk beban kerja berat pada sistem dengan listrik konstan.

### Observation
Gaya bahasa AI berubah cukup sentara. Teks tidak lagi kaku dalam bentuk poin-poin, melainkan dirangkai menjadi satu paragraf yang naratif, panjang, dan luwes seperti cerita. 

---

## Kesimpulan Experiment Temperature

**Apa perubahan yang paling terlihat?**
Yang paling berubah adalah gaya bahasa (*wording*) dan cara penyampaiannya. Di angka 0.0 jawabannya kaku dan *to the point*. Makin tinggi angkanya ke 0.8, kata-katanya jadi lebih bervariasi (kreatif) dan luwes. Tapi hebatnya, fakta dari dokumennya tidak berubah/ngarang, tetap akurat.

**Menurut kalian nilai mana yang paling cocok untuk aplikasi RAG ini?**
Menurut saya nilai `0.2` paling cocok.

**Kenapa?**
Karena di `0.2` bahasanya cukup enak dibaca, rapi pakai *bullet points*, tapi tidak terlalu kaku seperti `0.0` dan tidak terlalu bertele-tele / digabung jadi satu paragraf panjang seperti di `0.8`. 

---

# Experiment 2 - TOP_K

## TOP_K = 1

### Actual Output
**Question 1:**
Perbedaan utama yang dijelaskan dalam dokumen adalah bahwa pada arsitektur CISC (misalnya x86 Intel) instruksi aritmatika/logika (ALU) dapat mengakses memori (RAM) secara langsung, sehingga tidak terlalu bergantung pada jumlah register internal CPU. Akses langsung ini dapat menimbulkan kendala throughput karena keterbatasan bus alamat dan data (Von Neumann Bottleneck)【Makalah_CISC_vs_RISC.pdf | Page 1】.  
Informasi mengenai cara arsitektur RISC menangani akses memori tidak terdapat dalam dokumen yang diberikan, sehingga perbandingan lengkap tidak dapat disajikan.

**Question 2:**
Arsitektur RISC (ARM) lebih cocok untuk perangkat portabel karena unit kendali yang jauh lebih sederhana—disebabkan oleh struktur instruksi yang seragam. Penyederhanaan sirkuit ini menghasilkan konsumsi daya yang sangat efisien dan efisiensi termal yang tinggi, sehingga cocok untuk smartphone yang bergantung pada baterai. Sebaliknya, arsitektur CISC (x86) lebih dominan pada sistem berdaya tinggi dengan pasokan listrik konstan (PC, server).  
*Source: Makalah_CISC_vs_RISC.pdf, halaman 2*

### Sources / Similarity Score
* **Q1:** Makalah_CISC_vs_RISC.pdf | Page: 1 | Score: 0.7688 | content-length: 687
* **Q2:** Makalah_CISC_vs_RISC.pdf | Page: 2 | Score: 0.7375 | content-length: 613

### Observation
Karena TOP_K sangat kecil, AI hanya mengambil satu sumber halaman saja. Makanya di Pertanyaan 1, AI tidak bisa menjawab tentang RISC karena info itu ada di Halaman 2, tapi AI cuma dikasih bacaan Halaman 1.

---

## TOP_K = 4

### Actual Output
**Question 1:**
Perbedaan utama terletak pada cara instruksi ALU mengakses memori:
- CISC (misalnya x86 Intel)** – instruksi aritmatika/logika dapat **mengakses memori (RAM) secara langsung**, sehingga tidak terlalu bergantung pada banyak register internal CPU. Namun, akses langsung ini dapat menimbulkan bottleneck pada bus alamat dan data (Von Neumann Bottleneck)【Makalah_CISC_vs_RISC.pdf | Page: 1】.
- RISC – dokumen yang diberikan tidak menjelaskan secara spesifik bagaimana RISC menangani akses memori, sehingga perbedaan detailnya tidak dapat ditemukan dalam sumber yang di‑upload.

**Question 2:**
Arsitektur RISC (ARM) lebih dominan pada perangkat portabel karena :
* Sirkuit kontrol yang sederhana – Instruksi yang seragam membuat unit kendali pada RISC jauh lebih sederhana, sehingga konsumsi daya menjadi sangat rendah dan efisiensi termal tinggi【Makalah_CISC_vs_RISC.pdf | Page: 2】.  
* Fokus pada penghematan baterai – RISC dirancang khusus untuk menghemat daya baterai dan mengeksekusi perintah dengan cepat, sehingga cocok untuk smartphone dan perangkat elektronik kecil【Makalah_CISC_vs_RISC.pdf | Page: 2】.  
Sebaliknya, arsitektur CISC (x86) ditujukan untuk beban kerja berat dan performa tinggi pada sistem yang selalu terhubung ke listrik (PC, server). Karena kebutuhan daya dan termal yang ketat pada perangkat portabel, ARM/RISC menjadi pilihan yang lebih efisien.

### Sources / Similarity Score
* **Q1:** 
  - Makalah_CISC_vs_RISC.pdf | Page: 1 | Score: 0.7688
  - Makalah_CISC_vs_RISC.pdf | Page: 2 | Score: 0.7335 | content-length: 769
* **Q2:** 
  - Makalah_CISC_vs_RISC.pdf | Page: 2 | Score: 0.7322 | content-length: 907

### Observation
Meski konteks (content-length) yang diberikan sudah mulai nambah besar, di Pertanyaan 1 rupanya AI masih belum menangkap bagian penjelasan RISC dengan sempurna, mungkin karena bagian itu tertumpuk.

---

## TOP_K = 8

### Actual Output
**Question 1:**
Perbedaan utama terletak pada cara kedua arsitektur memperlakukan memori pada operasi ALU:
* CISC (x86 Intel) – instruksi aritmatika/logika dapat **mengakses memori secara langsung** tanpa harus memuat data ke register terlebih dahulu. Hal ini mengurangi ketergantungan pada register, tetapi dapat menimbulkan bottleneck pada bus memori (Von Neumann Bottleneck) [Source: Makalah_CISC_vs_RISC.pdf | Page 1].
* RISC (ARM) – Menganut arsitektur Load/Store; operasi aritmatika pada ALU hanya dapat dilakukan pada data yang sudah berada di register. Akses ke memori utama terjadi hanya melalui instruksi khusus LOAD dan STORE, sehingga prosesor dilengkapi dengan banyak register internal [Source: Makalah_CISC_vs_RISC.pdf | Page 2].
Jadi, CISC mengizinkan akses memori langsung dalam instruksi ALU, sementara RISC membatasi akses memori hanya pada instruksi load/store terpisah.

**Question 2:**
Arsitektur RISC (ARM) lebih dominan pada perangkat portabel karena :
* Unit kendali yang jauh lebih sederhana berkat struktur instruksi yang seragam, sehingga sirkuit menjadi lebih ringan dan **konsumsi daya sangat efisien serta termal tinggi (Makalah_CISC_vs_RISC.pdf, hal 2).  
* Desainnya mengutamakan penghematan baterai dan eksekusi perintah cepat, menjadikannya cocok untuk smartphone, tablet, dan perangkat IoT (hal 2).  
* Karakteristik ini menjadikan ARM standar de‑facto untuk perangkat yang mengandalkan daya baterai (hal 2).
Dengan demikian, efisiensi energi dan termal ARM membuatnya lebih sesuai untuk perangkat portabel dibandingkan CISC (x86) yang lebih ditujukan untuk sistem berdaya tinggi dengan listrik konstan.

### Sources / Similarity Score
* **Q1:** 
  - Makalah_CISC_vs_RISC.pdf | Page: 1 | Score: 0.7688
  - Makalah_CISC_vs_RISC.pdf | Page: 2 | Score: 0.7335 | content-length: 1097
* **Q2:** 
  - Makalah_CISC_vs_RISC.pdf | Page: 2 | Score: 0.7322 | content-length: 863

### Observation
AI akhirnya bisa menjawab Pertanyaan 1 dengan sangat lengkap karena context yang dibawa LLM sangat banyak (content-length tembus 1097), sehingga semua materi dari Halaman 1 dan Halaman 2.

---

## Kesimpulan Experiment TOP_K

**Apakah TOP_K yang lebih besar selalu menghasilkan jawaban yang lebih baik?**
Tidak selalu/tidak pasti karena di eksperimen saya ini TOP_K besar 8 hasilnya lebih bagus, tapi kalau terlalu besar AI malah bisa buta gara-gara banyak informasi sampah/enggak relevan yang masuk dan yang membuat token jadi boros.

**Menurut kalian TOP_K mana yang paling cocok untuk PDF yang digunakan?**
Untuk dokumen makalah saya ini, nilai `8` adalah yang paling cocok.

**Kenapa?**
Karena informasi tentang materi CISC ada di halaman 1, dan RISC ada di halaman 2. ketika TOP_K kecil, AI hanya baca separuh aja jadinya jawabannya buntung. Dengan TOP_K 8, AI mengambil banyak potongan jadi konteks jawabannya utuh.

---

# Experiment 3 - Chunk Size

(Menggunakan `CHUNK_OVERLAP = 20`)

## Chunk Size = 50

### Chunks Stored : 15

### Actual Output
**Q1:**
Perbedaan utama terletak pada cara instruksi mengakses memori:
- **CISC**: Instruksi aritmatika/logika (ALU) dapat mengakses memori (RAM) secara langsung. [Makalah_CISC_vs_RISC.pdf, hal 1]  
- **RISC**: Semua transaksi ke memori utama hanya dilakukan melalui instruksi khusus **LOAD** dan **STORE**; operasi ALU bekerja hanya pada register. [Makalah_CISC_vs_RISC.pdf, hal 2]

**Q2:**
Arsitektur RISC (ARM) lebih banyak dipakai pada perangkat portabel karena desainnya yang **sederhana dan hemat daya**.  Pada RISC unit kendali jauh lebih sederhana berkat struktur instruksi yang seragam, sehingga sirkuitnya mengonsumsi daya yang sangat rendah dan menghasilkan efisiensi termal tinggi — faktor‑faktor yang sangat penting untuk smartphone yang mengandalkan baterai (Makalah CISC_vs_RISC.pdf, hal 2).  Karena keunggulan ini, ARM telah **mendominasi perangkat mobile dan embedded systems** (hal 1).

### Sources / Similarity Score
* **Q1:** Page 1 (Score: 0.7479), Page 2 (Score: 0.7396) | content-length: 562
* **Q2:** Page 1 (Score: 0.7986), Page 2 (Score: 0.6993) | content-length: 700

### Observation
Karena ukurannya 50, potongan kalimatnya sedikit. Jawaban yang keluar jadi agak pendek/dangkal karena AI cuma dapat sepotong-sepotong info, meski intinya tetap benar.

---

## Chunk Size = 100

### Chunks Stored = 15

### Actual Output
**Q1:**
Perbedaan utama terletak pada cara kedua arsitektur mengakses memori:
- CISC (x86 Intel) – Instruksi aritmatika/logika pada ALU dapat mengakses memori (RAM) secara langsung tanpa harus memindahkan data ke register terlebih dahulu【Makalah_CISC_vs_RISC.pdf | Page: 1】.  
- RISC (ARM) – Menggunakan model Load/Store: operasi aritmatika hanya dapat dilakukan pada data yang sudah berada di dalam register; semua transaksi ke memori utama dilakukan melalui instruksi khusus LOAD dan STORE【Makalah_CISC_vs_RISC.pdf | Page: 2】. 

**Q2:**
Arsitektur RISC (ARM) lebih dominan pada perangkat portabel karena :
* Kontrol yang sederhana dan instruksi seragam – unit kendali pada ARM jauh lebih sederhana, sehingga sirkuitnya lebih kecil dan mengonsumsi daya yang sangat rendah serta menghasilkan panas minimal.
* Desain Load/Store dengan banyak register – operasi aritmatika hanya pada register internal, sementara akses memori dilakukan lewat instruksi LOAD/STORE khusus. Ini mempercepat eksekusi dan mengurangi konsumsi energi.
* Fokus pada penghematan baterai – ARM dirancang khusus untuk menghemat daya baterai dan menjalankan perintah secara cepat, sehingga menjadi standar de‑facto pada smartphone, tablet, dan perangkat IoT.
Sebaliknya, arsitektur CISC (x86) lebih cocok untuk beban kerja berat pada sistem dengan sumber listrik tetap...

### Sources / Similarity Score
* **Q1:** Page 1 (Score: 0.7688), Page 2 (Score: 0.7335) | content-length: 737
* **Q2:** Page 2 (Score: 0.7322) | content-length: 1179

### Observation
Jawaban AI lebih komprehensif, alasannya jadi lebih dijabarkan karena AI menerima potongan teks (*chunk*) yang lebih panjang dan utuh.

---

## Chunk Size = 120

### Chunks Stored = 15

### Actual Output
**Q1:**
Perbedaan utama terletak pada cara instruksi mengakses memori:
- CISC (x86 Intel) – Instruksi aritmatika/logika (ALU) dapat mengakses memori (RAM) secara langsung tanpa harus memuat data ke register terlebih dahulu.
- RISC (ARM) – Menggunakan model Load/Store: operasi aritmatika hanya dapat dilakukan pada data yang sudah berada di register internal, sedangkan akses ke memori utama hanya melalui instruksi khusus LOAD dan STORE.

**Q2:**
Arsitektur RISC (ARM) lebih dominan pada perangkat portabel karena :
* Unit kendali yang sederhana – Instruksi yang seragam membuat rangkaian kontrol jauh lebih simpel, sehingga konsumsi daya sangat rendah dan termal efisien.
* Desain Load/Store – Semua operasi aritmatika dilakukan pada register internal, sementara akses memori hanya lewat instruksi LOAD/STORE, sehingga eksekusi cepat dengan sedikit energi.
* Banyak register – Memungkinkan lebih banyak data disimpan di dalam CPU tanpa harus mengakses RAM yang lebih mahal secara energi.
Karena smartphone mengandalkan baterai, efisiensi daya dan panas menjadi prioritas utama...

### Sources / Similarity Score
* **Q1:** Page 1 (Score: 0.7688), Page 2 (Score: 0.7326) | content-length: 737
* **Q2:** Page 2 (Score: 0.7948), Page 1 (Score: 0.6553) | content-length: 1104

### Observation
Hasilnya mirip dengan ukuran 100, tapi dengan size 120 AI memasukkan lebih banyak detail pelengkap seperti "akses RAM yang lebih mahal secara energi".

---

## Kesimpulan Experiment Chunk Size

**Apa hubungan Chunk Size dengan jumlah chunk yang tersimpan?**
Makin kecil angka Chunk Size, maka jumlah potongan yang masuk ke database jadi makin banyak. seperti contoh memotong roti tipis-tipis yang akan menjadi banyak tapi porsinya sedikit.

**Apakah chunk yang lebih kecil selalu menghasilkan retrieval yang lebih baik?**
kalau Chunk yang terlalu kecil membuat maknanya sering putus, AI jadi cuma nerima kalimat sepotong-sepotong sehingga jawabannya kurang dalam.

**Menurut kalian Chunk Size mana yang paling cocok?**
Menurut saya 100 adalah yang paling pas.

**Kenapa?**
Ukurannya cukup panjang supaya konteks satu ide/paragraf tidak terpotong-potong, tapi juga tidak terlalu kebesaran yang berisiko bikin pencarian melenceng atau buang-buang token yang membuat mudah untuk menghapal.

---

# Experiment 4 - Chunk Overlap

(Menggunakan CHUNK_SIZE = 100)

## Chunk Overlap = 0

### Chunks Stored = 15

### Actual Output
**Q1:**
Perbedaan utama yang dijelaskan dalam dokumen adalah bahwa arsitektur RISC (misalnya ARM) menerapkan model Load/Store, di mana semua operasi aritmetika hanya dapat dilakukan pada data yang sudah berada di dalam register CPU, dan akses ke memori utama (RAM hanya terjadi melalui instruksi khusus LOAD dan STORE). [Makalah_CISC_vs_RISC.pdf, hal 2]
Dokumen tidak memuat penjelasan tentang cara arsitektur CISC mengakses memori, sehingga perbandingan lengkap tidak dapat diberikan. 

**Q2:**
RISC (ARM) dipilih untuk perangkat portabel karena arsitekturnya memiliki unit kendali yang jauh lebih sederhana berkat struktur instruksi yang seragam. Penyederhanaan sirkuit ini menghasilkan konsumsi daya yang sangat efisien dan efisiensi termal yang tinggi, sehingga cocok untuk perangkat yang mengandalkan baterai. Karena itu ARM “dikhususkan untuk menghemat daya baterai dan menjalankan perintah secara cepat,” sehingga menjadi pilihan utama pada smartphone dan perangkat elektronik kecil.

### Sources / Similarity Score
* **Q1:** Page 2 (Score: 0.7325) | content-length: 635
* **Q2:** Page 2 (Score: 0.7322) | content-length: 645

### Observation
Karena overlapnya 0, ada kalimat yang terpotong total pas di perbatasan chunk. Ini bikin AI sama sekali gagal nyari info soal CISC di Pertanyaan 1 (hanya dapat info RISC saja). 

---

## Chunk Overlap = 20

### Chunks Stored = 15

### Actual Output
**Q1:**
Perbedaan utama terletak pada cara instruksi mengakses memori:
- CISC (misalnya x86) memperbolehkan instruksi aritmatika/logika langsung mengakses memori (RAM) tanpa harus memindahkan data ke register terlebih dahulu【Source: Makalah_CISC_vs_RISC.pdf | Page: 1】.  
- RISC (misalnya ARM) menggunakan arsitektur load/store: hanya instruksi LOAD dan STORE yang dapat berinteraksi dengan memori, sedangkan semua operasi ALU harus dilakukan pada data yang sudah berada di dalam register【Source: Makalah_CISC_vs_RISC.pdf | Page: 2】.

**Q2:** (Jawaban normal, format rapi membandingkan ARM hemat baterai dan CISC PC beban berat).

### Sources / Similarity Score
* **Q1:** Page 1 (Score: 0.7688), Page 2 (Score: 0.7335) | content-length: 728
* **Q2:** Page 2 (Score: 0.7322) | content-length: 1108

### Observation
Dengan overlap 20, kalimat yang tadinya putus nyambung lagi. AI kembali bisa merangkai jawaban Q1 soal CISC dan RISC secara berbarengan.

---

## Chunk Overlap = 40

### Chunks Stored = 15

### Actual Output
**Q1:** Jawaban stabil dan komprehensif membandingkan CISC dan RISC.
**Q2:** Jawaban stabil, menyebutkan keunggulan baterai dan termal ARM.

### Sources / Similarity Score
* **Q1:** Page 1 (Score: 0.7688), Page 2 (Score: 0.7335) | content-length: 865
* **Q2:** Page 2 (Score: 0.7322) | content-length: 1061

### Observation
Hasilnya sebelas-dua belas dengan Overlap 20. Tidak ada perbaikan drastis, tapi ukuran konteksnya makin tebal di 865.

---

## Kesimpulan Experiment Chunk Overlap

**Apa pengaruh Chunk Overlap yang kalian lihat?**
Fungsinya seperti "perekat" kalimat. Kalau overlap-nya 0, kalimat sering kali putus di tengah jalan sehingga makna atau info pentingnya hilang, bikin AI bingung. Pas overlap ditambah, potongan di akhir chunk sebelumnya diulang sedikit di chunk yang baru, jadinya konteks kalimatnya terselamatkan.

**Apakah overlap yang lebih besar selalu menghasilkan jawaban yang lebih baik?**
tidak karena 20 saja udah putus apa lagi kalau di perbesar.

**Menurut kalian nilai mana yang paling cocok?**
Nilai 20. Cukup untuk mengamankan teks biar gak putus dan cukup efisien juga.

---

# Final Configuration

Setelah seluruh eksperimen, pilih konfigurasi yang menurut kalian menghasilkan hasil terbaik untuk PDF yang digunakan.

```text
Temperature: 0.2
TOP_K: 8
Chunk Size: 100
Chunk Overlap: 20
```

---

# Final Questions

### 1. Parameter mana yang paling terasa memengaruhi hasil aplikasi kalian?
TOP_K adalah parameter yang paling pengaruhnya dan Chunk Overlap juga karena kalau diset ke 0, ada info yang hilang terpotong.

### 2. Apakah Temperature memengaruhi Retrieval atau Generation? Jelaskan.
Temperature memengaruhi proses Generation bukan proses mencari. Buktinya, fakta yang diambil akan tetep konsisten terus. Yang berubah cuma cara ngomongnya aja di 0.0 bahasanya kayak robot/kaku, sedangkan di 0.8 bahasanya jadi panjang dan mengalir kayak orang lagi cerita.

### 3. Apakah TOP_K yang lebih besar selalu menghasilkan jawaban yang lebih baik?
Tidak selalu karena TOP_K yang besar akan coco dengan file yang kecil 1-5 halaman sedang kan jika banyak halaman dokumen yang banyak maka akan membuat sussah untuk mencarinya dan membuat boros token.

### 4. Apa yang terjadi ketika Chunk Size dibuat lebih kecil?
Potongan dokumennya jadi lebih pendek-pendek. karena AI merangkai apa yang dia baca.

### 5. Setelah melakukan eksperimen, apa fungsi Chunk Overlap menurut pemahaman kalian?
Menurut saya Chunk Overlap itu seperti lem perekat antar potongan. Kalau gak ada overlap batas potongannya kasar dan kalimat sering kepotong mendadak. Dengan overlap, beberapa kata di akhir digabung lagi di awal teks selanjutnya, jadi makna kalimatnya tetap nyambung pas diambil AI.

### 6. Kenapa perubahan Chunk Size dan Chunk Overlap membutuhkan ingestion ulang?
Karena proses potong-memotong PDF dilakukan paling awal, sebelum datanya dilempar dan disimpan di database vektor. Jadi kalau kita mau ganti ukuran potongannya, ya kita harus bongkar ulang hapus database lamanya, lalu potong-potong ulang PDF-nya dari awal pakai ukuran yang baru.

### 7. Kenapa perubahan Temperature tidak membutuhkan ingestion ulang?
Karena sumber bacaan di dalam database-nya tidak ada yang diubah, kita gak perlu repot-repot masukin PDF-nya lagi dari awal.

### 8. Menurut kalian, apakah ada satu konfigurasi RAG yang akan selalu paling bagus untuk semua jenis dokumen?
tidak ada karena Settingan paling bagus itu sangat bergantung sama jenis/banyak dokumennya. Kalau PDF-nya seperti makalah pendek, settingan TOP_K=8 dan Chunk Size=100 menurut saya sudah paling pas.

---

# Personal Reflection

### Bagian eksperimen mana yang hasilnya paling berbeda dari dugaan kalian?
ternyata ketika Chunk Overlap atau Chunk Size di naikan jawaban nya tetap sama tidak memiliki perbedaan yang.

### Parameter mana yang awalnya kalian anggap tidak terlalu penting tetapi ternyata berpengaruh?
Chunk Overlap karena ketika nilainya semaikn kecil maka akan membuat kalimat penting menghilanng

### Setelah mengerjakan tugas ini, bagaimana kalian menjelaskan hubungan antara Retrieval dan Generation pada RAG?
contoh seperti ngerjain ujian sekolah. Retrieval adalah proses nyari halaman buku di perpustakaan yang isinya sesuai sama pertanyaan. Sedangkan Generation itu kemampuan kita nulis ulang isi dari halaman buku tadi pakai kalimat sendiri di lembar jawaban.

### Jika aplikasi ini dikembangkan lebih lanjut, parameter atau bagian apa lagi yang ingin kalian coba?
ingin mencoba mengubah LLM Model-nya. Ingin tahu apakah kalau pakai model LLM yang lebih pintar, dia bakal langsung paham jawabannya walau TOP_K atau ukuran Chunk-nya kecil.

---

# AI Usage

### AI tools yang digunakan
Gemini AI.

### AI digunakan untuk membantu bagian apa?
Membantu menjelaskan fungsi teknis parameter (seperti fungsi overlap & temperature) pakai bahasa sehari-hari biar gampang dicerna, mencarikan referensi topik makalah yang cocok untuk dites, serta membantu ngerapihin *formatting* dan tata letak tulisan jawaban di file README ini biar enak dilihat. 

### Bagian eksperimen mana yang kalian lakukan dan evaluasi sendiri?
Saya mandiri mencari PDF yang dipakai, nge-clone dan ngerunning server RAG lokalnya, bongkar-pasang `config.py` dan `llm.py`, ngerestart database berulang kali, ngopi-paste output aplikasi mentah-mentah ke catatan, dan membuktikan sendiri jika overlap-nya 0 itu kalimatnya bakal putus.
