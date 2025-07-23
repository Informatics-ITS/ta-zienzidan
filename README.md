# 🏁 Tugas Akhir (TA) - Final Project

**Nama Mahasiswa**: Muhammad Zien Zidan  
**NRP**: 5025211122
**Judul TA**: Pengembangan Lini Masa Forensik Drone Melalui Analisis Artefak Penerbangan
**Dosen Pembimbing**: Hudan Studiawan, S.Kom., M.Kom.,Ph.D.  
**Dosen Ko-pembimbing**: Dr. Baskoro Adi Pratomo, S.Kom., M.Kom.

---

## 📺 Demo Aplikasi

Embed video demo di bawah ini :

[![image.jpg
](image.jpg)](https://youtu.be/Jabu_KPAWvw)  
_Klik gambar di atas untuk menonton demo_

---

## 🛠 Panduan Instalasi & Menjalankan Software

### Prasyarat

- Daftar dependensi (contoh):
  - Python 3.10+

### Langkah-langkah

1. **Clone Repository**
   ```bash
   git clone https://github.com/Informatics-ITS/TA.git
   ```
2. **Pull Request dan Clone Plaso**

- Lakukan Pull Request terhadap Log2timeline Plaso
- Lakukan clone Log2timeline Plaso dari repository pribadi
  ```bash
  https://github.com/{nama_akun}/plaso.git
  ```

3. **Salin Kode Sesuai dengan direktori**

- Salin parser `drone_binary.py` ke dalam direktori berikut
  ```bash
  📁 plaso
  └── 📁 plaso
        └── 📁 parsers
              └── drone_binary.py
  ```
- Tambahkan kode berikut atau sesuaikan abjad
  ```bash
  from plaso.parsers import drone_binary
  ```
- Pada direktori
  ```bash
  📁 plaso
  └── 📁 plaso
        └── 📁 parsers
              └── __init__.py
  ```
- Tambahkan kode berikut
  ```bash
  ---
  data_type: "drone:flight:event"
  attribute_mappings:
  - name: "timestamp"
     description: "Creation Time"
  place_holder_event: false
  ---
  ```
- pada direktori dan line 312 (atau sesuai abjad)
  ```bash
  📁 plaso
  └── 📁 plaso
        └── 📁 data
              └── timeliner.yaml
  ```
- Tambahkan kode berikut
  ```bash
  ---
  type: "conditional"
  data_type: "drone:flight:event"
  message:
  - "Longitude: {longitude}"
  - "Latitude: {latitude}"
  - "Height: {height}m"
  - "Distance: {distance}m"
  - "Speed: {speed}m/s"
  short_message:
  - "Flight at {timestamp}"
  - "Longitude: {longitude}"
  - "Latitude: {latitude}"
  - "Distance: {distance}m"
  - "Speed: {speed}m/s"
  short_source: "DJI"
  source: "DJI Flight Log"
  ---
  ```
- pada direktori dan line 210 (atau sesuai abjad)
  ```bash
  📁 plaso
  └── 📁 plaso
        └── 📁 data
              └── 📁 formatters
                    └── generic.yaml
  ```

4. **Setting Virtual Environment**
   ```bash
   virtualenv plaso-environment
   source ./plaso-environment/bin/activate # aktifkan environment
   pip install --upgrade pip # update pip
   ```
5. **Instalasi Dependensi**
   ```bash
   cd plaso/plaso
   pip install -r requirements.txt  # Contoh untuk Python
   pip install setuptools
   ```
6. **Testing Kode Parser**

- Log2timeline Plaso merupakan tool open source oleh karena itu terdapat gaya kepenulisan parser guna agar parser dapat dilihat dalam link berikut
  ```bash
  https://github.com/log2timeline/l2tdocs/blob/main/process/Style-guide.md
  ```
- lakukan testing parser `drone_binary.py` guna mengetahui apakah parser sudah sesuai gaya kepenulisan plaso dengan memnafaatkan tool pylint
  ```bash
  pylint path/to/drone_binary.py
  ```

7. **Konfigurasi**

- Masuk ke dalam direktori plaso/plaso dan lakukan build serta install
  ```bash
  python setup.py build
  python setup.py install
  ```

8. **Jalankan Aplikasi**

- Contoh dataset artefak, storage.plaso, dan output.csv sudah disediakan pada folder artefak dan Hasil
  ```bash
  log2timeline path/to/output.plaso path/to/artifact   # Membuat (timeline storage) Plaso storage
  psort -w path/to/output.csv path/to/storage.plaso   # Ekstrak Plaso Storage yang dibuat ke dalam CSV
  ```

9. **Pengecekan Hasil**
   Buka file hasil CSV yang telah dibuat untuk melihat hasil lini masa penerbangan yang berhasil di parsing

10. **Add Unit test**
    Setelah melakukan pengecekan terhadap hasil lini masa, dapat dilakukan unit test bawaan dari Log2timelin Plaso guna memastikan parser sudah bekerja dengan baik didalam tool tersebut dan membantu analis forensik yang lain untuk mencoba parser yang baru saja dibuat.
    Dengan cara sebagai berikut

- Tambahkan dataset artefak pada direktori berikut
  ````bash
  📁 plaso
     └── 📁 test_data
           └── artefak.txt
     ```
  ````
- Tambahkan kode `test_drone_binary.py` didalam direktori berikut
  ```bash
  📁 plaso
  └── 📁 test
         └── 📁 parsers
               └── test_drone_binary.py
  ```
- Gunakan command berikut guna mengetahui apakah parser memang bekerja dengan baik dan sesuai
  ```bash
  python -m tests.parsers.test_drone_binary.py
  ```

---

## 📚 Dokumentasi Tambahan

- [Log2timeline Plaso](https://plaso.readthedocs.io/en/latest/sources/user/index.html)

---

## ✅ Validasi

- Source code dapat di-build/run tanpa error
- Video demo jelas menampilkan fitur utama
- README lengkap dan terupdate
- Lini masa yang dihasilkan dari ekstraksi data penerbangan menggunakan parser yang dikembangkan telah sesuai dan valid

---

## ⁉️ Pertanyaan?

Hubungi:

- Penulis: zienzidan1@gmail.com
- Pembimbing Utama: hudan@its.ac.id
- Ko-pembimbing : baskoro@its.ac.id
