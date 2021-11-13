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
	Menginstal dhcp pada server Jipangu
	```
	apt-get install isc-dhcp-server
	```
	Mengedit file konfigurasi `isc-dhcp-server` pada `/etc/default/isc-dhcp-server` ubah `INTERFACES="eth0"`
	
	Mengedit file konfigurasi pada `/etc/dhcp/dhcpd.conf`
	
	![image](https://user-images.githubusercontent.com/66562311/141645322-c7b9857b-533e-4cae-8a8e-cd98f528c264.png)

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
	Menginstal squid pada server Water7
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
Mengupdate package list pada FOOSHA
```
apt-get update
```
Menginstal DHCP relay pada server Jipangu
```
apt-get install isc-dhcp-relay
```
Mengedit file konfigurasi `isc-dhcp-server` pada `/etc/default/isc-dhcp-server` ubah `server=""``INTERFACES="eth1 eth2 eth3"`

Mengedit file konfigurasi pada `/etc/dhcp/dhcpd.conf`

![image](https://user-images.githubusercontent.com/66562311/141644003-aa05410e-acb9-4e29-bd58-1f0e3a05a354.png)

Kemudian restart
```
service isc-dhcp-server relay
```


## No. 3
### Luffy dan Zoro menyusun peta tersebut dengan hati-hati dan teliti. Ada beberapa kriteria yang ingin dibuat oleh Luffy dan Zoro, yaitu:
### - Semua client yang ada HARUS menggunakan konfigurasi IP dari DHCP Server.
### - Client yang melalui Switch1 mendapatkan range IP dari `[prefix IP].1.20` - `[prefix IP].1.99` dan `[prefix IP].1.150` - `[prefix IP].1.169`

## Jawaban
Mengedit file konfigurasi pada `/etc/dhcp/dhcpd.conf` pada Jipangu

![image](https://user-images.githubusercontent.com/66562311/141644311-a73d0cfb-1e88-4d6a-96da-63c142b8dab7.png)

cek pada node Loguetwon dan Alabasta mendapatkan ip antara `192.202.1.20` - `192.202.1.99` dan `192.202.1.150` - `192.202.1.169`

![image](https://user-images.githubusercontent.com/66562311/141644418-812f9409-f5cb-4f94-ac33-369f835afb45.png)

![image](https://user-images.githubusercontent.com/66562311/141644507-4196ee6d-7f85-4f39-b0ad-3dc87f0ea4ee.png)



## No. 4
### Client yang melalui Switch3 mendapatkan range IP dari `[prefix IP].3.30` - `[prefix IP].3.50`

## Jawaban
Mengedit file konfigurasi pada `/etc/dhcp/dhcpd.conf` pada Jipangu

![image](https://user-images.githubusercontent.com/66562311/141644311-a73d0cfb-1e88-4d6a-96da-63c142b8dab7.png)

cek pada node Loguetwon mendapatkan ip antara `192.202.1.20` - `192.202.1.99` dan `192.202.1.150` - `192.202.1.169`

![image](https://user-images.githubusercontent.com/66562311/141644536-f0547b84-92e0-45e0-8c44-3f2ffcbfd896.png)

![image](https://user-images.githubusercontent.com/66562311/141644541-5d71d1b3-7d9a-45e6-8133-23a572020d34.png)


## No. 5
### Client mendapatkan DNS dari EniesLobby dan client dapat terhubung dengan internet melalui DNS tersebut.

## Jawaban
Mengedit domain name server pada konfigurasi file `/etc/dhcp/dhcpd.conf` pada Jipangu

![image](https://user-images.githubusercontent.com/66562311/141644311-a73d0cfb-1e88-4d6a-96da-63c142b8dab7.png)


## No. 6
### Lama waktu DHCP server meminjamkan alamat IP kepada Client yang melalui Switch1 selama 6 menit sedangkan pada client yang melalui Switch3 selama 12 menit. Dengan waktu maksimal yang dialokasikan untuk peminjaman alamat IP selama 120 menit.

## Jawaban
Mengedit `default-lease-time` dan `max-lease-time` pada konfigurasi file `/etc/dhcp/dhcpd.conf` pada Jipangu sehingga septi ini:

![image](https://user-images.githubusercontent.com/66562311/141644311-a73d0cfb-1e88-4d6a-96da-63c142b8dab7.png)

Mengecek pada setiap node di Switch1 dan Switch2
- Switch1
	
	Alabasta

	![image](https://user-images.githubusercontent.com/66562311/141644816-64e526ee-de7a-433b-a278-e89337290b88.png)

	Loguetown

	![image](https://user-images.githubusercontent.com/66562311/141644804-4c07d3f8-956d-4d09-8add-33527dc87b44.png)

- Switch2

	Skypie

	![image](https://user-images.githubusercontent.com/66562311/141644823-61d43aa3-d7d3-4a21-92c3-bf2912e46089.png)

	TottoLand

	![image](https://user-images.githubusercontent.com/66562311/141644831-3a935f7f-0204-4207-8d5b-6ebb9100ebed.png)


## No. 7
### Luffy dan Zoro berencana menjadikan Skypie sebagai server untuk jual beli kapal yang dimilikinya dengan alamat IP yang tetap dengan IP `[prefix IP].3.69`

## Jawaban
Mendapatkan `hwaddress_milik_Skypie`

![image](https://user-images.githubusercontent.com/66562311/141644891-8ff9f1b8-6fd3-4f5d-a683-69c4a0071512.png)

Buka dan edit file 
```
/etc/dhcp/dhcpd.conf
```
![image](https://user-images.githubusercontent.com/66562311/141644930-a7307e4b-2ef4-48d5-911d-b211ed737988.png)

Mengubah konfigurasi pada node Skypie

![image](https://user-images.githubusercontent.com/66562311/141644944-0475d5d8-15d5-4bf9-809d-a62a02097913.png)

Melakukan restart pada Skypie dengan stop kemudian start kembali node Skypie. kemudian cek ip Skypie.

![image](https://user-images.githubusercontent.com/66562311/141644983-d9d1823f-50ba-4c27-95a8-08d9004000a8.png)


## No. 8
### Loguetown digunakan sebagai client Proxy agar transaksi jual beli dapat terjamin keamanannya, juga untuk mencegah kebocoran data transaksi. Pada Loguetown, proxy harus bisa diakses dengan nama `jualbelikapal.yyy.com` dengan port yang digunakan adalah 5000

## Jawaban
- Pada EniesLobby

	Melakukan edit konfigurasi domain pada `/etc/bind/named.conf.local`

	![image](https://user-images.githubusercontent.com/66562311/141646773-7725d509-6f47-46ba-b47c-8f64797a2be4.png)

	Copykan file db.local pada path /etc/bind ke dalam folder jarkom yang baru saja dibuat dan ubah namanya menjadi jarkom2021.com
	```
	cp /etc/bind/db.local /etc/bind/jarkom/jarkom2021.com
	```

	Kemudian buka file jarkom2021.com dan edit seperti gambar berikut dengan IP EniesLobby masing-masing kelompok:
	```
	vim /etc/bind/jarkom/jarkom2021.com
	```

	![image](https://user-images.githubusercontent.com/66562311/141646851-d6a39411-8470-44e4-b3ee-a928f37908c3.png)

	Restart bind9 dengan perintah
	```
	service bind9 restart
	```
- Pada Water7

	Melakukan backup file konfigurasi default yang disediakan Squid.
	```
	mv /etc/squid/squid.conf /etc/squid/squid.conf.bak
	```
	Membuat konfigurasi Squid baru Pada file `/etc/squid/squid.conf`

	Kemudian, pada file config yang baru, masukkan script :

	![image](https://user-images.githubusercontent.com/66562311/141646871-13f0a710-a2a2-437b-af8e-05eb8daa58ed.png)

	Restart squid dengan cara mengetikkan perintah:
	```
	service squid restart
	```
- Pada Loguetown
	Melakukan konfigurasi proxy
	```
	export http_proxy="http://ip-proxy-server:port"
	```
	
	![image](https://user-images.githubusercontent.com/66562311/141646941-70133b1e-2c6f-437a-ae73-d69b4237395c.png)

	![image](https://user-images.githubusercontent.com/66562311/141646932-959ebc77-4e9a-44a3-816f-ed5cb7db2bdb.png)


## No. 9
### Agar transaksi jual beli lebih aman dan pengguna website ada dua orang, proxy dipasang autentikasi user proxy dengan enkripsi MD5 dengan dua username, yaitu `luffybelikapalyyy` dengan password `luffy_yyy` dan `zorobelikapalyyy` dengan password `zoro_yyy`

## Jawaban
- pada Water7
	Command -c digunakan untuk membuat file baru dan untuk MD5 sendiri sudah merupakan default
	
	![image](https://user-images.githubusercontent.com/66562311/141646984-8cc29bff-9a1f-41c8-9909-4b9bed99f758.png)

	![image](https://user-images.githubusercontent.com/66562311/141647078-d6cea1ad-ae20-43a6-89f3-a9166a916c75.png)
	
	Memasukkan innput password zoro_d07. Edit file /etc/squid/squid.conf menjadi seperti berikut:

	![image](https://user-images.githubusercontent.com/66562311/141647089-f71769c1-6931-4444-93d8-e94a825550f3.png)
	
	![image](https://user-images.githubusercontent.com/66562311/141647167-31c0171e-25e1-4c1d-8340-a9218ee38c9c.png)

	![image](https://user-images.githubusercontent.com/66562311/141647171-59ad385f-6f2d-4ebc-9897-14731b8fc259.png)


## No. 10
### Transaksi jual beli tidak dilakukan setiap hari, oleh karena itu akses internet dibatasi hanya dapat diakses setiap hari `Senin-Kamis pukul 07.00-11.00` dan setiap hari `Selasa-Jum’at pukul 17.00-03.00` keesokan harinya (sampai Sabtu pukul 03.00)

## Jawaban
- Pada Water7
	Menjalankan `vim /etc/squid/acl.conf` untuk memodifikasi file tersebut untuk ditambahkan
	
	![image](https://user-images.githubusercontent.com/66562311/141647219-fadc8d0a-9fac-491b-8498-756aa38c9111.png)
	
	Setelah itu edit file `/etc/squid/squid.conf`
	
	![image](https://user-images.githubusercontent.com/66562311/141647238-2859343b-15c9-4c9c-9c59-596e3de673cb.png)

Melakukan testing pabila waktu saat mengakses sebuah website tidak sesuai dengan jam pada file acl.conf maka akan terjadi error dan access akan di-deny. Apabila waktu sesuai dengan jam maka halaman akan terbuka sesuai dengan website yang ingin dituju.

	![image](https://user-images.githubusercontent.com/66562311/141647261-f63a858a-7547-49df-8ebd-98ee21a698f1.png)

	![image](https://user-images.githubusercontent.com/66562311/141647275-c1c7688f-5eee-4054-a61f-cd79eb0a3f03.png)


## No. 11
### Agar transaksi bisa lebih fokus berjalan, maka dilakukan redirect website agar mudah mengingat website transaksi jual beli kapal. Setiap mengakses `google.com`, akan diredirect menuju `super.franky.yyy.com` dengan website yang sama pada soal shift modul 2. Web server super.franky.yyy.com berada pada node Skypie

## Jawaban


## No. 12
### Saatnya berlayar! Luffy dan Zoro akhirnya memutuskan untuk berlayar untuk mencari harta karun di `super.franky.yyy.com`. Tugas pencarian dibagi menjadi dua misi, Luffy bertugas untuk mendapatkan gambar `(.png, .jpg)`, sedangkan Zoro mendapatkan sisanya. Karena Luffy orangnya sangat teliti untuk mencari harta karun, ketika ia berhasil mendapatkan gambar, ia mendapatkan gambar dan melihatnya dengan kecepatan 10 kbps

## Jawaban


## No. 13
### Sedangkan, Zoro yang sangat bersemangat untuk mencari harta karun, sehingga kecepatan kapal Zoro tidak dibatasi ketika sudah mendapatkan harta yang diinginkannya

## Jawaban

