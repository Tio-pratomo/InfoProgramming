# 📚 Dokumentasi Lengkap: PHP Development Environment Setup

## 1. Install PHPEnv

### 1.1 Persyaratan

- Linux atau macOS
- Git
- Curl
- Build tools (gcc, make, autoconf)

### 1.2 Install Dependencies (Ubuntu/Debian)

```bash
sudo apt-get update
sudo apt-get install -y \
  autoconf \
  automake \
  bison \
  build-essential \
  curl \
  git \
  libbz2-dev \
  libcurl4-openssl-dev \
  libedit-dev \
  libfreetype6-dev \
  libicu-dev \
  libjpeg-dev \
  libmcrypt-dev \
  libonig-dev \
  libpng-dev \
  libreadline-dev \
  libsqlite3-dev \
  libssl-dev \
  libxml2-dev \
  libzip-dev \
  pkg-config \
  re2c \
  zlib1g-dev
```

### 1.3 Clone dan Install PHPEnv

```bash
# Clone repository
git clone https://github.com/phpenv/phpenv.git ~/.phpenv

# Tambahkan ke PATH
echo 'export PATH="$HOME/.phpenv/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(phpenv init -)"' >> ~/.bashrc

# Reload shell
source ~/.bashrc

# Verifikasi instalasi
phpenv versions
```

### 1.4 Install PHP Menggunakan PHPEnv

```bash
# Lihat daftar PHP versi yang tersedia
phpenv install --list

# Install PHP 8.4.11
phpenv install 8.4.11

# Set versi PHP sebagai global
phpenv global 8.4.11

# Verifikasi
php --version
# Output: PHP 8.4.11 (/home/user_name/.phpenv/versions/8.4.11/bin/php)
```

### 1.5 PHP Extensions (Opsional)

Jika membutuhkan extension tambahan:

```bash
# Untuk memudahkan install extension, gunakan php-build
git clone https://github.com/php-build/php-build.git ~/.phpenv/plugins/php-build
```

---

## 2. Install Composer

### 2.1 Verifikasi PHP Terinstall

```bash
php --version
# Output: PHP 8.4.11 (/home/user_name/.phpenv/versions/8.4.11/bin/php)

composer --version  # Jika sudah terinstall
# Output: Composer version 2.8.12 2025-09-19 13:41:59
# Output jika belum terinstall ⟶ command not found: composer
```

### 2.2 Download dan Install Composer

```bash
# Download installer
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"

# Verifikasi hash (penting untuk keamanan)
php -r "if (hash_file('sha384', 'composer-setup.php') === 'c8b085408188070d5f52bcfe4ecfbee5f727afa458b2573b8eaaf77b3419b0bf2768dc67c86944da1544f06fa544fd47') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); exit(1); }"

# Install Composer
php composer-setup.php

# Hapus installer
php -r "unlink('composer-setup.php');"

# Pindahkan ke /usr/local/bin (butuh sudo)
sudo mv composer.phar /usr/local/bin/composer

# Verifikasi
composer --version
```

### 2.3 Install Composer Tanpa Sudo

Jika tidak punya akses root:

```bash
mkdir -p ~/.local/bin
mv composer.phar ~/.local/bin/composer

# Tambahkan ke PATH
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc

# Verifikasi
composer --version
```

### 2.4 Composer Bekerja dengan Semua Versi PHP

Composer akan menggunakan versi PHP yang sedang aktif di `$PATH`:

```bash
# Set PHP 8.4.11 (atau versi lainnya)
phpenv global 8.4.11

# Jalankan composer (akan pakai PHP 8.4.11)
composer install

# Untuk per-project, gunakan:
cd /path/to/project
phpenv local 8.4.11  # Hanya di folder ini
composer install
```

---

## 3. Install Phpactor

### 3.1 Install via PHAR (Recommended)

```bash
# Download latest release
curl -Lo phpactor.phar https://github.com/phpactor/phpactor/releases/latest/download/phpactor.phar

# Buat executable
chmod a+x phpactor.phar

# Install ke /usr/local/bin
sudo mv phpactor.phar /usr/local/bin/phpactor

# Verifikasi
phpactor --version
# Output: Phpactor 2025.10.17.0
```

### 3.2 Install via Composer (Alternative)

```bash
# Jika ingin menggunakan composer
composer global require phpactor/phpactor

# Pastikan ~/.composer/vendor/bin ada di PATH
echo 'export PATH="$HOME/.composer/vendor/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

### 3.3 Setup Project untuk Phpactor

Di setiap project PHP Anda:

```bash
cd /home/user_name/Desktop/CobaPHP

