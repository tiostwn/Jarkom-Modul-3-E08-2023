# Jarkom-Modul-3-E08-2023
Laporan Resmi Praktimum 3 JARKOM

**Anggota Kelompok ``E08``** 
| No | Nama | NRP |
| --- | --- | --- |
| 1 | Samuel Berkat Hulu | 5025201055 |
| 2 | Hanafi Satriyo Utomo Setiawan | 5025211195 |

## link : 
- [Soal 0](#soal0)
- [Soal 1](#soal1)
- [Soal 2](#soal2)
- [Soal 3](#soal3)
- [Soal 4](#soal4)
- [Soal 5](#soal5)
- [Soal 6](#soal6)
- [Soal 7](#soal7)
- [Soal 8](#soal8)
- [Soal 9](#soal9)
- [Soal 10](#soal10)
- [Soal 11](#soal11)
- [Soal 12](#soal12)
- [Soal 13](#soal13)
- [Soal 14](#soal14)
- [Soal 15](#soal15)
- [Soal 16](#soal16)
- [Soal 17](#soal17)
- [Soal 18](#soal18)
- [Soal 19](#soal19)
- [Soal 20](#soal20)

<a id="soal0"></a>
## Soal 0
Setelah mengalahkan Demon King, perjalanan berlanjut. Kali ini, kalian diminta untuk melakukan register domain berupa **riegel.canyon.yyy.com** untuk worker Laravel dan **granz.channel.yyy.com** untuk worker PHP (0) mengarah pada worker yang memiliki IP [prefix IP].x.1.

## Penyelesaian Soal 1
Jalankan script di DNS Server
```R
echo 'zone "riegel.canyon.e08.com" {
    type master;
    file "/etc/bind/sites/riegel.canyon.e08.com";
};

zone "granz.channel.e08.com" {
    type master;
    file "/etc/bind/sites/granz.channel.e08.com";
};

zone "1.210.192.in-addr.arpa" {
    type master;
    file "/etc/bind/sites/1.210.192.in-addr.arpa";
};' > /etc/bind/named.conf.local

mkdir -p /etc/bind/sites
cp /etc/bind/db.local /etc/bind/sites/riegel.canyon.e08.com
cp /etc/bind/db.local /etc/bind/sites/granz.channel.e08.com
cp /etc/bind/db.local /etc/bind/sites/1.210.192.in-addr.arpa

echo ';
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     riegel.canyon.e08.com. root.riegel.canyon.e08.com. (
                        2023111401      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      riegel.canyon.e08.com.
@       IN      A       192.210.4.1     ; IP Frieren
www     IN      CNAME   riegel.canyon.e08.com.' > /etc/bind/sites/riegel.canyon.e08.com

echo '
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     granz.channel.e08.com. root.granz.channel.e08.com. (
                        2023111401      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      granz.channel.e08.com.
@       IN      A       192.210.3.1     ; IP Lawine
www     IN      CNAME   granz.channel.e08.com.' > /etc/bind/sites/granz.channel.e08.com

echo 'options {
      directory "/var/cache/bind";

      forwarders {
              192.168.122.1;
      };

      // dnssec-validation auto;
      allow-query{any;};
      auth-nxdomain no;    # conform to RFC1035
      listen-on-v6 { any; };
}; ' >/etc/bind/named.conf.options

service bind9 start
```

Client (Masih Static)
```R
#!/bin/bash
echo 'nameserver 192.210.1.2    # IP Heiter' >  /etc/resolv.conf

ping riegel.canyon.e08.com -c 5
ping granz.channel.e08.com -c 5
```


<a id="soal1"></a>
## Soal 1
Semua CLIENT harus menggunakan konfigurasi dari DHCP Server.
## Penyelesaian Soal 1

ganti Network Configuration client menjadi berikut
```R
auto eth0
iface eth0 inet dhcp
```

<a id="soal2"></a>
## Soal 2
Client yang melalui Switch3 mendapatkan range IP dari ``192.210.3.16 - 192.210.3.32`` dan ``192.210.3.64 - 192.210.3.80``.
## Penyelesaian Soal 2
ubah `/etc/dhcp/dhcpd.conf` dan `/etc/default/isc-dhcp-server` seperti berikut
```R
apt-get update
apt-get install isc-dhcp-server

echo 'INTERFACES="eth0"' > /etc/default/isc-dhcp-server

echo '
#}
# START_DHCP_CONFIG

subnet 192.210.1.0 netmask 255.255.255.0 {
}

subnet 192.210.3.0 netmask 255.255.255.0 {
    range 192.210.3.16 192.210.3.32;
    range 192.210.3.64 192.210.3.80;
    option routers 192.210.3.0;
    option broadcast-address 192.210.3.255;
    option domain-name-servers 192.210.1.2;
    default-lease-time 180;
    max-lease-time 5760;
}' > /etc/dhcp/dhcpd.conf

service isc-dhcp-server restart
```

<a id="soal3"></a>
## Soal 3
Client yang melalui Switch4 mendapatkan range IP dari ``191.210.4.12 - 192.210.4.20`` dan ``192.210.4.160 - 192.210.4.168``.
## Penyelesaian Soal 3
ubah `/etc/dhcp/dhcpd.conf` dan `/etc/default/isc-dhcp-server` seperti berikut
```R
apt-get update
apt-get install isc-dhcp-server

echo 'INTERFACES="eth0"' > /etc/default/isc-dhcp-server

echo '
#}
# START_DHCP_CONFIG

subnet 192.210.1.0 netmask 255.255.255.0 {
}

subnet 192.210.3.0 netmask 255.255.255.0 {
    range 192.210.3.16 192.210.3.32;
    range 192.210.3.64 192.210.3.80;
    option routers 192.210.3.0;
    option broadcast-address 192.210.3.255;
    option domain-name-servers 192.210.1.2;
    default-lease-time 180;
    max-lease-time 5760;
}

subnet 192.210.4.0 netmask 255.255.255.0 {
    range 192.210.4.12 192.210.4.20;
    range 192.210.4.160 192.210.4.168;
    option routers 192.210.4.0;
    option broadcast-address 192.210.4.255;
    option domain-name-servers 192.210.1.2;
    default-lease-time 720;
    max-lease-time 5760;
}' > /etc/dhcp/dhcpd.conf

service isc-dhcp-server restart
```

<a id="soal4"></a>
## Soal 4
Client mendapatkan DNS dari Heiter dan dapat terhubung dengan internet melalui DNS tersebut.
## Penyelesaian Soal 4
Jalankan script berikut pada **Aura (DHCP Relay)**
```R
apt-get update
apt-get install isc-dhcp-relay -y
service isc-dhcp-relay start

echo 'SERVERS="192.210.1.1"  
INTERFACES="eth1 eth3 eth4"
OPTIONS=' > /etc/default/isc-dhcp-relay

echo 'net.ipv4.ip_forward=1' > /etc/sysctl.conf

service isc-dhcp-relay restart
```

stop dan start node client, otomatis client mendapatkan DNS dari heiter

![no5 - IP](https://github.com/tiostwn/Jarkom-Modul-3-E08-2023/assets/53292102/e06ad6e6-9d34-43bc-8ee2-8076d0884412)
![no5 - test ping](https://github.com/tiostwn/Jarkom-Modul-3-E08-2023/assets/53292102/26895071-9172-4456-9e2e-918565519cbf)



<a id="soal5"></a>
## Soal 5
Lama waktu DHCP server meminjamkan alamat IP kepada Client yang melalui Switch3 selama 3 menit sedangkan pada client yang melalui Switch4 selama 12 menit. Dengan waktu maksimal dialokasikan untuk peminjaman alamat IP selama 96 menit.
## Penyelesaian Soal 5
```R
echo '
#}
# START_DHCP_CONFIG

subnet 192.210.1.0 netmask 255.255.255.0 {
}

subnet 192.210.3.0 netmask 255.255.255.0 {
    ...
    default-lease-time 180;
    max-lease-time 5760;
    ...
}

subnet 192.210.4.0 netmask 255.255.255.0 {
    ...
    default-lease-time 720;
    max-lease-time 5760;
    ...
}' > /etc/dhcp/dhcpd.conf

service isc-dhcp-server restart
```


<a id="soal6"></a>
## Soal 6
Pada masing-masing worker PHP, lakukan konfigurasi virtual host untuk website [`berikut`](https://drive.google.com/file/d/1ViSkRq7SmwZgdK64eRbr5Fm1EGCTPrU1/view) dengan menggunakan php 7.3.
## Penyelesaian Soal 6

Masukkan script berikut pada .bashrc di Eisen (load Balancer)
```R
#.bashrc
echo 'nameserver 192.210.1.2' > /etc/resolv.conf
apt-get update
apt-get install apache2-utils -y
apt-get install nginx -y
apt-get install lynx -y

service nginx start
```

Setelah semua yang dibutuhkan terinstall, jalankan script berikut di Eisesn (Load Balancer)
```R
apt-get update
apt-get install bind9 nginx

echo '
 upstream myweb  {
        server 192.210.3.1; #IP Lawine
        server 192.210.3.2; #IP Linie
        server 192.210.3.3; #IP Lugner
 }

 server {
        listen 80;
        server_name granz.channel.e08.com;

        location / {
        proxy_pass http://myweb;
        }
 }' > /etc/nginx/sites-available/lb-jarkom

ln -s /etc/nginx/sites-available/lb-jarkom /etc/nginx/sites-enabled
rm -rf /etc/nginx/sites-enabled/default

service nginx restart
nginx -t
```

Masukkan script berikut pada .bashrc di Worker PHP (Lugner, Linie, Lawine)
```R
echo 'nameserver 192.210.1.2' > /etc/resolv.conf
apt-get update
apt-get install nginx -y
apt-get install wget -y
apt-get install unzip -y
apt-get install lynx -y
apt-get install htop -y
apt-get install apache2-utils -y
apt-get install php7.3-fpm php7.3-common php7.3-mysql php7.3-gmp php7.3-curl php7.3-intl php7.3-mbstring php7.3-xmlrpc php7.3-gd php7.3-xml php7.3-cli php7.3-zip -y

service nginx start
service php7.3-fpm start
```

Jalankan script berikut di Worker PHP (Lugner, Linie, Lawine)
```R
mkdir -p /var/www/granz.channel.e08

wget --no-check-certificate 'https://drive.google.com/uc?export=download&id=1ViSkRq7SmwZgdK64eRbr5Fm1EGCTPrU1' -O /var/www/granz.channel.e08.zip
unzip /var/www/granz.channel.e08.zip -d /var/www/granz.channel.e08
mv /var/www/granz.channel.e08/modul-3 /var/www/granz.channel.e08
rm -rf /var/www/granz.channel.e08.zip

echo '
server {

        listen 80;

        root /var/www/granz.channel.e08;

        index index.php index.html index.htm;
        server_name _;

        location / {
                        try_files $uri $uri/ /index.php?$query_string;
        }

        # pass PHP scripts to FastCGI server
        location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php7.3-fpm.sock;
        }

location ~ /\.ht {
                        deny all;
        }

        error_log /var/log/nginx/jarkom_error.log;
        access_log /var/log/nginx/jarkom_access.log;
 }' > /etc/nginx/sites-available/granz.channel.e08

echo '<!DOCTYPE html>
<html>
<head>
    <title>Granz Channel Map</title>
    <link rel="stylesheet" type="text/css" href="css/styles.css">
</head>
<body>
    <div class="container">
        <h1>Welcome to Granz Channel</h1>
        <p><?php
            $hostname = gethostname();
            echo "Request ini dihandle oleh: $hostname<br>"; ?> </p>
        <p>Enter your name to validate:</p>
        <form method="POST" action="index.php">
            <input type="text" name="name" id="nameInput">
            <button type="submit" id="submitButton">Submit</button>
        </form>
        <p id="greeting"><?php
            if(isset($_POST['name'])) {
                $name = $_POST['name'];
                echo "Hello, $name!";
            }
        ?></p>
    </div>

    <script src="js/script.js"></script>
</body>' > /var/www/granz.channel.e08/index.php

ln -s /etc/nginx/sites-available/granz.channel.e08 /etc/nginx/sites-enabled
rm -rf /etc/nginx/sites-enabled/default

service php7.3-fpm start
service php7.3-fpm restart
service nginx restart
nginx -t
```

Hasil `lynx granz.channel.e08.com` dari client
![no6 - Lawine](https://github.com/tiostwn/Jarkom-Modul-3-E08-2023/assets/53292102/40db429a-da37-4337-9157-ecc14ff5361b)
![no6 - Linie](https://github.com/tiostwn/Jarkom-Modul-3-E08-2023/assets/53292102/e4ce1e08-5255-46ee-8b0c-bf4a0c6272c5)
![no6 - Lugner](https://github.com/tiostwn/Jarkom-Modul-3-E08-2023/assets/53292102/878dcfd8-9890-4d4a-8d19-e5c1e6eb2630)


<a id="soal7"></a>
## Soal 7
Kepala suku dari Bredt Region memberikan resource server sebagai berikut:
a. Lawine, 4GB, 2vCPU, dan 80 GB SSD.
b. Linie, 2GB, 2vCPU, dan 50 GB SSD.
c. Lugner 1GB, 1vCPU, dan 25 GB SSD.
aturlah agar Eisen dapat bekerja dengan maksimal, lalu lakukan testing dengan 1000 request dan 100 request/second.

## Penyelesaian Soal 7
```R
ab -n 1000 -c 100 http://www.granz.channel.e08.com/ 
```

![no7 - AB](https://github.com/tiostwn/Jarkom-Modul-3-E08-2023/assets/53292102/215a8c4a-173c-425e-9822-1351b733143b)

Hasil `htop` pada setiap worker
![no7](https://github.com/tiostwn/Jarkom-Modul-3-E08-2023/assets/53292102/be8b525a-91ff-4f13-bfe2-19d2ec265442)
![no7 - req](https://github.com/tiostwn/Jarkom-Modul-3-E08-2023/assets/53292102/54149225-e429-4eb4-9db3-8a59c654c665)

<a id="soal8"></a>
## Soal 8
Karena diminta untuk menuliskan grimoire, buatlah analisis hasil testing dengan 200 request dan 10 request/second masing-masing algoritma Load Balancer dengan ketentuan sebagai berikut:
a. Nama Algoritma Load Balancer.
b. Report hasil testing pada Apache Benchmark.
c. Grafik request per second untuk masing masing algoritma. 
d. Analisis. 

## Penyelesaian Soal 8
Link Griomire -> https://docs.google.com/document/d/1ycT2eMasmnmWuV7xShepgMv7LoVVgGvD3gX82sGTbYQ/edit?usp=sharing

Jalankan script ini untuk menjalankan Apache Benchmark
```R
ab -n 200 -c 10 http://www.granz.channel.e08.com/ 
```

### Round Robin
```R
apt-get update
apt-get install bind9 nginx

echo '
 upstream myweb  {
        server 192.210.3.1; #IP Lawine
        server 192.210.3.2; #IP Linie
        server 192.210.3.3; #IP Lugner
 }

 server {
        listen 80;
        server_name granz.channel.e08.com;

        location / {
        proxy_pass http://myweb;
        }
 }' > /etc/nginx/sites-available/lb-jarkom

ln -s /etc/nginx/sites-available/lb-jarkom /etc/nginx/sites-enabled
rm -rf /etc/nginx/sites-enabled/default

service nginx restart
nginx -t
```

#### Hasil `Apache Benchmark` dan `htop` Round Robin 
![no8 - 1 RR AB](https://github.com/tiostwn/Jarkom-Modul-3-E08-2023/assets/53292102/3f64f5aa-09c6-40cb-8b68-b0eaab2c9756)
![no8 - 1 RR htop](https://github.com/tiostwn/Jarkom-Modul-3-E08-2023/assets/53292102/28c05a3a-97e5-4a27-81ae-6736cffaefe5)
![no8 - 1 RR req](https://github.com/tiostwn/Jarkom-Modul-3-E08-2023/assets/53292102/3441da8c-53f3-4617-8c99-0b95cfa1ee09)


### Weighted Round Robin
```R
echo '
 upstream myweb  {
        server 192.210.3.1 weight=4; #IP Lawine
        server 192.210.3.2 weight=2; #IP Linie
        server 192.210.3.3 weight=1; #IP Lugner
 }

 server {
        listen 80;
        server_name granz.channel.e08.com;

        location / {
              proxy_pass http://myweb;
              proxy_set_header    X-Real-IP $remote_addr;
              proxy_set_header    X-Forwarded-For $proxy_add_x_forwarded_for;
              proxy_set_header    Host $http_host;
        }
 }' > /etc/nginx/sites-available/lb-jarkom

unlink /etc/nginx/sites-enabled/lb-jarkom
ln -s /etc/nginx/sites-available/lb-jarkom /etc/nginx/sites-enabled
rm -rf /etc/nginx/sites-enabled/default

service nginx restart
nginx -t
```

#### Hasil `Apache Benchmark` dan `htop` Weighted Round Robin 
![no8 - 2 WRR AB](https://github.com/tiostwn/Jarkom-Modul-3-E08-2023/assets/53292102/2c0601ba-b0d4-483f-a2c8-ec124de67f61)
![no8 - 2 WRR htop](https://github.com/tiostwn/Jarkom-Modul-3-E08-2023/assets/53292102/3f45d18f-0cd1-48ff-83fd-c67e47a0cdef)
![no8 - 2 WRR req](https://github.com/tiostwn/Jarkom-Modul-3-E08-2023/assets/53292102/39c45516-9250-4fe3-8b81-f1653f9105b1)

### Least Connection
```R
echo '
 upstream myweb  {
        least_conn;
        server 192.210.3.1; #IP Lawine
        server 192.210.3.2; #IP Linie
        server 192.210.3.3; #IP Lugner
 }

 server {
        listen 80;
        server_name granz.channel.e08.com;

        location / {
              proxy_pass http://myweb;
              proxy_set_header    X-Real-IP $remote_addr;
              proxy_set_header    X-Forwarded-For $proxy_add_x_forwarded_for;
              proxy_set_header    Host $http_host;
        }
 }' > /etc/nginx/sites-available/lb-jarkom

unlink /etc/nginx/sites-enabled/lb-jarkom
ln -s /etc/nginx/sites-available/lb-jarkom /etc/nginx/sites-enabled
rm -rf /etc/nginx/sites-enabled/default

service nginx restart
nginx -t
```

#### Hasil `Apache Benchmark` dan `htop` Least Connection
![no8 - 3 leastCon AB](https://github.com/tiostwn/Jarkom-Modul-3-E08-2023/assets/53292102/a5734256-a2ea-4615-a6f9-5ff3da4735b8)
![no8 - 3 leastCon req](https://github.com/tiostwn/Jarkom-Modul-3-E08-2023/assets/53292102/a7263322-1311-49ce-9e17-247ab004e621)
![no8 - 3 leastCon htop](https://github.com/tiostwn/Jarkom-Modul-3-E08-2023/assets/53292102/f1668557-896e-43d1-a3f6-81ecd3481a2d)


### Ip Hash
```R
echo '
 upstream myweb  {
        ip_hash;
        server 192.210.3.1; #IP Lawine
        server 192.210.3.2; #IP Linie
        server 192.210.3.3; #IP Lugner
 }

 server {
        listen 80;
        server_name granz.channel.e08.com;

        location / {
              proxy_pass http://myweb;
              proxy_set_header    X-Real-IP $remote_addr;
              proxy_set_header    X-Forwarded-For $proxy_add_x_forwarded_for;
              proxy_set_header    Host $http_host;
        }
 }' > /etc/nginx/sites-available/lb-jarkom

unlink /etc/nginx/sites-enabled/lb-jarkom
ln -s /etc/nginx/sites-available/lb-jarkom /etc/nginx/sites-enabled
rm -rf /etc/nginx/sites-enabled/default

service nginx restart
nginx -t
```

#### Hasil `Apache Benchmark` dan `htop` IP Hash
![no8 - 4 ipHash AB](https://github.com/tiostwn/Jarkom-Modul-3-E08-2023/assets/53292102/49647c7a-77cb-45af-b9b2-8675be5737ac)
![no8 - 4 ipHash htop](https://github.com/tiostwn/Jarkom-Modul-3-E08-2023/assets/53292102/2376f06f-6263-4879-ac15-20214d492d54)
![no8 - 4 ipHash req](https://github.com/tiostwn/Jarkom-Modul-3-E08-2023/assets/53292102/e3123aaf-5f4e-4fd2-a87f-37aced388d54)

### Generic Hash
```R
echo '
 upstream myweb  {
        hash $request_uri consistent;
        server 192.210.3.1; #IP Lawine
        server 192.210.3.2; #IP Linie
        server 192.210.3.3; #IP Lugner
 }

 server {
        listen 80;
        server_name granz.channel.e08.com;

        location / {
              proxy_pass http://myweb;
              proxy_set_header    X-Real-IP $remote_addr;
              proxy_set_header    X-Forwarded-For $proxy_add_x_forwarded_for;
              proxy_set_header    Host $http_host;
        }
 }' > /etc/nginx/sites-available/lb-jarkom

unlink /etc/nginx/sites-enabled/lb-jarkom
ln -s /etc/nginx/sites-available/lb-jarkom /etc/nginx/sites-enabled
rm -rf /etc/nginx/sites-enabled/default

service nginx restart
nginx -t
```

#### Hasil `Apache Benchmark` dan `htop` Generic Hash
![no8 - 5 genericHash AB](https://github.com/tiostwn/Jarkom-Modul-3-E08-2023/assets/53292102/7126d00b-bbbd-4521-beb9-94864a57c487)
![no8 - 5 genericHash htop](https://github.com/tiostwn/Jarkom-Modul-3-E08-2023/assets/53292102/ca49b4bf-8645-4ad5-aea0-7e831012317b)
![no8 - 5 genericHash req](https://github.com/tiostwn/Jarkom-Modul-3-E08-2023/assets/53292102/ed66291f-2883-44a1-9ebf-456f53f47d77)


<img width="654" alt="image" src="https://github.com/tiostwn/Jarkom-Modul-3-E08-2023/assets/53292102/02ee4c0f-9d70-43db-92e4-ee7f8a3c1d3c">

<a id="soal9"></a>
## Soal 9
Dengan menggunakan algoritma Round Robin, lakukan testing dengan menggunakan 3 worker, 2 worker, dan 1 worker sebanyak 100 request dengan 10 request/second, kemudian tambahkan grafiknya pada grimoire.


## Penyelesaian Soal 9
```R
ab -n 100 -c 10 http://www.granz.channel.e08.com/ 
```

matikan nginx pada worker dengan cara `service nginx stop`

### 3 Worker
![no9 - 3 worker AB](https://github.com/tiostwn/Jarkom-Modul-3-E08-2023/assets/53292102/9b14a8ed-69de-46e2-9cec-7132d36d8eef)
![no9 - 3 worker htop](https://github.com/tiostwn/Jarkom-Modul-3-E08-2023/assets/53292102/6a368703-b7b1-4f8f-96f4-77b351740297)
![no9 - 3 worker req](https://github.com/tiostwn/Jarkom-Modul-3-E08-2023/assets/53292102/a6583baa-097c-4a91-b293-32fb535d14f9)

### 2 Worker
![no9 - 2 worker AB](https://github.com/tiostwn/Jarkom-Modul-3-E08-2023/assets/53292102/201532fd-d5cb-42d3-b44b-cf85183f46a3)
![no9 - 2 worker htop](https://github.com/tiostwn/Jarkom-Modul-3-E08-2023/assets/53292102/d8e41d5a-cd20-4c91-8196-9a791f582a26)
![no9 - 2 worker req](https://github.com/tiostwn/Jarkom-Modul-3-E08-2023/assets/53292102/4f8fa68b-c714-4da2-bbf2-8a62ca935aa6)

### 1 Worker
![no9 - 1 worker AB](https://github.com/tiostwn/Jarkom-Modul-3-E08-2023/assets/53292102/e245e1a6-3429-4aae-ae13-7efebe2a34d0)
![no9 - 1 worker htop](https://github.com/tiostwn/Jarkom-Modul-3-E08-2023/assets/53292102/7f9be9ad-d4a9-4ba6-95ab-4ed6201d7aff)
![no9 - 1 worker req](https://github.com/tiostwn/Jarkom-Modul-3-E08-2023/assets/53292102/8f258516-0b35-4f95-931e-23d1ba852592)


<a id="soal10"></a>
## Soal 10
Selanjutnya coba tambahkan konfigurasi autentikasi di LB dengan dengan kombinasi ``username: “netics”`` dan ``password: “ajkyyy”``, dengan ``yyy`` merupakan kode kelompok. Terakhir simpan file ``“htpasswd”`` nya di ``/etc/nginx/rahasisakita/`` 

## Penyelesaian Soal 10
Jalankan script ini pada Eisen (Load Balancer)
```R
echo '
 upstream myweb  {
        server 192.210.3.1; #IP Lawine
        server 192.210.3.2; #IP Linie
        server 192.210.3.3; #IP Lugner
 }

 server {
        listen 80;
        server_name granz.channel.e08.com;

        location / {
        proxy_pass http://myweb;
        auth_basic "Restricted Access";
        auth_basic_user_file /etc/nginx/rahasisakita/.htpasswd;
        }
 }' > /etc/nginx/sites-available/lb-jarkom

unlink /etc/nginx/sites-enabled/lb-jarkom
ln -s /etc/nginx/sites-available/lb-jarkom /etc/nginx/sites-enabled
rm -rf /etc/nginx/sites-enabled/default

mkdir /etc/nginx/rahasisakita/
htpasswd -c -b /etc/nginx/rahasisakita/.htpasswd netics ajke08

service nginx restart
nginx -t
```

Jalankan `lynx granz.channel.e08.com` pada client
![no10](https://github.com/tiostwn/Jarkom-Modul-3-E08-2023/assets/53292102/665b4a98-9fdc-4b40-a7c2-c824be010cdb)
![no10 - a](https://github.com/tiostwn/Jarkom-Modul-3-E08-2023/assets/53292102/790582dc-6630-465a-8aaf-0f8707ced270)
![no10 - b](https://github.com/tiostwn/Jarkom-Modul-3-E08-2023/assets/53292102/22081c06-745d-4e41-be5e-dc160c77085d)

<a id="soal11"></a>
## Soal 11
Lalu buat untuk setiap request yang mengandung ``/its`` akan di proxy passing menuju halaman [`https://www.its.ac.id.`](https://www.its.ac.id/) hint: (proxy_pass)

## Penyelesaian Soal 11
Jalankan script ini pada Eisen (Load Balancer)
```R
echo '
 upstream myweb  {
        server 192.210.3.1; #IP Lawine
        server 192.210.3.2; #IP Linie
        server 192.210.3.3; #IP Lugner
 }

 server {
        listen 80;
        server_name granz.channel.e08.com;

        location / {
                proxy_pass http://myweb;
                auth_basic "Restricted Access";
                auth_basic_user_file /etc/nginx/rahasisakita/.htpasswd;
        }

        location ~* /its {
                proxy_pass https://www.its.ac.id;
        }

 }' > /etc/nginx/sites-available/lb-jarkom

unlink /etc/nginx/sites-enabled/lb-jarkom
ln -s /etc/nginx/sites-available/lb-jarkom /etc/nginx/sites-enabled
rm -rf /etc/nginx/sites-enabled/default

mkdir -p /etc/nginx/rahasisakita/
htpasswd -c -b /etc/nginx/rahasisakita/.htpasswd netics ajke08

service nginx restart
nginx -t
```

Jalankan `lynx granz.channel.e08.com` pada client
![no11](https://github.com/tiostwn/Jarkom-Modul-3-E08-2023/assets/53292102/b28e9d36-6215-425f-ab57-92948bd399ff)

<a id="soal12"></a>
## Soal 12
Selanjutnya LB ini hanya boleh diakses oleh client dengan IP ``192.210.3.69``, ``192.210.3.70``, ``192.210.4.167``, dan ``192.210.4.168``. hint: (fixed in dulu clinetnya)
## Penyelesaian Soal 12
```R
echo '
 upstream myweb  {
        server 192.210.3.1; #IP Lawine
        server 192.210.3.2; #IP Linie
        server 192.210.3.3; #IP Lugner
 }

 server {
        listen 80;
        server_name granz.channel.e08.com;

        location / {
                proxy_pass http://myweb;
                auth_basic "Restricted Access";
                auth_basic_user_file /etc/nginx/rahasisakita/.htpasswd;

                allow 192.210.3.69;
                allow 192.210.3.70;
                allow 192.210.4.167;
                allow 192.210.4.168;
                deny all;
        }

        location ~* /its {
                proxy_pass https://www.its.ac.id;
        }

 }' > /etc/nginx/sites-available/lb-jarkom

unlink /etc/nginx/sites-enabled/lb-jarkom
ln -s /etc/nginx/sites-available/lb-jarkom /etc/nginx/sites-enabled
rm -rf /etc/nginx/sites-enabled/default

mkdir -p /etc/nginx/rahasisakita/
htpasswd -c -b /etc/nginx/rahasisakita/.htpasswd netics ajke08

service nginx restart
nginx -t
```


<a id="soal13"></a>
## Soal 13
Semua data yang diperlukan, diatur pada Denken dan harus dapat diakses oleh ``Frieren``, ``Flamme``, dan ``Fern``.
## Penyelesaian Soal 13
```R
    code.....
```


<a id="soal14"></a>
## Soal 14
``Frieren``, ``Flamme``, dan ``Fern`` memiliki Riegel Channel sesuai dengan [`quest guide`](https://github.com/martuafernando/laravel-praktikum-jarkom) berikut. Jangan lupa melakukan instalasi PHP8.0 dan Composer.
## Penyelesaian Soal 14
```R
    code.....
```


<a id="soal15"></a>
## Soal 15
Riegel Channel memiliki beberapa endpoint yang harus ditesting sebanyak 100 request dengan 10 request/second. Tambahkan response dan hasil testing pada grimoire.
a. POST /auth/register 
## Penyelesaian Soal 15
```R
    code.....
```


<a id="soal16"></a>
## Soal 16
Riegel Channel memiliki beberapa endpoint yang harus ditesting sebanyak 100 request dengan 10 request/second. Tambahkan response dan hasil testing pada grimoire.
b. POST /auth/login (Lanjutan soal 15)
## Penyelesaian Soal 16
```R
    code.....
```


<a id="soal17"></a>
## Soal 17
Riegel Channel memiliki beberapa endpoint yang harus ditesting sebanyak 100 request dengan 10 request/second. Tambahkan response dan hasil testing pada grimoire.
c. GET /me (Lanjutan soal 15)
## Penyelesaian Soal 17
```R
    code.....
```


<a id="soal18"></a>
## Soal 18
Untuk memastikan ketiganya bekerja sama secara adil untuk mengatur Riegel Channel maka implementasikan Proxy Bind pada Eisen untuk mengaitkan IP dari ``Frieren``, ``Flamme``, dan ``Fern``.
## Penyelesaian Soal 18
```R
    code.....
```


<a id="soal19"></a>
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


<a id="soal20"></a>
## Soal 20
Nampaknya hanya menggunakan PHP-FPM tidak cukup untuk meningkatkan performa dari worker maka implementasikan Least-Conn pada Eisen. Untuk testing kinerja dari worker tersebut dilakukan sebanyak 100 request dengan 10 request/second
## Penyelesaian Soal 20
```R
    code.....
```

