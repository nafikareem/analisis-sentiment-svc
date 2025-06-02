# Optimasi Klasifikasi Sentimen Ulasan Gojek dengan Support Vector Classifier dan Genetic Algorithm

Proyek ini melakukan analisis sentimen pada ulasan pengguna aplikasi Gojek menggunakan pendekatan machine learning dan leksikon Bahasa Indonesia. Pipeline mencakup preprocessing data, ekstraksi fitur, pelabelan sentimen, pemodelan SVC, dan optimasi hyperparameter dengan Genetic Algorithm.

## Instalasi

1. **Clone repository**  
   Jalankan perintah berikut di terminal:
   ```
   git clone [<repo-url>](https://github.com/nafikareem/analisis-sentiment-svc)
   cd sentiment
   ```
2. **Install dependecies**

   Disarankan menggunakan virtual environment.
   ```
    pip install -r requirements.txt
   ```

## Alur Analisis

1. Preprocessing (`notebooks/preprocessing.ipynb`)

- Cleaning: Menghapus karakter non-alfabet, URL, mention, hashtag, angka, dan karakter berulang.
- Normalisasi: Menggunakan kamus kata baku untuk mengganti kata tidak baku.
- Stopwords Removal: Menghapus stopwords Bahasa Indonesia dengan Sastrawi.
- Stemming: Mengubah kata ke bentuk dasar.
- Tokenisasi: Memecah kalimat menjadi token.
- Labelling: Menggunakan VADER yang dimodifikasi dengan leksikon Bahasa Indonesia (INSET & SentiStrength) untuk memberi label sentimen (`positive`, `negative`, `neutral`).
- Output: Data hasil preprocessing disimpan di `data/data_preprocessed.csv`.

2. Modelling (`notebooks/modelling.ipynb`)

- Ekstraksi Fitur: Menggunakan `CountVectorizer` dan `TfidfTransformer`.
- Train-Test Split: 80% data latih, 20% data uji.
- Modelling:
  - Menggunakan Genetic Algorithm (DEAP) untuk mencari kombinasi optimal parameter `C`, `kernel`, dan `gamma`.
  - Model terbaik disimpan di `models/svc_tuned.joblib`.
- Evaluasi: Model hasil tuning dievaluasi ulang dan dibandingkan dengan model awal.

## Dataset

- Ulasan Gojek: Diambil dari file CSV, subset data digunakan untuk efisiensi.
- Kamus Kata Baku: `data/kamuskatabaku.xlsx`
- Leksikon Sentimen:
  - INSET (`data/inset/`): Leksikon sentimen Bahasa Indonesia.
  - SentiStrength (`data/sentistrength_id/`): Leksikon dan skrip analisis sentimen.

## Menjalankan Notebook

1. Jalankan `notebooks/preprocessing.ipynb` untuk preprocessing dan pelabelan data.
2. Jalankan `notebooks/modelling.ipynb` untuk training, tuning, dan evaluasi model.

## Hasil

- Model SVC dengan tuning hyperparameter menggunakan Genetic Algorithm mencapai akurasi sekitar 91%.
- Model mampu mengklasifikasikan sentimen positif, negatif, dan netral dengan baik, meskipun sentimen netral lebih sulit dibedakan.

## Referensi

- Fajri Koto, and Gemala Y. Rahmaningtyas "InSet Lexicon: Evaluation of a Word List for Indonesian
  Sentiment Analysis in Microblogs". IEEE in the 21st International Conference on Asian Language Processing
  (IALP), Singapore, December 2017.
- Wahid, D. H., & Azhari, S. N. (2016). Peringkasan Sentimen Esktraktif di Twitter Menggunakan Hybrid TF-IDF dan Cosine Similarity. IJCCS (Indonesian Journal of Computing and Cybernetics Systems), 10(2), 207-218.
- Fajri, M., & Primajaya, A. (2023). Komparasi teknik hyperparameter optimization pada SVM untuk permasalahan klasifikasi dengan menggunakan Grid Search dan Random Search. Journal of Applied Informatics and Computing (JAIC), 7(1), 10–15. https://doi.org/10.30871/jaic.v7i1.4585
