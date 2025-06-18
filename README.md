# Laporan Proyek Machine Learning - Radya Ardi Ninang Pudyastuti

## Project Overview

Minat baca masyarakat merupakan aspek penting dalam pembangunan sumber daya manusia, terutama dalam dunia pendidikan dan literasi. Di era _digital_ saat ini, akses terhadap bacaan semakin luas melalui berbagai platform daring yang menyediakan ribuan hingga jutaan judul buku. Namun, kelimpahan informasi ini justru menimbulkan tantangan baru, di mana pengguna sering kesulitan menemukan buku yang sesuai dengan preferensi atau kebutuhannya. Untuk mengatasi hal tersebut, sistem rekomendasi hadir sebagai solusi yang menyajikan pilihan bacaan secara personal, baik berdasarkan riwayat perilaku pengguna maupun karakteristik konten. Penerapannya yang telah terbukti efektif di industri hiburan seperti musik dan film, kini mulai diadopsi dalam ranah literasi digital untuk membantu pengguna menemukan buku secara efisien, relevan, dan sesuai minat.

Beberapa penelitian menunjukkan bahwa sistem rekomendasi berbasis Machine Learning mampu meningkatkan relevansi saran kepada pengguna. Misalnya, penelitian yang dilakukan oleh Rosidah dan Dellia (2024) mengembangkan sistem rekomendasi buku menggunakan Content-Based Filtering dengan TF-IDF dan _cosine similarity_, yang terbukti efektif dengan tingkat kelayakan sistem mencapai 91,4% [1]. Sementara itu, penelitian yang dilakukan oleh Guo (2024) menggabungkan Collaborative Filtering dengan CNN (model VGG16) untuk mengekstraksi fitur visual dari poster film, yang meningkatkan akurasi rekomendasi dari 70% menjadi 85% serta memperkaya keragaman dan kesesuaian saran dengan minat pengguna [2]. 

Dengan memanfaatkan metode Machine Learning, sistem rekomendasi mampu menganalisis data historis seperti rating pengguna dan informasi buku untuk menghasilkan rekomendasi yang bersifat personal. Dalam proyek ini, dibangun dua pendekatan utama: Collaborative Filtering yang dikombinasikan dengan algoritma Convolutional Neural Network (CNN) untuk menangkap pola perilaku pengguna serta fitur visual, dan Content-Based Filtering yang merekomendasikan buku berdasarkan kemiripan konten seperti judul dan penulis. Kedua pendekatan ini dibandingkan untuk mengevaluasi efektivitasnya dalam memberikan rekomendasi yang relevan dan sesuai dengan preferensi pengguna berdasarkan karakteristik data yang digunakan.


Referensi:
1. Rosidah, L., & Dellia, P. (2024). Library book recommendation system using content-based filtering. Iota: Journal of Informatics and Data Science, 4(1). https://doi.org/10.31763/iota.v4i1.693

2. Guo, R. (2024). Enhancing movie recommendation systems through CNN-based feature extraction and optimized collaborative filtering. Proceedings of the 2nd International Conference on Machine Learning and Automation. https://doi.org/10.54254/2755-2721/81/20241080

## Business Understanding
### Problem Statements

1. Bagaimana cara membangun sistem rekomendasi buku yang dapat memberikan saran bacaan secara personal kepada pengguna?
2. Bagaimana cara menerapkan metode Collaborative Filtering dan Content-Based Filtering dalam menghasilkan rekomendasi buku yang relevan?

### Goals
1. Mengembangkan sistem rekomendasi buku yang dapat menyajikan rekomendasi secara personal berdasarkan preferensi pengguna.
2. Menerapkan dua pendekatan sistem rekomendasi, yaitu Collaborative Filtering dengan CNN dan Content-Based Filtering berbasis kemiripan konten, untuk menguji efektivitasnya dalam menyajikan saran bacaan yang relevan.

### Solution Statements
1. Mengimplementasikan metode Content-Based Filtering dengan pendekatan TF-IDF dan cosine similarity, yang merekomendasikan buku berdasarkan kemiripan konten seperti judul dan penulis.
2. Membangun model Collaborative Filtering dengan menggunakan Convolutional Neural Network (CNN) untuk mempelajari pola interaksi antara pengguna dan buku berdasarkan data rating.
3. Menguji hasil rekomendasi dari kedua pendekatan untuk melihat efektivitasnya dalam memberikan saran bacaan yang relevan dan sesuai dengan preferensi pengguna, tanpa melakukan perbandingan performa secara langsung antar metode.

