---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: citi bike performance
parent: Portfolio
nav_order: 3
---

# Citi Bike Performance

## Program Bike Sharing

Citi Bike adalah layanan bike sharing yang melayani Kota New York dan sekitarnya yang diresmikan pada Mei 2013. Bandung telah lebih dulu meluncurkan program bike sharing bernama Bike Bdg yang diinisiasi oleh Bandung Creative City Forum. Program ini diluncurkan pada tahun 2012 dengan total sepuluh shelter. Walaupun jalur sepeda yang ada masih kurang memadai dan kebanyakan hanya berada di tengah kota, penulis sebagai warga Bandung saat itu yang punya hobi bersepeda merasa pembukaan Bike Bdg saat itu menjadi salah satu titik balik maraknya pesepeda di Bandung.

Sayangnya karena banyaknya batasan teknis program tersebut tidak terlalu banyak diadopsi warga Bandung. Salah satu batasannya adalah sepeda yang dipinjam harus dikembalikan di shelter yang sama, sehingga penggunaannya lebih cocok untuk rekreasi dan bukan untuk transportasi dari suatu titik ke titik lain. Di sisi lain, Citi Bike memiliki stasiun dimana pengguna bisa meminjam dan mengembalikan sepeda di titik yang berbeda. Pada Juli 2017 Pemkot Bandung meluncurkan program bike sharing bernama Boseh. Di program ini pengguna dapat meminjam dan mengembalikan sepeda di shelter yang berbeda. Dengan skema tersebut dan jumlah shelter yang lebih banyak, program Boseh mungkin bisa bertahan lebih lama dibanding pendahulunya yaitu Bike Bdg.

