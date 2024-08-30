# 1. **Business Problem Understanding**

### **1.1 Context:**

Layanan keuangan perbankan yang digunakan masyarakat semakin beragam. Salah satu layanan yang dikenal masyarakat adalah deposito berjangka. Mekanisme deposito berjangka adalah nasabah menitipkan sejumlah uang di bank atau lembaga keuangan, dan uang tersebut baru dapat ditarik setelah jangka waktu tertentu. Sebagai kompensasinya, nasabah akan diberikan bunga tetap sesuai dengan nominal uang yang disetorkan. Sedangkan untuk bank, deposito tersebut digunakan sebagai biaya operasional dan juga sumber dana untuk melakukan layanan-layanan lainnya seperti peminjaman dana dan lain sebaginya.

Namun demikian, sebagai badan usaha yang memiliki produk keuangan dan nasabah masing-masing, bank tetap harus bersaing agar tidak kehilangan nasabah. Salah satu cara untuk mendapatkan nasabah baru adalah dengan melakukan kampanye pemasaran. Kampanye pemasaran ini dilakukan dengan cara telemarketing, yaitu melakukan panggilan telepon kebada nasabah bank dalam jumlah banyak untuk menarik nasabah melakukan layanan deposito.


### **1.2 Business Statement:**


`Cost per acquisition (CPA)`

Definisi: CPA = Total biaya kampanye / Jumlah nasabah yang melakukan deposit

Baseline CPA (berdasarkan data):
CPA = €702.326 / 3730 = €188.19 per nasabah yang melakukan deposit

- menurut https://www.worldwidecallcenters.com/call-center-pricing/, call center cost di western europe adalah sebesar  $35 - $45 per jam atau sebesar €31.3 - €40.2 atau rata-rata sekitar €35.7
- Berdasarkan dataset, total panggilan yang dilakukan selama campaign adalah 19673 kali panggilan.
Dengan biaya €35.7 per panggilan, untuk total 19673 panggilan, bank telah mengeluarkan biaya sebesar €702.326 per campaign.

Bank telah melakukan kampanye pemasaran untuk produk deposito berjangka, menghasilkan 3732 nasabah yang melakukan deposit dari total 7813 nasabah yang dihubungi. Kampanye ini memerlukan total 19673 panggilan dengan biaya €35.7 per panggilan, menghasilkan total biaya €702,326.10. Cost per Acquisition (CPA) saat ini adalah €188.19. Meskipun tingkat konversi cukup baik (47.77%), biaya per akuisisi masih tinggi. Bank bertujuan untuk menurunkan CPA untuk kampanye-kampanye kedepannya.


### **1.3 Problem Statement:**

Dengan CPA saat ini sebesar €188.19, pendekatan bank dalam menargetkan nasabah terbukti tidak efisien. Sekitar 52.23% dari upaya pemasaran (11704 dari 19673 panggilan) digunakan untuk nasabah yang tidak melakukan deposit, mengakibatkan pemborosan sumber daya sebesar €417,832.80. Bank memerlukan pendekatan yang lebih terarah untuk mengidentifikasi calon nasabah yang lebih mungkin melakukan deposit. Tantangannya adalah bagaimana menurunkan CPA secara signifikan, misalnya di bawah €150, sambil mempertahankan atau meningkatkan jumlah total nasabah yang melakukan deposit.

### **1.4 Goals:**

Menurunkan campaign cost dengan menerapkan model machine learning.


### **1.5 Stakeholder**:
`Divisi Marketing pada Bank`

Dari seluruh divisi pada bank, divisi yang paling sesuai dengan machine learning ini adalah divisi marketing. Hal ini karena tujuan inti dari model machine learning ini adalah untuk memprediksi nasabah yang melakukan deposito, yang sejalan dengan tujuan divisi marketing yaitu untuk memperoleh nasabah yang melakukan deposito.

