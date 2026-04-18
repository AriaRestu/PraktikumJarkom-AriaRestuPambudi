# TCP
TCP (Transmission Control Protocol) merupakan protokol pada lapisan transport yang bersifat connection-oriented, yaitu proses pengiriman data harus diawali dengan pembentukan koneksi terlebih dahulu. TCP memastikan data dikirim secara andal melalui penggunaan mekanisme seperti sequence number, acknowledgment, flow control, dan congestion control.

## Analisis Transfer File Menggunakan Protocol TCP
Berikut Langkah-Langkahnya:
1. Download file http://gaia.cs.umass.edu/wireshark-labs/alice.txt

![](../image/modul6_ss/tcp1.png)

2. Buka browser http://gaia.cs.umass.edu/wireshark-labs/TCP-wireshark-file1.html dan pilih file alice.txt

![](../image/modul6_ss/tcp2.png)

3. Buka wireshark, kemudian pilih wif dan start

![](../image/modul6_ss/tcp3.png)

4. Kembali ke browser klik Upload alice.txt hingga muncul tampilan “Congratulations”

![](../image/modul6_ss/tcp4.png)

5. Stop wireshark kemudian filter "tcp"
    
    ![](../image/modul6_ss/tcp5.png)
    - Paket yang muncul terdiri dari segmen TCP serta beberapa paket HTTP. Ini berarti bahwa proses upload file dilakukan menggunakan protokol HTTP yang berjalan di atas
    - Paket SYN digunakan untuk memulai koneksi TCP antara client dan server (proses three-way handshake), bukan untuk mengirim file. Proses ini memastikan bahwa koneksi siap digunakan sebelum data ditransfer. Setelah koneksi berhasil dibuat, data file akan dikirim dalam beberapa segmen kecil melalui TCP. Hal ini terjadi karena TCP membagi data menjadi bagian-bagian kecil agar pengiriman lebih efisien dan dapat dikontrol
    
    ![](../image/modul6_ss/tcp6.png)
    - Selanjutnya, setelah proses upload selesai, server mengirimkan respon HTTP/1.1 200 OK. Pesan ini menandakan bahwa file telah berhasil diterima dan diproses oleh server. Setelah itu, halaman web menampilkan pesan “Congratulations” sebagai indikasi bahwa proses upload berhasil

### Menjawab Pertanyaan
1) IP dan port TCP komputer klien mencari data di filter "HTTP" dan pilih paket POST
    - IP Server: 128.119.245.12
    
    ![](../image/modul6_ss/tcp7.png)
    - Port server : 52551
    
    ![](../image/modul6_ss/tcp8.png)
    
2) IP dan port TCP server mencari data di filter "HTTP" dan pilih paket HTTP/1.1 200 OK
    - IP Server: 172.20.10.9
    
    ![](../image/modul6_ss/tcp9.png)
    - Port server : 80
    
    ![](../image/modul6_ss/tcp10.png)

#  Dasar TCP
## Berikut Langkah-Langkahnya:
1. Download dan extrak file http://gaia.cs.umass.edu/wireshark-labs/wireshark-traces.zip
![](../image/modul6_ss/dtcp1.png)

2. Buka file dan pilih paket paket tcp-ethereal-trace-1, buka dengan wireshark
![](../image/modul6_ss/dtcp2.png)

### Menjawab Pertanyaan
1) Nomor urut SYN, mencari data di filter tcp.flags.syn == 1 && tcp.flags.ack == 0
    
    ![](../image/modul6_ss/dtcp3.png)
    - Nomor urut pada segmen TCP SYN adalah 0. Segmen ini teridentifikasi sebagai SYN karena memiliki flag SYN pada bagian TCP Flags.
   
    ![](../image/modul6_ss/dtcp4.png)

2) SYN-ACK, mencari data di filter tcp.flags.syn == 1 && tcp.flags.ack == 1
    ![](../image/modul6_ss/dtcp5.png)
    - Nomor urut (sequence number) pada segmen SYN-ACK adalah 0, sedangkan nilai acknowledgment adalah 1. Nilai acknowledgment diperoleh dari sequence number pada segmen SYN sebelumnya yang ditambah 1. Segmen ini dapat diidentifikasi sebagai SYN-ACK karena memiliki flag SYN dan ACK pada bagian TCP Flags
    ![](../image/modul6_ss/dtcp6.png)

