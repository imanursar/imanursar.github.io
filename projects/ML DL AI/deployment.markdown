---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: Machine Learning System Design
parent: ML DL AI
permalink: /ml_dl_ai/ml_sd
nav_order: 99
---

#  Machine Learning System Design
machine learning
{: .badge .badge-pill .badge-primary }
supervised learning
{: .badge .badge-pill .badge-secondary }
evaluation
{: .badge .badge-pill .badge-secondary }

* Do not remove this line (it will not be displayed)
{:toc}

# Machine Learning System Design
Sebuah sistem machine learning minimal harus memenuhi persyaratan utama berikut:
1. **Bersifat andal (reliable)**
   - **Antisipasi Kegagalan**
     - kualitas data yang buruk dan tidak memadai.
     - kesalahan terkait model           -> pemeriksaan terhadap asumsi model.
     - kerapuhan model (model fragility) -> prediksi model sangat sensitif terhadap gangguan pada masukan.
   - **Pemeliharaan**
     - Dalam proses ini kita perlu mendeteksi kapan pembaruan sistem harus dilakukan dan bagaimana cara melakukannya dengan aman?
     - Sistem machine learning adalah proses iteratif.
     - Siklus pengembangan machine learning memerlukan umpan balik (feedback) selama proses pembelajaran yang berkelanjutan.
     - Feedback loops adalah proses di mana perubahan atau output dari salah satu bagian sistem dikirimkan kembali ke dalam sistem sebagai input sehingga mempengaruhi tindakan atau output sistem selanjutnya.
     - Umpan balik ini berguna untuk meningkatkan akurasi prediksi dan merupakan bagian dari pemeliharaan sistem machine learning.
2. **Memiliki kemampuan untuk menangani perubahan (scalable)**
- Proses penanganan terhadap perubahan kapasitas tidak hanya berarti peningkatan sumber daya untuk menangani pertumbuhan data (scaling up), tetapi juga penanganan untuk mengurangi sumber daya yang tidak kita butuhkan (scaling down).
3. **Memiliki kemampuan untuk beradaptasi (adaptable)**
- Beberapa cara untuk membuat sistem bersifat adaptif terhadap perubahan distribusi data:
  - Memantau statistik deskriptif untuk masukan dan keluaran.
  - Menggunakan arsitektur pelatihan yang dinamis.
  - Melatih model Anda secara berkala.
1. **Mudah dalam pemeliharaan (maintainable)**
- Tahapan siklus pemeliharaan, yaitu:
  - Melatih model
  - Evaluasi secara offline
  - Evaluasi secara online
  - Pengawasan model

- Saat membuat infrastruktur machine learning, ada beberapa hal yang perlu dijadikan bahan pertimbangan, antara lain:
  - sumber daya komputasi
  - infrastruktur jaringan
  - infrastruktur penyimpanan
  - faktor keamanan

- Proses pemeliharaan sistem machine learning yaitu keterlibatan subject matter experts (melibatkan beberapa pihak).

# 6 tahap utama dalam siklus ML
1. **Cakupan proyek**: Ini merupakan tahapan saat seorang machine learning engineer menentukan perencanaan proyek, menetapkan tujuan dan sasaran, kendala-kendala yang mungkin dihadapi, dan kriteria evaluasi. Tahap ini melibatkan para pemangku kepentingan (stakeholder) antara lain tim bisnis/penjualan, tim infrastruktur, tim produk, dan tim DevOps. Proses estimasi dan alokasi sumber daya yang mendukung proyek juga dilakukan di tahap ini.
2. **Manajemen Data**: Pada tahap ini kita melakukan pemrosesan data, kontrol data, dan mengatur penyimpanan data. Tahapan ini berkaitan erat dengan infrastruktur dalam memproses dan mengakses data secara cepat dan andal.
3. **Pengembangan Model Machine Learning**: Tahapan inilah yang sering dibahas di berbagai kursus atau kelas machine learning. Di sini, kita akan mengimplementasikan pengetahuan machine learning untuk melatih model, melakukan optimalisasi, dan mengevaluasi hasilnya.
4. **Deployment**: Ini adalah tahap produksi agar model machine learning mudah digunakan dan bisa diakses oleh pengguna.
5. **Pengawasan dan Pemeliharaan**: Setelah melewati tahap produksi, model harus tetap dipantau dan dikelola secara berkala agar bisa adaptif terhadap berbagai perubahan.
6. **Analisis Bisnis**: Pada tahapan ini kita menganalisis dan mengevaluasi kinerja model terhadap tujuan bisnis untuk mendapatkan wawasan (insight) yang berguna bagi kebutuhan bisnis. Hasil analisis pada tahapan ini bisa digunakan sebagai umpan balik bagi proyek atau untuk bahan perencanaan proyek baru.

