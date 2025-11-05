# XDEBUG SETUP GUIDE - SIMPLIFIED

## ⚡ Ringkasan Singkat

Saya berasumsi Anda **sudah punya XDebug v3.4.5** di PHP 8.4.11 (terbaru) via phpenv. Tinggal:

1. Configure `php.ini`
2. Install VS Code extension
3. Create `launch.json`
4. Done! ✅

---

## Step 1: Konfigurasi `php.ini`

### Temukan lokasi `php.ini`

```bash
php -i | grep "php.ini" | grep "Loaded Configuration"
```

Output akan seperti:

```
Loaded Configuration File => /home/sulis/.phpenv/versions/8.4.11/etc/php.ini
```

### Edit php.ini

- Arahkan ke path : `/home/sulis/.phpenv/versions/8.4.11/etc/php.ini`
- Gunakan vscode atau editor yang kalian gunakan, untuk mengedit file `php.ini`

Bisa juga menggunakan `nano` bawaan linux

```bash
nano /home/sulis/.phpenv/versions/8.4.11/etc/php.ini
```

### Tambahkan Konfigurasi XDebug

Scroll ke akhir file, tambahkan:

```ini
; ===== XDEBUG CONFIGURATION =====
[xdebug]
xdebug.mode=debug
xdebug.start_with_request=trigger
xdebug.client_port=9003
xdebug.client_host=127.0.0.1
xdebug.idekey=vscode
```

**Penjelasan**:

- `mode=debug` → Enable debugging
- `start_with_request=trigger` → Hanya aktif saat ada trigger (XDEBUG_TRIGGER)
- `client_port=9003` → Port untuk komunikasi dengan VS Code
- `client_host=127.0.0.1` → Localhost (development machine)
- `idekey=vscode` → Identifier untuk VS Code

### Save dan Exit

- Tekan `Ctrl+X` → `Y` → `Enter`

### Verifikasi Konfigurasi

```bash
php -v
```

Output harus menampilkan:

```
PHP 8.4.11 (cli) (built: Aug 19 2025 13:22:26) (NTS)
with Zend OPcache v8.4.11
with Xdebug v3.4.5
```

✅ Jika muncul "with Xdebug", XDebug sudah configured!

---

## Step 2: Install VS Code Extension

### Via Command Line (Fastest)

```bash
code --install-extension xdebug.php-debug
```

### Atau Via VS Code UI

1. Press `Ctrl+Shift+X`
2. Search "PHP Debug"
3. Click **Install**

---

## Step 3: Buat launch.json

### Buat Folder `.vscode`

```bash
cd /home/sulis/Desktop/CobaPHP
mkdir -p .vscode
```

### Buat `launch.json`

```bash
cat > .vscode/launch.json << 'EOF'
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Listen for Xdebug",
      "request": "launch",
      "type": "php",
      "port": 9003
    },
    {
      "name": "Launch currently open script",
      "type": "php",
      "request": "launch",
      "program": "${file}",
      "cwd": "${fileDirname}",
      "port": 9003
    }
  ]
}
EOF
```

### Verify No Errors

1. Buka `.vscode/launch.json` di VS Code
2. Tidak boleh ada red squiggles ❌
3. Save dengan `Ctrl+S` ✅

---

## Step 4: Test Debugging

### Create Test File

```bash
cd /home/sulis/Desktop/CobaPHP

cat > debug_test.php << 'EOF'
<?php
$name = "Sulis";
$age = 25;
$cities = ["Jakarta", "Bandung", "Surabaya"];

echo "Name: " . $name . PHP_EOL;
echo "Age: " . $age . PHP_EOL;
echo "Cities: " . implode(", ", $cities) . PHP_EOL;
EOF
```

### Test Method 1: CLI with Trigger (Recommended for Learning)

**Terminal 1: Start Listening**

1. Buka `debug_test.php` di VS Code
2. Tekan `F5`
3. Pilih "Listen for Xdebug"
4. Status bar akan berubah warna (orange) → Listening ✅

**Terminal 2: Run Script with Trigger**

