# TaxLens ID — #SadarDipalak

Personal statutory & tax flow tracker untuk Indonesia. Menghitung PPh 21, BPJS, dan pajak konsumsi tahunan, memvisualisasikan komposisinya, lalu membuat gambar JPG "bukti kontribusi" yang bisa langsung dibagikan.

**Live:** https://ajiarya.github.io/taxlens-id/

## Fitur

- **Profil wajib pajak** — PTKP (TK/0 s.d. K/3) dan kategori TER A/B/C.
- **Input THP setelah PPh 21** — input memakai pemisah ribuan (contoh: 200.000.000); bruto dihitung dengan rumus gross-up PPh 21 (D = PTKP + biaya jabatan maksimum Rp6 juta); BPJS dihitung terpisah dari bruto.
- **Pekerjaan utama** — BPJS Kesehatan (1%, cap Rp 12 jt), JHT (2%), JP (1%, cap Rp 11.086.300 per Maret 2026), dan PPh 21 berbasis THP setelah pajak.
- **Pekerjaan tambahan** — hingga 3 sumber penghasilan, PPh 21 progresif tanpa PTKP.
- **Rekonsiliasi tahunan** — Pasal 17, biaya jabatan 5% (maks Rp 6 jt per pemberi kerja), PTKP sekali. Satu pekerjaan: selisih Desember ditampilkan sebagai info dan diselesaikan pemberi kerja. Multi-pekerjaan: kurang/lebih bayar SPT ditampilkan.
- **Pajak konsumsi** — PPN 11% dan PB1 10%.
- **Visualisasi aliran gaji** — Sankey dan Donut memakai data yang sama: **Gaji Bruto** → PPh 21, BPJS Kesehatan, BPJSTK (JHT + JP), PPN 11%, PB1 10%, dan **Dompet Kamu** (sisa setelah pajak & iuran). Sankey jadi tampilan utama; Donut opsi sekunder.
- **Belanja Pajak** — katalog 126 item lintas elektronik, bahan pokok, transportasi, properti, pemerintah, olahraga, gaming, hiburan, liburan, ibadah, keluarga, emas, lifestyle, produktifitas, luxury, dan wearable. Ada **pencarian sederhana** dan filter kategori; setiap item punya gambar/ikon; gambar produk brand memakai aset resmi bila tersedia.
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

