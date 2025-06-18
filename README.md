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

  ![image](https://github.com/user-attachments/assets/9b1d216b-ae0f-40ac-bf15-c3a4fb52cce0)

- Pada data buku terdapat duplikasi data pada judul buku sebanyak 29225 baris.
- Agathe Christie merupakan penulis dengan karya buku terbanyak, yaitu sebanyak 632 buku

  ![image](https://github.com/user-attachments/assets/c2b6d7a1-9a43-4664-982d-6734ac41b2a7)

- Harlequin merupakan publisher dengan karya buku terbanyak, yaitu sebanyak 7535 buku.

  ![image](https://github.com/user-attachments/assets/e1404e74-e93c-40ba-8b57-b27e2f3d4b49)

#### Data Rating
| Nama Kolom           | Deskripsi                                           |
| -------------------- | --------------------------------------------------- |
| User-ID              | ID unik user dalam sistem                           |
| ISBN                 | Kode unik buku                                      |
| Book-Rating          | Nilai yang diberikan pengguna terhadap buku (0-10)  |

- Pada data rating memiliki dimensi data 1149780 baris dan 3 kolom
- Pada data rating tidak memiliki missing value dan data yang duplikat
- Pada data rating, rating 0 memiliki jumlah buku paling banyak, yaitu 716109 karya

  ![image](https://github.com/user-attachments/assets/2a0764d9-a5fa-487a-a357-6eb7699914b0)

- Pada data rating, user 11676 merupakan user yang paling sering memberikan rating.

  ![image](https://github.com/user-attachments/assets/dc68a9f8-a792-4536-af41-7103f47313b8)

- Pada data rating, buku dengan nomor ISBN 0971880107 merupakan buku yang paling sering diberikan rating.

  ![image](https://github.com/user-attachments/assets/4c8ed359-f689-464a-af88-79db10b443b6)

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

**6. Mempersiapkan Data untuk Modeling.**
Dataset akhir yang digunakan hanya terdiri dari tiga kolom utama: `user`, `book`, dan `Book-Rating`. Pemilihan ini bertujuan untuk menyederhanakan data agar dapat langsung digunakan dalam proses pelatihan model rekomendasi.

**7. Memisahkan Variabel dan Splitting Data.**
Pada tahapan ini data dipisahkan menjadi: 
- Fitur (X): user, book
- Label (y): book-rating

Split Data Data dibagi menjadi data latih dan data uji dengan rasio 80:20 menggunakan `train_test_split`.

# Modelling
Untuk menyelesaikan permasalahan dalam menyajikan rekomendasi buku yang relevan kepada pengguna, proyek ini mengimplementasikan dua pendekatan sistem rekomendasi, yaitu Content-Based Filtering dan Collaborative Filtering berbasis CNN. Kedua pendekatan ini dirancang untuk menghasilkan rekomendasi personal berdasarkan preferensi pengguna, namun dengan cara yang berbeda.

## Content-Based Filtering
Pada pendekatan ini, sistem merekomendasikan buku berdasarkan kemiripan konten antar item. Fitur-fitur seperti judul, penulis, dan penerbit digabungkan ke dalam satu kolom `combined_features`, lalu diubah menjadi representasi vektor menggunakan `TF-IDF Vectorization`. Selanjutnya, cosine similarity digunakan untuk mengukur tingkat kemiripan antar buku.

Fungsi `recommend_books_content_based()` digunakan untuk menerima input judul buku dan menghasilkan daftar top-5 buku dengan kemiripan tertinggi. Evaluasi dilakukan menggunakan metrik Precision@5 yang membandingkan ISBN dari buku yang direkomendasikan dengan buku yang disukai pengguna (berdasarkan rating ≥ 7). Hasil evaluasi menunjukkan nilai Precision@5 sebesar **0.0093**, yang mengindikasikan bahwa meskipun sistem dapat mengenali kemiripan konten, tingkat relevansi rekomendasi terhadap preferensi pengguna masih rendah dibandingkan pendekatan Collaborative Filtering.

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
Evaluasi dilakukan untuk mengukur seberapa baik model dalam memberikan rekomendasi yang relevan terhadap preferensi pengguna. Pada proyek ini, digunakan dua pendekatan, yaitu Content-Based Filtering dan Collaborative Filtering berbasis CNN. Evaluasi mencakup metrik Root Mean Squared Error (RMSE) untuk prediksi rating, serta Precision@5 untuk mengukur relevansi rekomendasi buku.

### 1. Content-Based Filtering
Pada pendekatan ini, sistem merekomendasikan buku berdasarkan kemiripan konten seperti judul, penulis, dan penerbit, menggunakan TF-IDF dan cosine similarity. Evaluasi dilakukan menggunakan metrik Precision@5. berikut ini adalah Rumus dari precision@k:

![image](https://github.com/user-attachments/assets/339a3a53-333f-4458-bd12-ed28b6f91864)

keterangan:
- K = jumlah item yang direkomendasikan 
- Rekomendasi yang relevan = item dalam daftar rekomendasi yang benar-benar disukai oleh pengguna

#### Hasil pengujian
Model menghasilkan nilai Precision@5 sebesar 0.0093, yang menunjukkan bahwa hanya sedikit dari rekomendasi yang sesuai dengan preferensi pengguna (berdasarkan rating ≥ 7). Nilai ini tergolong rendah, mengindikasikan bahwa meskipun sistem mampu mengenali kemiripan konten, namun belum mampu secara akurat menangkap relevansi terhadap selera pengguna.

### 2. Collaborative Filtering
Pendekatan ini menggunakan arsitektur CNN untuk mempelajari pola interaksi antara pengguna dan item (buku), dengan target memprediksi nilai rating. Evaluasi dilakukan menggunakan metrik RMSE.

##### Metrik Evaluasi: RMSE
Root Mean Squared Error (RMSE) mengukur rata-rata kesalahan kuadrat antara nilai prediksi dan aktual. Semakin kecil RMSE, semakin akurat model. Berikut ini formula RMSE:

![image](https://github.com/user-attachments/assets/32565a8a-ab51-4f7e-b84c-f6575cc76780)

##### Hasil Pengujian:
Setelah pelatihan selama 5 epoch, model diuji pada data uji dan menghasilkan RMSE sebesar 1.6089, menandakan bahwa model cukup baik dalam memprediksi rating pengguna terhadap buku.

##### Grafik Training vs Validation Loss:
![image](https://github.com/user-attachments/assets/26f0d159-4925-41b1-a192-a6b7eced2b46)

Berdasarkan grafik di atas, kedua kurva menunjukkan penurunan yang stabil tanpa gap signifikan, menandakan proses pelatihan berlangsung efektif dan model tidak mengalami overfitting.

# Kesimpulan
Berdasarkan penelitian yang telah dilakukan, sistem rekomendasi dibangun menggunakan dua pendekatan, yaitu Content-Based Filtering dan Collaborative Filtering. Pada pendekatan Content-Based, rekomendasi diberikan berdasarkan kemiripan judul buku menggunakan metode TF-IDF dan cosine similarity. Meskipun berhasil menghasilkan rekomendasi buku yang mirip secara konten, evaluasi menggunakan metrik Precision@5 menunjukkan nilai yang cukup rendah, yaitu sebesar 0.0093. Hal ini menandakan bahwa rekomendasi yang dihasilkan belum sepenuhnya relevan dengan preferensi pengguna.

Sebaliknya, pada pendekatan Collaborative Filtering, sistem mempelajari pola interaksi antara pengguna dan buku melalui model embedding dan jaringan neural sederhana. Evaluasi model dilakukan menggunakan metrik RMSE, dan diperoleh nilai sebesar 1.6089. Nilai ini menunjukkan bahwa model cukup baik dalam memprediksi rating pengguna terhadap buku yang belum mereka baca. Dengan demikian, dapat disimpulkan bahwa pendekatan Collaborative Filtering memberikan performa yang lebih baik dibandingkan dengan Content-Based Filtering dalam konteks dataset dan eksperimen yang dilakukan.
