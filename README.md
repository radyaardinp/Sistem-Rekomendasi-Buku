# Laporan Proyek Machine Learning - Radya Ardi Ninang Pudyastuti

## Project Overview

Minat baca masyarakat merupakan aspek penting dalam pembangunan sumber daya manusia, terutama dalam dunia pendidikan dan literasi. Di era digital saat ini, akses terhadap bacaan semakin luas melalui berbagai platform daring yang menyediakan ribuan hingga jutaan judul buku. Namun, kelimpahan informasi ini justru menimbulkan tantangan baru, di mana pengguna sering kesulitan menemukan buku yang sesuai dengan preferensi atau kebutuhannya. Untuk mengatasi hal tersebut, sistem rekomendasi hadir sebagai solusi yang menyajikan pilihan bacaan secara personal, baik berdasarkan riwayat perilaku pengguna maupun karakteristik konten. Penerapannya yang telah terbukti efektif di industri hiburan seperti musik dan film, kini mulai diadopsi dalam ranah literasi digital untuk membantu pengguna menemukan buku secara efisien, relevan, dan sesuai minat.

Beberapa penelitian menunjukkan bahwa sistem rekomendasi berbasis machine learning mampu meningkatkan relevansi saran kepada pengguna. Misalnya, penelitian yang dilakukan oleh Rosidah dan Dellia (2024) mengembangkan sistem rekomendasi buku menggunakan content-based filtering dengan TF-IDF dan cosine similarity, yang terbukti efektif dengan tingkat kelayakan sistem mencapai 91,4% [1]. Sementara itu, penelitian yang dilakukan oleh Guo (2024) menggabungkan collaborative filtering dengan CNN (model VGG16) untuk mengekstraksi fitur visual dari poster film, yang meningkatkan akurasi rekomendasi dari 70% menjadi 85% serta memperkaya keragaman dan kesesuaian saran dengan minat pengguna [2]. 

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

#### Insight yang dida