```bash
cd /home/sulis/Desktop/CobaPHP
XDEBUG_TRIGGER=1 php debug_test.php
```

**What Happens:**

- Script akan pause di line pertama
- VS Code akan menampilkan variables di left panel
- Anda bisa step through code

### Test Method 2: Direct Launch from VS Code

1. Buka `debug_test.php` di VS Code
2. Tekan `F5`
3. Pilih "Launch currently open script"
4. Script akan run langsung dengan debug

---

## How to Use Breakpoints

### Set Breakpoint

Klik di **nomor baris** (sebelah kiri) → Red dot akan muncul

### Step Through Code

Saat execution pause:

- **F10** = Step over (baris selanjutnya)
- **F11** = Step into (masuk ke function)
- **Shift+F11** = Step out (keluar dari function)
- **F5** = Continue (lanjut sampai breakpoint berikutnya)

### Inspect Variables

Di **Variables panel** (left side) Anda bisa lihat:

- Local variables
- Superglobals ($\_GET, $\_POST, dll)
- Watch expressions

---

## For Web Debugging (PHP Built-in Server)

### Terminal 1: Start PHP Server

```bash
cd /home/sulis/Desktop/CobaPHP
php -S localhost:8000
```

### Terminal 2: Start Listening in VS Code

1. Tekan `F5`
2. Pilih "Listen for Xdebug"
3. Status bar orange = listening

### Browser: Trigger Debug

Visit dengan query parameter:

```
http://localhost:8000/debug_test.php?XDEBUG_TRIGGER=1
```

Atau install **Xdebug Helper** browser extension (Chrome/Firefox) untuk easier trigger.

---

## Troubleshooting

### Problem: "No Connection" or Timeout

**Check 1: XDebug installed?**

```bash
php -m | grep xdebug
php -v | grep -i xdebug
```

Both harus menampilkan xdebug.

**Check 2: php.ini configured?**

```bash
php -i | grep "xdebug.mode"
php -i | grep "xdebug.client_port"
```

Harus output:

```
xdebug.mode => debug => debug
xdebug.client_port => 9003 => 9003
```

**Check 3: VS Code listening?**
Status bar di bawah seharusnya show "Listen for Xdebug" dengan warna orange.

**Check 4: Enable logging for debugging**

Add ke `php.ini`:

```ini
xdebug.log=/tmp/xdebug.log
xdebug.log_level=debug
```

Then check:

```bash
tail -f /tmp/xdebug.log
```

---

## 📊 Quick Reference Card

| Action              | Command/Hotkey                             |
| ------------------- | ------------------------------------------ |
| Start Listening     | F5 → Select "Listen for Xdebug"            |
| Launch Current File | F5 → Select "Launch currently open script" |
| Step Over           | F10                                        |
| Step Into           | F11                                        |
| Step Out            | Shift+F11                                  |
| Continue            | F5                                         |
| Pause               | F6                                         |
| Stop                | Shift+F5                                   |
| Disconnect          | Shift+F5                                   |
| Set Breakpoint      | Click nomor baris                          |
| Toggle Breakpoint   | Ctrl+Shift+B                               |
| Run CLI with Debug  | `XDEBUG_TRIGGER=1 php file.php`            |
| Run Server          | `php -S localhost:8000`                    |

---

## 🎯 Checklist - Sebelum Mulai Coding

- [ ] Edit `php.ini` dengan XDebug config
- [ ] Install extension "PHP Debug" di VS Code
- [ ] Create `.vscode/launch.json` di project
- [ ] Test dengan `debug_test.php`
- [ ] Verify no errors di launch.json
- [ ] Can set breakpoint dan pause execution
- [ ] Can inspect variables
- [ ] Can step through code

---

## 🚀 You're Ready!

Sekarang Anda punya **professional PHP debugging setup** yang sama dengan developers di industri!

Setiap kali ada bug yang sulit dipahami:

1. Set breakpoint
2. F5 → Listen for Xdebug
3. Run script dengan XDEBUG_TRIGGER=1
4. Step through code
5. Inspect variables
6. Find bug! ✅

Happy debugging! 🐛⛔