# 1. Init Git repository
git init
git config user.name "user_name"
git config user.email "user_name@example.com"

# 2. Init Composer
composer init
# Atau langsung dengan config:
cat > composer.json << 'EOF'
{
    "name": "user_name/coba-php",
    "description": "Test project",
    "require": {},
    "require-dev": {},
    "minimum-stability": "dev"
}
EOF

composer install

# 3. Buat file konfigurasi Phpactor
cat > .phpactor.yml << 'EOF'
# Phpactor configuration untuk project ini
language_server_phpstan.enabled: false
language_server_psalm.enabled: false
EOF

# 4. Init Git dengan .gitignore
echo "vendor/" > .gitignore
git add .
git commit -m "Initial commit"

# 5. Index project
phpactor index:build
```

### 3.4 Check Status Phpactor

```bash
cd /home/user_name/Desktop/CobaPHP
phpactor status

# Output yang diharapkan:
# Version: 2025.10.17.0
# ✔ XDebug is disabled
# ✔ Composer detected
# ✔ Git detected
# ✔ Path is trusted
```

---

## 4. Install VS Code Extensions (Optional Namun Disarankan)

### 4.1 Install via Command Line

```bash
# Phpactor Action (untuk refactoring & code actions)
code --install-extension andresmeireles.phpactor-action

# Intelephense (untuk autocomplete & IntelliSense)
code --install-extension bmewburn.vscode-intelephense-client

# Prettier (untuk code formatting)
code --install-extension esbenp.prettier-vscode

# Material Icon Theme (recommended, sesuai setting Anda)
code --install-extension pkief.material-icon-theme

# Indent Rainbow (recommended, untuk visualisasi indent)
code --install-extension oderwat.indent-rainbow

# Mayukai Dark Theme (recommended, sesuai setting Anda)
# Note: Install manual via VS Code marketplace
```

### 4.2 Install via VS Code UI

1. Tekan `Ctrl+Shift+X`
2. Cari extension name di atas
3. Klik Install

### 4.3 Disable Built-in PHP Extension

Untuk menghindari konflik:

1. Tekan `Ctrl+Shift+X`
2. Ketik `@builtin php`
3. Pada "PHP Language Features", klik icon gear
4. Pilih "Disable"
5. Reload VS Code (`Ctrl+Shift+P` → "Reload Window")

---

## 5. Project Setup

### 5.1 Struktur Project Lengkap

```
/home/user_name/Desktop/CobaPHP/
├── .git/                          # Git repository
├── .gitignore                     # Git ignore file
├── .phpactor.yml                  # Phpactor config
├── .prettierrc                    # Prettier config
├── .prettierignore                # Prettier ignore file
├── composer.json                  # PHP dependencies
├── composer.lock                  # Lock file (auto-generated)
├── package.json                   # Node dependencies
├── package-lock.json              # Lock file (auto-generated)
├── node_modules/                  # Node packages
│   ├── prettier/
│   ├── @prettier/plugin-php/
│   └── ...
├── vendor/                        # PHP packages (auto-generated)
│   ├── autoload.php
│   └── ...
├── src/                           # Source code
│   ├── Controller/
│   ├── Model/
│   └── Utils/
└── public/
    └── index.php                  # Entry point
```

### 5.2 Setup Prettier untuk PHP

```bash
cd /home/user_name/Desktop/CobaPHP

# Install Prettier dan plugin PHP
npm install --save-dev prettier @prettier/plugin-php

# Buat file .prettierrc
cat > .prettierrc << 'EOF'
{
  "plugins": ["@prettier/plugin-php"],
  "phpVersion": "8.4",
  "printWidth": 100,
  "tabWidth": 4,
  "useTabs": false,
  "singleQuote": true,
  "trailingCommaPHP": true,
  "braceStyle": "per-cs"
}
EOF

# Buat file .prettierignore
cat > .prettierignore << 'EOF'
vendor/
node_modules/
*.min.js
*.min.css
EOF
```

### 5.3 Initialize Project dari Awal (Optional)

Script lengkap untuk setup project baru:

```bash
#!/bin/bash
# setup-project.sh

PROJECT_NAME="coba-php"
PROJECT_PATH="/home/user_name/Desktop/$PROJECT_NAME"

# Buat folder
mkdir -p "$PROJECT_PATH"
cd "$PROJECT_PATH"

# Git setup
git init
git config user.name "user_name"
git config user.email "user_name@example.com"

