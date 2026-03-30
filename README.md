# service-management

# Alfa Comp — Panduan Install (Laravel 11 + PHP 8.3 + Laragon Terbaru)

## Prasyarat

| Kebutuhan | Versi |
|-----------|-------|
| Laragon | Full Latest (6.0+) |
| PHP | 8.3+ |
| MySQL | 8.0+ |
| Composer | 2.7+ |

Semua sudah tersedia di Laragon Full Latest. Tidak perlu install manual.

---

## Langkah 1 — Pastikan PHP 8.3 Aktif

1. Klik kanan ikon Laragon di taskbar
2. Pilih PHP → 8.3.x → Reload
3. Verifikasi: buka Terminal Laragon → ketik `php -v` → harus muncul PHP 8.3.x

---

## Langkah 2 — Buat Project Laravel 11

```bash
cd C:\laragon\www
composer create-project laravel/laravel:^11.0 alfa-comp
cd alfa-comp
php artisan --version
```
Output harus: `Laravel Framework 11.x.x`

---

## Langkah 3 — Copy File Project

Salin semua isi folder ZIP ini ke `C:\laragon\www\alfa-comp\` (replace semua):
- `app/` → `alfa-comp/app/`
- `database/` → `alfa-comp/database/`
- `resources/views/` → `alfa-comp/resources/views/`
- `routes/web.php` → `alfa-comp/routes/web.php`
- `public/css/app.css` → `alfa-comp/public/css/app.css`
- `config/auth.php` → `alfa-comp/config/auth.php`
- `bootstrap/app.php` → `alfa-comp/bootstrap/app.php`
- `bootstrap/providers.php` → `alfa-comp/bootstrap/providers.php`
- `composer.json` → `alfa-comp/composer.json`
- `.env.example` → `alfa-comp/.env.example`

---

## Langkah 4 — Install Package

```bash
composer require simplesoftwareio/simple-qrcode
composer require barryvdh/laravel-dompdf
```

---

## Langkah 5 — Setup Database

1. Buka Laragon → Start All
2. Buka HeidiSQL → buat database `alfa_comp` (charset: utf8mb4)
3. Copy .env:

```bash
copy .env.example .env
```

4. Edit `.env`:
```env
APP_NAME="Alfa Comp"
APP_URL=http://alfa-comp.test
DB_DATABASE=alfa_comp
DB_USERNAME=root
DB_PASSWORD=
```

5. Generate key:
```bash
php artisan key:generate
```

---

## Langkah 6 — Migrasi & Seed

```bash
php artisan migrate --seed
php artisan db:seed --class=SparepartSeeder
php artisan storage:link
php artisan config:clear
```

---

## Langkah 7 — Buka Browser

Akses: `http://alfa-comp.test`

Login default:
- `admin` / `password` (Admin)
- `fuad` / `password` (Teknisi)
- `resta` / `password` (Teknisi)

---

## Nota Customer vs Nota Internal

| Info | Customer | Internal |
|------|:---:|:---:|
| Data customer & unit | Yes | Yes |
| Rincian biaya (harga jual) | Yes | Yes |
| Garansi & QR Code | Yes | Yes |
| Nama Supplier | No | Yes |
| No. Invoice Supplier | No | Yes |
| Metode Bayar ke Supplier | No | Yes |
| Harga Beli Sparepart | No | Yes |
| Margin Keuntungan | No | Yes |
| Catatan Teknisi | No | Yes |

---

## Troubleshooting

**Error Class QrCode not found:**
```bash
php artisan config:clear && composer dump-autoload
```
Pastikan `bootstrap/providers.php` sudah berisi QrCodeServiceProvider.

**Error saat migrate:**
Pastikan charset database `utf8mb4` di HeidiSQL.

**php artisan tidak dikenal:**
Aktifkan PHP 8.3 di Laragon → Reload.

**Vite manifest not found:**
```bash
npm install && npm run build
```
