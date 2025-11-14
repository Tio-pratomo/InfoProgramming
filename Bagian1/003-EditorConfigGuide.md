# 📝 Panduan _.editorconfig_

## 🔹 Apa itu .editorconfig?

**.editorconfig** adalah file konfigurasi yang membantu menjaga konsistensi format kode di berbagai editor dan IDE. File ini berisi aturan penulisan kode yang akan diterapkan secara otomatis oleh editor yang mendukung .editorconfig (seperti VS Code, Sublime Text, Atom, Vim, dll).

### 🔸 Tujuan .editorconfig:

- Menjaga **konsistensi format kode** dalam tim
- Mencegah perubahan format yang tidak perlu di commit
- Mengatur format otomatis tanpa harus mengatur manual di masing-masing editor
- Memudahkan kolaborasi dalam proyek tim

---

## 🔹 Struktur Dasar .editorconfig

File .editorconfig biasanya diletakkan di **root direktori proyek** dan memiliki struktur seperti ini:

```ini
# Petunjuk untuk editor bahwa ini adalah file .editorconfig
root = true

# Aturan untuk semua file
[*]
end_of_line = lf
charset = utf-8
trim_trailing_whitespace = true
insert_final_newline = true

# Aturan untuk file JavaScript
[*.js]
indent_style = space
indent_size = 2

# Aturan untuk file Python
[*.py]
indent_style = space
indent_size = 4

# Aturan untuk file Markdown
[*.md]
trim_trailing_whitespace = false
```

---

## 🔹 Property Umum dalam .editorconfig

### 🔸 indent_style

- **space**: Gunakan spasi untuk indentasi
- **tab**: Gunakan tab untuk indentasi

### 🔸 indent_size

- Jumlah karakter untuk satu unit indentasi (jika indent_style=space)
- Jika indent_style=tab, maka ini akan mengatur lebar tab

### 🔸 tab_width

- Mengatur lebar tab dalam jumlah karakter
- Diabaikan jika indent_style=space kecuali indent_size tidak ditentukan

### 🔸 end_of_line

- **lf**: Gunakan line feed (`\n`) - untuk Unix/Linux
- **crlf**: Gunakan carriage return + line feed (`\r\n`) - untuk Windows
- **cr**: Gunakan carriage return (`\r`) - untuk Mac Classic

### 🔸 charset

- **utf-8**: Rekomendasi standar
- **latin1**, **utf-8-bom**: Charset lain yang didukung

### 🔸 trim_trailing_whitespace

- **true**: Hapus spasi di akhir baris
- **false**: Biarkan spasi di akhir baris

### 🔸 insert_final_newline

- **true**: Tambahkan baris baru di akhir file
- **false**: Tidak tambahkan baris baru di akhir file

### 🔸 max_line_length

- Batasi panjang maksimum baris (dalam jumlah karakter)
- Contoh: `max_line_length = 80`

---

## 🔹 Contoh Konfigurasi Lengkap

Berikut adalah contoh `.editorconfig` yang bisa Anda gunakan untuk proyek:

