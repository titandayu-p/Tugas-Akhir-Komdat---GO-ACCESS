# Aplikasi Web "GoAccess"


## Sekilas Tentang

GoAccess adalah sebuah *real-time web log analyzer* yang *open source* dan visualisasi interaktif yang dapat berjalan di **Terminal** dalam *nix systems atau melalui browser. 


#### Membuat VM Ubuntu Server
Telah tersedia virtual disk image (VDI) instalasi Ubuntu Server 18.04 di direktori /opt/vm. 
Salin file ubuntu-server.vdi tersebut ke direktori home anda. Kemudian, buat VM baru pada VirtualBox dengan tipe "Ubuntu 64-bit". 
Gunakan virtual disk yang sudah disalin tadi.

File VDI di atas dapat diunduh di http://repo.apps.cs.ipb.ac.id/lab/ubuntu-server.vdi.gz.

#### Setting port-forwarding VM

Tujuannya adalah agar VM bisa diakses dari luar melalui alamat IP host (localhost). Masuk ke 'Settings -> Network -> Advanced -> Port Forwarding' dan tambahkan dua aturan berikut.
Dengan demikian, jika kita mengakses port 8000 di host, maka akan diteruskan ke port 80 di guest (VM). Begitu juga dengan SSH, jika kita mengakses port 2200 di host, maka akan diteruskan ke port 22 di guest.
Setelah semuanya beres, jalankan VM dengan mode headless (tanpa tampilan).


### Sebelum Instalasi
* Karena prosesnya dilakukan dalam windows, fungsi ssh tidak terdapat dalam command prompt. Oleh karena itu, kami menggunakan aplikasi pihak ketiga (PuTTY) untuk mengakses virtual mesinnya.
```
Berikut adalah langkah-langkah untuk mengakses VM dengan PuTTY via cmd.
1. Ubah directory cmd ke directory instalasi PuTTY
2. Lalu, masukkan codingan berikut:

"putty.exe -ssh student@localhost 2200"
```
* Sebelum melakukan instalasi paket pada instansi server Ubuntu, sebaiknya melakukan update sistem terlebih dahulu.Log in dengan sudo user dan lakukan perintah berikut ini.
```
> set repo:

sudo tee /etc/apt/sources.list << !
deb http://repo.apps.cs.ipb.ac.id/ubuntu bionic          main restricted universe multiverse
deb http://repo.apps.cs.ipb.ac.id/ubuntu bionic-updates  main restricted universe multiverse
deb http://repo.apps.cs.ipb.ac.id/ubuntu bionic-security main restricted universe multiverse
!

> update system:
sudo apt-get update
sudo apt-get -y upgrade
```
## Instalasi
* #### Install dependencies
```
sudo apt-get -y install libncursesw5-dev gcc make
```
Optional package
```
sudo apt-get -y install libgeoip-dev libtokyocabinet-dev
```
* #### Install GoAccess
```
> Download the GoAccess tarball by running:
wget http://tar.goaccess.io/goaccess-1.2.tar.gz

> Extract the tarball:
sudo tar -xzvf goaccess-1.2.tar.gz -C /var/www/html

> Configure and install the package:
cd goaccess-1.2
sudo ./configure --enable-utf8 --enable-geoip=legacy
sudo make
sudo make install

> Create a soft link of goaccess in the /usr/bin directory by running:
sudo ln -s /usr/local/bin/goaccess /usr/bin/goaccess

> GoAccess is now installed on your server.
```
* #### Using GoAccess
```
> GoAccess is a web log analyzer. If you do not have a web server running, install the Apache web server:
sudo apt-get -y install apache2

> Start and enable the web server to run at boot time:
sudo systemctl start apache2
sudo systemctl enable apache2

> Allow the required HTTP port through the system firewall:
sudo firewall-cmd --add-service=http --permanent
sudo firewall-cmd --reload

> To analyze the log using GoAccess from a terminal, type:
sudo goaccess /var/log/apache2/access.log --log-format=COMBINED

> To generate an HTML report, type:
sudo goaccess /var/log/apache2/access.log --log-format=COMBINED -a -o /var/www/html/report.html

Open your web browser and navigate to the URL http://Vultr_Server_IP/report.html using your favorite web browser. 
The browser will show you many types of statistics using interactive graphs.
```


## Cara Pemakaian

- Tampilan aplikasi web
- Fungsi-fungsi utama
- Isi dengan data real/dummy (jangan kosongan) dan sertakan beberapa screenshot


## Pembahasan

- Pendapat anda tentang aplikasi web ini
    - kelebihan
    - kekurangan
- Bandingkan dengan aplikasi web lain yang sejenis


## Referensi

Cantumkan tiap sumber informasi yang anda pakai.
