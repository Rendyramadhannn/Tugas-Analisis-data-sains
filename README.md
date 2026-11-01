# analisis-pendapatan-pos

Analisis ini menghitung total pendapatan per tahun (2024 dan 2025) dari 5.030 baris data transaksi POS. Sebelum dihitung, data dibersihkan terlebih dahulu. Sebanyak 30 baris duplikat (ID transaksi dan seluruh isinya sama persis) dihapus sehingga tersisa 5.000 transaksi unik, karena transaksi yang tercatat dua kali akan membuat pendapatan terhitung ganda. Kolom kode_kasir yang kosong pada 261 baris data mentah (260 baris setelah duplikat dihapus) diisi dengan penanda "TIDAK_DIKETAHUI" dan tidak dibuang, sebab kolom ini tidak memengaruhi perhitungan pendapatan sehingga transaksinya tetap layak dihitung. Format harga satuan yang tidak seragam (misalnya 7500,00 dan 12.000) diseragamkan menjadi angka murni, dan format tanggal yang bervariasi (YYYY-MM-DD, DD/MM/YYYY, dan DD-MM-YYYY) diseragamkan agar tahun transaksi dapat diambil dengan benar.

Pendapatan dihitung dengan rumus jumlah × harga satuan × (1 − diskon/100), karena diskon mengurangi uang yang benar-benar diterima toko dari pelanggan. Hanya transaksi berstatus SELESAI yang dihitung sebagai pendapatan. Transaksi BATAL tidak menghasilkan uang masuk, dan transaksi RETUR berarti barang dikembalikan sehingga uangnya dikembalikan kepada pelanggan. Jika seluruh status dan diskon diabaikan, pendapatan akan terlihat lebih besar sekitar 11 juta rupiah pada 2024 dan sekitar 10,6 juta rupiah pada 2025.

Terdapat tiga asumsi dalam pembersihan data. Pertama, 40 baris dengan jumlah negatif (setelah duplikat dihapus) dianggap sebagai kesalahan pengetikan tanda minus, sehingga nilainya diubah menjadi positif. Kedua, 12 baris dengan jumlah di atas 100 (nilai terbesar mencapai 2.375, sedangkan jumlah normal pada data paling banyak 12) dianggap sebagai kesalahan input dan dikeluarkan dari perhitungan. Ketiga, transaksi RETUR tidak dihitung sama sekali, bukan dihitung lalu dikurangkan, karena data tidak menunjukkan apakah retur terjadi pada tahun yang sama dengan penjualan aslinya.

## Hasil

Total pendapatan tahun 2024 adalah Rp128.048.525 dan tahun 2025 adalah Rp136.467.375, atau naik sekitar 6,6%.

| Tahun | Total Pendapatan (Rp) |
|---|---|
| 2024 | 128.048.525 |
| 2025 | 136.467.375 |

## Isi Repository

### analisis_pendapatan.ipynb

File ini adalah Jupyter Notebook yang berisi seluruh program Python untuk analisis. Di dalamnya terdapat langkah-langkah pembacaan data, penghapusan duplikat, penanganan nilai kosong pada kolom kode_kasir, penyeragaman format harga dan tanggal, pembersihan jumlah yang tidak wajar, serta perhitungan pendapatan per tahun dengan memperhitungkan diskon dan status transaksi. Karena notebook menyimpan hasil eksekusi, keluaran program seperti jumlah baris sebelum dan sesudah pembersihan serta tabel total pendapatan juga dapat dibaca langsung tanpa perlu menjalankan ulang kodenya.

### hasil_pendapatan_per_tahun.csv

File ini berisi keluaran akhir dari program, yaitu tabel ringkas dengan dua kolom, Tahun dan Total Pendapatan (Rp), untuk tahun 2024 dan 2025. File ini dibuat otomatis oleh notebook pada langkah terakhir, sehingga angkanya selalu sama dengan hasil perhitungan di notebook dan dapat dibuka dengan Excel atau aplikasi spreadsheet lain untuk keperluan pelaporan.

### paket_a_transaksi_pos_2024_2025.csv

File ini adalah data asli transaksi point of sale (POS) yang menjadi bahan analisis, terdiri atas 5.030 baris untuk periode 2024 sampai 2025. Setiap baris mencatat satu transaksi dengan sembilan kolom, yaitu id_transaksi, tanggal, kode_gerai, kode_kasir, kode_produk, jumlah, harga_satuan, diskon_persen, dan status. File ini disimpan tanpa diubah agar proses pembersihan data di notebook dapat ditelusuri dan diulang dari data aslinya.

## Cara Menjalankan

Letakkan file CSV data asli dan notebook di folder yang sama, buka notebook dengan Jupyter, lalu jalankan semua cell dari atas ke bawah. Hasil akan tercetak di bawah cell dan tersimpan ke file hasil_pendapatan_per_tahun.csv.
