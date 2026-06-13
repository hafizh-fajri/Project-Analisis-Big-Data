# Project-Analisis-Big-Data

Pipeline Big Data untuk Analisis Tren Lowongan Kerja di Indonesia

Proyek ini membangun pipeline Big Data end-to-end mulai dari web scraping, penyimpanan NoSQL, pemrosesan dengan Apache Spark, hingga machine learning dan visualisasi — untuk menjawab pertanyaan: skill apa yang paling dicari, dan seperti apa profil lowongan kerja di Indonesia saat ini?


Latar Belakang

Pasar kerja Indonesia berkembang pesat, namun informasi mengenai tren skill dan pola lowongan kerja masih tersebar dan sulit dianalisis secara massal. Proyek ini menjawab tiga pertanyaan utama:

1. Skill apa yang paling sering diminta perusahaan di Indonesia?
2. Kombinasi skill apa yang selalu muncul bersama dalam satu lowongan?
3. Seperti apa profil segmen lowongan berdasarkan pengalaman, tipe kerja, dan pendidikan?

Data dikumpulkan melalui web scraping dari tiga platform rekrutmen: Glints, Karir.com, dan Kalibrr, menghasilkan 1.465 lowongan kerja yang kemudian diproses dengan ekosistem Big Data.


Arsitektur Pipeline

[Web Scraping]          [Ingestion & Storage]        [Processing]
Glints                  ──────────────────────>      Apache Spark
Karir.com    ──────>    MongoDB Atlas                PySpark MLlib
Kalibrr                                              
                        
       │                                                   │
       ▼                                                   ▼
[Machine Learning]                              [Visualization]
K-Means Clustering (K=4)                        Matplotlib / Seaborn
Market Basket Analysis                          Dashboard
Association Rules                               Google Colab


Dataset

Atribut         Detail
-------------------
Sumber          Glints, Karir.com, Kalibrr
Total baris     1.465 lowongan kerja
Kolom           11 kolom (job_title, company_name, location, job_type, experience_level, education_req, salary_range, job_requirements, job_responsibilities, posted_date, source_platform)
Periode         2024 – 2025
Format          CSV (separator: ;)

*File dataset lengkap tidak disertakan karena ukurannya besar. Folder data/ hanya berisi sampel 100 baris (raw_data_sample.csv). Dataset asli disimpan di MongoDB Atlas (lihat bagian Cara Menjalankan).


Struktur Repositori

JobMarketAnalytics/
├── data/
│   └── raw_data_sample.csv          # Sampel 100 baris untuk referensi struktur data
├── notebooks/
│   ├── 01_data_cleaning.ipynb       # Pembersihan & transformasi data (Pandas + MongoDB)
│   ├── 02_kmeans_clustering.ipynb   # K-Means Clustering dengan PySpark MLlib
│   ├── 03_market_basket.ipynb       # Market Basket Analysis (Association Rules)
│   └── 04_visualization.ipynb       # Dashboard & visualisasi akhir
├── src/
│   └── scraper.py                   # Script web scraping (Glints, Karir.com, Kalibrr)
├── results/
│   └── association_rules.csv        # Output rules dari Market Basket Analysis
├── visualizations/
│   ├── 00_dashboard.png
│   ├── 01_elbow_method.png
│   ├── 02_cluster_profile.png
│   ├── 03_pca_scatter.png
│   ├── 04_top_skills.png
│   ├── 05_cooccurrence_heatmap.png
│   └── 06_association_rules.png
├── README.md
└── requirements.txt