# Upgrade Libreoffice

Ada beberapa cara untuk upgrade **LibreOffice** di Linux Mint XFCE, tergantung kamu ingin yang paling mudah atau versi terbaru langsung dari situs resmi. Saya jelaskan opsi-opsinya ya:

---

### 🔹 1. Upgrade via Update Manager (paling aman & mudah)

Biasanya Linux Mint akan menyediakan update LibreOffice lewat repositori resmi.

1. Buka **Update Manager** (Manajer Pembaruan).
2. Klik **Refresh** untuk memperbarui daftar paket.
3. Cari **libreoffice** di daftar update.
4. Jika ada update → pilih dan klik **Install Updates**.

!> Kekurangannya: versi di repo Mint kadang tertinggal dari versi terbaru LibreOffice.

---

### 🔹 2. Upgrade via PPA Resmi LibreOffice

Kalau mau versi yang lebih baru dibanding repo Mint, gunakan PPA resmi dari tim LibreOffice:

```bash
sudo add-apt-repository ppa:libreoffice/ppa
sudo apt update
sudo apt upgrade
```

?> Setelah ini, LibreOffice akan di-upgrade ke versi terbaru yang stabil dari PPA.

---

### 🔹 3. Download versi terbaru dari situs resmi (manual)

Jika ingin versi _paling baru_ langsung dari LibreOffice:

1. Pergi ke [halaman download resmi](https://www.libreoffice.org/download/download/).
2. Pilih versi **Linux (deb)** → 64-bit.
3. Download file `.tar.gz`.
4. Ekstrak dan masuk ke folder hasil ekstrak.
5. Jalankan:

```bash
cd LibreOffice_*-Linux_x86-64_deb/DEBS
sudo dpkg -i *.deb
```

?> Cara ini memberi kamu versi terbaru, tapi update berikutnya harus dilakukan manual juga.

---

### 🔹 4. Gunakan Flatpak (selalu update ke versi terbaru)

Linux Mint sudah mendukung Flatpak. Jalankan:

```bash
flatpak install flathub org.libreoffice.LibreOffice
```

Lalu update dengan:

```bash
flatpak update
```

?> Cocok kalau kamu mau selalu punya versi terbaru tanpa repot manual.

---

<sl-alert variant="primary" open>
   👉 Jadi, kalau kamu mau <b>aman & stabil</b>, pakai cara <b>Update Manager.</b>  
   Kalau mau <b>lebih baru</b>, pilih <b>PPA</b> atau <b>Flatpak</b>.
</sl-alert>

---

## Upgrade LibreOffice via PPA di Linux Mint XFCE

1. Tambahkan PPA resmi LibreOffice:

   ```bash
   sudo add-apt-repository ppa:libreoffice/ppa
   ```

2. Perbarui daftar paket:

   ```bash
   sudo apt update
   ```

3. Upgrade LibreOffice:

   ```bash
   sudo apt upgrade libreoffice
   ```

4. Setelah selesai, cek versi yang terinstall:

   ```bash
   libreoffice --version
   ```

---

### 📌 Catatan:

- Jika sebelumnya sudah ada LibreOffice bawaan Linux Mint, cara ini akan **meng-upgrade langsung** (bukan install ganda).
- PPA ini biasanya cukup cepat dapat update dari rilis resmi LibreOffice.
