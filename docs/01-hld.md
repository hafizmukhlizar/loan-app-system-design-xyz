# High Level Design Architecture

## Architecture Diagram
```
+--------------------------------------------------+
|                  Client Layer                    |
|                                                  |
| Mobile Application (Android / iOS)               |
+-------------------------+------------------------+
                          |
                          v
+--------------------------------------------------+
|                   API Gateway                    |
|                                                  |
| Entry Point untuk seluruh request dari aplikasi  |
+-------------------------+------------------------+
                          |
                          v
+--------------------------------------------------+
|                Application Layer                 |
|                                                  |
| Menangani seluruh proses bisnis aplikasi         |
| pinjaman online                                  |
+-------------------------+------------------------+
                          |
                          v
+--------------------------------------------------+
|             Database & Storage Layer             |
|                                                  |
| Penyimpanan data aplikasi dan dokumen pengguna   |
+-------------------------+------------------------+
                          |
                          v
+--------------------------------------------------+
|              External Integrations               |
|                                                  |
| Integrasi dengan layanan pihak ketiga            |
+--------------------------------------------------+
```

## Layer Description

### Client Layer
Client Layer merupakan aplikasi mobile yang digunakan oleh pengguna untuk mengakses layanan pinjaman online.  
Fitur yang tersedia pada aplikasi meliputi registrasi pengguna, login menggunakan password atau biometrik, upload foto dan KTP, pengajuan pinjaman, melihat status pinjaman, serta melihat sisa hutang dan tagihan bulanan.

### API Gateway
API Gateway berfungsi sebagai pintu masuk seluruh komunikasi antara aplikasi mobile dan backend.  
Seluruh request dari aplikasi mobile akan diteruskan melalui layer ini sebelum diproses lebih lanjut oleh sistem.

### Application Layer
Application Layer merupakan pusat proses bisnis aplikasi.  
Layer ini menangani seluruh kebutuhan bisnis seperti pengelolaan data pengguna, verifikasi identitas, proses pengajuan pinjaman, penilaian kelayakan kredit, pengelolaan tagihan, serta pengiriman notifikasi kepada pengguna.

### Database & Storage Layer
Layer ini digunakan untuk menyimpan seluruh data yang dibutuhkan oleh aplikasi.  
Data yang disimpan meliputi, data pengguna, data pinjaman, data pembayaran, status pengajuan pinjaman, hasil verifikasi dan penilaian kredit, dokumen yang diunggah pengguna seperti foto KTP dan foto selfie.

### External Integrations
Layer ini digunakan untuk berkomunikasi dengan layanan pihak ketiga yang mendukung operasional aplikasi.  
Contoh integrasi yang digunakan antara lain Email Gateway untuk pengiriman email, SMS Gateway untuk pengiriman SMS, Biometric Authentication untuk login biometrik, Layanan verifikasi identitas (KTP Verification), Layanan Credit Scoring.
