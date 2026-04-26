# Menguji Serangan CSRF ( Cross-Site Request Forgery) pada Web sederhana

## 📌 Deskripsi
Project ini merupakan implementasi sederhana untuk memahami serangan **CSRF (Cross-Site Request Forgery)** pada aplikasi web berbasis PHP.

Melalui project ini, dilakukan simulasi:
- Sistem tanpa proteksi CSRF
- Serangan menggunakan file HTML
- Analisis request
- Implementasi pencegahan menggunakan CSRF Token

---

## ⚙️ Tools yang Digunakan
- XAMPP (Web Server)
- Visual Studio Code
- Google Chrome

---

## 🚨 Tahap 1: Sistem Tanpa Proteksi CSRF

### 🔹 Form Ubah Password
```html
<form action="update_password.php" method="POST">
  <input type="text" name="password" placeholder="Masukkan password baru">
  <button type="submit">Ubah Password</button>
</form>

<form action="http://localhost:8080/csrf-lab/update_password.php" method="POST">
  <input type="hidden" name="password" value="hacked_by_csrf">
</form>

<script>
  document.forms[0].submit();
</script>

🔥 Hasil Serangan

Password berhasil diubah tanpa konfirmasi pengguna.

🔍 Analisis

Server tidak mampu membedakan request asli dan request dari attacker karena:

Session masih aktif
Tidak ada validasi tambahan
📡 Request Payload (Network)

🛡️ Tahap 2: Implementasi CSRF Protection
🔹 CSRF Token
<input type="hidden" name="csrf_token" value="random_token">

🔒 Hasil Setelah Mitigasi

Serangan CSRF gagal karena token tidak valid.

Perbandingan
Sebelum Mitigasi
Request dari luar diterima
Serangan berhasil
Sesudah Mitigasi
Request tanpa token ditolak
Sistem lebih aman
📚 Kesimpulan

Berdasarkan eksperimen yang telah dilakukan, serangan CSRF terbukti sangat berbahaya karena memanfaatkan sesi login pengguna tanpa perlu mengetahui kredensial akun.

Pada tahap awal, sistem yang tidak memiliki proteksi menerima semua request yang dikirim, sehingga memungkinkan perubahan data tanpa sepengetahuan pengguna. Hal ini menunjukkan bahwa server tidak mampu membedakan request sah dan request berbahaya.

Melalui analisis menggunakan fitur Network di browser, terlihat bahwa data dikirim melalui metode POST tanpa validasi tambahan, sehingga celah keamanan sangat terbuka.

Setelah dilakukan mitigasi menggunakan CSRF Token, sistem menunjukkan peningkatan keamanan yang signifikan. Request tanpa token yang valid langsung ditolak oleh server, sehingga serangan tidak lagi berhasil dilakukan.

Dengan demikian, penerapan mekanisme keamanan seperti CSRF Token sangat penting dan wajib diterapkan dalam pengembangan aplikasi web untuk melindungi data dan aktivitas pengguna.

Referensi
1. OWASP Foundation (2024)
https://owasp.org/www-community/attacks/csrf
2. MDN Web Docs (2024)
https://developer.mozilla.org
3. PortSwigger (2024)
https://portswigger.net/web-security/csrf
4. PHP Documentation (2024)
https://www.php.net/manual/en/book.session.php
5. Eksperimen pribadi (2026)
