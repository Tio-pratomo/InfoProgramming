# Catatan Instalasi & Setup MariaDB (Linux)

## 1. Download MariaDB

- Untuk mendapatkan versi terbaru MariaDB **Community Edition**, unduh file `.tar` berisi paket `.deb` dari repo resmi:

  ```bash
  wget https://dlm.mariadb.com/4425371/MariaDB/mariadb-11.8.3/repo/ubuntu/mariadb-11.8.3-ubuntu-noble-amd64-debs.tar
  ```

- Ekstrak:

  ```bash
  tar -xvf mariadb-11.8.3-ubuntu-noble-amd64-debs.tar
  cd mariadb-11.8.3-ubuntu-noble-amd64-debs
  ```

- Install semua paket:

  ```bash
  sudo apt install ./*.deb
  ```

---

## 2. Menjalankan MariaDB

- Start & enable service:

  ```bash
  sudo systemctl start mariadb
  sudo systemctl enable mariadb
  ```

- Cek status:

  ```bash
  systemctl status mariadb
  ```

    <sl-alert variant="success" open>
        <sl-icon slot="icon" name="check2-circle"></sl-icon>
        <strong>Jika <i>Active (running)</i> berarti MariaDB sudah berjalan.</strong>
    </sl-alert>

---

## 3. ColumnStore (Opsional)

- Saat instalasi, ada komponen **mariadb-columnstore**.
- Jika tidak dibutuhkan, biarkan service-nya **disabled/masked**.
  Ini khusus untuk analitik data skala besar, bukan kebutuhan umum development.
- Oleh karena itu jika muncul Error seperti:

  <sl-alert variant="danger" open>
    <sl-icon slot="icon" name="exclamation-octagon"></sl-icon>
    <strong>Failed to start mariadb-columnstore.service: Unit mariadb-columnstore.service is masked</strong>
  </sl-alert>

  bisa diabaikan bila Anda tidak butuh ColumnStore.

---

## 4. Secure Installation

Jalankan:

```bash
sudo mysql_secure_installation
```

Option yang muncul:

1. **Enter current password for root (Enter for none)** → tekan **Enter**.
2. **Switch to unix_socket authentication \[Y/n]**

   - **Y**: login root hanya bisa dari sistem Linux via `sudo mysql`.
   - **N**: Anda bisa set password root database.
   - Untuk server production → biasanya pilih **N** (pakai password).
   - Untuk laptop development → bisa pilih **Y** (lebih praktis).

3. **Set root password?** → jika sebelumnya pilih `N`, di sini Anda diminta membuat password root.
4. **Remove anonymous users? \[Y/n]** → pilih **Y** (keamanan).
5. **Disallow root login remotely? \[Y/n]** → pilih **Y** (server production), **N** kalau butuh remote root (jarang disarankan).
6. **Remove test database and access to it? \[Y/n]** → pilih **Y**.
7. **Reload privilege tables now? \[Y/n]** → pilih **Y**.

---

## 5. Membuat User untuk Development

Setelah login ke MariaDB:

```bash
sudo mariadb
```

Buat user khusus untuk development:

```sql
CREATE USER 'devuser'@'localhost' IDENTIFIED BY 'passwordku';
GRANT ALL PRIVILEGES ON *.* TO 'devuser'@'localhost' WITH GRANT OPTION;
FLUSH PRIVILEGES;
```

**Penjelasan Kode**:

- `CREATE USER 'devuser'@'localhost' IDENTIFIED BY 'passwordku';` membuat akun baru bernama devuser dan menetapkan kata sandinya menjadi 'passwordku' untuk autentikasi akun tersebut.
- Bagian '@'localhost'' membatasi agar devuser hanya dapat terhubung dari host lokal, bukan dari jaringan lain atau publik.
- `GRANT ALL PRIVILEGES ON *.* TO 'devuser'@'localhost' WITH GRANT OPTION;` memberikan semua hak atas semua database dan tabel, dan WITH GRANT OPTION membuat devuser bisa meneruskan/menugaskan hak tersebut ke akun lain, yang berisiko bila tidak benar-benar diperlukan.
- `FLUSH PRIVILEGES;` memuat ulang tabel hak akses agar perubahan hak segera berlaku, dan umum dijalankan setelah operasi CREATE USER/GRANT.

<sl-alert variant="neutral" open>
  <sl-icon slot="icon" name="info-circle"></sl-icon>
  <strong><code>passwordku</code> merupakan password anda untuk masuk ke mariadb.</strong><br/>
  <strong>Jadi, ganti dengan password sesuai preferensi kamu</strong>
  
</sl-alert>

**Login dengan user baru:**

```bash
mariadb -u devuser -p
```

<sl-alert variant="primary" open>
  <sl-icon slot="icon" name="info-circle"></sl-icon>
  <strong>Untuk server production: sebaiknya jangan pakai `ALL PRIVILEGES`.</strong><br />
  <strong>Gunakan hak akses lebih terbatas sesuai kebutuhan database.</strong>
</sl-alert>

---

## 6. Export & Import Database

Jika nanti pindah ke server:

- **Export** dari lokal:

  ```bash
  mysqldump -u devuser -p namadb > namadb.sql
  ```

- **Import** ke server:

  ```bash
  mysql -u devuser -p namadb < namadb.sql
  ```

---

## 7. Versi MariaDB

- Yang terpasang: **MariaDB 11.8.3 Community Server (Stable, LTS)** → versi terbaru saat ini.
- **Gratis & open-source**.
- Enterprise Edition hanya perlu jika butuh support resmi & fitur tambahan.

---

# Rangkuman

1. **Install** dari `.tar` → ekstrak `.deb` → `apt install`.
2. **ColumnStore** error bisa diabaikan (opsional, bukan untuk umum).
3. **Secure installation** penting untuk keamanan, meski di laptop bisa pilih opsi praktis (unix socket, skip remote, dll).
4. **Buat user development** agar tidak selalu pakai root.
5. **Export/import** database mudah dilakukan dengan `mysqldump`.
6. Versi yang terpasang (11.8.3) adalah **versi Community terbaru & gratis**.