Divisi marketing kemudian dapat segera menerapkan hasil model machine learning ini ke kampanye mereka. Mereka dapat menggunakan prediksi untuk menyempurnakan strategi penargetan, menyesuaikan pesan, dan mengalokasikan sumber daya secara lebih efektif. Selain itu  divisi marketing juga dapat dengan mudah mengukur dampak model machine learning dengan membandingkan kinerja kampanye sebelum dan sesudah penerapan. Lalu saat  divisi marketing menggunakan model dan memberikan feedback, model machine learning dapat disempurnakan, dengan harapan model tersebut digunakan oleh  divisi marketing untuk membuat keputusan yang lebih terarah dan didasari oleh data tentang nasabah mana yang akan ditargetkan.


### **1.6 Target:**

`0`: Nasabah **tidak melakukan** penyetoran deposito<br>
`1`: Nasabah **melakukan** penyetoran deposito


### **1.7 Analytical Approach:**

- Melakukan analisis data untuk memahami karakteristik nasabah yang melakukan deposit dan yang tidak.

- Membangun model klasifikasi menggunakan teknik machine learning untuk memprediksi kemungkinan nasabah melakukan penyetoran deposito.

- Memberikan rekomendasi untuk strategi pemasaran yang lebih efektif berdasarkan wawasan dari model dan analisis data.

### **1.8 Metric Evaluation:**

#### **1.8.1 Precision**

Precision adalah sebuah metrik evaluasi dalam machine learning yang mengukur seberapa akurat model kita dalam memprediksi kelas positif. Dengan kata lain, precision menjawab pertanyaan: "Dari semua prediksi positif yang diberikan model, berapa banyak yang benar-benar positif?"

Dalam konteks memprediksi nasabah yang akan melakukan deposito, precision membantu kita menjawab pertanyaan: "Dari semua nasabah yang kita prediksi akan melakukan deposito, seberapa benar prediksi kita?"

#### **1.8.2 Error Types and Consequences:**

**Type 1 error `(False Positive)`**: Model memprediksi nasabah akan melakukan penyetoran deposito, tetapi nasabah tidak melakukan penyetoran depostio.

**Konsekuensi**: 
- Peningkatan CPA karena biaya kampanye dikeluarkan untuk nasabah yang tidak menghasilkan deposit.
- Pemborosan sumber daya pemasaran dan pengeluaran kampanye yang tidak efisien.


**Type 2 error `(False Negative)`**: Model memprediksi nasabah tidak akan melakukan penyetoran deposito, tetapi nasabah melakukan penyetoran deposito.

**Konsekuensi**: 
- Potensi penurunan jumlah nasabah yang melakukan deposit, yang dapat meningkatkan CPA jika total biaya kampanye tidak berkurang secara proporsional.
- Hilangnya peluang untuk mendapatkan nasabah yang berharga dan potensi kerugian pendapatan.

## Attribute Information

### Customer Profile
| Kolom | Tipe Data | Deskripsi |
| --- | --- | --- |
| age | Integer | Usia Nasabah |
| job | Categorical |  Pekerjaan Nasabah. ("admin." "unknown", "unemployed", "management", "housemaid", "entrepreneur", "student",  "blue-collar", "self-employed", "retired", "technician", "services") |
| balance | Integer | Rata-rata saldo tahunan|
| housing | Binary | Apakah nasabah memiliki pinjaman untuk pembelian rumah? ("yes", "no") |
| loan | Binary | Apakah nasabah memiliki pinjaman pribadi? ("yes", "no") |

### Marketing Data
| Kolom | Tipe Data | Deskripsi |
| --- | --- | --- |
| contact | Categorical | Jenis kontak komunikasi ("unknown", "telephone", "cellular") |
| month | String | Bulan terakhir bank melakukan kontak dengan nasabah dalam setahun |
| campaign | Integer | Jumlah kontak yang dilakukan selama kampanye ini dan untuk nasabah ini |
| pdays | Integer | Jumlah hari yang berlalu setelah nasabah terakhir dihubungi dari kampanye sebelumnya (-1 berarti klien tidak dihubungi sebelumnya) |
| poutcome | Categorical | Hasil dari kampanye sebelumnya ("unknown", "other", "failure", "success") |
| deposit | Binary | Apakah nasabah telah melakukan penyetoran deposito atau belum? ("yes", "no") |

