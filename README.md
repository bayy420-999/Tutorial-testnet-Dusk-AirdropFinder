# Tutorial testnet Dusk AirdropFinder

<p style="font-size:14px" align="right">
<a href="https://t.me/airdropfind" target="_blank">Join Telegram Airdrop Finder<img src="https://user-images.githubusercontent.com/50621007/183283867-56b4d69f-bc6e-4939-b00a-72aa019d1aea.png" width="30"/></a>
</p>

<p align="center">
  <img height="auto" width="auto" src="https://raw.githubusercontent.com/bayy420-999/airdropfind/main/NavIcon.png">
</p>


Testnet Dusk akan berjalan selama 6 minggu, 2 minggu (15-30 November) untuk grace periode (persiapan node dll) dan 4 minggu (1 bulan dari 1-31 Desember) untuk testnet yang sebenarnya. Peserta yang berhasil menjalankan node selama 1 bulan akan mendapatkan hadiah dari total 100K $DUSK

## Referensi

[Dokumen resmi](https://dusk.network/pages/incentivized-testnet)

[Explorer](https://explorer.dusk.network/charts/)

[Form pendaftaran peserta testnet](https://forms.gle/3h4wDbab9f6bZ68L8)

[Discord server](https://discord.gg/dusknetwork)

## Persyaratan hardware & software

### Persyaratan hardware

| Komponen | Spesifikasi minimal |
|----------|---------------------|
|CPU|4 Cores|
|RAM|32 GB DDR4 RAM|
|Penyimpanan|1 TB HDD|
|Koneksi|10Mbit/s port|

| Komponen | Spesifikasi rekomendasi |
|----------|---------------------|
|CPU|32 Cores|
|RAM|32 GB DDR4 RAM|
|Penyimpanan|2 x 1 TB NVMe SSD|
|Koneksi|1 Gbit/s port|

### Persyaratan software/OS

| Komponen | Spesifikasi minimal |
|----------|---------------------|
|Sistem Operasi|Ubuntu 16.04|

| Komponen | Spesifikasi rekomendasi |
|----------|---------------------|
|Sistem Operasi|Ubuntu 18.04 atau lebih tinggi|

## Setup


### Pasang dependensi

```console
sudo apt-get update
sudo apt-get install -y tar wget curl
```

### Unduh dan pasang `rusk-wallet`

Unduh executable `rusk-wallet`

```console
cd $HOME
wget https://github.com/dusk-network/wallet-cli/releases/download/v0.12.0/ruskwallet0.12.0-linux-x64.tar.gz
```

Lalu extract dengan menggunakan `tar`

```console
tar -xvf ruskwallet0.12.0-linux-x64.tar.gz
rm ruskwallet0.12.0-linux-x64.tar.gz
cd ruskwallet0.12.0-linux-x64
```

### Buat dompet

Kemudian buat dompet dengan menggunakan perintah dibawah

```console
./rusk-wallet
```

* Pilih `Create a new wallet`
* Masukan password (bebas)
* Ulangi password (yang tadi)
* Salin dan simpan mnemonic 
* Setelah itu, pilih dompet yang tadi dibuat
* Pilih `Export provisioner key-pair`

### Simpan key-pair

Pastikan bahwa key-pair telah ter-export

```console
cd $HOME
ls .dusk/rusk-wallet
```

Jika key-pair telah ter-export akan ada file dengan ekstensi `.key` dan `.cpk`

Langkah selanjutnya adalah menyalin file `.key` dan `.cpk` tadi ke hp/pc anda

* Download termius 
* Login ke VPS anda menggunakan termius 
* Pilih gambar folder
  ![gambar1](/assets/img1.jpg)
* Pilih Local
  ![gambar2](/assets/img2.jpg)
* Pilih `Termius Local`
  ![gambar3](/assets/img3.jpg)
* Pilih `Local`
  ![gambar4](/assets/img4.jpg)
* Pilih `Choose different directory`
  ![gambar5](/assets/img5.jpg)
* Pilih `CREATE NEW FOLDER` lalu buat folder baru
  ![gambar6](/assets/img6.jpg)
* Pilih `USE THIS FOLDER`
  ![gambar7](/assets/img7.jpg)
* Pilih `ALLOW`
  ![gambar8](/assets/img8.jpg)
* Kembali ke host, cari folder `.dusk` lalu masuk ke folder tersebut
  ![gambar9](/assets/img9.jpg)
* Setelah itu akan muncul folder `rusk-wallet`, press folder 
  ![gambar10](/assets/img10.jpg)
* Pilih titik tiga di pojok kanan atas layar
  ![gambar11](/assets/img11.jpg)
* Pilih `Transfer to`
  ![gambar12](/assets/img12.jpg)

### Registrasi dan klaim faucet

Setelah semuanya tersetting isi form [ini](https://forms.gle/3h4wDbab9f6bZ68L8) dan upload file `.cpk` tadi

Tunggu beberapa saat sampai admin memproses request kalian, nanti akan dapat 30K Testnet DUSK untuk menjalankan node

### Unduh dan jalankan `rusk-node`

```console
curl --proto '=https' --tlsv1.2 -sSf https://dusk-infra.ams3.digitaloceanspaces.com/rusk/itn-installer.sh | sh
```

### Buka akses port `9000/udp`

```console
ufw allow 9000:9005/udp
```

### Pindahkan file `.key` ke folder `/opt/dusk/conf`

```console
mv $(ls -a .dusk/rusk-wallet | grep *.key) /opt/dusk/conf/consensus.keys
```

### Set password `consensus.keys`

```console
echo 'DUSK_CONSENSUS_KEYS_PASS=<MASUKAN_PASSWORD_TADI>' > /opt/dusk/services/dusk.conf
```

### Jalankan node

```console
service rusk start
service dusk start
```

### Stake Dusk

```console
cd $HOME
cd ruskwallet0.12.0-linux-x64
./rusk-wallet
```

Lalu ikuti step dibawah

* Pilih `Access your wallet`
* Masukan password anda 
* Pilih address anda
* Cek apakah balance sudah dikirim admin
* Jika sudah, Pilih `Stake Dusk`
* Masukan nominal Dusk yang ingin distake (Minimal 1000 Dusk dan fee 2 Dusk)
* Isi gas limit dengan `2000000000`
* Untuk gas price bisa dibiarkan default
* Lalu ketik `y` untuk mengkonfirmasi transaksi
* Simpan tx hash (Untuk berjaga-jaga bila dibutuhkan)

## Perintah berguna

### Menjalankan service

Menjalankan service rusk

```console
service rusk start
```

Menjalankan service dusk

```console
service dusk start
```

### Menghentikan service

Menghentikan service rusk

```console
service rusk stop
```

Menghentikan service dusk

```console
service dusk stop
```

### Cek logs

Cek log rusk

```console
tail -f /var/log/rusk.log
```

Cek log dusk

```console
tail -f /var/log/dusk.log
```

## Troubleshoot

### Jika anda menggunakan VPS dari Vultr

```console
nano /opt/dusk/services/rusk.conf.user
```

Masukan text ini, lalu ganti `IP_ADDRESS` dengan IP Address VPSmu

```console
KADCAST_PUBLIC_ADDRESS=IP_ADDRESS:9000
KADCAST_LISTEN_ADDRESS=IP_ADDRESS:9000
```

### Error while loading shared libraries: libssl.so.1.1

```console
wget https://www.openssl.org/source/openssl-1.1.1o.tar.gz
tar -zxvf openssl-1.1.1o.tar.gz
cd openssl-1.1.1o
./config
make
make test
sudo make install
```