# Infrastruktur Machine Learning

## Infrastruktur yang dibutuhkan untuk Data antara lain:
1. **Sumber data**: antara lain berasal dari Database, layanan penyimpanan (storage services), atau log files (data yang dihasilkan dari komputer).
2. **Data warehouse**: Databricks, Google Bigquery, Snowflake, atau Redshift.
3. **Pemrosesan data (data processing)**: Dapat dilakukan dengan Apache Spark, Airflow, atau Dagster.
4. **Eksplorasi data (data exploration)**: Contohnya adalah Pandas, library yang sering kita gunakan selama ini.
5. **Data versioning**: Contohnya menggunakan tools Pachyderm, atau DVC.
6. **Data labeling**: Dapat dilakukan menggunakan Scale, atau Aquarium.

## Infrastruktur yang dibutuhkan untuk Training/Evaluasi antara lain:
1. **Sumber daya komputasi**: menggunakan infrastruktur penyedia layanan cloud seperti Google Cloud Platform (GCP), Microsoft Azure, dan AWS. Dengan membeli peralatan infrastruktur Anda sendiri misalnya dari  Lambda Labs, NVIDIA, dan CoreWeave.
2. **Sumber daya manajemen**: Docker/Kubernetes atau menggunakan perangkat lunak machine learning seperti AWS Sagemaker, Paperspace Gradient, SPSS, Weka, atau Determined AI.
3. **Rekayasa perangkat lunak**: membutuhkan infrastruktur seperti Python IDE, Git, Streamlit, atau Jupyter Notebook.
4. **Frameworks dan Distributed Training Libraries**: antara lain TensorFlow, Pytorch, Keras, atau Fast.ai.
5. **Manajemen Eksperimen**: contohnya TensorBoard, MLFlow, atau Neptune.
6. **Hyperparameter Tuning**: opsinya antara lain SigOpt, Ray Tune, atau Weight and Biases.

## Infrastruktur yang dibutuhkan untuk Deployment antara lain:
1. **CI (Continuous Integration) dan Testing**: Jenkins, Buildkite, atau CircleCI.
2. **Edge Deployment**: TensorFlow Lite, ONNX, atau ML Kit.
3. **Web Deployment**: Kubernetes, SLURM, atau Algorithmia.
4. **Monitoring**: Fiddler.
5. **Feature Store**: Tecton.

# Kategori Data kepemilikan
- Data pihak pertama adalah data yang dikumpulkan perusahaan tentang pengguna atau pelanggan.
- Data pihak kedua adalah data yang dikumpulkan oleh perusahaan lain tentang pelanggan mereka.
- Data pihak ketiga mengumpulkan data tentang masyarakat umum yang bukan pelanggan mereka.
- Data sintesis (data yang dihasilkan dari teknik pemrograman)
- Data augmentation (strategi yang memungkinkan kita untuk meningkatkan keragaman data tanpa perlu menambah jumlah data baru).

# Baseline model
Ada beberapa teknik dalam membuat baseline model, antara lain:
- Random algorithm, algoritma paling sederhana melakukan prediksi hasil acak yang diamati dalam data pelatihan.
- Zero rule algorithm. Baseline untuk permasalahan klasifikasi dan regresi.
  - Untuk kasus regresi, zero rule algorithm memprediksi rata-rata dari dataset latih.
  - Untuk kasus klasifikasi, algoritma ini memprediksi nilai kelas yang paling banyak diobservasi data training.
  
# Machine Learning Deployment
Umumnya model machine learning di-deploy dengan menggunakan 3 cara utama, yakni sebagai berikut:
- **Menggunakan model server**: User menginput live data langsung ke model server, kemudian server mengembalikan hasil prediksi. Kemudian model tersebut dijalankan pada suatu environment seperti kontainer yang berisi model dan banyak library penting untuk membangun API. 2 jenis API yaitu REST dan gRPC yang keduanya merupakan protokol komunikasi:
  - REST API digunakan oleh aplikasi web dan mendefinisikan cara berkomunikasi antara user dengan layanan web. API ini akan menerima permintaan berupa data JSON, memasukkan data tersebut kedalam fungsi, dan mengembalikan respon berupa hasil prediksi.
  - gRPC mendukung lebih beragam format data dibanding REST, namun standar data yang digunakan adalah protocol buffer.