## Conclusion
Bredasarkan hasil classification report dari model Gradient Boosting Classificaton kita, kita dapat menyimpulkan/mengambil konklusi bahwa bila seandainya nanti kita menggunakan model kita untuk menyaring list nasabah yang akan dilakukan kampanye, maka model kita dapat mengurangi 56% nasabah yang tidak ingin melakukan term deposit atau tidak tertarik untuk kita approach, dan model kita dapat memprediksi ketepatan sebesar 87% total nasabah yang akan melakukan term deposit. (Semua ini berdasarkan dari precision karena kita menitik beratkan model pada ketepatan prediksi true positive untuk nasabah yang melakukan term deposit).

1.  Performa Model: <br>
 Model Gradient Boosting yang telah di-tune menunjukkan akurasi 59% dan F1-score rata-rata 0.50. Nilai precision untuk kelas 1 (nasabah yang melakukan deposit) cukup tinggi (0.87), namun recall-nya rendah (0.17). Dapat dilihat bahwa model sangat baik dalam memprediksi nasabah yang tidak akan melakukan deposit (recall 0.98 untuk kelas 0). dapat disimpulkan bahwa model ini memiliki kemampuan yang cukup baik dalam mengidentifikasi nasabah yang benar-benar akan melakukan term deposit. Dengan nilai precision sebesar 87% untuk kelas 1 (nasabah yang melakukan term deposit).


2. Efektivitas Kampanye:<br>
Meskipun model kurang efektif dalam mengidentifikasi semua nasabah yang akan melakukan deposit, ia sangat efektif dalam mengidentifikasi nasabah yang tidak akan melakukan deposit. Hal ini dapat dimanfaatkan untuk mengurangi biaya kampanye dengan menghindari nasabah yang kemungkinan besar tidak akan melakukan deposit.


3. Goals:
Pengurangan biaya kampanye dapat diukur dengan membandingkan biaya sebelum dan sesudah implementasi model. Efisiensi dapat dihitung dari rasio nasabah yang dihubungi vs yang melakukan deposit.


## Recomemendation

1. Penggunaan Model:
Model ini baik digunakan untuk menyaring nasabah yang sangat kecil kemungkinannya melakukan deposit, namun kurang dapat dipercaya untuk mengidentifikasi semua nasabah potensial yang akan melakukan deposit.


2. Implementasi dalam Proses Bisnis:
Gunakan model untuk mengeliminasi nasabah dengan probabilitas deposit rendah dari daftar kontak. Fokuskan upaya pemasaran pada nasabah yang tidak diidentifikasi sebagai "tidak akan deposit" oleh model.


3. Dampak yang Terukur:
   - Penurunan biaya kampanye dapat diukur dengan: (Biaya Kampanye Sebelumnya - Biaya Kampanye Setelah Implementasi Model) / Biaya Kampanye Sebelumnya * 100%.
   - Peningkatan efisiensi: (Jumlah Nasabah yang Melakukan Deposit / Jumlah Nasabah yang Dihubungi) sebelum vs setelah implementasi model.


4. Batasan Project dan Rekomendasi Perbaikan:
   - Data: Mungkin ada ketidakseimbangan kelas yang signifikan. Rekomendasi: Gunakan teknik oversampling atau undersampling.
   - Model: Recall rendah untuk kelas positif. Rekomendasi: Eksperimen dengan model lain atau ensemble methods.


5. Kumpulkan lebih banyak data, terutama untuk kasus positif (nasabah yang melakukan deposit).
6. Lakukan feature engineering lebih mendalam untuk meningkatkan prediktabilitas model.
7. Pertimbangkan penggunaan model yang lebih kompleks atau ensemble methods.
8. Kombinasikan hasil model dengan pengetahuan domain expert untuk pengambilan keputusan final.

Dengan memanfaatkan kekuatan model dalam mengidentifikasi nasabah yang tidak akan melakukan deposit, bank dapat secara signifikan mengurangi biaya kampanye dan meningkatkan efisiensi operasional, meskipun model mungkin melewatkan beberapa nasabah potensial. Pendekatan ini harus diimplementasikan dengan hati-hati dan terus dievaluasi untuk memastikan keseimbangan antara pengurangan biaya dan potensi pendapatan.