# Composer setup
cat > composer.json << 'EOF'
{
    "name": "user_name/coba-php",
    "description": "PHP Project",
    "require": {
        "php": "^8.4"
    },
    "require-dev": {},
    "autoload": {
        "psr-4": {
            "App\\": "src/"
        }
    },
    "minimum-stability": "dev"
}
EOF

# PHP stubs untuk Intelephense
composer require --dev jetbrains/phpstorm-stubs

# Phpactor config
cat > .phpactor.yml << 'EOF'
language_server_worse_reflection.stub_dir: "%project_root%/vendor/jetbrains/phpstorm-stubs"
language_server_phpstan.enabled: false
language_server_psalm.enabled: false
EOF

# NPM/Prettier setup
cat > package.json << 'EOF'
{
  "name": "coba-php",
  "version": "1.0.0",
  "devDependencies": {
    "@prettier/plugin-php": "^0.22.0",
    "prettier": "^3.0.0"
  }
}
EOF

npm install

# Prettier config
cat > .prettierrc << 'EOF'
{
  "plugins": ["@prettier/plugin-php"],
  "phpVersion": "8.4",
  "printWidth": 100,
  "tabWidth": 4,
  "useTabs": false,
  "singleQuote": true,
  "trailingCommaPHP": true,
  "braceStyle": "per-cs"
}
EOF

# Git ignore
cat > .gitignore << 'EOF'
vendor/
node_modules/
composer.lock
.DS_Store
.vscode/workspace
*.swp
*.swo
*~
EOF

# Create directories
mkdir -p src public

# Initial commit
git add .
git commit -m "Initial commit: PHP dev environment setup"

# Build Phpactor index
phpactor index:build

echo "✅ Project setup complete!"
echo "📁 Location: $PROJECT_PATH"
echo "🚀 Ready to code!"
```

Jalankan script:

```bash
chmod +x setup-project.sh
./setup-project.sh
```

---

## 6. VS Code Configuration (Optional)

### 6.1 Complete settings.json

Buka `Ctrl+Shift+P` → "Preferences: Open User Settings (JSON)", kemudian copy-paste:

```json
{
  // ===== UI Theme =====
  "workbench.colorTheme": "Mayukai Dark",
  "workbench.iconTheme": "material-icon-theme",

  // ===== Editor Global Settings =====
  "editor.formatOnSave": true,
  "editor.minimap.enabled": false,
  "editor.multiCursorModifier": "ctrlCmd",
  "editor.tabSize": 2,
  "editor.insertSpaces": true,
  "editor.trimAutoWhitespace": true,

  // ===== File Settings =====
  "files.associations": {
    "*.html": "html"
  },
  "files.trimTrailingWhitespace": true,
  "files.insertFinalNewline": true,

  // ===== Emmet =====
  "emmet.includeLanguages": {
    "markdown": "html"
  },

  // ===== JavaScript/TypeScript =====
  "javascript.suggest.paths": false,
  "typescript.suggest.paths": false,

  // ===== Indent Rainbow =====
  "indentRainbow.indicatorStyle": "light",
  "indentRainbow.lightIndicatorStyleLineWidth": 2,

  // ===== Prettier Configuration =====
  "prettier.documentSelectors": ["**/*.{js,jsx,ts,tsx,vue,html,css,scss,less,json,md,mdx,graphql,yaml,yml,php}"],
  "prettier.printWidth": 100,
  "prettier.tabWidth": 4,
  "prettier.useTabs": false,
  "prettier.singleQuote": true,
  "prettier.trailingComma": "es5",

  // ===== PHP General Settings =====
  "php.suggest.basic": false,
  "php.validate.enable": false,
  "[php]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode",
    "editor.formatOnSave": true,
    "editor.formatOnPaste": true,
    "editor.tabSize": 4,
    "editor.insertSpaces": true,
    "editor.rulers": [100, 120],
    "editor.quickSuggestions": {
      "other": true,
      "comments": false,
      "strings": true
    }
  },

  // ===== Intelephense Configuration =====
  "intelephense.format.enable": false,
  "intelephense.files.maxSize": 5000000,
  "intelephense.completion.insertUseDeclaration": true,
  "intelephense.completion.fullyQualifyGlobalConstantsAndFunctions": false,
  "intelephense.diagnostics.enable": true,
  "intelephense.telemetry.enabled": false,
  "intelephense.stubs": [
    "apache",
    "bcmath",
    "bz2",
    "calendar",
    "com_dotnet",
    "Core",
    "ctype",
    "curl",
    "date",
    "dba",
    "dom",
    "enchant",
    "exif",
    "FFI",
    "fileinfo",
    "filter",
    "fpm",
    "ftp",
    "gd",
    "gettext",
    "gmp",
    "hash",
    "iconv",
    "imap",
    "intl",
    "json",
    "ldap",
    "libxml",
    "mbstring",
    "meta",
    "mysqli",
    "oci8",
    "odbc",
    "openssl",
    "pcntl",
    "pcre",
    "PDO",
    "pdo_ibm",
    "pdo_mysql",
    "pdo_pgsql",
    "pdo_sqlite",
    "pgsql",
    "Phar",
    "posix",
    "pspell",
    "readline",
    "Reflection",
    "session",
    "shmop",
    "SimpleXML",
    "snmp",
    "soap",
    "sockets",
    "sodium",
    "SPL",
    "sqlite3",
    "standard",
    "superglobals",
    "sysvmsg",
    "sysvsem",
    "sysvshm",
    "tidy",
    "tokenizer",
    "xml",
    "xmlreader",
    "xmlrpc",
    "xmlwriter",
    "xsl",
    "Zend OPcache",
    "zip",
    "zlib"
  ],

  // ===== Phpactor Configuration =====
  "phpactor-action.enabled": true,
  "phpactor-action.phpactorBinPath": "/usr/local/bin/phpactor",

  // ===== Language-Specific Formatting =====
  "[html]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[css]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[javascript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[javascriptreact]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[typescript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[json]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[jsonc]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[markdown]": {
    "editor.quickSuggestions": {
      "other": true,
      "comments": true,
      "strings": true
    },
    "diffEditor.ignoreTrimWhitespace": false
  }
}
```

### 6.2 Workspace Settings (Per-Project) (Optional)

Buat file `.vscode/settings.json` di folder project:

```bash
mkdir -p .vscode
cat > .vscode/settings.json << 'EOF'
{
  "[php]": {
    "editor.tabSize": 4,
    "editor.defaultFormatter": "esbenp.prettier-vscode",
    "editor.formatOnSave": true
  },
  "phpactor-action.phpactorBinPath": "/usr/local/bin/phpactor"
}
EOF
```

---

## 7. Troubleshooting

### 7.1 Phpactor Tidak Terdeteksi di VS Code

**Masalah**: Extension tidak bekerja atau autocomplete tidak muncul

**Solusi**:

```bash
# 1. Verifikasi Phpactor terinstall
which phpactor
phpactor --version