Studi oleh [Sobolevsky (2009)](https://www.researchgate.net/publication/327153225_Impact_Of_Bike_Sharing_In_New_York_City) menunjukkan program Citi Bike membawa banyak keuntungan dari berbagai aspek ekonomi, sosial, dan lingkungan. Jika kita ingin mereplikasi keberhasilan program Citi Bike, tentu banyak aspek yang harus diperbaiki, tidak hanya dari sisi program bike sharing. Namun untuk menuju hal tersebut setidaknya kita bisa mempelajari kinerja dan karakteristik pengguna Citi Bike melalui data yang tersedia untuk publik di Google Big Query. Data yang tersedia berupa data tiap perjalanan dengan informasi tentang durasi perjalanan, detail stasiun awal dan akhir, dan detail pengguna.

Tujuan dari analisis ini adalah:

1. Mengukur kinerja Citi Bike berdasarkan jumlah dan durasi perjalanan
2. Mengetahui karakteristik pengguna Citi Bike

## Dataset

Dataset publik Citi Bike tersedia untuk tahun 2013-2018. Walaupun demikian, tidak seluruh tahun trip memiliki data di tiap bulan, sehingga untuk analisis ini penulis akan menggunakan data Januari 2014 - September 2016. Terdapat total 28 juta baris data di rentang tersebut, sehingga untuk keperluan proyek ini akan dilakukan random sampling untuk mendapatkan subset 50 ribu baris data.

Kolom yang tersedia adalah sebagai berikut.

1. tripduration: durasi tiap perjalanan dalam detik
2. starttime: waktu perjalanan dimulai
3. stoptime: waktu perjalanan diakhiri
4. start_station_id: ID stasiun awal
5. start_station_name: nama stasiun awal
6. start_station_latitude: latitude dari stasiun awal
7. start_station_longitude: longitude dari stasiun awal
8. end_station_id: ID stasiun akhir
9. end_station_name: nama stasiun akhir
10. end_station_latitude: latitude dari stasiun akhir
11. end_station_longitude: longitude dari stasiun akhir
12. bikeid: ID bike
13. usertype: jenis pengguna
14. birth_year: tahun lahir pengguna
15. gender: jenis kelamin pengguna

## Data Preprocessing

### Anomali Durasi

Berdasarkan [info jenis layanan dan harganya](https://ride.citibikenyc.com/pricing), New York Citi Bike diperuntukkan bagi orang yang ingin melakukan perjalanan singkat untuk keperluan commuting, bukan perjalanan jauh. Durasi perjalanan maksimal paling besar terdapat di plan annual membership yaitu 45 menit. Terdapat tambahan biaya tiap kelebihan durasi pemakaian, dengan biaya paling rendah adalah \\$0.18 per menit.

Anomali durasi dapat dilihat dari persebaran data durasi (Gambar 1). Nilai maksimum durasi mencapai 96 ribu menit. Di sisi lain sepeda yang disediakan CitiBike bukanlah sepeda yang dirancang untuk perjalanan lama, sehingga selain alasan biaya terdapat alasan kenyamanan yang membuat pengguna condong menggunakan sepeda ini untuk perjalanan singkat. Anomali durasi yang sangat singkat, misalnya 1 menit ke bawah, mungkin terjadi di kasus sepeda rusak sehingga pengguna segera mengembalikan sepeda. Anomali ini juga dapat disingkirkan dengan mengecek perjalanan dengan durasi di bawah 1 menit sekaligus dimulai dan diakhiri di stasiun yang sama (`start_station_id = end_station_id`). 

<img src="/portfolio/static/nycitibike/Untitled.png" alt="Gambar 1: Persebaran durasi perjalanan" width="300"/>
<!-- ![Gambar 1: Persebaran durasi perjalanan](/portfolio/static/nycitibike/Untitled.png) -->

Gambar 1: Persebaran durasi perjalanan

Salah satu alasan orang menggunakan CitiBike adalah [bisa menghemat lebih banyak dibanding menggunakan subway](https://ride.citibikenyc.com/how-it-works). Oleh karena itu pemakaian CitiBike dengan durasi melebihi waktu default bukanlah pilihan yang paling ekonomis. Perjalanan yang menghabiskan uang hampir sebanyak [tiket mingguan subway, $29](https://newyorkpass.com/en-us/blog/public-transportation-new-york-city-new-york-metrocard), dapat dianggap sebagai anomali, misalnya karena kasus sepeda hilang atau lainnya. Di sini diambil asumsi penggunaan New York MetroCard weekly pass sejarang-jarangnya yaitu untuk 2 hari, yang berarti tiap trip memiliki biaya sebesar \\$29/2 hari atau \\$14.5 per trip. Plan paling murah yaitu annual membership mendekati harga tersebut ketika perjalanan mencapai 140 menit (\\$3 + 95*\\$0.12 = \\$14.4). Dengan memberikan margin error 30% dari 140 menit, didapat durasi ~180 menit yang akan dipakai sebagai cut-off penanda durasi anomali.

| Plan | Harga dasar | Durasi harga dasar | Harga untuk durasi tambahan | Durasi tiap ~$29/2 |
| --- | --- | --- | --- | --- |
| Annual membership | $3 | 45 menit | $0.12 per menit | 140 menit |
| Day pass | $15 | 30 menit | $4 per 15 menit | 30 menit |
| Single ride | $3.5 | 30 menit | $0.18 per menit | 91 menit |

Persebaran durasi perjalanan setelah anomali dihapus ditunjukkan dalam Gambar 2. Nilai persentil ke-95 hanya sedikit lebih besar dari durasi default, yaitu 33.25 menit. 

<img src="/portfolio/static/nycitibike/Untitled 1.png" alt="Gambar 2: Persebaran durasi perjalanan tanpa anomali" width="300"/>
<!-- ![Gambar 2: Persebaran durasi perjalanan tanpa anomali](/portfolio/static/nycitibike/Untitled 1.png) -->

Gambar 2: Persebaran durasi perjalanan tanpa anomali

## EDA

### Jarak perjalanan relatif meningkat

Tren jarak perjalanan relatif meningkat dalam periode tahun 2014-2016, yang mungkin disebabkan ditambahnya stasiun di berbagai titik di New York. Musim panas (area grafik hijau) memiliki rata-rata jarak tiap perjalanan yang paling tinggi dibanding musim lainnya (Gambar 3). Rata-rata jarak perjalanan di musim panas 2014, 2015, dan 2016 masing-masing adalah 1.72, 1.77, dan 1.87 km. Tren jarak perjalanan meningkat tiap tahunnya dapat disebabkan adanya perluasan area operasi Citi Bike dengan penambahan stasiun.

![Gambar 3: Jarak perjalanan. Highlight pink = musim semi, hijau = musim panas, oranye = musim gugur](/portfolio/static/nycitibike/Untitled 2.png)

Gambar 3: Jarak perjalanan. Highlight pink = musim semi, hijau = musim panas, oranye = musim gugur

Ekspansi layanan untuk menjangkau daerah yang lebih luas dapat dilihat pada Gambar 4 yang menunjukkan penambahan lokasi stasiun yang beroperasi pada 2014, 2015, dan 2016. Adanya stasiun yang tersebar secara luas memungkinkan pengguna berpindah ke stasiun yang lebih jauh, sehingga jarak perjalanannya pun menjadi lebih jauh.

<img src="/portfolio/static/nycitibike/Untitled%203.png" alt="Gambar 4: Stasiun yang beroperasi pada Januari 2014 - September 2016" width="500"/>

<!-- Gambar 4: Stasiun yang beroperasi pada Januari 2014 - September 2016 -->

### Jumlah perjalanan harian rata-rata meningkat

Secara umum, jumlah perjalanan harian meningkat pada periode 2014-2016 seperti yang ditunjukkan Gambar 5. Peningkatan ini mungkin berhubungan dengan penambahan stasiun yang dibahas di bagian sebelumnya. Jumlah perjalanan umumnya mengalami peningkatan konstan sejak musim dingin berakhir (Januari) dan mencapai puncaknya ketika memasuki awal musim gugur (minggu terakhir September) lalu kemudian menurun seiring dengan penurunan suhu. Jumlah perjalanan harian rata-rata paling tinggi tiap tahunnya terjadi pada transisi musim panas ke musim gugur. Jumlah perjalanan harian rata-rata di minggu pucak ini mengalami kenaikan tiap tahun dengan peningkatan pada 2015 sebesar 22.7% disusul peningkatan 33.9% pada 2016.

![Gambar 5: Rata-rata perjalanan harian](/portfolio/static/nycitibike/Untitled%204.png)

Gambar 5: Rata-rata perjalanan harian

Terdapat dua jenis pengguna CitiBike, yaitu Subscriber dan General Customer. Subscriber adalah pengguna annual membership sedangkan General Customer adalah pengguna dengan tarif Single Ride atau Day Pass. Sebanyak 88.31% pengguna adalah tipe "Subscriber" (Gambar 6). 

<img src="/portfolio/static/nycitibike/Untitled%205.png" alt="Gambar 6: Proporsi pengguna Citi Bike" width="400"/>

Gambar 6: Proporsi pengguna Citi Bike

Tren peningkatan jumlah perjalanan harian rata-rata di minggu puncak tiap tahun ditemukan pada kedua jenis pengguna. Peningkatan per tahun yang besar ditemukan pada tipe pengguna General Customer sebesar 55.3% pada 2015 diikuti tipe pengguna Subscriber sebesar 38.9% pada 2016 (Gambar 7). Peningkatan jumlah tipe pengguna Subscriber mungkin disebabkan **ekspansi layanan CitiBike yang meningkatkan minat warga New York untuk mendaftar annual membership.**

![Gambar 7: Jumlah perjalanan harian rata-rata berdasarkan jenis pengguna](/portfolio/static/nycitibike/Untitled%206.png)

Gambar 7: Jumlah perjalanan harian rata-rata berdasarkan jenis pengguna

### Durasi perjalanan cenderung konstan

Selama periode 2014-2016 durasi perjalanan cenderung konstan untuk kedua tipe pengguna. Durasi perjalanan cenderung konstan terutama bagi tipe Subscriber karena kelompok ini menggunakan CitiBike untuk keperluan yang bersifat rutin seperti commuting sehari-hari dari dan ke tempat kerja, atau dari satu daerah ke daerah lainnya. Pada tipe Customer ditemukan durasi yang lebih bervariasi walau cenderung berkisar di 25 menit (Gambar 8). Durasi maksimal pemakaian bagi pengguna Subscriber dengan plan Annual Membership yaitu 45 menit, lebih panjang dibanding General Customer dengan plan Day Pass atau Single Ride yang hanya 30 menit. Walaupun demikian, tipe General Customer secara konsisten memiliki durasi perjalanan yang lebih lama dibanding Subscriber. Hal ini menunjukkan tipe General Customer menggunakan CitiBike untuk kegiatan santai alih-alih rutinitas.

![Gambar 8: Rata-rata durasi perjalanan berdasarkan tipe pengguna](/portfolio/static/nycitibike/Untitled%207.png)

Gambar 8: Rata-rata durasi perjalanan berdasarkan tipe pengguna

Perbedaan pola penggunaan sepeda bagi tipe Subscriber dan General Customer juga dapat dilihat dari kecepatan bersepeda masing-masing kelompok (Gambar 9). Perlu diperhatikan bahwa jarak yang dipakai untuk menghitung kecepatan di sini adalah jarak terdekat antara stasiun awal dan akhir, bukan jarak yang sebenarnya ditempuh selama pengguna bersepeda, sehingga kecepatannya jauh lebih kecil dari kecepatan bersepeda dalam kota pada umumnya (19-26 km/h). General Customer memiliki kecepatan rata-rata di bawah Subscriber, menunjukkan penggunaan sepeda untuk kegiatan santai.

Jika CitiBike ingin **meningkatkan durasi perjalanan** pengguna, hal yang paling memungkinkan adalah **meningkatkan batas maksimal waktu sewa bagi pengguna General Customer** karena merekalah yang paling mungkin berlama-lama memakai sepeda. 

![Gambar 9: Kecepatan bersepeda berdasarkan tipe pengguna](/portfolio/static/nycitibike/Untitled%208.png)

Gambar 9: Kecepatan bersepeda berdasarkan tipe pengguna

## Visualisasi

Tableau link: [https://public.tableau.com/app/profile/azukacchi/viz/NYCitiBike_16649331133530/Story1?publish=yes](https://public.tableau.com/app/profile/azukacchi/viz/NYCitiBike_16649331133530/Story1?publish=yes)

![](/portfolio/static/nycitibike/Untitled%209.png)

![](/portfolio/static/nycitibike/Untitled%2010.png)

![](/portfolio/static/nycitibike/Untitled%2011.png)

## Referensi

1. Sobolevsky, Stanislav & Levitskaya, Ekaterina & Chan, Henry & Postle, Marc & Kontokosta, Constantine. (2018). Impact Of Bike Sharing In New York City.
2. [https://ride.citibikenyc.com/](https://ride.citibikenyc.com/pricing)
3. [https://newyorkpass.com/en-us/blog/public-transportation-new-york-city-new-york-metrocard](https://newyorkpass.com/en-us/blog/public-transportation-new-york-city-new-york-metrocard)