- **Browser**: Terdapat beberapa situasi di mana user tidak ingin menginput data langsung ke model server. model machine learning dapat di-deploy ke browser user. Jadi, hasil prediksi bisa didapatkan sebelum data diunggah ke cloud server. Contoh mekanisme ini berlaku pada Tensorflow.js atau ONNX.js.
- **Edge devices**: Mekanisme ini digunakan jika user tidak dapat terkoneksi dengan model server untuk mendapatkan hasil prediksi. Misalnya karena model tersebut ditanamkan pada IoT device alias peranti dengan sensor jarak jauh. Model dilatih terlebih dahulu dari pusat, kemudian model dibuat dalam format portable dan dipindahkan ke edge devices.

Semakin lama kinerja model akan menurun seiring waktu. Istilah ini dikenal dengan model drift.

## Machine Learning Deployment Schema
- **Batch scoring**: Ini adalah kategori deployment saat model memproses seluruh dataset yang telah dikumpulkan dari waktu ke waktu untuk menghasilkan prediksi baru.Kategori ini digunakan saat keputusan model tidak harus segera ditetapkan.

Pada kategori ini, proses scoring biasanya dilakukan pada jadwal tertentu. Untuk menjadwalkan proses batch scoring, pertimbangkan beberapa hal berikut:
1. Ketersediaan data.
2. Seberapa sering keputusan bisnis harus diambil.
3. Berapa lama proses yang dibutuhkan untuk menjalankan proses batch scoring.

- **Real-time scoring**: Pertumbuhan dan peningkatan data digital berimbas pada kebutuhan untuk memproses data segera saat diterima atau disebut juga secara real-time. Kategori ini digunakan saat waktu merupakan sumber daya yang penting dalam model machine learning.

Berikut beberapa hal yang perlu Anda pertimbangkan saat menggunakan teknik deployment ini.
1. Siapa yang menerima hasil prediksi, apakah manusia atau sistem otomatis?
2. Jika manusia yang akan menerima, bagaimana ia akan menerima hasilnya? Apakah lewat perangkat seluler, atau lewat media lain?
3. Jika sistem otomatis yang menerima, apa yang selanjutnya akan dilakukan oleh sistem setelah menerima prediksi?
4. Apakah hasilnya akan digunakan sebagai sistem peringatan untuk manusia (misal peringatan dini terjadi bencana) atau untuk mengontrol proses lain?

## Machine Learning Deployment Strategy
Tiga strategi deployment yang umum digunakan:
1. **Recreate Deployment**: Strategi penerapan ulang bekerja dengan sepenuhnya menurunkan versi aplikasi lama sebelum Anda meningkatkan versi aplikasi baru. Saat melakukan pembaruan, Anda harus menurunkan atau mematikan versi lama, kemudian melakukan penerapan dengan versi baru.

Kelebihan dari strategi ini adalah kesederhanannya. Anda tidak perlu mengelola lebih dari satu versi aplikasi secara paralel. Sehingga Anda tidak perlu melakukan penyesuaian lagi terhadap data dan aplikasi. Sedangkan kekurangan dari strategi ini adalah adanya downtime (waktu henti) selama proses pembaruan. Hal ini tentu akan berdampak pada pengguna yang harus menunggu sistem mati dan menyala kembali dalam durasi waktu tertentu.

2. **Blue-Green Deployment**: Pada blue-green deployment, Anda melakukan dua penerapan yang identik dari aplikasi. Strategi ini berguna saat Anda ingin menerapkan versi baru aplikasi sekaligus memastikan bahwa layanan aplikasi tetap tersedia saat penerapan diperbarui. Pada diagram di atas, warna biru merepresentasikan versi aplikasi saat ini, sedangkan warna hijau adalah aplikasi versi baru. Hanya satu versi yang menyala/hidup pada satu waktu. Rute lalu lintas diarahkan ke penerapan biru sementara penerapan hijau dibuat dan diuji. Setelah proses pengujian selesai, Anda mengubah rute lalu lintas ke versi baru (versi hijau). Jika penerapan berhasil, Anda dapat mempertahankan penerapan biru untuk kemungkinan proses muat ulang atau menonaktifkannya.

Kelebihan strategi ini adalah rilis aplikasi dapat dilakukan dengan segera tanpa perlu ada waktu henti. Versi yang lebih baru dapat diuji secara internal sebelum merilisnya ke pengguna. Penerapan biru/hijau memastikan bahwa proses yang terjadi di lingkungan hijau tidak mempengaruhi sumber daya di lingkungan biru. Hal ini tentu mengurangi risiko penerapan.

Akan tetapi, strategi ini memiliki kekurangan yaitu kebutuhan sumber daya seperti biaya dan operasional menjadi dua kali lipat selama proses penerapan.

