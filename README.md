# Case-Based Reasoning untuk Putusan MA

Repositori ini berisi pipeline lengkap untuk sistem *Case-Based Reasoning* dalam menemukan kasus hukum lama yang mirip dan memprediksi solusi berdasarkan kasus baru (query). Studi kasus: Perkara Pidana Penipuan/Penggelapan di PN Sidoarjo.

## Instalasi

### 1. Clone Repository (Opsional)
git clone https://github.com/nama-kamu/cbr-mahkamah.git
cd cbr-mahkamah

### 2. Install Dependencies
Buat virtual environment (opsional), lalu:
pip install -r requirements.txt

### 3. Install Tambahan (OCR & PDF)
sudo apt install poppler-utils tesseract-ocr tesseract-ocr-ind -y

## Struktur Folder
```
project-root/
├── tahap_1_5.py
├── requirements.txt
├── /Data
│   ├── /raw/               ← Hasil OCR teks
│   ├── /processed/         ← Hasil representasi kasus
│   ├── /results/           ← Hasil prediksi
│   └── /eval/              ← Query & evaluasi model
├── /CSV                   ← Hasil scraping awal
└── /PDF                   ← PDF putusan
```

## Menjalankan Pipeline End-to-End

### Tahap 1: Scraping + Download PDF + OCR
Jalankan `tahap_1_5.py`, atau secara bertahap:
run_scraper()  # dari tahap_1_5.py

### lanjutkan OCR PDF → hasil ke /Data/raw/*.txt


### Tahap 2: Representasi Kasus
Mengubah hasil scraping & OCR menjadi dataset terstruktur
Output: cases.csv

### Tahap 3: Case Retrieval
TF-IDF: retrieve(query, k=3)
BERT: retrieve_bert(query, k=3)

### Tahap 4: Solution Reuse
predict_outcome(query)
Output: predictions.csv

### Tahap 5: Evaluasi & Visualisasi
Menghitung accuracy, precision, recall, F1
Membuat plot perbandingan performa


Contoh Query Evaluasi
```
json
[
  {"query_id": "q1", "query_text": "Penipuan jual beli rumah secara online"},
  {"query_id": "q2", "query_text": "Investasi bodong oleh terdakwa"},
  {"query_id": "q3", "query_text": "Penipuan kendaraan bermotor"},
  {"query_id": "q4", "query_text": "Mengaku pegawai bank dan menipu korban"},
  {"query_id": "q5", "query_text": "Transaksi fiktif pengadaan barang"}
]
```

Output Utama

* cases.csv`: Data kasus lengkap
* queries.json`: Daftar query uji
* predictions.csv`: Prediksi solusi untuk query
* retrieval_metrics.csv`: Evaluasi TF-IDF
* retrieval_metrics_bert.csv`: Evaluasi BERT
* performance_comparison.png`: Bar chart performa
