# TaxLens ID — #SadarDipalak

Personal statutory & tax flow tracker untuk Indonesia. Menghitung PPh 21, BPJS, dan pajak konsumsi tahunan, memvisualisasikan komposisinya, lalu membuat gambar JPG "bukti kontribusi" yang bisa langsung dibagikan.

**Live:** https://ajiarya.github.io/taxlens-id/

## Fitur

- **Profil wajib pajak** — PTKP (TK/0 s.d. K/3) dan kategori TER A/B/C.
- **Input gaji bersih (take-home)** — input memakai pemisah ribuan (contoh: 200.000.000); bruto dihitung otomatis dengan gross-up tahunan; PPh 21 terutang dan BPJS dihitung dari bruto hasil rekonstruksi.
- **Pekerjaan utama** — BPJS Kesehatan (1%, cap Rp 12 jt), JHT (2%), JP (1%, cap Rp 11.086.300 per Maret 2026), dan PPh 21 TER Jan–Nov.
- **Pekerjaan tambahan** — hingga 3 sumber penghasilan, PPh 21 progresif tanpa PTKP.
- **Rekonsiliasi tahunan** — Pasal 17, biaya jabatan 5% (maks Rp 6 jt per pemberi kerja), PTKP sekali. Satu pekerjaan: selisih Desember ditampilkan sebagai info dan diselesaikan pemberi kerja. Multi-pekerjaan: kurang/lebih bayar SPT ditampilkan.
- **Pajak konsumsi** — PPN 11% dan PB1 10%.
- **Visualisasi aliran gaji** — Sankey dan Donut memakai data yang sama: **Gaji Bruto** → PPh 21, BPJS Kesehatan, BPJSTK (JHT + JP), PPN 11%, PB1 10%, dan **Dompet Kamu** (sisa setelah pajak & iuran). Sankey jadi tampilan utama; Donut opsi sekunder.
- **Belanja Pajak** — elektronik (harga iBox), bahan pokok (e-commerce), pemerintah (MBG & UMP DKI 2026), olahraga, gaming, liburan per hari, ibadah, keluarga, emas, dan lifestyle.
- **Download JPG 1080 × 1350 (4:5)** — poster berisi total kontribusi, grafik sesuai pilihan (Sankey atau Donut), barang setara, dan branding **#SadarDipalak** dengan tiga warna solid: hijau `#1b8a3e`, biru `#123c8a`, merah `#dc2626`; pas untuk Threads, Instagram, dan foto TikTok. Dibuat sepenuhnya di browser dengan Canvas API.
- **Bantu posting** — tombol bagikan memakai Web Share API di HP; di desktop gambar disalin ke clipboard atau diunduh. Tersedia juga Salin Gambar, Simpan Foto, dan tombol Threads/Instagram/TikTok.
- **Privasi** — tanpa backend, tanpa cookie, tanpa localStorage. Tidak ada data yang dikirim atau disimpan.
- **Build ID** — footer menampilkan build ID dari commit deploy (tanggal + SHA pendek) untuk memudahkan verifikasi versi yang sedang dilihat.

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

- Input adalah gaji bersih bulanan (take-home); gross-up dilakukan pada basis tahunan: BPJS + PPh 21 terutang (Pasal 17) + take-home. PPh 21 bulanan Jan–Nov memakai TER; Desember direkonsiliasi.
- TER PPh 21 mengikuti PP 58/2023 & PMK 168/2023; tabel TER dan tarif Pasal 17 diverifikasi terhadap [Buku PPh 21/26 DJP](https://static.pajak.go.id/download/kalkulator/Buku_PPh2126_Release_20240108.pdf). Desember memakai tarif Pasal 17 UU HPP.
- Satu pemberi kerja: rekonsiliasi Desember diselesaikan pemberi kerja, sehingga tidak ada kurang bayar tambahan.
- Multi-pekerjaan: total PPh tahunan dibandingkan dengan potongan Jan–Nov; selisih kurang/lebih bayar ditampilkan sebagai rekonsiliasi Desember (bukan komponen pajak tambahan).
- PTKP hanya dikurangkan sekali pada rekonsiliasi tahunan.
- Biaya jabatan 5% dari bruto, maksimal Rp 6 juta/tahun per pemberi kerja; PKP dibulatkan ke bawah ribuan penuh.
- JHT dan JP mengurangi PKP; BPJS Kesehatan tidak.
- Pekerjaan tambahan tidak mendapat PTKP dan dihitung progresif dari rupiah pertama.
- PPN 11% (UU HPP) dan PB1 10% (UU HKPD).
- Dompet Kamu pada Sankey/Donut adalah sisa setelah PPh 21, BPJS, PPN, dan PB1; Sankey dan Donut memakai komponen yang sama.
- Effective out-of-pocket rate dihitung terhadap Dompet Kamu (sisa setelah pajak & iuran).

## Sumber harga & foto

- Apple: iBox (iPhone 18 Pro Max 256GB Rp 29.999.000; iPad Pro 11-inch M5 256GB Rp 24.999.000; MacBook Pro 14-inch seri terbaru Rp 38.999.000 — M6 belum tersedia di katalog iBox, dipakai sebagai estimasi).
- Bahan pokok: harga e-commerce (beras, gula, minyak goreng).
- GTA 6: PlayStation Store (estimasi pre-order).
- PS5, sewa lapangan, refleksi keluarga: harga pasar/Google.
- UMR Jakarta: UMP DKI Jakarta 2026 Rp 5.729.876.
- Foto produk Apple: iBox/Eraspace. Foto pendukung: Wikimedia Commons — PS5 © Soberian/Osh33m (CC BY-SA 4.0), Bali © Jakub Hałun (CC BY-SA 4.0), MBG/ompreng © Fitrah 9131 (CC0), Fuji © Romain Guy (CC0), emas © Stevebidmead (CC0), beras & gula dari Wikimedia Commons.
- Semua harga bersifat ilustratif dan dapat berubah, bukan penawaran.

> Aplikasi ini adalah alat edukasi dan estimasi, bukan bukti potong resmi, nasihat pajak, atau pengganti perhitungan konsultan/pemberi kerja.