3. **Rolling Update Deployment**: Rolling Update Deployment adalah strategi pembaruan yang mengalihkan lalu lintas secara bertahap ke versi baru. Pada strategi ini, Anda memperbarui bagian demi bagian aplikasi yang sedang berjalan dan tidak melakukan pembaruan secara bersamaan.

Kelebihan strategi ini antara lain, tidak ada waktu henti (downtime) dan Anda dapat memperbarui target penerapan secara bertahap, misalnya satu per satu atau dua per dua. Lalu lintas produksi dapat diarahkan ke target deployment setelah versi baru aplikasi siap menerimanya. Pembaruan secara bertahap ini mengurangi risiko penerapan yang disebabkan oleh ketidakstabilan. Risiko yang mungkin terjadi ini hanya akan mempengaruhi sebagian pengguna.

Kekurangan strategi ini adalah proses muat ulang yang lambat karena proses penerapannya secara bertahap. Selain itu, ada kemungkinan terjadi masalah dengan kompatibilitas. Hal ini karena kode baru dan kode lama berjalan secara bersamaan. Oleh karena itu, Anda perlu memastikan bahwa penerapan baru dapat membaca dan menangani data yang disimpan oleh versi lama.

## Model type
Jenis-jenis ML model dibedakan menjadi 2 berdasarkan cara dilatihnya:
- **model statis**: Model statis dilatih secara offline dari jumlah data yang sangat banyak. Pelatihan dilakukan hanya sekali lalu model tersebut sudah siap digunakan.Jika data yang kita gunakan tidak cepat berubah oleh waktu, maka model statis lebih cocok diterapkan.
- **model dinamis**: dilatih secara online. Model dinamis beradaptasi dengan cepat terhadap data sehingga model ini lebih cocok diterapkan untuk data yang mudah berubah.
- **continuous learning**: menggunakan sistem otomasi untuk mengevaluasi dan latih ulang model. Dimulai dengan menyimpan data latih baru misalnya data harga rumah yang paling baru, kemudian simpan pada basis data. uji akurasi model lama dengan data tersebut, Jika akurasi model menurun, maka gunakan data harga rumah yang paling baru,atau gunakan kombinasi data lama dan baru untuk membuat dan mengembangkan model baru.

## Risk in Deployment
1. **Permasalahan dengan Penyimpangan Model**: Penyimpangan model (model drift) adalah permasalahan umum terkait performa model machine learning di tahap produksi.Penyimpangan ini terjadi ketika kinerja model turun di bawah tolok ukur yang bisa diterima (benchmark). Perubahan pada data umumnya menjadi penyebab utama penyimpangan ini. Oleh karena itu, Anda harus mampu mengenali berbagai perubahan pada data.
2. **Permasalahan yang berkaitan dengan sistem rekayasa perangkat lunak**: Anda perlu membuat keputusan terkait pilihan-pilihan ini, antara lain:
   - Menentukan sumber daya komputasi, berapa banyak CPU, GPU, atau memory yang diperlukan dalam proses produksi?
   - Menentukan proses scoring, apakah batch scoring atau real-time?
   - Menentukan di mana layanan produksi dijalankan, apakah di cloud, web, atau peranti edge?
   - Menentukan apakah Anda akan menjalankan proses produksi di cloud atau on-premise server?
   - Mengatur dan mengoptimasi performa untuk menekan latency (waktu tunda antara tindakan pengguna dan respons aplikasi web terhadap tindakan itu) dan mempercepat inference (proses menjalankan data ke dalam algoritma machine learning).


# Degenerate Model
2 tipe penurunan kualitas pada model yaitu:
- **sudden degradation**: ditemukan bug pada model terbaru yang menyebabkan penurunan akurasi yang signifikan. Cek kualitas model terbaru dengan membandingkan akurasinya terhadap model sebelumnya.
- **slow degradation**: penurunan kualitas dalam beberapa versi model yang telah diperbarui, tidak terdeteksi. Pada kasus ini pastikan akurasi model Anda pada data validasi memenuhi ambang batas nilai yang ditentukan (threshold).

Penurunan kualitas model dapat disebabkan oleh beberapa hal seperti: masuknya data yang belum pernah dilihat oleh model sebelumnya, perubahan environment atau relasi antar variabel, dan perubahan ekstrim pada data.

# Monitoring model

