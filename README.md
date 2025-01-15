# Laporan Proyek Machine Learning - Istia Budi

## Project Overview

Industri game telah berkembang pesat dalam beberapa dekade terakhir, dengan konsol seperti Nintendo menjadi salah satu pemain utama yang menghadirkan inovasi dan pengalaman bermain yang unik. Sejak peluncurannya, Nintendo telah merilis berbagai konsol yang ikonik, mulai dari Nintendo Entertainment System (NES) hingga Nintendo Switch, serta ribuan judul game yang mencakup berbagai genre dan audiens. Popularitas platform Nintendo tidak hanya berasal dari kualitas game eksklusifnya, tetapi juga dari keberhasilan menarik komunitas pemain yang luas dan loyal.

Namun, dengan semakin banyaknya judul game yang dirilis setiap tahunnya, pemain sering kali menghadapi tantangan dalam memilih game yang sesuai dengan preferensi mereka. Ketika katalog game semakin luas, kebutuhan akan sebuah sistem rekomendasi yang efektif menjadi sangat penting. Sistem rekomendasi dapat membantu pengguna menemukan game berdasarkan genre, kategori, mekanik permainan, atau bahkan popularitas game di kalangan komunitas Nintendo.

## Business Understanding

Sistem Rekomendasi memiliki potensi untuk memberikan banyak manfaat kepada pengguna dan platform jual beli game Nintendo. Sistem ini dapat membantu pengguna untuk menemukan game yang sesuai dengan selera mereka dengan mudah dan efisien. Platform jual beli juga mendapatkan engagement dari pengguna.

### Problem Statements

- Banyaknya jumlah game Nintendo membuat pemain kesulitan dalam menemukan judul yang sesuai dengan preferensi pribadi mereka.
- Pengembangan sistem rekomendasi yang kompleks sering kali memerlukan sumber daya yang besar, sehingga perlu solusi sederhana yang tetap efektif.

### Goals

- Memberikan rekomendasi game yang relevan untuk mencocokkan preferensi pengguna dengan karakteristik game yang tersedia.
- Merancang solusi berbasis cosine similarity yang mudah diimplementasikan dan memberikan hasil rekomendasi dengan waktu proses yang cepat dan hasil yang akurat.

### Solution statements

Menggunakan algoritma cosine similarity untuk menghitung kesamaan antara preferensi pengguna dan atribut game (genre, kategori, atau deskripsi). Sistem akan menganalisis judul dan genre dari setiap game, lalu mencocokkannya dengan data preferensi pengguna. Pendekatan ini cocok untuk pengguna yang memiliki preferensi jelas terhadap jenis game tertentu.

## Data Understanding

