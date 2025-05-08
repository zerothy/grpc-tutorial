## Reflection
### Joe Mathew Rusli
### 2306152310

1. Perbedaan utama antara unary, server streaming, dan bi-directional streaming RPC terletak pada pola komunikasi data antara klien dan server. Unary RPC mengirim satu request dan menerima satu response, cocok untuk operasi sederhana seperti payment request. Server streaming RPC memungkinkan server mengirimkan banyak response untuk satu request, ideal untuk kasus seperti riwayat transaksi. Sementara itu, bi-directional streaming memungkinkan klien dan server saling bertukar pesan secara bersamaan, sangat sesuai untuk aplikasi chat atau komunikasi real-time.

2. Dalam mengimplementasikan gRPC di Rust, aspek keamanan yang perlu diperhatikan meliputi autentikasi (memastikan identitas pengguna), otorisasi (mengatur hak akses), dan enkripsi data (menggunakan TLS untuk melindungi data selama transmisi). Tanpa mekanisme ini, service rentan terhadap penyadapan, penyalahgunaan, dan serangan pihak ketiga.

3. Tantangan dalam menangani bidirectional streaming di Rust gRPC, terutama pada aplikasi chat, antara lain sinkronisasi pesan, penanganan error secara asinkron, dan pengelolaan resource agar tidak terjadi memory leak. Selain itu, menjaga performa dan skalabilitas saat banyak klien terhubung secara bersamaan juga menjadi perhatian.

4. Penggunaan `tokio_stream::wrappers::ReceiverStream` memudahkan implementasi streaming karena integrasi yang baik dengan ekosistem Tokio dan channel asinkron. Keuntungannya adalah kemudahan penggunaan dan efisiensi resource, namun kekurangannya bisa muncul pada granular control terhadap aliran data dan potensi bottleneck jika tidak dikelola dengan baik.

5. Agar kode Rust gRPC mudah dimaintain dan diextend, struktur kode sebaiknya modular, misalnya dengan memisahkan business logic, service implementation, dan utility. Penggunaan trait, modul, dan dependency injection dapat meningkatkan reusability dan memudahkan pengujian.

6. Pada implementasi MyPaymentService, untuk menangani payment logic yang lebih kompleks, perlu ditambahkan validasi data, integrasi dengan sistem pembayaran eksternal, penanganan error yang lebih detail, serta pencatatan transaksi dan audit.

7. Adopsi gRPC mempengaruhi arsitektur sistem terdistribusi dengan meningkatkan interoperability antar platform berkat penggunaan Protocol Buffers dan HTTP/2. Namun, integrasi dengan sistem non-gRPC atau berbasis REST memerlukan adapter atau gateway tambahan.

8. HTTP/2 sebagai protokol dasar gRPC menawarkan multiplexing, header compression, dan komunikasi lebih efisien dibanding HTTP/1.1 atau WebSocket. Namun, kompleksitas implementasi dan debugging kode bisa lebih tinggi, serta tidak semua infra mendukung HTTP/2 secara penuh.

9. Model request-response pada REST API membatasi real-time communication, sedangkan gRPC dengan streaming memungkinkan pertukaran data dua arah secara langsung, meningkatkan responsivitas aplikasi seperti chat atau monitoring.

10. Pendekatan schema-based pada gRPC dengan Protocol Buffers memastikan data contract yang kuat dan validasi otomatis, namun kurang fleksibel dibanding JSON pada REST API yang schema-less dan mudah diubah. Hal ini berdampak pada proses pengembangan dan kompatibilitas antar layanan.