# 2. Check path di settings
# Pastikan "phpactor-action.phpactorBinPath" sesuai dengan output `which phpactor`

# 3. Reload VS Code
Ctrl+Shift+P → "Developer: Reload Window"

# 4. Check output log
Ctrl+Shift+U → Pilih "Phpactor" dari dropdown
```

### 7.2 Intelephense Tidak Show Built-in Functions

**Masalah**: Autocomplete untuk `echo`, `PHP_EOL`, dll tidak muncul

**Solusi**:

```bash
# 1. Install PHP stubs di project
cd /home/user_name/Desktop/CobaPHP
composer require --dev jetbrains/phpstorm-stubs

# 2. Configure Phpactor untuk menggunakan stubs
nano .phpactor.yml
# Tambahkan:
# language_server_worse_reflection.stub_dir: "%project_root%/vendor/jetbrains/phpstorm-stubs"

# 3. Rebuild Phpactor index
phpactor index:reset
phpactor index:build

# 4. Reload VS Code
Ctrl+Shift+P → "Reload Window"
```

### 7.3 Prettier Tidak Format PHP Files

**Masalah**: Format on save tidak bekerja untuk PHP

**Solusi**:

```bash
# 1. Pastikan prettier dan plugin terinstall
cd /home/user_name/Desktop/CobaPHP
npm ls prettier @prettier/plugin-php

# 2. Pastikan .prettierrc ada
ls -la .prettierrc

# 3. Test prettier dari CLI
npx prettier test.php --write

# 4. Jika CLI berhasil tapi VS Code tidak:
# - Reload VS Code
# - Check Output panel (Prettier)
# - Verifikasi defaultFormatter di settings.json
```

### 7.4 Composer Warning Root Package Version

**Masalah**: Peringatan "Composer could not detect the root package version"

**Solusi**:

```bash
# Opsi 1: Buat branch alias di composer.json
nano composer.json
# Tambahkan:
# "extra": {
#   "branch-alias": {
#     "dev-main": "1.0-dev"
#   }
# }

