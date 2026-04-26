# 🔐 Mengenal dan Menguji Serangan CSRF (Cross-Site Request Forgery)

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
