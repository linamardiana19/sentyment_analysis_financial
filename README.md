Project : Fine-Tuning IndoNLU for Financial Sentiment Analysis (SMSA-Stok)
Proyek ini merupakan implementasi fine-tuning model IndoNLU (Indonesian BERT) untuk task analisis sentimen pada data berita saham Indonesia. Dataset yang digunakan merupakan hasil adaptasi dan pembersihan dari "ID-SMSA: Indonesian Stock Market Dataset for Sentiment Analysis", dengan 3 label sentimen: positif, netral, dan negatif.

Model :
Model dasar yang digunakan adalah IndoBERT dari IndoNLU, yaitu pretrained BERT berbahasa Indonesia. Fine-tuning dilakukan menggunakan skrip `finetune_smsa_stock.ipynb` untuk task single-sentence classification.

IndoNLU adalah benchmark dan kumpulan model NLP Bahasa Indonesia yang telah dipublikasikan di AACL-IJCNLP 2020.  
Paper: https://www.aclweb.org/anthology/2020.aacl-main.85.pdf


Struktur Dataset :
```
dataset_smsa_stok/
├── data_clean/
│   ├── data_smsa_clean.xlsx     # Dataset hasil preprocessing manual
│   └── data_train/              # File train/valid/test dalam format .tsv IndoNLU
├── dataset/                     # Folder utama untuk eksekusi fine-tuning
├── save_model/                  # Model hasil fine-tuning disimpan di sini
```

Cara Menjalankan : 
1. download github IndoNLU : https://github.com/IndoNLP/indonlu
2. simpan notebook `finetune_smsa_stock.ipynb` dan `finetune_smsa_stock_preparing.ipynb` di dalam folder `examples/`
2. Jalankan sel sesuai urutanpada `finetune_smsa_stock.ipynb`


Dataset Referensi :
> Hartanto, Jason; Liundi, Timothy; Sutoyo, Rhio (2025),  
> “ID-SMSA: Indonesian Stock Market Dataset for Sentiment Analysis”,  
> Mendeley Data, V3, doi: [10.17632/tn4vzs8tdw.3](https://data.mendeley.com/datasets/tn4vzs8tdw/3)

Hasil Evaluasi:
Model IndoBERT yang telah dilatih menghasilkan hasil evaluasi terbaik pada epoch ke-2 sebagai berikut:

| Label   | Precision | Recall | F1-score | Support |
| ------- | --------- | ------ | -------- | ------- |
| Positif | 0.87      | 0.85   | 0.86     | 340     |
| Netral  | 0.79      | 0.77   | 0.78     | 158     |
| Negatif | 0.76      | 0.81   | 0.79     | 160     |
- Accuracy keseluruhan: 82% 

Catatan Tambahan :
- File `data_smsa_clean.xlsx` adalah hasil pembersihan.
- Data kemudian diubah ke format `.tsv` sesuai format yang diharuskan oleh IndoNLU (`data_train/data_smsa_train.tsv`, `data_smsa_valid.tsv`, dll).
- Model yang telah dilatih dapat digunakan untuk inference pada berita saham baru dan dapat digunakan sebagai fitur sentimen dalam forecasting harga saham sesuai row date.
