# WordPress Dokploy Deployment

Deploy WordPress menggunakan Docker Compose di Dokploy dengan metode Git.

## Konfigurasi PHP

File `uploads.ini` sudah dikonfigurasi dengan:

| Setting | Value |
|---------|-------|
| `memory_limit` | 512M |
| `upload_max_filesize` | 512M |
| `post_max_size` | 512M |
| `max_execution_time` | 600s |
| `max_input_time` | 600s |
| `max_input_vars` | 5000 |

## Deployment di Dokploy

### 1. Push ke Repository Git

```bash
git init
git add .
git commit -m "Initial WordPress setup"
git remote add origin <YOUR_REPO_URL>
git push -u origin main
```

### 2. Setup di Dokploy

1. Buat project baru di Dokploy
2. Pilih **Compose** sebagai tipe service
3. Pilih **Git** sebagai provider
4. Masukkan URL repository
5. Set branch ke `main`

### 3. Environment Variables

Di Dokploy, set environment variables berikut:

```
WORDPRESS_DB_HOST=db
WORDPRESS_DB_USER=wordpress
WORDPRESS_DB_PASSWORD=<password_aman>
WORDPRESS_DB_NAME=wordpress
MYSQL_ROOT_PASSWORD=<root_password_aman>
```

### 4. Domain Configuration

Di Dokploy:
1. Pergi ke tab **Domains**
2. Tambahkan domain Anda
3. Pilih port `80` (service wordpress)
4. SSL akan otomatis di-generate

## Volumes

Data akan disimpan di Docker volumes:
- `wordpress_data`: File WordPress
- `db_data`: Database MySQL

## Struktur File

```
.
├── docker-compose.yml    # Konfigurasi Docker Compose
├── uploads.ini           # Konfigurasi PHP
├── .env.example          # Contoh environment variables
├── .gitignore            # Git ignore
└── README.md             # Dokumentasi
```
