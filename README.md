# TaxLens ID — #SadarDipalak

Personal statutory & tax flow tracker untuk Indonesia. Menghitung PPh 21, BPJS, dan pajak konsumsi tahunan, memvisualisasikan komposisinya, lalu membuat gambar JPG "bukti kontribusi" yang bisa langsung dibagikan.

**Live:** https://ajiarya.github.io/taxlens-id/

## Fitur

- **Profil wajib pajak** — PTKP (TK/0 s.d. K/3) dan kategori TER A/B/C.
- **Input gaji bersih (take-home)** — bruto dihitung otomatis; PPh 21 dan BPJS dihitung dari bruto hasil rekonstruksi.
- **Pekerjaan utama** — BPJS Kesehatan (1%, cap Rp 12 jt), JHT (2%), JP (1%, cap Rp 10.547.400), dan PPh 21 TER Jan–Nov.
- **Pekerjaan tambahan** — hingga 3 sumber penghasilan, PPh 21 progresif tanpa PTKP.
- **Rekonsiliasi tahunan** — Pasal 17, biaya jabatan 5% (maks Rp 6 jt), PTKP sekali. Satu pekerjaan: tidak ada kurang bayar tambahan karena diselesaikan pemberi kerja. Multi-pekerjaan: selisih tahunan ditampilkan.
- **Pajak konsumsi** — PPN 11% dan PB1 10%.
- **Belanja Pajak** — elektronik (harga iBox), bahan pokok (e-commerce), pemerintah (MBG & UMP DKI 2026), olahraga, gaming, liburan per hari, ibadah, keluarga, emas, dan lifestyle.
- **Download JPG 1080 × 1350 (4:5)** — poster berisi total kontribusi, grafik per jenis, dan barang setara; pas untuk Threads, Instagram, dan foto TikTok. Dibuat sepenuhnya di browser dengan Canvas API.
- **Privasi** — tanpa backend, tanpa cookie, tanpa localStorage. Tidak ada data yang dikirim atau disimpan.

## Menjalankan lokal

Aplikasi statis: `index.html` + folder `assets/`. Cukup jalankan server statis dari root repo:

```bash
python3 -m http.server 4173
# buka http://127.0.0.1:4173
```

## Deploy

Push ke `main`. Workflow `.github/workflows/deploy.yml` akan menerbitkan `index.html` ke branch `gh-pages`; GitHub Pages menyajikan branch tersebut secara otomatis.

Situs: **https://ajiarya.github.io/taxlens-id/**

## Metodologi singkat

- Input adalah gaji bersih (take-home). Bruto dihitung dengan iterasi BPJS + TER; PPh 21 tahunan dihitung dari bruto tersebut.
- TER PPh 21 mengikuti PP 58/2023 & PMK 168/2023; Desember memakai tarif Pasal 17 UU HPP.
- Satu pemberi kerja: rekonsiliasi Desember diselesaikan pemberi kerja, sehingga tidak ada kurang bayar tambahan.
- Multi-pekerjaan: total PPh tahunan dibandingkan dengan potongan Jan–Nov; selisihnya ditampilkan sebagai kurang bayar.
- PTKP hanya dikurangkan sekali pada rekonsiliasi tahunan.
- Biaya jabatan 5% dari bruto, maksimal Rp 6 juta/tahun; PKP dibulatkan ke bawah ribuan penuh.
- JHT dan JP mengurangi PKP; BPJS Kesehatan tidak.
- Pekerjaan tambahan tidak mendapat PTKP dan dihitung progresif dari rupiah pertama.
- PPN 11% (UU HPP) dan PB1 10% (UU HKPD).
- Effective out-of-pocket rate dihitung terhadap gaji bersih tahunan.

## Sumber harga & foto

- Apple: iBox (iPhone 18 Pro Max 256GB Rp 29.999.000; iPad Pro 11-inch M5 256GB Rp 24.999.000; MacBook Pro 14-inch seri terbaru Rp 38.999.000 — M6 belum tersedia di katalog iBox, dipakai sebagai estimasi).
- Bahan pokok: harga e-commerce (beras, gula, minyak goreng).
- GTA 6: PlayStation Store (estimasi pre-order).
- PS5, sewa lapangan, refleksi keluarga: harga pasar/Google.
- UMR Jakarta: UMP DKI Jakarta 2026 Rp 5.729.876.
- Foto produk Apple: iBox/Eraspace. Foto pendukung: Wikimedia Commons — PS5 © Soberian/Osh33m (CC BY-SA 4.0), Bali © Jakub Hałun (CC BY-SA 4.0), MBG © Indonesiagood (CC BY 4.0), Jakarta © Sam Hidayat (CC BY-SA 4.0), Fuji © Romain Guy (CC0), emas © Stevebidmead (CC0), beras/gula/minyak dari Wikimedia Commons.
- Semua harga bersifat ilustratif dan dapat berubah, bukan penawaran.

> Aplikasi ini adalah alat edukasi dan estimasi, bukan bukti potong resmi, nasihat pajak, atau pengganti perhitungan konsultan/pemberi kerja.
