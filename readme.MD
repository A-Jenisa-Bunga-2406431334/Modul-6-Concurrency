# Commit 1 Reflection Notes

## Handle-connection, check response

Pada milestone ini, saya mempelajari bagaimana server menerima dan membaca HTTP request 
dari browser menggunakan fungsi `handle_connection`.

Beberapa hal yang saya pelajari:

**`TcpListener`** digunakan untuk "mendengarkan" koneksi masuk pada alamat 
`127.0.0.1:7878`. Setiap kali ada koneksi masuk, stream-nya diproses oleh 
`handle_connection`.

**`BufReader`** membungkus TcpStream agar bisa dibaca baris per baris secara efisien. 
Tanpa BufReader, kita harus membaca byte satu per satu.

**HTTP Request Format** terdiri dari beberapa header yang diakhiri dengan blank line. 
Itulah mengapa `.take_while(|line| !line.is_empty())` digunakan — untuk berhenti 
membaca ketika menemukan baris kosong.

Dari output yang saya terima, browser mengirimkan informasi seperti:
- `GET / HTTP/1.1` — method, path, dan versi HTTP
- `Host` — alamat server yang dituju
- `User-Agent` — informasi browser yang digunakan
- `Accept` — format konten yang bisa diterima browser

Request muncul beberapa kali karena browser otomatis me-retry ketika tidak mendapat 
response dari server.

