# Ujian Tengah Semester (UTS) Pemrograman Web 2
## Menguji Serangan CSRF (Cross-Site Request Forgery) pada Web Sederhana

|                |                                      |
| -------------- | ------------------------------------ |
| Nama           | Dwi Okta Ramadhani                   |
| NIM            | 312410056                            |
| Kelas          | I.24.1A                              |
| Universitas    | Universitas Pelita Bangsa            |
| Mata Kuliah    | Pemrograman Web 2                    |
| Dosen Pengampu | Agung Nugroho, S.Kom., M.Kom.        |

## Deskripsi
Project ini merupakan implementasi sederhana untuk memahami serangan **CSRF (Cross-Site Request Forgery)** pada aplikasi web berbasis PHP.

Melalui project ini, dilakukan simulasi:
- Sistem tanpa proteksi CSRF
- Serangan menggunakan file HTML
- Analisis request
- Implementasi pencegahan menggunakan CSRF Token

---

## Tools yang Digunakan
- XAMPP (Web Server)
- Visual Studio Code
- Google Chrome/Firefox

---

## Tahap 1: Sistem Tanpa Proteksi CSRF
<img width="1920" height="1128" alt="1" src="https://github.com/user-attachments/assets/1e6a8d47-9ec1-4d8c-9ad7-0de0b877eb88" />
<img width="1711" height="647" alt="y" src="https://github.com/user-attachments/assets/4bc107a8-8c2a-42ca-b7a2-465c203bf290" />

### Form Ubah Password
```html
<form action="update_password.php" method="POST">
  <input type="text" name="password" placeholder="Masukkan password baru">
  <button type="submit">Ubah Password</button>
</form>
````

---

### Script Serangan (CSRF Attack)
<img width="1275" height="647" alt="2" src="https://github.com/user-attachments/assets/27581e26-ff2d-48d2-a374-ab36be0f3c4a" />

```html
<form action="http://localhost:8080/csrf-lab/update_password.php" method="POST">
  <input type="hidden" name="password" value="hacked_by_csrf">
</form>

<script>
  document.forms[0].submit();
</script>
```

---

### Hasil Serangan

Password berhasil diubah tanpa konfirmasi pengguna.
<img width="1920" height="1128" alt="4" src="https://github.com/user-attachments/assets/fa3836ba-60d3-4f88-921f-8449be5d5e2c" />

---

## Analisis

Server tidak mampu membedakan request asli dan request dari attacker karena:

* Session masih aktif
* Tidak ada validasi tambahan

### Request Payload (Network)

(Dapat dilihat melalui Inspect → Network pada browser)
<img width="1536" height="1024" alt="6" src="https://github.com/user-attachments/assets/46d28ba2-a1df-4cad-859a-c3534b555820" />

---

### Hasil Setelah Mitigasi
<img width="1653" height="703" alt="5" src="https://github.com/user-attachments/assets/b869c7b6-c0ea-4424-83bd-90e629625d00" />


Serangan CSRF gagal karena token tidak valid.

---

## Perbandingan

### Sebelum Mitigasi

* Request dari luar diterima
* Serangan berhasil

### Sesudah Mitigasi

* Request tanpa token ditolak
* Sistem lebih aman

---

## Kesimpulan

Berdasarkan eksperimen yang telah dilakukan, serangan **CSRF** terbukti sangat berbahaya karena memanfaatkan sesi login pengguna tanpa perlu mengetahui kredensial akun.

Pada tahap awal, sistem yang tidak memiliki proteksi menerima semua request yang dikirim, sehingga memungkinkan perubahan data tanpa sepengetahuan pengguna. Hal ini menunjukkan bahwa server tidak mampu membedakan request sah dan request berbahaya.

Melalui analisis menggunakan fitur **Network** di browser, terlihat bahwa data dikirim melalui metode POST tanpa validasi tambahan, sehingga celah keamanan sangat terbuka.

Setelah dilakukan mitigasi menggunakan **CSRF Token**, sistem menunjukkan peningkatan keamanan yang signifikan. Request tanpa token yang valid langsung ditolak oleh server, sehingga serangan tidak lagi berhasil dilakukan.

Dengan demikian, penerapan mekanisme keamanan seperti CSRF Token sangat penting dan wajib diterapkan dalam pengembangan aplikasi web untuk melindungi data dan aktivitas pengguna.

---

## Referensi

1. OWASP Foundation (2024)
   [https://owasp.org/www-community/attacks/csrf](https://owasp.org/www-community/attacks/csrf)

2. MDN Web Docs (2024)
   [https://developer.mozilla.org](https://developer.mozilla.org)

3. PortSwigger (2024)
   [https://portswigger.net/web-security/csrf](https://portswigger.net/web-security/csrf)

4. PHP Documentation (2024)
   [https://www.php.net/manual/en/book.session.php](https://www.php.net/manual/en/book.session.php)

5. Eksperimen pribadi (2026)
