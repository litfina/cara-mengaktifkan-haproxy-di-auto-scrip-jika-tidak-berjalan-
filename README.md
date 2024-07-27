# cara-mengaktifkan-haproxy-di-auto-scrip-jika-tidak-berjalan-
##bahan yang di bututhkan agar bisa berjalan siapkan##
domain/subdomain di vps kalian gunakan yang kalian pasang di auto scrip 
### tutor cara membuat nya ##
###1. Membuat Sertifikat Self-Signed dan Private Key ###
Jika Anda tidak memiliki sertifikat SSL dan private key, Anda bisa membuat sertifikat self-signed menggunakan OpenSSL. Berikut adalah perintah untuk membuat sertifikat dan private key
```
sudo openssl req -newkey rsa:2048 -nodes -keyout /etc/haproxy/hap.key -x509 -days 365 -out /etc/haproxy/hap.crt
```
isi dalam membuat sertifikat adalah 
sudo openssl req -newkey rsa:2048 -nodes -keyout /etc/haproxy/hap.key -x509 -days 365 -out /etc/haproxy/hap.crt
Generating a RSA private key
..............................+++++
..+++++
writing new private key to '/etc/haproxy/hap.key'
-----
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) [AU]:

$ isi nya paling ke gitu setelah itu isi nya seperti ini $
1. Masukkan Informasi Sertifikat:
# 1 Country Name (2 letter code): Masukkan kode negara Anda (misalnya, ID untuk Indonesia) atau tekan Enter untuk menggunakan default.
# 2 State or Province Name (full name): Masukkan nama provinsi atau negara bagian Anda (misalnya, Jakarta) atau tekan Enter untuk menggunakan default.
# 3 Locality Name (e.g. city): Masukkan nama kota Anda (misalnya, Jakarta) atau tekan Enter untuk menggunakan default.
# 4 Organization Name (e.g. company): Masukkan nama organisasi Anda (misalnya, MyCompany) atau tekan Enter untuk menggunakan default.
# 5 Organizational Unit Name (e.g. section): Masukkan nama unit organisasi Anda (misalnya, IT Department) atau tekan Enter untuk menggunakan default.
# 6 Common Name (e.g. server FQDN or YOUR name): Masukkan nama domain Anda (misalnya, example.com) atau nama server Anda (misalnya, localhost) atau tekan Enter untuk menggunakan default.
# 7 Email Address: Masukkan alamat email Anda (misalnya, admin@example.com) atau tekan Enter untuk menggunakan default.
##isi nya seperti itu domain nya adalah gunakan domain kalian yang di pasang di auto scrip ###
###2. Menggabungkan Sertifikat dan Private Key ke dalam File PEM ###
```
sudo cat /etc/haproxy/hap.key /etc/haproxy/hap.crt > /etc/haproxy/hap.pem
```
### 3. Atur Izin File ### 
di gunakan untuk mengatur perizinan file nya 
```
sudo chown haproxy:haproxy /etc/haproxy/hap.pem
sudo chmod 600 /etc/haproxy/hap.pem
```
### 4. Restart HAProxy ###
agar haproxy kalian bekerja kembali / restart 
```
sudo systemctl restart haproxy
```
### 5. Verifikasi Status HAProxy ###
cek apakah dia runing atau failed 
```
sudo systemctl status haproxy
```



