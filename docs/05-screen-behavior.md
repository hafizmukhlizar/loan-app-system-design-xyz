# Screen Behavior

## Splash Screen
| State/Trigger           | UI              | Action                |
|:----------------------- |:--------------- | :-------------------- |
| **App dibuka**          | Tampilkan logo  | Cek token tersimpan   |
| **Token ditemukan**     | Loading singkat | Navigate ke Dashboard |
| **Token tidak ditemukan** | Loading singkat | Navigate ke Login Screen |

## Login Screen
| State/Trigger           | UI              | Action                |
|:----------------------- |:--------------- | :-------------------- |
| **Screen dibuka**                | Tampilkan input email/no hp, password, tombol "Masuk", link "Registrasi" | - |
| **Device support biometric**     | Tampilkan tombol tambahan "Masuk dengan Biometric"                       | - |
| **Tap Masuk**                    | Loading singkat                                                          | Validasi field tidak kosong & format email/HP benar |
| **Validasi berhasil**            | -                                                                        | Simpan token, navigate ke Dashbord |
| **Validasi gagal**               | Tampilkan "Email/No HP atau password salah"                              | Tetap di login screen |
| **Tap "Masuk dengan Biometric"** | Trigger native biometric prompt perangkat                                | Berhasil → simpan token → Dashboard. Gagal → fallback ke form password |
| **Tap "Registrasi"**             | -                                                                        | Navigate ke Register Screen |

## Register Screen
| State/Trigger           | UI              | Action                |
|:----------------------- |:--------------- | :-------------------- |
| **Screen dibuka**           | Tampilkan Form: nama, email, no HP, password, konfirmasi password, no KTP, upload foto KTP, ambil foto selfie | - |
| **Tap "Upload Foto KTP"**   | Buka kamera atau galeri | Foto tersimpan di state form |
| **Tap "Ambil Foto Selfie"** | Buka kamera langsung | Foto tersimpan di state form |
| **Tap "Daftar"**            | Loading singkat | Validasi: nama wajib, format email/HP valid, password min 8 karakter, konfirmasi password cocok, no KTP 16 digit, kedua foto wajib ada |
| **Validasi lolos**          | Loading singkat | upload file |
| **Registrasi berhasil**     | Tampilkan "Registrasi berhasil, dokumen sedang diverifikasi" | Navigate ke Dashboard |
| **Sudah terdaftar**         | Tampilkan "Registrasi gagal, data sudah terdaftar" | Tetap di register screen |
| **Validasi gagal**          | Tampilkan "Registrasi gagal" | Tetap di register screen |

## Dashboard Screen
| State/Trigger           | UI              | Action                |
|:----------------------- |:--------------- | :-------------------- |
| **Screen dibuka/refresh** | Loading | Loading data |
| **Ada pinjaman aktif** | Tampilkan Card: nominal, sisa hutang, status, tagihan berikutnya, list cicilan per bulan | Tombol "Ajukan Pinjaman" disembunyikan/disabled |
| **Tidak ada pinjaman aktif** | Tampilkan ilustrasi + "Belum ada pinjaman aktif" | Tombol "Ajukan Pinjaman Sekarang" aktif |
| **Gagal memuat (error jaringan)** | Tampilkan message error dan tombol "Coba lagi" | Tap "coba lagi" -> refresh screen dashboard |
| **Tap "Ajukan Pinjaman"** | - | Navigate ke Apply Loan Screen |
| **Tap icon profile** | - | Navigate ke Profile Screen |

## Apply Loan Screen
| State/Trigger           | UI              | Action                |
|:----------------------- |:--------------- | :-------------------- |
| **Screen dibuka** | Tampilkan input nominal (Rp500rb–12jt), input tenor (1–12 bulan), estimasi cicilan per bulan (kalkulasi kasar di FE: amount/tenor) | - |
| **verif_status belum verified** | Tampilkan Banner "KTP Anda masih diverifikasi", form disabled | Tombol "Ajukan" Disabled |
| **User ubah nominal/tenor** | - | Validasi real-time: amount ≤ 12.000.000, tenor ≤ 12, estimasi cicilan terupdate otomatis |
| **Tap "Ajukan"** | Tampilkan loading | - |
| **Diterima** | Tampilkan Dialog "Pengajuan sedang diproses, hasil dikirim ke email/SMS" | Navigate ke dashboard |
| **Data field tidak sesuai** | Tampilkan pesan error di field terkait | Tetap di Apply Loan Screen |

## Profile Screen
| State/Trigger           | UI              | Action                |
|:----------------------- |:--------------- | :-------------------- |
| **Screen dibuka** | Loading | Loading Data |
| **Data dimuat** | Tampilkan Nama, email, no HP, badge status verifikasi KTP | - |
| **Device support biometric & belum terdaftar biometric** | Tampilkan Toggle "Aktifkan Login Biometric" (off) | - |
| **Tap toggle aktifkan biometric** | Native biometric enrollment di OS | Berhasil → toggle jadi "on" |
| **Tap "Logout"** | Dialog konfirmasi "Apakah anda ingin logout?" | Hapus token lokal → Navigate ke Login |