```ini
# Menandakan ini adalah file konfigurasi root. Editor tidak akan mencari file .editorconfig
# di direktori yang lebih tinggi. Ini adalah praktik terbaik untuk proyek.
root = true

# Aturan universal yang berlaku untuk semua jenis file
[*]
# Gunakan newline (lf) sebagai karakter akhir baris. Standar untuk Linux dan macOS.
end_of_line = lf
# Gunakan set karakter utf-8 untuk semua file teks.
charset = utf-8
# Hapus spasi kosong yang tidak perlu di akhir baris.
trim_trailing_whitespace = true
# Pastikan ada satu baris kosong di akhir setiap file.
insert_final_newline = true
# Atur gaya indentasi menjadi spasi, bukan tab, untuk konsistensi.
indent_style = space
# Anda bisa mengatur panjang baris maksimum, meskipun tidak semua editor mendukungnya.
# 120 adalah pilihan modern, namun bisa disesuaikan (misalnya 80 atau 100).
# max_line_length = 120

# Aturan untuk file web dan konfigurasi umum (indentasi 2 spasi)
# Mengelompokkan ekstensi file dengan aturan yang sama membuatnya lebih ringkas.
[*.{js,jsx,ts,tsx,html,css,scss,less,json,yaml,yml,vue}]
indent_size = 2

# Aturan spesifik untuk file Python, sesuai standar PEP 8
[*.py]
indent_size = 4

# Aturan untuk file XML dan terkait (indentasi 2 spasi)
[*.{xml,svg,csproj,user,config}]
indent_size = 2

# Aturan spesifik untuk file Markdown
[*.md]
# Jangan hapus spasi di akhir baris, karena dua spasi di akhir
# baris digunakan untuk membuat 'hard line break'.
trim_trailing_whitespace = false
# Beberapa parser Markdown sensitif terhadap baris baru di akhir file.
insert_final_newline = false

# Aturan untuk file Makefile yang secara sintaksis memerlukan tab
[Makefile]
indent_style = tab

# Aturan untuk file skrip Windows (menggunakan CRLF)
[*.{bat,cmd}]
end_of_line = crlf
```

---

## 🔹 Best Practices saat Menggunakan .editorconfig

### 1. Letakkan di Root Proyek

- Simpan file .editorconfig di direktori utama proyek agar semua editor bisa membacanya

### 2. Gunakan Format Umum

- Ikuti format standar untuk memastikan kompatibilitas dengan berbagai editor

### 3. Sesuaikan dengan Style Guide Proyek

- Atur konfigurasi sesuai dengan style guide tim Anda (contoh: 2 spasi untuk JS, 4 spasi untuk Python)

### 4. Konsultasikan dengan Tim

- Pastikan semua anggota tim mengetahui dan menyetujui aturan yang ditetapkan

### 5. Gunakan Konfigurasi yang Konsisten

- Jika proyek menggunakan 2 spasi untuk indentasi, tetapkan itu untuk semua file terkait

### 6. Dokumentasikan Konfigurasi

- Tambahkan keterangan di README atau dokumentasi proyek tentang aturan yang digunakan

### 7. Hindari Konflik dengan Linter

- Pastikan konfigurasi .editorconfig tidak bertentangan dengan linter (ESLint, Prettier, dll.)

---

## 🔹 Integrasi dengan Tool Lain

### 🔸 Dengan Prettier

- Prettier memiliki prioritas lebih tinggi dari .editorconfig
- Jika Anda menggunakan Prettier, beberapa aturan .editorconfig akan diabaikan
- Gunakan .prettierrc untuk aturan format yang lebih kompleks

### 🔸 Dengan ESLint

- ESLint juga dapat menangani aturan format kode
- Atur konfigurasi agar tidak saling bertentangan

### 🔸 Dengan Git

- .editorconfig bisa membantu mencegah perubahan format yang tidak disengaja di commit
- Gunakan hooks Git untuk menjalankan format sebelum commit jika perlu

---

## 📌 Tips dan Trik

- EditorConfig adalah **alat konsistensi format**, bukan formatter penuh
- Untuk formatting yang lebih kompleks, gunakan formatter seperti Prettier, Black, atau clang-format
- Beberapa editor memerlukan plugin tambahan untuk mendukung .editorconfig
- Pastikan semua anggota tim menginstal plugin yang diperlukan
- Gunakan `max_line_length` untuk membatasi panjang baris agar lebih mudah dibaca
- Gunakan wildcard untuk mengelompokkan tipe file dengan aturan yang sama

---

## 🔹 Kesimpulan

`.editorconfig` adalah alat yang sangat berguna untuk menjaga konsistensi format kode dalam tim. Dengan file konfigurasi sederhana, semua anggota tim bisa menggunakan aturan format yang sama tanpa harus mengatur manual di masing-masing editor mereka. Ini membantu mengurangi konflik format dalam commit dan memastikan kode tetap konsisten di seluruh proyek.
