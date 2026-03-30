# DNS
DNS (Domain Name System) adalah sistem yang berfungsi mengubah nama domain atau host menjadi alamat IP. DNS cukup berperan mengirimkan permintaan ke server DNS lokal dan menerima hasilnya. Proses yang lebih kompleks sebenarnya terjadi di sisi server, di mana server DNS yang tersusun secara hierarkis saling berkomunikasi untuk menyelesaikan permintaan tersebut, baik secara rekursif maupun iteratif, tanpa terlihat oleh klien.

## 1. Nslookup
Nslookup merupakan perintah yang digunakan untuk melakukan query ke server DNS guna memperoleh berbagai informasi terkait domain atau host, seperti alamat IP, nama domain, serta record DNS lainnya. Perintah ini bekerja dengan mengirimkan permintaan ke server DNS tertentu, kemudian menampilkan hasil respons yang diterima kepada pengguna.

### Berikut penggunaan nslookup pada command prompt:
1) Perintah nslookup www.nit.edu digunakan untuk melakukan pencarian informasi DNS terhadap domain tersebut dengan tujuan mengetahui apakah domain tersebut terdaftar dan memiliki alamat IP. Perintah ini bekerja dengan mengirimkan permintaan ke server DNS yang digunakan, kemudian menampilkan hasil respons yang diterima. Pada hasil yang ditunjukkan, domain tidak ditemukan, yang menandakan bahwa domain tersebut tidak tersedia atau tidak terdaftar dalam sistem DNS.
![](../image/modul4_ss/nslookup1.png)

2) Perintah nslookup -type=NS mit.edu digunakan untuk memperoleh informasi mengenai Name Server (NS) yang bertanggung jawab atas domain mit.edu. Perintah ini mengirimkan permintaan ke server DNS untuk mengetahui server mana saja yang mengelola dan melayani resolusi nama domain tersebut.
![](../image/modul4_ss/nslookup2.png)

3) Perintah nslookup www.aiit.or.kr bitsy.mit.edu digunakan untuk melakukan pencarian informasi DNS terhadap domain www.aiit.or.kr dengan menggunakan server DNS tertentu, yaitu bitsy.mit.edu, sebagai tujuan query.
![](../image/modul4_ss/nslookup3.png)

## 2. Ipconfig
Ipconfig berguna untuk mengelola informasi DNS yang tersimpan dalam host. Yang mana host dapat menyimpan catatan DNS yang baru saja diperolehnya. Untuk melihat record yang telah disimpan, setelah prompt C:\> masukkan  perintah berikut:

1) Perintah "ipconfig /all" digunakan untuk menampilkan informasi lengkap konfigurasi jaringan pada komputer. Perintah ini memberikan detail seperti nama host, status koneksi jaringan, alamat IP, subnet mask, gateway, DNS server, serta informasi lain yang berkaitan dengan adaptor jaringan yang digunakan.
![](../image/modul4_ss/ipconfig1.png)

2) Perintah "ipconfig /all > networkinfo.txt" digunakan untuk menampilkan seluruh informasi konfigurasi jaringan, kemudian menyimpannya ke dalam file bernama networkinfo.txt. Hal ini berguna untuk dokumentasi atau analisis lebih lanjut tanpa harus melihat langsung di Command Prompt. Sedangkan perintah ipconfig /flushdns berfungsi untuk menghapus cache DNS yang tersimpan di komputer. Cache ini biasanya berisi hasil pencarian DNS sebelumnya, dan dengan menghapusnya, sistem akan meminta ulang informasi DNS terbaru dari server. Perintah ini sering digunakan untuk mengatasi masalah koneksi atau kesalahan DNS.
![](../image/modul4_ss/ipconfig2.png)

## 3. Tracing DNS dengan Wireshark 