- Input adalah THP bulanan setelah PPh 21. Gross-up PPh 21 memakai D = PTKP + biaya jabatan maksimum Rp6 juta dan rumus bracket tahunan; BPJS dihitung terpisah dari bruto. PPh 21 bulanan ditampilkan sebagai rata-rata tahunan; TER kategori A/B/C menjadi referensi potongan Jan–Nov dan Desember direkonsiliasi.
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
- Bahan pokok: harga e-commerce (beras, gula, minyak goreng, air mineral, isi ulang galon, Indomie); nasi padang: harga pasar.
- Transportasi: Pertamax Rp 16.500/liter (Pertamina); Whoosh First Class Rp 600.000 (KCIC); Honda BeAT Rp 19.380.000 (AHM OTR Jakarta); Daihatsu Sigra Rp 144.400.000, Toyota Calya Rp 170.200.000, Honda Brio Rp 170.400.000 (OTR 2026).
- Properti: sewa kosan Rp 1.000.000/bulan, sewa apartment Rp 3.000.000/bulan, sewa kontrakan Rp 5.000.000/tahun (harga pasar).
- Liburan: Singapura Rp 8.500.000, Malaysia Rp 5.500.000, Vietnam Rp 6.500.000 (estimasi paket).
- Tiket pesawat pulang-pergi per orang (estimasi 2026): Bali ekonomi Rp 2.000.000 / bisnis Rp 6.500.000; Jepang Rp 8.000.000 / Rp 28.000.000; Singapura Rp 2.800.000 / Rp 9.500.000; Malaysia Rp 2.500.000 / Rp 8.500.000; Vietnam Rp 3.500.000 / Rp 12.000.000.
- Ibadah: Umrah 9 Hari Rp 32.000.000; Ziarah Holyland 9 Hari Rp 45.000.000 (estimasi paket).
- Elektronik: iPhone Duo 256GB Rp 45.678.910 (iBox); Samsung Z Fold8 Rp 28.499.000, S26 Rp 16.499.000, S26+ Rp 19.499.000, S26 Ultra Rp 24.499.000 (Samsung Indonesia); Mac mini M6 Rp 15.900.000 (estimasi Apple); RTX 5060 8GB Rp 11.000.000, 5060 Ti 16GB Rp 16.300.000, 5070 12GB Rp 19.650.000, 5070 Ti 16GB Rp 32.400.000, 5080 16GB Rp 33.100.000, 5090 32GB Rp 182.000.000; DGX Spark Rp 150.000.000, DGX Rubin NVL8/NVL72 estimasi.
- Olahraga: sewa lapangan padel/tenis/futsal dan membership gym Rp 800.000/bulan. Garmin dipindah ke Elektronik; sepatu lari dipindah ke Wearable.
- Gaming: Nintendo Switch 2 Rp 9.999.000, Steam Deck Rp 15.999.000, game Steam rata-rata Rp 300.000, game PS5 rata-rata Rp 900.000; Roblox 400 Robux Rp 79.000, Fortnite 1.000 V-Bucks Rp 159.000, Valorant 1.000 VP Rp 100.000, PUBG 660 UC Rp 149.000, MLBB 86 Diamonds Rp 20.000 (estimasi).
- Keluarga: tiket Annual Pass Dufan Rp 500.000 (Dufan/Ancol); refleksi keluarga: harga pasar.
- Lifestyle: Dubai Chewy Cookie Rp 35.000, paket data Rp 100.000, AYCE Rp 400.000/orang, Meta Verified Instagram Rp 149.000/bulan (estimasi).
- Produktifitas: Claude Pro Rp 349.000/bulan, ChatGPT Plus Rp 349.000/bulan, Gemini Pro Rp 329.000/bulan; ChatGPT Pro Rp 3.300.000/bulan, Claude Max Rp 1.650.000/bulan, Google AI Ultra Rp 4.000.000/bulan, Grok (SuperGrok) Rp 500.000/bulan (estimasi kurs).
- Wearable: sepatu lari Adidas, Nike, Hoka, On, Puma, Asics; sempak segitiga Rp 50.000, baju kaos Rp 150.000, baju kemeja Rp 200.000, celana Rp 400.000.
- Luxury: Porsche 911/GT3 RS, BMW M2/M3/M4, Mercedes G-Class/Maybach, Lexus LM/RX/LX, Toyota Alphard/Land Cruiser, Patek Philippe/Rolex/AP, rumah mewah Rp 15.000.000.000 (estimasi).
- Hiburan: Netflix Rp 2.280.000/tahun, YouTube Premium Rp 69.000/bulan, Spotify Premium Rp 59.900/bulan, Disney+ Premium Rp 199.000/bulan, HBO Max Rp 119.000/bulan, Vidio Premier Rp 99.000/bulan, tiket Mens Rea Diamond Rp 2.000.000 (estimasi).
- GTA 6: PlayStation Store (estimasi pre-order).
- PS5, sewa lapangan, refleksi keluarga: harga pasar/Google.
- UMR Jakarta: UMP DKI Jakarta 2026 Rp 5.729.876; Bangunan Kopdes Rp 1.600.000.000; Bangunan SPPG Rp 4.500.000.000 (estimasi program); listrik PLN 1300 VA Rp 1.445/kWh (tarif 2026).
- Foto item: foto produk brand dan langganan digital (Apple, Samsung, Garmin, otomotif, PlayStation, Nintendo, Steam, Indomie, Netflix, Disney+, HBO Max, Vidio, Claude, ChatGPT, Gemini, Grok, Spotify, YouTube, PLN, Roblox, Fortnite, Valorant, PUBG, MLBB, Meta) berasal dari situs resmi masing-masing dan merupakan hak cipta pemilik merek; foto nasi padang dari Grab Indonesia; foto lain dari Wikimedia Commons dengan lisensi bebas (CC0, Public Domain, CC BY, CC BY-SA). Semua di-crop/resize untuk kartu. Daftar lengkap sumber, kreator, dan lisensi ada di [assets/CREDITS.md](assets/CREDITS.md).
- Semua harga bersifat ilustratif dan dapat berubah, bukan penawaran.

> Aplikasi ini adalah alat edukasi dan estimasi, bukan bukti potong resmi, nasihat pajak, atau pengganti perhitungan konsultan/pemberi kerja.