3) Sequence number POST, mencari data di filter tcp.port == 1161 && tcp contains "POST"
    ![](../image/modul6_ss/dtcp7.png)
    - Nomor urut segmen TCP yang berisi perintah HTTP POST adalah 1
    ![](../image/modul6_ss/dtcp8.png)

4) 6 segmen pertama + RTT
    ![](../image/modul6_ss/dtcp9.png)
    - Nilai RTT diperoleh dari selisih waktu antara pengiriman segmen TCP dan penerimaan acknowledgment. Berdasarkan grafik Round Trip Time, nilai RTT berkisar antara sekitar 100 ms hingga 300 ms. Nilai RTT ini bervariasi karena dipengaruhi oleh kondisi jaringan selama proses transfer

5) Panjang 6 segmen
   
    ![](../image/modul6_ss/dtcp10.png)
   
    - Panjang 6 segmen adalah 8760 byte

6) Buffer receiver
    
    ![](../image/modul6_ss/dtcp11.png)
    - Nilai minimum ruang buffer yang tersedia pada penerima adalah 5840 byte, yang terlihat dari nilai window size pada segmen TCP

7) Retransmission
    ![](../image/modul6_ss/dtcp12.png)
    - Tidak ditemukan retransmission / ditemukan retransmission. Hal ini dapat dilihat dari tidak adanya / adanya label “TCP Retransmission” pada Wireshark.

8) ACK behavior
    ![](../image/modul6_ss/dtcp13.png)
    - Jumlah data yang di-ACK tidak tetap dan bisa banyak. Penerima dapat mengakui beberapa segmen sekaligus, tidak selalu satu per satu

9) Thoroughtput
    ![](../image/modul6_ss/dtcp14.png)
    - Throughput adalah jumlah data yang ditransfer per satuan waktu. Berdasarkan grafik throughput, kecepatan transfer meningkat secara bertahap hingga mencapai sekitar 200 kbps hingga 270 kbps. Nilai ini menunjukkan performa koneksi TCP selama proses pengiriman data

# Congestion Control pada TCP
## Berikut Langkah-Langkahnya dan Menjawab Pertanyaan:
1. Identifikasi Slow Start & Congestion Avoidance (file tcp-ethereal-trace-1)

    - Buka file tcp-ethereal-trace-1 dengan wireshark
    - Filter "TCP"
    - Klik Statistics -> TCP Stream Graph -> Time-Sequence Graph (Stevens)
    ![](../image/modul6_ss/dtcp15.png)
    - Fase slow start terjadi pada awal koneksi (0 – ±1 detik) dengan pertumbuhan eksponensial. Fase ini berakhir ketika mencapai threshold, ditandai perubahan grafik menjadi linear. Selanjutnya TCP masuk ke fase congestion avoidance dengan pertumbuhan linear. Data nyata menunjukkan sedikit deviasi dari teori karena kondisi jaringan seperti delay dan variasi ACK. Koneksi TCP pada grafik dapat dikatakan relatif stabil karena tidak menunjukkan penurunan drastis pada sequence number yang mengindikasikan packet loss besar atau timeout. Namun, grafik tidak sepenuhnya halus seperti pada model TCP ideal.

2. Identifikasi Slow Start & Congestion Avoidance (alice.txt)

    - Start wireshark
    - Uploud file alice.txt ke http://gaia.cs.umass.edu/wireshark-labs/TCP-wireshark-file1.html
    - Kembali ke wireshark dan filter "TCP"
    - Klik Statistics -> TCP Stream Graph -> Time-Sequence Graph (Stevens)
    ![](../image/modul6_ss/dtcp16.png)
    - Pada grafik kedua, fase slow start terjadi pada awal koneksi dengan pertumbuhan eksponensial yang sangat cepat. Transisi ke congestion avoidance terjadi lebih cepat dibandingkan grafik sebelumnya. Hal ini menunjukkan bahwa koneksi Wi-Fi memiliki respon yang lebih cepat, namun juga lebih rentan terhadap variasi delay. Secara umum, koneksi tetap stabil, meskipun tidak sepenuhnya mengikuti perilaku ideal TCP akibat kondisi jaringan nirkabel.