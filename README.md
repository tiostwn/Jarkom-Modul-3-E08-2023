# Jarkom-Modul-3-E08-2023
Laporan Resmi Praktimum 3 JARKOM

**Anggota Kelompok ``E08``** 
| No | Nama | NRP |
| --- | --- | --- |
| 1 | Samuel Berkat Hulu | 5025201055 |
| 2 | Hanafi Satriyo Utomo Setiawan | 5025211195 |


## Soal 1
Semua CLIENT harus menggunakan konfigurasi dari DHCP Server.
## Penyelesaian Soal 1
```R
    code.....
```


## Soal 2
Client yang melalui Switch3 mendapatkan range IP dari ``192.210.3.16 - 192.210.3.32`` dan ``192.210.3.64 - 192.210.3.80``.
## Penyelesaian Soal 2
```R
    code.....
```


## Soal 3
Client yang melalui Switch4 mendapatkan range IP dari ``191.210.4.12 - 192.210.4.20`` dan ``192.210.4.160 - 192.210.4.168``.
## Penyelesaian Soal 3
```R
    code.....
```


## Soal 4
Client mendapatkan DNS dari Heiter dan dapat terhubung dengan internet melalui DNS tersebut.
## Penyelesaian Soal 4
```R
    code.....
```


## Soal 5
Lama waktu DHCP server meminjamkan alamat IP kepada Client yang melalui Switch3 selama 3 menit sedangkan pada client yang melalui Switch4 selama 12 menit. Dengan waktu maksimal dialokasikan untuk peminjaman alamat IP selama 96 menit.
## Penyelesaian Soal 5
```R
    code.....
```



## Soal 6
Pada masing-masing worker PHP, lakukan konfigurasi virtual host untuk website [`berikut`](https://drive.google.com/file/d/1ViSkRq7SmwZgdK64eRbr5Fm1EGCTPrU1/view) dengan menggunakan php 7.3.
## Penyelesaian Soal 6
```R
    code.....
```



## Soal 7
Kepala suku dari Bredt Region memberikan resource server sebagai berikut:
a. Lawine, 4GB, 2vCPU, dan 80 GB SSD.
b. Linie, 2GB, 2vCPU, dan 50 GB SSD.
c. Lugner 1GB, 1vCPU, dan 25 GB SSD.
aturlah agar Eisen dapat bekerja dengan maksimal, lalu lakukan testing dengan 1000 request dan 100 request/second.

## Penyelesaian Soal 7
```R
    code.....
```



## Soal 8
Karena diminta untuk menuliskan grimoire, buatlah analisis hasil testing dengan 200 request dan 10 request/second masing-masing algoritma Load Balancer dengan ketentuan sebagai berikut:
a. Nama Algoritma Load Balancer.
b. Report hasil testing pada Apache Benchmark.
c. Grafik request per second untuk masing masing algoritma. 
d. Analisis. 

## Penyelesaian Soal 8
```R
    code.....
```



## Soal 9
Dengan menggunakan algoritma Round Robin, lakukan testing dengan menggunakan 3 worker, 2 worker, dan 1 worker sebanyak 100 request dengan 10 request/second, kemudian tambahkan grafiknya pada grimoire. 
## Penyelesaian Soal 9
```R
    code.....
```


## Soal 10
Selanjutnya coba tambahkan konfigurasi autentikasi di LB dengan dengan kombinasi ``username: “netics”`` dan ``password: “ajkyyy”``, dengan ``yyy`` merupakan kode kelompok. Terakhir simpan file ``“htpasswd”`` nya di ``/etc/nginx/rahasisakita/`` 
## Penyelesaian Soal 10
```R
    code.....
```



## Soal 11
Lalu buat untuk setiap request yang mengandung ``/its`` akan di proxy passing menuju halaman [`https://www.its.ac.id.`](https://www.its.ac.id/) hint: (proxy_pass)

## Penyelesaian Soal 11
```R
    code.....
```




## Soal 12
Selanjutnya LB ini hanya boleh diakses oleh client dengan IP ``192.210.3.69``, ``192.210.3.70``, ``192.210.4.167``, dan ``192.210.4.168``. hint: (fixed in dulu clinetnya)
## Penyelesaian Soal 12
```R
    code.....
```



## Soal 13
Semua data yang diperlukan, diatur pada Denken dan harus dapat diakses oleh ``Frieren``, ``Flamme``, dan ``Fern``.
## Penyelesaian Soal 13
```R
    code.....
```



## Soal 14
``Frieren``, ``Flamme``, dan ``Fern`` memiliki Riegel Channel sesuai dengan [`quest guide`](https://github.com/martuafernando/laravel-praktikum-jarkom) berikut. Jangan lupa melakukan instalasi PHP8.0 dan Composer.
## Penyelesaian Soal 14
```R
    code.....
```



## Soal 15
Riegel Channel memiliki beberapa endpoint yang harus ditesting sebanyak 100 request dengan 10 request/second. Tambahkan response dan hasil testing pada grimoire.
a. POST /auth/register 
## Penyelesaian Soal 15
```R
    code.....
```



## Soal 16
Riegel Channel memiliki beberapa endpoint yang harus ditesting sebanyak 100 request dengan 10 request/second. Tambahkan response dan hasil testing pada grimoire.
b. POST /auth/login (Lanjutan soal 15)
## Penyelesaian Soal 16
```R
    code.....
```



## Soal 17
Riegel Channel memiliki beberapa endpoint yang harus ditesting sebanyak 100 request dengan 10 request/second. Tambahkan response dan hasil testing pada grimoire.
c. GET /me (Lanjutan soal 15)
## Penyelesaian Soal 17
```R
    code.....
```



## Soal 18
Untuk memastikan ketiganya bekerja sama secara adil untuk mengatur Riegel Channel maka implementasikan Proxy Bind pada Eisen untuk mengaitkan IP dari ``Frieren``, ``Flamme``, dan ``Fern``.
## Penyelesaian Soal 18
```R
    code.....
```



## Soal 19
Untuk meningkatkan performa dari Worker, coba implementasikan PHP-FPM pada Frieren, Flamme, dan Fern. Untuk testing kinerja naikkan 
- pm.max_children
- pm.start_servers
- pm.min_spare_servers
- pm.max_spare_servers
sebanyak tiga percobaan dan lakukan testing sebanyak 100 request dengan 10 request/second kemudian berikan hasil analisisnya pada Grimoire.
## Penyelesaian Soal 19
```R
    code.....
```



## Soal 20
Nampaknya hanya menggunakan PHP-FPM tidak cukup untuk meningkatkan performa dari worker maka implementasikan Least-Conn pada Eisen. Untuk testing kinerja dari worker tersebut dilakukan sebanyak 100 request dengan 10 request/second
## Penyelesaian Soal 20
```R
    code.....
```

