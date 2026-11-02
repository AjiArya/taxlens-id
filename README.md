# TaxLens ID

Personal statutory & tax flow tracker untuk Indonesia. Menghitung PPh 21, BPJS, dan pajak konsumsi tahunan, memvisualisasikan komposisinya, lalu membuat gambar JPG "bukti kontribusi" yang bisa langsung dibagikan.

**Live:** https://ajiarya.github.io/taxlens-id/

## Fitur

- **Profil wajib pajak** — PTKP (TK/0 s.d. K/3) dan kategori TER A/B/C.
- **Pekerjaan utama** — BPJS Kesehatan (1%, cap Rp 12 jt), JHT (2%), JP (1%, cap Rp 10.547.400), dan PPh 21 TER Jan–Nov.
- **Pekerjaan tambahan** — hingga 3 sumber penghasilan, PPh 21 progresif tanpa PTKP.
- **Rekonsiliasi tahunan** — Pasal 17, biaya jabatan 5% (maks Rp 6 jt), PTKP sekali, dan perhitungan kurang bayar Desember.
- **Pajak konsumsi** — PPN 11% dan PB1 10%.
- **Visualisasi barang** — daya beli total outflow terhadap katalog barang ilustratif (termasuk iPhone 18 Pro Max 2TB Burgundy).
- **Download JPG 1080 × 1350** — poster berisi total kontribusi, grafik per jenis, dan barang yang setara. Dibuat sepenuhnya di browser dengan Canvas API.
- **Privasi** — tanpa backend, tanpa cookie, tanpa localStorage. Tidak ada data yang dikirim atau disimpan.

## Menjalankan lokal

Karena seluruh aplikasi ada dalam satu file, cukup buka `index.html` di browser. Untuk hasil terbaik (dan agar CDN/font termuat normal):

```bash
python3 -m http.server 4173
# buka http://127.0.0.1:4173
```

## Deploy

Push ke `main`. Workflow `.github/workflows/deploy.yml` akan menerbitkan `index.html` ke branch `gh-pages`; GitHub Pages menyajikan branch tersebut secara otomatis.

Situs: **https://ajiarya.github.io/taxlens-id/**

## Metodologi singkat

- TER PPh 21 mengikuti PP 58/2023 & PMK 168/2023; Desember memakai tarif Pasal 17 UU HPP.
- PTKP hanya dikurangkan sekali pada rekonsiliasi tahunan.
- Biaya jabatan 5% dari bruto, maksimal Rp 6 juta/tahun; PKP dibulatkan ke bawah ribuan penuh.
- JHT dan JP mengurangi PKP; BPJS Kesehatan tidak.
- Pekerjaan tambahan tidak mendapat PTKP dan dihitung progresif dari rupiah pertama.
- PPN 11% (UU HPP) dan PB1 10% (UU HKPD).
- Harga barang pada visualisasi bersifat ilustratif, bukan penawaran.

> Aplikasi ini adalah alat edukasi dan estimasi, bukan bukti potong resmi, nasihat pajak, atau pengganti perhitungan konsultan/pemberi kerja.
