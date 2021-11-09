# Jarkom-Modul-3-E05-2021

Nama Kelompok:
1. Muhammad Rafki Mardi 05111940000054
2. Hana Machmudah 05111940000072
3. Achmad Fadillah  05111940000155

![image](https://user-images.githubusercontent.com/66562311/140715335-a5fc5d3c-b829-4906-ba60-9418b1f63bc0.png)

## No. 1
### Luffy bersama Zoro berencana membuat peta tersebut dengan kriteria EniesLobby sebagai DNS Server, Jipangu sebagai DHCP Server, Water7 sebagai Proxy Server

## Jawaban
Membuat topologi sesuai gambar yang diatas. Dengan mengubah konfigurasi FOOSHA dan node lainnya seperti di bawah ini:
#### FOOSHA
```
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
	address 192.202.1.1
	netmask 255.255.255.0

auto eth2
iface eth2 inet static
	address 192.202.2.1
	netmask 255.255.255.0

auto eth3
iface eth3 inet static
	address 192.202.3.1
	netmask 255.255.255.0
```
#### Loguetown
```
auto eth0
iface eth0 inet static
	address 192.202.1.2
	netmask 255.255.255.0
	gateway 192.202.1.1
```
#### Alabasta
```
auto eth0
iface eth0 inet static
	address 192.202.1.3
	netmask 255.255.255.0
	gateway 192.202.1.1
```
#### EniesLoby
```
auto eth0
iface eth0 inet static
	address 192.202.2.2
	netmask 255.255.255.0
	gateway 192.202.2.1
```
#### Water7
```
auto eth0
iface eth0 inet static
	address 192.202.2.3
	netmask 255.255.255.0
	gateway 192.202.2.1
```
#### Jipangu
```
auto eth0
iface eth0 inet static
	address 192.202.2.4
	netmask 255.255.255.0
	gateway 192.202.2.1
```
#### Skypie
```
auto eth0
iface eth0 inet static
	address 192.202.3.2
	netmask 255.255.255.0
	gateway 192.202.3.1
```
#### TottoLand
```
auto eth0
iface eth0 inet static
	address 192.202.3.3
	netmask 255.255.255.0
	gateway 192.202.3.1
```
Melakukan koneksi ke internet untuk semua node. mengetik `iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 192.202.0.0/16` pada router FOOSHA.
Kemudian ketiikan command `echo nameserver 192.168.122.1 > /etc/resolv.conf` pada setiap ubuntu.
- EniesLoby sebagai DNS Server
	Mengupdate package list pada EniesLobby
	```
	apt-get update
	```
	Menginstal bind9 pada server EniesLobby
	```
	apt-get install bind9
	```
	Kemudian restart
	```
	service bind9 restart
	```
	Untuk mengecek bind9 berjalan, menggunakan perintah
	```
	service bind9 status
	```
	![image](https://user-images.githubusercontent.com/66562311/140881936-25b45340-5941-4196-8303-5e8bcc9dbc30.png)


- Jipangu sebagai DHCP Server
	Mengupdate package list pada Jipangu
	```
	apt-get update
	```
	Menginstal bind9 pada server Jipangu
	```
	apt-get install isc-dhcp-server
	```
	Kemudian restart
	```
	service isc-dhcp-server restart
	```
	Untuk mengecek isc-dhcp-server berjalan, menggunakan perintah
	```
	service isc-dhcp-server status
	```
	![image](https://user-images.githubusercontent.com/66562311/140882027-91a8ed19-d49e-4413-86c5-61a8984da4bd.png)


- Water7 sebagai Proxy Server
	Mengupdate package list pada Water7
	```
	apt-get update
	```
	Menginstal bind9 pada server Water7
	```
	apt-get install squid
	```
	Kemudian restart
	```
	service squid restart
	```
	Untuk mengecek squid berjalan, menggunakan perintah
	```
	service squid status
	```
	![image](https://user-images.githubusercontent.com/66562311/140882112-ce6a7c72-f73b-48ca-9f12-a4fb5c671c89.png)


## No. 2
### Foosha sebagai DHCP Relay

## Jawaban


## No. 3
### Luffy dan Zoro menyusun peta tersebut dengan hati-hati dan teliti. Ada beberapa kriteria yang ingin dibuat oleh Luffy dan Zoro, yaitu:
### - Semua client yang ada HARUS menggunakan konfigurasi IP dari DHCP Server.
### - Client yang melalui Switch1 mendapatkan range IP dari `[prefix IP].1.20` - `[prefix IP].1.99` dan `[prefix IP].1.150` - `[prefix IP].1.169`


## Jawaban


## No. 4
### Client yang melalui Switch3 mendapatkan range IP dari `[prefix IP].3.30` - `[prefix IP].3.50`

## Jawaban


## No. 5
### Client mendapatkan DNS dari EniesLobby dan client dapat terhubung dengan internet melalui DNS tersebut.

## Jawaban


## No. 6
### Lama waktu DHCP server meminjamkan alamat IP kepada Client yang melalui Switch1 selama 6 menit sedangkan pada client yang melalui Switch3 selama 12 menit. Dengan waktu maksimal yang dialokasikan untuk peminjaman alamat IP selama 120 menit.

## Jawaban


## No. 7
### Luffy dan Zoro berencana menjadikan Skypie sebagai server untuk jual beli kapal yang dimilikinya dengan alamat IP yang tetap dengan IP `[prefix IP].3.69`

## Jawaban


## No. 8
### Loguetown digunakan sebagai client Proxy agar transaksi jual beli dapat terjamin keamanannya, juga untuk mencegah kebocoran data transaksi. Pada Loguetown, proxy harus bisa diakses dengan nama `jualbelikapal.yyy.com` dengan port yang digunakan adalah 5000

## Jawaban


## No. 9
### Agar transaksi jual beli lebih aman dan pengguna website ada dua orang, proxy dipasang autentikasi user proxy dengan enkripsi MD5 dengan dua username, yaitu `luffybelikapalyyy` dengan password `luffy_yyy` dan `zorobelikapalyyy` dengan password `zoro_yyy`

## Jawaban


## No. 10
### Transaksi jual beli tidak dilakukan setiap hari, oleh karena itu akses internet dibatasi hanya dapat diakses setiap hari `Senin-Kamis pukul 07.00-11.00` dan setiap hari `Selasa-Jum’at pukul 17.00-03.00` keesokan harinya (sampai Sabtu pukul 03.00)

## Jawaban


## No. 11
### Agar transaksi bisa lebih fokus berjalan, maka dilakukan redirect website agar mudah mengingat website transaksi jual beli kapal. Setiap mengakses `google.com`, akan diredirect menuju `super.franky.yyy.com` dengan website yang sama pada soal shift modul 2. Web server super.franky.yyy.com berada pada node Skypie

## Jawaban


## No. 12
### Saatnya berlayar! Luffy dan Zoro akhirnya memutuskan untuk berlayar untuk mencari harta karun di `super.franky.yyy.com`. Tugas pencarian dibagi menjadi dua misi, Luffy bertugas untuk mendapatkan gambar `(.png, .jpg)`, sedangkan Zoro mendapatkan sisanya. Karena Luffy orangnya sangat teliti untuk mencari harta karun, ketika ia berhasil mendapatkan gambar, ia mendapatkan gambar dan melihatnya dengan kecepatan 10 kbps

## Jawaban


## No. 13
### Sedangkan, Zoro yang sangat bersemangat untuk mencari harta karun, sehingga kecepatan kapal Zoro tidak dibatasi ketika sudah mendapatkan harta yang diinginkannya

## Jawaban