## Data Understanding
Dataset yang digunakan dalam penelitian ini adalah [Book-Recommendation Dataset](https://www.kaggle.com/datasets/arashnic/book-recommendation-dataset/data) dari _platform_ kaggle. Pada dataset ini terdapat 3 file data, dimana memuat data buku, rating, dan user. Namun, pada penelitian ini, hanya digunakan data buku dan rating saja. Data ini nantinya akan digunakan untuk membuat sistem rekomendasi menggunakan pendekatan _content-based filtering_ dan _collaborative filtering_. 

Adapun penjelasan masing-masing data adalah sebagai berikut:
#### Data Buku 
| Nama Kolom           | Deskripsi                                         |
| -------------------- | ------------------------------------------------- |
| ISBN                 | Kode unik buku                                    |
| Book-Title           | Judul buku                                        |
| Book-Author          | Nama penulis buku                                 |
| Year-Of-Publication  | Tahun publikasi                                   |
| Publisher            | Nama penerbit                                     |
| Image-URL-S          | URL gambar berukuran kecil (small)                |
| Image-URL-M          | URL gambar berukuran sedang (medium)              |
| Image-URL-L          | URL gambar berukuran besar (large)                |

- Pada data buku memiliki dimensi data 271360 baris dan 8 kolom
- Pada data buku terdapat missing value pada beberapa kolom, diantaranya Book-Author, Publisher, dan Image URL L

  ![image](https://github.com/user-attachments/assets/a1ed2787-bbb3-4678-8767-48a803e5532b)
- Pada data buku terdapat duplikasi data pada judul buku sebanyak 29225 baris.
- Agathe Christie merupakan penulis dengan karya buku terbanyak, yaitu sebanyak 632 buku

  ![image](https://github.com/user-attachments/assets/11808e78-f35b-404a-ab75-6bd73179dcbd)
- Harlequin merupakan publisher dengan karya buku terbanyak, yaitu sebanyak 7535 buku.

  ![image](https://github.com/user-attachments/assets/c812331b-717b-47f9-9542-cc69d21a55ca)

#### Data Rating
| Nama Kolom           | Deskripsi                                           |
| -------------------- | --------------------------------------------------- |
| User-ID              | ID unik user dalam sistem                           |
| ISBN                 | Kode unik buku                                      |
| Book-Rating          | Nilai yang diberikan pengguna terhadap buku (0-10)  |

- Pada data rating memiliki dimensi data 1149780 baris dan 3 kolom
- Pada data rating tidak memiliki missing value dan data yang duplikat
- Pada data rating, rating 0 memiliki jumlah buku paling banyak, yaitu 716109 karya

   ![image](https://github.com/user-attachments/assets/b31fd158-bbe3-485b-8d97-c077e96544cd)

- Pada data rating, user 11676 merupakan user yang paling sering memberikan rating.

  ![image](https://github.com/user-attachments/assets/f4d6183e-3e18-467d-95ff-951424e70d07)

- Pada data rating, buku dengan nomor ISBN 0971880107 merupakan buku yang paling sering diberikan rating.

  ![image](https://github.com/user-attachments/assets/bb53f135-f1c2-4185-b447-38feee24e2f7)

## Data Preparation
Pada tahap ini, dilakukan serangkaian proses untuk menyiapkan data sebelum masuk ke proses pelatihan model. Langkah-langkah yang dilakukan disusun secara sistematis untuk memastikan data bersih, konsisten, dan relevan. Berikut adalah tahapan data preparation yang dilakukan:

### Data buku
**1. Mengisi Missing Value.**
Pada kolom `Book-Author` dan `Publisher` diisi dengan nilai "unknown" agar tidak mengganggu proses pengolahan data berbasis teks. Sementara itu, kolom `Image-URL-L` dihapus karena tidak digunakan dalam proses modeling dan memiliki nilai kosong yang lebih dari satu.

**2. Menghapus Duplikasi.**
Data duplikat dihapus untuk memastikan bahwa tidak ada entri buku yang terduplikasi, sehingga sistem rekomendasi tidak memberikan saran yang redundan.

**3. Mengonversi Tipe Data Tahun.**
Kolom `Year-Of-Publication` diubah menjadi tipe numerik (int) untuk memastikan keseragaman format. Tahun-tahun yang tidak valid, seperti nilai `<1000 atau >2025`, juga disaring untuk menjaga keakuratan informasi terbit.

**4. Normalisasi Teks.**
Kolom `Book-Title`, `Book-Author`, dan `Publisher` dinormalisasi dengan mengubah semua huruf menjadi huruf kecil (_lowercase_) dan menghapus spasi di awal/akhir teks. Hal ini dilakukan agar pencocokan data teks lebih akurat dan konsisten.

**5. Menyaring Buku Populer.**
Buku-buku yang jarang dirating (kurang dari 50 rating) disaring dari dataset. Hanya buku dengan jumlah rating lebih dari 50 yang dipertahankan agar model lebih fokus pada item yang cukup dikenal pengguna dan memiliki data interaksi yang memadai. Duplikasi juga dihapus berdasarkan judul buku (Book-Title) untuk menjaga keunikan setiap entri.

**6. Menggabungkan Fitur Teks.**
Fitur `Book-Title`, `Book-Author`, dan `Publisher` digabungkan menjadi satu kolom baru bernama `combined_features`. Penggabungan ini bertujuan untuk membentuk representasi teks yang lebih kaya dalam proses content-based filtering, sehingga kemiripan antar buku dapat dihitung berdasarkan gabungan kontennya.

### Data Rating
**1. Menghapus Rating Nol.**
Data rating dengan nilai 0 dihapus karena dianggap tidak merepresentasikan penilaian pengguna secara eksplisit terhadap buku tersebut.

**2. Menyaring Buku Aktif.**
Data disaring agar hanya mencakup buku-buku yang dianggap aktif, yaitu buku yang memiliki jumlah rating di atas ambang batas tertentu. Ini dilakukan untuk mengurangi _sparsity_ dan meningkatkan kualitas hasil rekomendasi.

**3. Encoding Identitas User dan Buku.**
ID pengguna ( `User-ID`) dan ID buku (`ISBN`) diubah ke format numerik menggunakan LabelEncoder. Proses ini dilakukan karena algoritma pembelajaran mesin, khususnya model neural network, membutuhkan input dalam bentuk angka, bukan string atau format teks.

**4. Transformasi Kolom Baru.**
Hasil encoding disimpan ke dalam kolom baru `user` dan `book`. Kolom ini akan digunakan sebagai input utama untuk model collaborative filtering berbasis neural network.

**5. Menghitung Jumlah User dan Buku Unik.**
Jumlah total pengguna dan buku dihitung menggunakan `nunique()` untuk menentukan dimensi embedding pada tahap pembuatan model. Ini penting agar ukuran representasi vektor sesuai dengan jumlah entitas unik yang akan dipelajari.

**6. Mempersiapkan Data untuk Modeling**
Dataset akhir yang digunakan hanya terdiri dari tiga kolom utama: `user`, `book`, dan `Book-Rating`. Pemilihan ini bertujuan untuk menyederhanakan data agar dapat langsung digunakan dalam proses pelatihan model rekomendasi.

**7. Memisahkan Variabel dan Splitting Data**
Pada tahapan ini data dipisahkan menjadi: 
- Fitur (X): user, book
- Label (y): book-rating

Split Data Data dibagi menjadi data latih dan data uji dengan rasio 80:20 menggunakan train_test_split.


# Modelling
Untuk menyelesaikan permasalahan dalam menyajikan rekomendasi buku yang relevan kepada pengguna, proyek ini mengimplementasikan dua pendekatan sistem rekomendasi, yaitu Content-Based Filtering dan Collaborative Filtering berbasis CNN. Kedua pendekatan ini dirancang untuk menghasilkan rekomendasi personal berdasarkan preferensi pengguna, namun dengan cara yang berbeda.

## Content-Based Filtering
Pada pendekatan ini, sistem merekomendasikan buku berdasarkan kemiripan konten antar item. Fitur-fitur seperti judul, penulis, dan penerbit digabungkan ke dalam satu kolom `combined_features`, lalu diubah menjadi vektor numerik menggunakan TF-IDF Vectorization. Kemiripan antar buku dihitung menggunakan cosine similarity, yang menghasilkan skor kesamaan antara satu buku dengan buku lainnya.

Fungsi  `recommend_books()` dibangun untuk menerima input judul buku dan mengembalikan daftar top-5 buku yang paling mirip. Sebagai contoh, ketika pengguna memilih buku "American Gods", sistem berhasil merekomendasikan buku-buku karya Neil Gaiman lainnya seperti "Coraline" dan "Good Omens", yang menunjukkan bahwa pendekatan ini efektif dalam menangkap kesamaan gaya dan konten penulis.

![image](https://github.com/user-attachments/assets/b3600731-6ad2-4084-8252-083f661703f3)


## Collaborative Filtering dengan CNN
Pada pendekatan kedua, sistem menggunakan Collaborative Filtering berbasis Neural Network dengan arsitektur yang melibatkan embedding layer dan Convolutional Neural Network (CNN) sederhana untuk mempelajari interaksi antara pengguna dan buku. Data yang digunakan adalah pasangan `user`, `book`, dan `Book-Rating`, yang telah di-encode secara numerik. Model dilatih menggunakan data train-test split sebesar 80:20 dan dioptimasi dengan loss function Mean Squared Error (MSE).

Setelah model dilatih selama 5 epoch, sistem diuji dengan menghasilkan top-5 rekomendasi untuk pengguna tertentu (dalam pengujian ini menggunakan User-ID: 276747). Hasilnya menunjukkan buku-buku dengan genre dan penulis yang relevan, seperti karya oleh Douglas Adams dan beberapa buku Calvin & Hobbes oleh Bill Watterson, yang sesuai dengan preferensi pengguna.

![image](https://github.com/user-attachments/assets/1c67e6ed-5a2b-4930-904e-20a8c283b959)

## Top-N Recommendation
Kedua pendekatan berhasil menghasilkan top-N recommendation yang relevan. Pada content-based, rekomendasi diberikan berdasarkan input buku; sedangkan pada collaborative filtering, rekomendasi dihasilkan untuk user yang belum memberikan rating pada buku tertentu. Output masing-masing berupa daftar 5 buku teratas yang diprediksi paling relevan.

## Kelebihan dan Kekurangan Pendekatan Kedua Model
|  Pendekatan                     | 	Kelebihan	                                                             |  Kekurangan
|---------------------------------| -------------------------------------------------------------------------| -------------------------------------------------------------------------|
| Content-Based Filtering	        | Tidak bergantung pada data pengguna lain, cocok untuk user/item baru	   | Kurang bervariasi, hanya merekomendasikan buku yang mirip dari konten    |
| Collaborative Filtering (CNN)   |	Lebih fleksibel dan personal, dapat menangkap pola interaksi kompleks	   | Membutuhkan banyak data dan proses pelatihan model yang lebih berat      |


# Evaluasi
Evaluasi dilakukan untuk mengukur seberapa baik model dalam memprediksi rating pengguna terhadap buku. Pada proyek ini, pendekatan Collaborative Filtering berbasis CNN dievaluasi menggunakan metrik Root Mean Squared Error (RMSE) serta visualisasi training vs validation loss untuk menilai stabilitas proses pelatihan model.

### Metrik Evaluasi: RMSE
Root Mean Squared Error (RMSE) mengukur rata-rata kesalahan kuadrat antara nilai prediksi dan nilai aktual, dan sangat umum digunakan dalam sistem rekomendasi berbasis regresi (rating prediksi). Semakin kecil nilai RMSE, semakin akurat prediksi model terhadap preferensi pengguna. Berikut ini merupakan formula RMSE adalah:

![image](https://github.com/user-attachments/assets/e6f2fe8d-e025-404c-b144-47c1a0167989)

### Hasil Pengujian
Setelah pelatihan selama 5 epoch, model diuji pada data uji dan menghasilkan **nilai RMSE sebesar 1.6089.** Nilai ini menunjukkan bahwa rata-rata kesalahan prediksi rating pengguna terhadap buku masih tergolong kecil, menandakan bahwa **model cukup baik dalam mempelajari pola interaksi user-item**.

### Grafik Training vs Validation Loss
Grafik berikut menunjukkan tren penurunan loss pada data pelatihan dan validasi:

![image](https://github.com/user-attachments/assets/95ea79e5-a500-4c77-b76b-a67a948b591e)

Kedua kurva menurun dengan stabil, tanpa adanya perbedaan signifikan antara training loss dan validation loss. Hal ini menunjukkan bahwa model tidak mengalami overfitting, dan proses pembelajaran berlangsung efektif.

### Interpretasi
Hasil evaluasi menunjukkan bahwa model Collaborative Filtering dengan CNN dapat bekerja secara stabil dan cukup akurat. Nilai RMSE yang relatif rendah dan grafik loss yang konvergen membuktikan bahwa model mampu melakukan generalisasi yang baik terhadap data baru. Meskipun arsitektur model lebih kompleks dibanding content-based, pendekatan ini unggul dalam menangkap preferensi pengguna secara lebih dinamis dan personal.

# Kesimpulan
Berdasarkan hasil pengujian yang telah dilakukan, proyek ini berhasil membangun sistem rekomendasi buku menggunakan dua pendekatan utama, yaitu Content-Based Filtering dan Collaborative Filtering berbasis CNN. Content-Based Filtering mampu memberikan rekomendasi berdasarkan kemiripan konten seperti judul, penulis, dan penerbit, dan terbukti efektif dalam menyarankan buku-buku serupa dari penulis yang sama. Sementara itu, pendekatan Collaborative Filtering menggunakan neural network dengan arsitektur embedding dan CNN menunjukkan hasil yang cukup baik, dengan nilai RMSE sebesar 1.60 dan grafik loss yang stabil tanpa indikasi overfitting.

Kedua metode mampu menghasilkan top-N recommendation yang relevan dan personal. Content-based cocok digunakan untuk pengguna baru atau item baru, sedangkan collaborative filtering lebih kuat dalam menangkap pola interaksi kompleks antar pengguna. Hasil pengujian menunjukkan bahwa masing-masing pendekatan memiliki keunggulan tersendiri dan dapat saling melengkapi. Dengan demikian, sistem yang dibangun dapat digunakan sebagai dasar dalam pengembangan sistem rekomendasi literasi digital yang adaptif dan efisien.
