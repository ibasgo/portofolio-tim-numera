# Portofolio Tim — Quarto Website

Situs portofolio tim konsultan data: beranda, profil tim, proyek/studi kasus (termasuk satu
analisis **R** yang dirender langsung), dan blog. Semua nama, angka, dan proyek adalah
**contoh** — ganti dengan data tim Anda.

## Struktur

```
_quarto.yml                  ← judul situs, menu, tema, URL situs
index.qmd                    ← beranda (hero, statistik, layanan, proyek & tulisan terbaru)
tim.qmd                      ← halaman daftar tim (otomatis dari folder tim/)
tim/<nama>.qmd               ← profil tiap anggota (+ foto <nama>.svg/.jpg)
proyek.qmd                   ← galeri proyek (otomatis dari folder proyek/)
proyek/<slug>/index.qmd      ← satu studi kasus per folder (+ thumbnail)
blog.qmd                     ← daftar tulisan + RSS
blog/posts/<tgl-slug>/index.qmd
_templates/tim.ejs           ← template kartu anggota tim
assets/light.scss, dark.scss ← warna brand mode terang/gelap
assets/custom.scss           ← gaya tambahan (hero, kartu, dsb.)
_freeze/                     ← hasil eksekusi kode yang disimpan (WAJIB di-commit)
DESCRIPTION                  ← daftar paket R yang dibutuhkan (dibaca GitHub Actions)
.github/workflows/publish.yml← deploy otomatis ke GitHub Pages
```

## Menjalankan di komputer sendiri

1. Pasang [Quarto](https://quarto.org/docs/get-started/) dan [R](https://cran.r-project.org/) (≥ 4.1; RStudio/Positron opsional).
2. Di konsol R: `install.packages(c("knitr", "rmarkdown", "dplyr", "tidyr", "ggplot2", "scales"))`
3. `quarto preview` → situs terbuka di browser dan otomatis ter-refresh saat file disimpan.

## Mengganti konten

| Ingin mengubah… | Edit file |
|---|---|
| Nama tim, menu, link sosial | `_quarto.yml` |
| Teks beranda & angka statistik | `index.qmd` |
| Anggota tim | salin `tim/andi.qmd` → ubah `title`, `subtitle` (peran), `description`, `image`, `categories` (skill), `order` (urutan) |
| Foto anggota | taruh `tim/<nama>.jpg` (rasio 1:1), lalu ubah `image:` |
| Proyek baru | salin satu folder di `proyek/`, ubah front matter; isi `author:` dengan nama anggota persis agar proyek muncul di profil mereka |
| Tulisan blog | buat folder baru di `blog/posts/` berisi `index.qmd` |
| Paket R baru untuk halaman berkode | tambahkan di bagian `Imports:` pada `DESCRIPTION` |
| Warna brand | `$primary` di `assets/light.scss` dan `assets/dark.scss` |

## Deploy ke GitHub Pages

1. Buat repositori baru di GitHub (mis. `portofolio-tim`) dan push seluruh folder ini ke branch `main`
   — **termasuk folder `_freeze/`**.
2. Di repositori: **Settings → Pages → Build and deployment → Source: GitHub Actions**.
3. Setiap push ke `main` akan merender dan memublikasikan situs. Status bisa dilihat di tab **Actions**.
4. Ganti `site-url` di `_quarto.yml` dengan alamat situs Anda
   (`https://<username>.github.io/<nama-repo>`) agar RSS dan tautan berbagi benar.

> **Tentang `_freeze/`**: halaman berkode R hanya dieksekusi ulang jika file `.qmd`-nya
> berubah. Jalankan `quarto render` secara lokal setelah mengubah halaman berkode, lalu commit
> perubahan di `_freeze/`. Workflow tetap memasang R dan paket di `DESCRIPTION` sebagai cadangan.
