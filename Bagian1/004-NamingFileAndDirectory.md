
### Aturan 1: Jangan Gunakan Spasi
Spasi dalam nama file dan direktori mungkin terlihat lebih mudah dibaca oleh pengguna biasa, tetapi dapat menyebabkan masalah serius. Secara khusus, saat kita bekerja dengan *command line* atau terminal, spasi memiliki arti. Alat-alat ini sering mengasumsikan bahwa spasi berarti beralih ke bagian lain dari perintah, bukan bagian dari nama file yang sama.

Untuk mengatasi file dengan spasi, kita harus menambahkan karakter tambahan yang disebut *escape characters* atau membungkusnya dengan tanda kutip. Contoh lain adalah dalam pengembangan web. Spasi tidak valid dalam URL dan harus diganti dengan karakter `%20`. Mengatasi spasi dalam nama file setidaknya merepotkan, dan paling buruk dapat merusak perintah atau kode Anda.

Sebagai gantinya, para profesional biasanya menggunakan salah satu dari opsi berikut untuk nama yang terdiri dari beberapa kata:
*   **Underscores (Garis Bawah)**: Ini mungkin yang paling umum. Contoh: `my_project_file.py`.
*   **Hyphens (Tanda Hubung)**: Pilihan populer untuk file web, meskipun beberapa alat dan bahasa pemrograman mungkin menganggapnya sebagai operator pengurangan. Contoh: `my-project-file.py`.
*   **camelCase**: Tidak ada pemisah antar kata. Kata pertama dimulai dengan huruf kecil, dan setiap kata berikutnya dimulai dengan huruf kapital. Contoh: `myProjectFile.py`.
*   **PascalCase**: Juga disebut *UpperCamelCase*. Setiap kata, termasuk yang pertama, dimulai dengan huruf kapital. Contoh: `MyProjectFile.py`.

### Aturan 2: Hindari Karakter Khusus
Selain spasi, hindari karakter khusus. Karakter yang paling aman adalah huruf A-Z, angka 0-9, dan garis bawah (`_`). Tanda hubung (`-`) biasanya aman, tetapi hindari karakter seperti tanda seru (`!`), dolar (`$`), dan sejenisnya karena berisiko. Karakter-karakter tersebut mungkin memiliki arti khusus pada alat atau perangkat lunak yang berbeda dan dapat menyebabkan masalah.

Karakter titik (`.`) adalah kasus khusus. Titik digunakan untuk menandai *file extension* (misalnya `.txt`, `.py`) dan untuk membuat file tersembunyi (misalnya `.env`). Gunakan titik hanya untuk tujuan tersebut.

### Aturan 3: Deskriptif namun Ringkas
Menamai sesuatu adalah sebuah seni. Kita ingin memilih nama yang cukup deskriptif agar jelas bagi orang lain, tetapi tidak terlalu panjang sehingga sulit untuk diketik.
*   **Contoh Buruk**: `file1.txt`, `data.csv`, `script.py`
*   **Contoh Baik**: `user_profiles.csv`, `calculate_monthly_report.py`

Jika Anda melakukannya dengan baik, diri Anda di masa depan dan rekan kerja Anda akan berterima kasih atas nama yang jelas dan deskriptif.

### Aturan 4: Perhatikan Sensitivitas Huruf (Case Sensitivity)
Dalam dunia teknologi profesional, penggunaan huruf besar dan kecil sering kali penting. `File.txt` tidak sama dengan `file.txt` di banyak sistem (terutama di server berbasis Linux). Untuk menghindari frustrasi, selalu asumsikan bahwa penulisan huruf besar dan kecil itu penting. Jika ragu, gunakan huruf kecil secara konsisten, karena ini adalah konvensi yang paling umum.

### Aturan 5: Gunakan Format Tanggal yang Benar
Terkadang, menyertakan tanggal dalam nama file sangat berguna, seperti untuk file log atau data laporan harian. Agar file dapat diurutkan secara kronologis dengan benar, selalu gunakan format **YYYY-MM-DD** (Tahun-Bulan-Tanggal).

*   **Contoh Buruk (Tidak akan terurut dengan benar)**:
    *   `report_12-25-2024.csv`
    *   `report_jan_10_2025.csv`
*   **Contoh Baik (Akan terurut dengan benar)**:
    *   `report_2024-12-25.csv`
    *   `report_2025-01-10.csv`

Format `YYYY-MM-DD` memastikan bahwa pengurutan berdasarkan abjad sama dengan pengurutan kronologis.

### Aturan Bonus: Jadilah Konsisten
Setelah Anda memutuskan pola penamaan dalam sebuah proyek, tetaplah menggunakannya. Dalam tim pengembangan perangkat lunak profesional, sering kali ada panduan gaya (*style guides*) yang menentukan cara menamai dan mengatur file. Jika Anda tidak konsisten, Anda akan menyulitkan rekan kerja Anda.

### Poin Penting dari Transkrip

Berikut adalah poin-poin utama yang bisa dipelajari dari transkrip tersebut:
*   **Hindari Spasi**: Spasi dapat merusak skrip dan *command line*. Gunakan pemisah alternatif seperti `_` (underscore), `-` (hyphen), **camelCase**, atau **PascalCase**.
*   **Hindari Karakter Khusus**: Hanya gunakan huruf (a-z), angka (0-9), garis bawah, dan tanda hubung. Karakter lain seperti `!`, `@`, `#`, `$` berisiko menimbulkan masalah.
*   **Buat Nama yang Jelas**: Nama file harus cukup deskriptif untuk menjelaskan isinya tetapi tetap ringkas agar mudah diketik.
*   **Asumsikan *Case-Sensitive***: Selalu anggap bahwa huruf besar dan kecil berbeda (`File.txt` ≠ `file.txt`), terutama saat bekerja di lingkungan server. Menggunakan huruf kecil secara konsisten adalah praktik yang aman.
*   **Gunakan Format Tanggal Standar**: Untuk menyertakan tanggal, gunakan format **YYYY-MM-DD** (contoh: `2025-10-30`) agar file dapat diurutkan dengan benar.
*   **Konsistensi adalah Kunci**: Pilih satu standar penamaan untuk proyek Anda dan patuhi aturan tersebut secara konsisten untuk memudahkan kolaborasi dan pemeliharaan.
