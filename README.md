# RFM & Cohort Retention Analysis — Online Retail

Analisis perilaku pelanggan pada data transaksi *online retail* menggunakan pendekatan **Cohort Retention Analysis**, sebagai dasar untuk memahami pola *repeat purchase* dan loyalitas pelanggan dari waktu ke waktu.

## 📌 Deskripsi Proyek

Proyek ini bertujuan untuk menganalisis retensi pelanggan berdasarkan bulan akuisisi (cohort) pada data transaksi ritel online tahun 2010. Analisis ini membantu menjawab pertanyaan bisnis seperti:

- Seberapa besar pelanggan yang kembali bertransaksi setelah pembelian pertama?
- Apakah kualitas pelanggan baru berubah sepanjang tahun?
- Apakah ada pola musiman dalam perilaku pembelian ulang?

## 🗂️ Dataset

Dataset berupa data transaksi ritel online dengan kolom:

| Kolom | Deskripsi |
|---|---|
| `order_id` | ID unik transaksi (diawali `C` jika dibatalkan) |
| `product_code` | Kode produk |
| `product_name` | Nama produk |
| `quantity` | Jumlah item yang dibeli |
| `order_date` | Tanggal & waktu transaksi |
| `price` | Harga satuan produk |
| `customer_id` | ID unik pelanggan |

## 🧹 Data Cleaning

Beberapa langkah pembersihan data yang dilakukan:
- Konversi `order_date` ke format datetime
- Menghapus baris tanpa `customer_id` dan `product_name`
- Menyeragamkan `product_name` (huruf kecil, produk duplikat digabung berdasarkan nama paling sering muncul)
- Menghapus data uji coba (produk dengan kata "test")
- Menandai status pesanan (`delivered` / `cancelled`) berdasarkan awalan `order_id`
- Menghitung kolom `amount` = `quantity` × `price`
- Menghapus outlier menggunakan Z-score pada `quantity` dan `amount`

## ⚙️ Metodologi

1. **Agregasi transaksi bulanan per pelanggan**
2. **Penentuan cohort**: bulan pertama kali pelanggan bertransaksi
3. **Perhitungan `period_num`**: jarak bulan antara transaksi dengan bulan cohort
4. **Pivot table & retention rate**: proporsi pelanggan yang kembali di setiap periode dibanding ukuran cohort awal
5. **Visualisasi**: heatmap retention rate per cohort menggunakan `seaborn`

## 📊 Temuan Utama

![Retensi Bulan ke-2 per Cohort](images/barchart.png)

- **Churn tinggi pasca pembelian pertama** — hanya 20–39% pelanggan kembali bertransaksi di bulan ke-2, mayoritas hanya membeli satu kali.
- **Kualitas cohort menurun** sepanjang paruh pertama tahun: cohort Januari paling loyal (retensi stabil 35–47%), sementara cohort Mei–Juni paling lemah (~20%), lalu sedikit membaik di September–Oktober (~28%).
- **Efek musiman November** — retensi naik hampir di semua cohort pada bulan November, kemungkinan terkait musim belanja akhir tahun.
- **Penurunan di Desember** kemungkinan besar artefak data (data transaksi hanya tersedia sampai 23 Desember), bukan sinyal bisnis yang sebenarnya.

## 💡 Rekomendasi

- Fokuskan program retensi (voucher pembelian kedua, email follow-up) pada **30 hari pertama** setelah pembelian pertama.
- Telusuri faktor yang membuat cohort Januari lebih loyal, lalu replikasi ke cohort lainnya.
- Siapkan kampanye dan kapasitas layanan menjelang **November** untuk memanfaatkan momentum musiman.
- Verifikasi kelengkapan data Desember sebelum menjadikannya dasar pengambilan keputusan.
- Kembangkan analisis lebih lanjut dengan **skoring RFM (Recency, Frequency, Monetary)** untuk segmentasi pelanggan (Champions, Loyal, At Risk, Lost).

## 🛠️ Tools & Library

- Python
- Pandas, NumPy
- SciPy (deteksi outlier)
- Matplotlib, Seaborn (visualisasi)

## 🚀 Cara Menjalankan

```bash
# clone repository
git clone <repo-url>
cd <repo-folder>

# install dependencies
pip install pandas numpy scipy matplotlib seaborn

# jalankan notebook
jupyter notebook RFM-Analysis.ipynb
```

> Catatan: sesuaikan path dataset pada baris `pd.read_csv(...)` dengan lokasi file dataset di komputer Anda.

## 📁 Struktur File

```
├── data/
│   └── Online Retail Data.csv   # dataset transaksi
├── images/
│   └── barchart.png             # visualisasi retensi bulan ke-2 per cohort
├── RFM-Analysis.ipynb            # notebook analisis utama
└── README.md                     # dokumentasi proyek
```

## ✍️ Author

M. Fatta Arya Irwanda