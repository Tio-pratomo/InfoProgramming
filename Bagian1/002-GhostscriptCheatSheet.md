# 📑 Ghostscript Cheat Sheet (PDF)

## 🔹 Apa itu Ghostscript?

**Ghostscript** adalah interpreter untuk bahasa PostScript dan PDF.  
Biasanya dipakai untuk:

- Mengubah file PDF ke gambar (JPG/PNG)
- Mengompres ukuran file PDF
- Menggabungkan / memisahkan PDF
- Konversi PostScript (.ps) ↔ PDF

***

## 🔹 Instalasi Ghostscript

Di Linux Mint, cukup:

```bash
sudo apt update
sudo apt install ghostscript
```

### 🔹 Cek Versi

```bash
gs --version
```

## 🔹 Konversi PDF → Gambar

```bash
gs -sDEVICE=png16m -r300 -o out.png in.pdf
```

- `png16m` = PNG warna
- `-r300` = resolusi 300 DPI  
- Output multi-halaman jadi `out-1.png`, `out-2.png`, ...

***

## 🔹 Kompres PDF

```bash
gs -sDEVICE=pdfwrite -dCompatibilityLevel=1.4 \
   -dPDFSETTINGS=/ebook -o out.pdf in.pdf
```

Mode kualitas (`-dPDFSETTINGS`):

- `/screen` → sangat kecil (72 dpi, presentasi)
- `/ebook` → sedang (150 dpi, default)
- `/printer` → tinggi (300 dpi)
- `/prepress` → sangat tinggi (publikasi)

***

## 🔹 Gabung Beberapa PDF

```bash
gs -dBATCH -dNOPAUSE -q -sDEVICE=pdfwrite \
   -sOutputFile=merged.pdf file1.pdf file2.pdf
```

## 🔹 Ambil Range Halaman

```bash
gs -sDEVICE=pdfwrite -dFirstPage=2 -dLastPage=5 \
   -o out.pdf in.pdf
```

👉 Menyimpan hanya halaman 2–5

## 🔹 Hapus Semua Metadata

```bash
gs -sDEVICE=pdfwrite -dNOPAUSE -dQUIET -dBATCH \
   -sOutputFile=clean.pdf in.pdf
```

## 🔹 Konversi PostScript → PDF

```bash
gs -sDEVICE=pdfwrite -o out.pdf in.ps
```

## 🔹 Konversi PDF → PostScript

```bash
gs -sDEVICE=ps2write -o out.ps in.pdf
```

***

## 📌 Tips

- `-o out.pdf` = cara singkat menulis `-sOutputFile=out.pdf`
- `-q` = quiet mode (minim output di terminal)
- `-dBATCH -dNOPAUSE` = otomatis selesai tanpa prompt interaktif