### Informasi Dataset
| **Jenis** | **Keterangan** |
| ---- | ---- |
| Sumber	 | [Nintendo Games - Kaggle](https://www.kaggle.com/datasets/joebeachcapital/nintendo-games) |
| Dataset Owner | [Joakim Arvidsson](https://www.kaggle.com/joebeachcapital) |
| License | Database: Open Database, Contents: Database Contents |
| Tags | Software, Games, Video Games, Classification, Ratings and Reviews |
| Usability | 10.0 |

Kumpulan dataset ini merupakan hasil scrapping dari platform (Metacritic.com)(https://www.metacritic.com/). Metacritic adalah situs web yang mengumpulkan ulasan dan memberikan skor untuk berbagai produk, seperti film, acara TV, album musik, permainan video, dan buku. Skor yang diberikan oleh Metacritic disebut Metascore. Dataset yang akan digunakan adalah dataset khusus untuk game Nintendo.
Dataset ini dapat diunduh di Kaggle : [Nintendo Games - Kaggle](https://www.kaggle.com/datasets/joebeachcapital/nintendo-games).

### Kondisi Data
- Jumlah Data: Dataset terdiri dari 1094 baris dan 9 kolom.
- Missing Value: Ditemukan nilai yang hilang (missing values) pada kolom ```meta_score``` sebanyak 385 data, kolom ```user_score``` sebanyak 238 data, kolom ```esrb_rating``` sebanyak 122 data, kolom ```developers``` sebanyak 3 data.
- Duplikat Data: Terdapat 35 data yang duplikat.

Berdasarkan data tersebut variabel-variabel pada Nintendo Games Dataset adalah sebagai berikut:

- Meta Score: Skor review dari kritikus profesional platform Metacritic (0-100)
- Title: Judul game Nintendo
- Platform: Platform atau konsol yang tersedia untuk game (NDS, 3DS, Switch dll)
- Release Date: Tanggal rilis resmi game
- User Score: Skor ulasan yang diberikan pengguna untuk game (0-10)
- Details Page Link: Tautan ke halaman detail game di situs Metacritic
- ESRB Rating: Rating ERSB (Entertainment Software Rating Board) yang menunjukkan tingkat kesesuaian usia pemain untuk game tersebut (misalnya E untuk Everyone, T untuk Teen, M untuk Mature, dll.)
- Developers: Nama pengembang game
- Genres: Genre atau kategori game (Action, Puzzle, dll)


### EDA

![pie chart esrb](https://github.com/user-attachments/assets/3cae320c-e3e7-4979-ad2d-e8056a2f103c)

Berdasarkan grafik diatas sebagian besar game di Nintendo memiliki rating E (Everyone) dengan presentase 67.9% dan yang paling terkecil adalah RP (Rating Pending) game yang ratingnya masih belum ditentukan. Jadi game Nintendo sangat cocok dimainkan untuk semua orang.

![bar chart meta score](https://github.com/user-attachments/assets/b6076bee-8461-4a84-af68-98cae45682eb)

Meta score adalah hasil dari review dari kritikus professional yang dipilih langsung oleh Metacritics, The Legend Of Zelda: Ocarina of Time mendapatkan rating yang paling tinggi.

![bar chart user score](https://github.com/user-attachments/assets/338b64ff-8221-4a1f-863b-0b47ea282599)

Berdasarkan grafik diatas, Metal Torrent merupakan game yang memiliki skor tertinggi berdasarkan review dari pengguna metacritics.

![line chart tahun](https://github.com/user-attachments/assets/61fb343d-871d-4518-a160-e495c4600377)

Pada tahun 2009, para pengembang mencatat rekor dengan merilis total 90 game dalam satu tahun, menjadikannya tahun dengan jumlah perilisan game terbanyak. Pencapaian ini didorong oleh popularitas konsol Nintendo DS yang sedang berada di puncak kejayaannya.

## Data Preparation

Data preparation bertujuan untuk mempersiapkan data agar proses pengembangan model diharapkan akurasi model akan menjadi lebih baik dan mengurangi bias pada data. Tahapan preparation data yaitu:
- **Seleksi Fitur**: Dataset ini memiliki banyak fitur yang dapat digunakan tetapi dalam proyek sistem rekomendasi sederhana ini hanya menggunakan dua kolom yaitu ```title``` dan ```genres```. Fitur yang lainnya mungkin dapat menjadi nilai tambah untuk membuat model yang lebih kompleks.
- **Menghapus Missing Values**: Menghapus missing values yang ada di kolom ```title``` dan ```genres```. Menghapus missing values setelah seleksi fitur yang relevan untuk memastikan informasi terkait game tetap terjaga.
- **Menghapus Duplikasi Data**: Terdapat 35 data duplikasi yang perlu dihapus.

## Modeling
Cosine Similarity diterapkan dalam sistem rekomendasi berbasis content-based filtering untuk mengukur tingkat kesamaan antara satu game dengan game lainnya, berdasarkan fitur-fitur yang dimiliki oleh masing-masing game.

Dalam membangun model content-based filtering, langkah awalnya adalah memanfaatkan TF-IDF Vectorizer sebagai metode feature engineering untuk mengidentifikasi fitur penting pada setiap game. Proses ini dilakukan menggunakan fungsi ```TfidfVectorizer()``` dari library sklearn. Setelah itu, data difit dan ditransformasikan ke dalam bentuk matriks. Hasil akhirnya adalah matriks berukuran (1046, 133), di mana angka 1046 merepresentasikan jumlah data, sedangkan angka 133 menunjukkan jumlah genre game yang terwakili dalam matriks tersebut.

Untuk menentukan tingkat kesamaan (degree of similarity) antara game, metode Cosine Similarity diterapkan menggunakan fungsi ```cosine_similarity``` dari library sklearn. Konsep ini dihitung berdasarkan persamaan matematika berikut:

Rumus Cosine Similarity

Tahapan selanjutnya melibatkan penggunaan metode argpartition untuk mengidentifikasi sejumlah nilai k tertinggi dalam data similarity. Setelah itu, sistem akan menyusun hasil berdasarkan bobot kesamaan, dimulai dari yang tertinggi hingga terendah. Akhirnya, akurasi sistem rekomendasi diuji untuk memastikan kemampuannya dalam menemukan game yang memiliki kemiripan dengan game yang dicari pengguna.

- Kelebihan Cosine Similarity:
  - Efisien dan Sederhana: Metode ini mudah diimplementasikan dan dapat menangani data berdimensi tinggi dengan baik.
  - Tidak Bergantung pada Skala: Cosine Similarity hanya mempertimbangkan orientasi vektor, bukan magnitudonya, sehingga cocok untuk data dengan skala yang berbeda.
  - Cocok untuk Data Sparsity: Efektif digunakan pada dataset dengan banyak elemen nol, seperti matriks fitur game atau dokumen.
- Kekurangan Cosine Similarity:
  - Tidak Mempertimbangkan Nilai Absolut: Karena hanya mengukur sudut antar vektor, metode ini tidak memperhitungkan intensitas atau nilai absolut dari fitur.
  - Kurang Relevan pada Data Bukan Vektor: Performanya menurun jika digunakan pada data yang tidak dapat direpresentasikan sebagai vektor numerik.
  - Keterbatasan pada Data Non-Linear: Tidak ideal untuk dataset dengan hubungan kompleks yang memerlukan pendekatan non-linear.

## Evaluation

### Prediksi
Berikut ini adalah konten yang dijadikan referensi untuk menentukan 5 rekomendasi game tertinggi yang memiliki kesamaan genre yang sama:

| title | genres |
| ----- | ---- |
| The Legend of Zelda: Ocarina of Time | ['Action Adventure', 'Fantasy'] |

Pengujian dilakukan dengan menggunakan judul game "The Legend of Zelda: Ocarina of Time" yang memiliki genre "Action Adventure" dan "Fantasy".

Berikut ini adalah hasil rekomendasi dari sistem yang menampilkan lima game dengan kesamaan genre yang sama dengan "The Legend of Zelda: Ocarina of Time":

| title | genres |
| ----- | ---- |
| The Legend of Zelda: Twilight Princess | ['Action Adventure', 'Fantasy'] |
| The Legend of Zelda: Four Swords Adventures	| ['Action Adventure', 'Fantasy'] |
| Chibi-Robo!	| ['Action Adventure', 'Fantasy'] |
| The Legend of Zelda: The Minish Cap	| ['Action Adventure', 'Fantasy'] |
| The Legend of Zelda: Link's Awakening DX | ['Action Adventure', 'Fantasy'] |

Sistem rekomendasi berhasil mengidentifikasi lima game yang serupa dengan "The Legend of Zelda: Ocarina of Time", yaitu game dengan genre yang sama.

### Evaluasi Model
Evaluasi model Content-Based Filtering dilakukan dengan menggunakan metrik Precision. Metrik ini mengukur sejauh mana model dapat memprediksi kejadian yang relevan atau positif.

Berdasarkan rekomendasi yang diberikan di atas, game "The Legend of Zelda: Ocarina of Time" memiliki dua genre. Dari lima game yang direkomendasikan, semuanya memiliki dua genre yang sama, yaitu "Action Adventure" dan "Fantasy". Hal ini menunjukkan bahwa precision dari sistem rekomendasi ini adalah 100%.

Rumus Precision:

![precision_formula](https://github.com/user-attachments/assets/0943cb5f-fcf1-450c-aa48-e694e4b2ecda)

Pada contoh rekomendasi di atas: Precision = 5/5. Jadi presisinya = 100%.

### Dampak terhadap Business Understanding
Implementasi sistem rekomendasi berbasis content-based filtering dengan algoritma Cosine Similarity memberikan dampak positif signifikan bagi platform Nintendo, baik dari segi pengguna maupun bisnis.
- Apakah model sudah menjawab problem statement?
Model yang dibangun dengan menggunakan algoritma cosine similarity berhasil menjawab masalah yang dihadapi oleh pengguna dalam menemukan game yang sesuai dengan preferensi mereka. Dengan ribuan game Nintendo yang tersedia, sistem rekomendasi ini dapat menyaring dan menyarankan game yang relevan berdasarkan genre dan preferensi pengguna, sehingga memudahkan pengguna untuk menemukan pilihan yang tepat. Ini membantu mengatasi tantangan besar yang dihadapi pemain terkait pilihan game yang berlimpah dan membuat proses pencarian menjadi lebih efisien.
- Apakah goals tercapai?
Goals dari proyek ini tercapai dengan baik. Sistem rekomendasi berhasil memberikan game yang relevan berdasarkan genre, yang langsung mencocokkan preferensi pengguna dengan karakteristik game yang tersedia. Selain itu, solusi berbasis cosine similarity yang diimplementasikan juga memenuhi tujuan untuk menyediakan rekomendasi yang cepat dan akurat, dengan proses yang efisien. Dengan menggunakan metode yang sederhana dan mudah diimplementasikan, hasil rekomendasi tidak hanya cepat tetapi juga sangat relevan dengan input preferensi pengguna.
- Apakah solusi yang direncanakan berdampak?
Solusi yang direncanakan memberikan dampak signifikan bagi platform jual beli game Nintendo. Dengan sistem rekomendasi yang efektif, pengguna akan lebih mudah menemukan game yang sesuai dengan preferensi mereka, meningkatkan pengalaman pengguna dan meningkatkan kepuasan pengguna secara keseluruhan. Ini dapat meningkatkan engagement pengguna di platform jual beli game, yang pada gilirannya berpotensi meningkatkan penjualan dan loyalitas pelanggan.

### Kesimpulan
Sistem rekomendasi berbasis cosine similarity yang dibangun berhasil memenuhi tujuan untuk membantu pengguna menemukan game yang relevan dengan preferensi mereka secara efisien. Dengan memanfaatkan genre dan deskripsi game, model ini memberikan hasil rekomendasi yang akurat dan cepat. Solusi ini tidak hanya efektif dalam mengatasi tantangan pencarian game yang sesuai, tetapi juga memberikan dampak positif pada platform jual beli game dengan meningkatkan pengalaman pengguna dan engagement, sekaligus menggunakan sumber daya yang efisien.
