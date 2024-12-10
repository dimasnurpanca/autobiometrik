# AutoBiometrik 🚀  

**AutoBiometrik** adalah aplikasi ringan untuk integrasi biometrik BPJS (Fingerprint & Frista) dalam sistem informasi rumah sakit. Aplikasi ini dirancang untuk mempermudah validasi biometrik dengan login otomatis, pengisian nomor BPJS otomatis, dan API endpoint untuk integrasi dengan APM rumah sakit.  

---

https://github.com/user-attachments/assets/090a629b-fc95-42fc-a0f8-3db7fbe5c8a8



## 🎯 Fitur Utama  
- **Makro Ringan**  
  Jalankan `autobiometrik.exe` untuk otomatisasi biometrik menggunakan Fingerprint atau Frista.  
- **Konfigurasi Mudah**  
  File `config.json` memungkinkan Anda untuk:  
  - Menentukan path aplikasi Fingerprint dan Frista.  
  - Mengatur username dan password.  
- **Login Otomatis**  
  Masuk ke aplikasi Frista atau Fingerprint secara otomatis.  
- **Isi Nomor BPJS Otomatis**  
  Nomor peserta BPJS pasien langsung terisi tanpa input manual.  
- **Auto Block Input User**  
  Input pengguna diblokir selama makro berjalan untuk menghindari gangguan.  
- **Endpoint API untuk Integrasi**  
  Dapat diintegrasikan dengan berbagai sistem APM rumah sakit melalui API endpoint yang disediakan.  

---

## 🔧 Endpoint API  

| Endpoint | Deskripsi | Parameter |
|----------|-----------|-----------|
| `http://127.0.0.1:5000/run_exe?no_peserta=NOKA` | Jalankan aplikasi Frista | `no_peserta` = Nomor BPJS |
| `http://127.0.0.1:5000/run_finger_exe?no_peserta=NOKA` | Jalankan aplikasi Fingerprint | `no_peserta` = Nomor BPJS |
| `http://127.0.0.1:5000/stop_exe` | Tutup aplikasi Frista | - |
| `http://127.0.0.1:5000/stop_finger_exe` | Tutup aplikasi Fingerprint | - |

**Catatan:**  
- Ganti `NOKA` dengan nomor peserta BPJS pasien.  
- Endpoint dapat dikembangkan lebih lanjut untuk fitur auto-close berdasarkan status fingerprint di vClaim.  

---

## 📁 Konfigurasi `config.json`  

Contoh isi file `config.json`:  
```json
{
  "pathfinger": "C:\\Program Files\\Fingerprint\\fingerprint.exe",
  "path": "C:\\Program Files\\Frista\\frista.exe",
  "username": "your_username",
  "password": "your_password"
}
```
Penjelasan:
- pathfinger: Path lengkap ke aplikasi Fingerprint.
- path: Path lengkap ke aplikasi Frista.
- username & password: Login untuk aplikasi Frista/Fingerprint.

## 🚀 **Cara Kerja AutoBiometrik**  

1. **Persiapan**  
   - Pastikan aplikasi `autobiometrik.exe` sudah di extract dan file `config.json` telah disesuaikan dengan kebutuhan.  
   - Konfigurasi `config.json` untuk path aplikasi Fingerprint/Frista, username, dan password.  

2. **Proses Validasi Biometrik**  
   - Jalankan `autobiometrik.exe` dan panggil salah satu endpoint berikut:
     - Jalankan Frista:  
       ```plaintext
       http://127.0.0.1:5000/run_exe?no_peserta=NOKA
       ```
     - Jalankan Fingerprint:  
       ```plaintext
       http://127.0.0.1:5000/run_finger_exe?no_peserta=NOKA
       ```
   - Aplikasi biometrik akan terbuka, login otomatis dilakukan, dan nomor peserta BPJS (`NOKA`) langsung terisi.  

3. **Setelah Proses Selesai**  
   - Tutup aplikasi Frista/Finger untuk menjaga performa komputer:  
     - Tutup Frista:  
       ```plaintext
       http://127.0.0.1:5000/stop_exe
       ```
     - Tutup Fingerprint:  
       ```plaintext
       http://127.0.0.1:5000/stop_finger_exe
       ```  

---

## 💡 **Tips untuk Fitur Auto Close**  

Fitur auto-close dapat dikembangkan untuk menutup aplikasi Frista/Finger secara otomatis setelah validasi selesai, menghemat memori dan sumber daya komputer. Berikut tips untuk mengimplementasikannya:  

### 1. **Cek Status Fingerprint di vClaim**  
Gunakan API vClaim untuk memeriksa status validasi biometrik:  
- Jika validasi sudah selesai, panggil endpoint untuk menutup aplikasi.  

### 2. **Integrasikan ke Sistem APM Rumah Sakit**  
Anda dapat melakukan polling atau event-driven checks terhadap status fingerprint di vClaim, lalu memanggil endpoint auto-close secara otomatis.  

### 3. **Contoh Workflow Auto Close**  
- **Polling Status Validasi**  
  1. Sistem memeriksa status fingerprint di vClaim secara berkala.  
  2. Jika validasi selesai (`status = valid`), sistem memanggil endpoint:  
     - `http://127.0.0.1:5000/stop_exe` untuk Frista.  
     - `http://127.0.0.1:5000/stop_finger_exe` untuk Fingerprint.  

- **Event-Driven**  
  1. Sistem mendeteksi perubahan status secara real-time dari vClaim.  
  2. Endpoint close dipanggil saat status berubah menjadi valid.  

### 4. **Optimasi Interval Cek Status**  
- Sesuaikan interval polling status (misalnya, setiap 5 detik).  

---
https://hugaf.com


