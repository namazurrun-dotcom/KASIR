# Aplikasi Kasir (GitHub Pages)

Aplikasi kasir berbasis web, satu file (`index.html`), tanpa server dan tanpa instalasi.

## Fitur

- **Upload data produk** dari CSV atau Excel (`.xlsx`/`.xls`), mode *ganti semua* atau *gabung/update* berdasarkan kode.
- **PPN 11%** otomatis (bisa dimatikan lewat checkbox).
- **Diskon diketik manual**, dalam persen (%) atau rupiah (Rp).
- Keranjang dengan tombol +/−, pencarian produk, stok otomatis berkurang saat transaksi.
- Hitung uang diterima dan kembalian.
- Cetak struk (lebar 72 mm, cocok untuk printer thermal) lewat dialog cetak browser.
- Data produk tersimpan di browser (localStorage).

## Format file produk

Baris pertama adalah header. Kolom `nama` dan `harga` wajib; `kode` dan `stok` opsional.

```csv
kode,nama,harga,stok
P001,Beras 5 kg,68000,40
P002,Minyak Goreng 1 L,18000,60
```

Pemisah koma (`,`), titik koma (`;`), atau tab dikenali otomatis. Contoh: `produk-contoh.csv`.

## Rumus perhitungan

```
Subtotal = Σ (harga × qty)
Diskon   = Subtotal × % / 100   (atau nominal Rp, maksimal sebesar subtotal)
DPP      = Subtotal − Diskon
PPN 11%  = DPP × 11%
Total    = DPP + PPN
```

Harga produk dianggap **belum termasuk PPN**.

## Cara hosting di GitHub Pages

1. Buat repository baru di GitHub, misalnya `kasir`.
2. Upload `index.html`, `README.md`, dan `produk-contoh.csv` (tombol **Add file → Upload files**).
3. Buka **Settings → Pages**.
4. Pada **Build and deployment**, pilih **Deploy from a branch**, branch `main`, folder `/ (root)`, lalu **Save**.
5. Tunggu 1–2 menit. Aplikasi bisa dibuka di `https://USERNAME.github.io/kasir/`.

## Catatan

- Upload Excel memakai library SheetJS dari CDN, jadi perlu koneksi internet. File CSV tetap bisa dipakai tanpa library tersebut.
- Data tersimpan per browser/perangkat. Jika membersihkan data situs, produk harus di-upload ulang.
