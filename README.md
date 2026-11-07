# Dashboard Penerimaan Barang Gudang

Proyek latihan analisis data untuk melihat seberapa baik supplier dan ekspedisi mengirim barang ke gudang: tepat waktu atau tidak, lengkap atau tidak, dan berapa yang diretur.

**File:** `data_latihan_gudang_perbaikan.xlsx` (Excel)

## Tujuan

Membantu tim pembelian menjawab:
- Supplier dan ekspedisi mana yang sering telat?
- Berapa banyak barang yang datang dibanding yang dipesan?
- Berapa nilai retur, dan apa penyebab terbesarnya?
- PO mana yang belum datang dan sudah berapa lama?

## Isi File

| Sheet | Fungsi |
|---|---|
| Data | Data asli (100 baris), tidak diubah |
| Data_Bersih | Data setelah dirapikan (97 PO) + kolom hitungan baru |
| Pivot | Tabel pivot: penerimaan barang, tepat waktu, lead time |
| Data for dashboard | Tabel pivot untuk grafik dan angka KPI |
| Dashboard | Angka KPI, 3 slicer (Supplier, Ekspedisi, Bulan), dan 3 grafik |
| Ringkasan_KPI | Ringkasan semua KPI per supplier, ekspedisi, dan bulan |
| Alasan_Bisnis | Alasan setiap perbaikan data, definisi KPI, dan temuan |

## Langkah Kerja

**1. Merapikan data**
- Menghapus 3 PO yang tercatat ganda (100 menjadi 97 baris).
- Menyeragamkan penulisan nama supplier (24 menjadi 5), ekspedisi (12 menjadi 4), barang (49 menjadi 12), status, dan keterangan masalah.
- PO yang belum diterima: Qty_Terima diisi 0, lead time dan telat dikosongkan agar tidak dianggap tepat waktu.

**2. Menambah kolom hitungan**
Selisih qty, lead time, telat, status tepat waktu, nilai retur, nilai selisih, bulan, dan umur PO pending (aging).

**3. Membuat KPI**

| KPI | Cara hitung |
|---|---|
| On-Time Delivery (OTD) | PO yang diterima sesuai janji / PO yang sudah diterima |
| Lead Time | Tanggal terima - tanggal PO |
| Fill Rate | Qty diterima / Qty PO (target 95%) |
| Return Rate | Qty retur / Qty diterima |
| Aging | Tanggal cut-off - tanggal janji kirim (hanya PO pending) |

**4. Membuat dashboard**
Dashboard berisi kartu KPI (Total PO, Total Qty PO, Qty Diterima, Fill Rate, Selisih Qty) dan slicer agar bisa difilter per supplier, ekspedisi, dan bulan.

## Temuan Utama

- **Supplier:** UD. Sumber Rejeki paling sering telat (54,5% PO telat). PT. Maju Jaya paling konsisten (4,3% telat).
- **Ekspedisi:** persentase telat Wahana Express 33,3%, Indah Logistik 32,1%, JNE Trucking 24,0%, Sicepat Cargo 10,0%.
- **Retur:** 29 PO (29,9%) ada retur, nilainya Rp15.661.000. Penyebab terbesar: Kurang Kirim (Rp6.282.000).
- **PO pending:** 3 PO belum diterima (400 unit), umurnya 67 sampai 145 hari.
- **Fill Rate:** 95,9% untuk semua PO. Masalah utamanya PO yang belum datang, bukan kurang kirim.

## Catatan dan Asumsi

- Tanggal cut-off 30 Juni 2026 adalah asumsi (data terakhir diterima 23 Juni 2026). Bisa diubah di sheet Ringkasan_KPI, sel kuning.
- Kolom Stok_Awal dan Qty_Keluar tidak dipakai karena nilainya tidak konsisten (21 baris stok awal lebih kecil dari qty keluar).
- 12 dari 18 baris berketerangan "Kurang Kirim" ternyata Qty_Terima-nya sama dengan Qty_PO. Tidak diubah karena perlu konfirmasi sumber data.
- Slicer membutuhkan Excel 2013 atau lebih baru.

## Alat yang Dipakai

Microsoft Excel: Tabel, rumus, PivotTable, grafik, dan slicer.