## Strategic keys
Beberapa prinsip kunci yang dapat diterapkan dalam pemantauan sistem ML yaitu:
- Monitor perubahan dependency (ketergantungan) sebaiknya dibuat dalam bentuk notifikasi.
- Monitor perbedaan data training dan data yang mungkin muncul pada live data. Data training seharusnya merepresentasikan data yang mungkin akan muncul pada live sistem.
- Monitor fitur pada training dan pada penyajian model.
- Monitor perbaruan model. Jangan sampai model tidak up to date.
- Monitor kestabilan model.
- Model seharusnya tidak mengalami kelambatan lantensi pengembalian output, penggunaan RAM, throughput, atau pada kecepatan training.
- Model tidak mengalami penurunan kualitas prediksi terhadap live data.

## Model Monitoring
Sistem monitoring dirancang untuk memberikan peringatan dini terhadap berbagai kesalahan yang mungkin terjadi pada model machine learning di tahap produksi.

Kesalahan-kesalahan ini umumnya disebabkan oleh:
1. Data yang tidak seimbang. Hal ini terjadi saat data yang digunakan pada proses pelatihan tidak mewakili data pada sistem.
2. Model drift akibat perubahan lingkungan, perilaku pengguna, atau perubahan interpretasi data.
3. Umpan balik negatif yang bisa mengakibatkan bias dan penurunan performa.

matriks apa yang perlu kita monitor?
1. **Performa model**: Matriks ini membantu kita mendeteksi terjadinya penyimpangan dalam model. Ini adalah matriks yang paling sulit untuk dimonitor secara real time karena label sulit didapatkan dan perlu disesuaikan seiring waktu.
2. **Model Input**: Matriks ini digunakan untuk mengukur perubahan distribusi data masukan.
3. **Performa sistem**: Matriks ini membantu kita menentukan bagaimana kinerja model yang ditetapkan dari sudut pandang penggunaan atau layanan


# Test the model
- **A/B testing**: Pengujian A/B dilakukan untuk mengumpulkan data dengan menggunakan acuan nilai statistik tertentu dan ditujukan untuk membuat sebuah keputusan bisnis.Pengujian A/B dilakukan untuk mempelajari dampak dari tiap variasi model.
- **Multi Armed Bandit (MAB)**: 
  - tipe pengujian A/B yang menggunakan ML untuk belajar dari data yang dikumpulkan selama pengujian. Konsep MAB ini ada pada traffic yang diubah-ubah secara dinamis. MAB menjalankan 2 fase yaitu exploration dan exploitation.Mirip dengan A/B testing namun pada MAB ditambahkan mode exploitation di mana mode tersebut dijalankan secara paralel dengan mode exploration sehingga resource seperti traffic pengunjung secara mayoritas terus-menerus dialokasikan ke model yang memiliki peluang menjadi model yang paling unggul (eksploitasi).
  - Kelebihan dari MAB yaitu secara bertahap aplikasi akan meluncurkan model versi terbaik tanpa harus menunggu hasil pengujian mencapai nilai statistik yang signifikan. Optimasi lebih maksimal dan dapat dilakukan secara kontinu karena pengembang dapat fokus ke satu model saja.
  - MAB merupakan suatu algoritma yang digunakan untuk fokus memaksimalkan kinerja menggunakan suatu acuan metrik. pengembang sedang menguji suatu skema yang spesifik, maka skema itu saja yang dimaksimalkan.

# Scale the ML model
- **Scaling With Respect To training data**: Your model is only as good as the underlying data on which it is trained, and it usually is. Retraining your model is absolutely necessary when underlying assumptions about the data change.
- **Scaling With Respect To data deluge**: big business -> big data -> might want to consider parallel computing or batch processing (say using SGD optimization) and parallelize processes like cross-validation and hyperparameter tuning.
  >look for a distributed version of algorithms!
It is also prudent to use checkpoints while retraining serialized/pickled models, as you do not have to rebuild it from scratch just because you received an additional data.
- **Scaling With Respect To framework**: what is the level of abstraction you desire?
Compare the frameworks based on how good their community support is, how easily does it allow third-party integrations, and whether or not it can support Distributed ML
- **Scaling With Respect To features**: It is only reasonable to find that with the passage of time, new predictors come to light, which were previously ignored or considered unimportant.

Make sure that the addition of these features is not leading towards overfitting the model and that you are able to witness an improvement on your validation sets as well.

Even better, implement regularization techniques to be extra sure that your coefficients don’t take extreme values and that the model isn’t too complex.

The accuracy improvements must justify increased maintenance and training costs.

- **Scaling With Respect To actual predictions**: As your the number of prediction requests keep pouring in, it is time to think about whether your model is churning out predictions fast enough. especially without GPU support.

Deployment using backend APIs or make it available to the world as hardware-accelerated models on the web