# Opsi 2: Set environment variable
COMPOSER_ROOT_VERSION=1.0.0 composer install

# Opsi 3: Buat git tag
git tag -a v1.0.0 -m "Version 1.0.0"
```

### 7.5 Permission Denied pada phpactor

**Masalah**: "Permission denied" saat menjalankan phpactor

**Solusi**:

```bash
# Pastikan phpactor executable
chmod +x /usr/local/bin/phpactor

# Verifikasi
phpactor --version
```

---

## 8. Quick Command Reference

### PHPEnv Commands

```bash
# List terinstall versions
phpenv versions

# Install PHP versi tertentu
phpenv install 8.4.11

# Set global PHP version
phpenv global 8.4.11

# Set local PHP version (per-folder)
phpenv local 8.4.11

# Set session PHP version (temporary)
phpenv shell 8.4.11

# Rehash
phpenv rehash
```

### Composer Commands

```bash
# Initialize project
composer init

# Install dependencies
composer install

# Install dengan lock file
composer install --prefer-locked

# Update dependencies
composer update

# Require package
composer require vendor/package

# Require dev package
composer require --dev vendor/package

# Clear cache
composer clear-cache

# Diagnose issues
composer diagnose

# Check version
composer --version
```

### Phpactor Commands

```bash
# Check status
phpactor status

# Build index
phpactor index:build

# Reset index
phpactor index:reset

# Search symbol
phpactor index:search --short-name echo

# Get version
phpactor --version
```

### VS Code Shortcuts

```
Ctrl+Shift+X          - Buka Extensions
Ctrl+,                - Buka Settings
Ctrl+Shift+P          - Command Palette
Shift+Alt+F           - Format Document
Ctrl+K Ctrl+F         - Format Selection
F12                   - Go to Definition
Ctrl+Shift+O          - Go to Symbol
Shift+F12             - Find All References
F2                    - Rename Symbol
Ctrl+Shift+U          - Output Panel
Ctrl+Shift+L          - Select All Occurrences
```

### NPM Commands (untuk Prettier)

```bash
# Install dependencies
npm install

# Format semua PHP files
npx prettier . --write --parser php

# Format file tertentu
npx prettier test.php --write

# Check format (tanpa write)
npx prettier test.php --check
```

---

## 9. Environment Verification Checklist

Jalankan checklist ini untuk verifikasi semua sudah terinstall dengan benar:

```bash
#!/bin/bash
echo "=== PHP Development Environment Verification ==="
echo ""

echo "1. PHP Version:"
php --version
echo ""

echo "2. PHPEnv:"
phpenv --version
echo "   Available versions:"
phpenv versions
echo ""

echo "3. Composer:"
composer --version
echo ""

echo "4. Phpactor:"
phpactor --version
echo ""

echo "5. Node.js (untuk Prettier):"
node --version
npm --version
echo ""

echo "6. VS Code:"
code --version
echo ""

echo "7. VS Code Extensions:"
code --list-extensions | grep -E "phpactor|intelephense|prettier|material-icon"
echo ""

echo "✅ Verification Complete!"
```

Simpan sebagai `verify-env.sh` dan jalankan:

```bash
chmod +x verify-env.sh
./verify-env.sh
```

---

## 10. Quick Start untuk Project Baru

Setiap kali membuat project PHP baru, gunakan command berikut:

```bash
# 1. Buat folder project
mkdir -p ~/Projects/my-project && cd ~/Projects/my-project

# 2. Init Git
git init
git config user.name "user_name"
git config user.email "user_name@example.com"

# 3. Init PHP Project
cat > composer.json << 'EOF'
{
  "name": "user_name/my-project",
  "require": {"php": "^8.4"},
  "autoload": {"psr-4": {"App\\": "src/"}}
}
EOF

composer install
npm install --save-dev prettier @prettier/plugin-php

# 4. Create config files
cat > .phpactor.yml << 'EOF'
language_server_worse_reflection.stub_dir: "%project_root%/vendor/jetbrains/phpstorm-stubs"
EOF

cat > .prettierrc << 'EOF'
{"plugins": ["@prettier/plugin-php"], "phpVersion": "8.4", "tabWidth": 4}
EOF

# 5. Init Git
mkdir -p src
echo "vendor/" > .gitignore
git add . && git commit -m "Initial setup"

# 6. Build index
phpactor index:build

# 7. Open in VS Code
code .
```

---

**Dokumentasi ini lengkap mencakup semua yang sudah Anda setup!** Anda bisa print atau save dokumentasi ini untuk referensi ke depannya. 🎉
