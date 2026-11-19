# Studio Proyek 3: Fine-Tuning Transformer Pretrained untuk NLP

Tugas Studio Proyek 3 mata kuliah Pembelajaran Mendalam (IF25-40401), kelas Deep Learning RA, Teknik Informatika ITERA.

Kelompok 15:

| No | Nama Lengkap | NIM |
|:-:|---|---|
| 1 | Muhammad Fadhilah Akbar | 123140003 |
| 2 | Muhammad Fajri Firdaus | 123140050 |

## Isi repositori

`Studio_Proyek_3_FineTuning_SmSA.ipynb` adalah notebook utama yang berisi seluruh eksperimen.

## Ringkasan

Kami melakukan fine-tuning model Transformer pretrained dari HuggingFace untuk klasifikasi sentimen kalimat Bahasa Indonesia (negatif, netral, positif) pada dataset SmSA dari IndoNLU (Wilie dkk., 2020).

Eksperimen terdiri dari 3 backbone, 3 strategi, dan 3 seed, sehingga totalnya 27 run dengan pengaturan yang sama.

- Backbone: mBERT (`bert-base-multilingual-cased`), DistilmBERT (`distilbert-base-multilingual-cased`), dan IndoBERT (`indobenchmark/indobert-base-p1`). Model khusus bahasa Inggris tidak dipakai karena datanya berbahasa Indonesia.
- Strategi: full fine-tuning sebagai baseline, partial freezing (embedding dan separuh lapis awal dibekukan), dan linear probing (hanya head yang dilatih).
- Head klasifikasi diganti menjadi 3 kelas di semua run.
- Data latih berjumlah 6.000 kalimat (subset terstratifikasi). Data validasi resmi hanya dipakai untuk memilih epoch terbaik, dan data uji memakai seluruh 500 kalimat uji resmi (`test_preprocess.tsv`).
- Sebagai pembanding, kami memakai TF-IDF + regresi logistik dan tebakan acak pada data uji yang sama.

Setiap run mencatat akurasi, F1 makro, waktu latih, waktu inferensi (ms/kalimat), jumlah parameter total dan yang dilatih, serta memori puncak. Hasil dilaporkan sebagai rata-rata dan simpangan baku dari 3 seed.

## Cara menjalankan

1. Buka notebook di Google Colab atau Kaggle, lalu aktifkan GPU T4. Di Kaggle, nyalakan juga akses Internet.
2. Untuk uji jalan, ubah `UJI_JALAN = True` di bagian 2 lalu jalankan semua sel. Mode ini hanya memakai subset kecil, 1 seed, dan 1 epoch, dan hasilnya disimpan terpisah di berkas `*_uji_*`.
3. Untuk eksperimen sebenarnya, kembalikan `UJI_JALAN = False`, periksa bagian Rancangan (bagian 3), ubah `RANCANGAN_DIKONFIRMASI = True`, lalu jalankan semua sel.
4. Setiap run langsung disimpan ke CSV. Jika sesi Colab terputus, jalankan ulang notebook dan run yang sudah selesai akan dilewati.

## Berkas hasil

- `hasil_smsa_<kode>.csv`: hasil semua run.
- `rekap_agregat_smsa_<kode>.csv`: rata-rata dan simpangan baku antar-seed.
- `baseline_smsa_<kode>.csv`: skor TF-IDF dan tebakan acak.
- Grafik (performa, trade-off, sebaran antar-seed, confusion matrix) dan arsip zip dari bagian 14.

## Pertanyaan riset

1. Backbone mana yang memberi keseimbangan terbaik antara akurasi dan efisiensi?
2. Apakah strategi yang lebih hemat (probing dan partial) cukup bersaing dengan full fine-tuning?
3. Kombinasi mana yang kami rekomendasikan, dan apa alasannya?

Tabel pendukungnya ada di bagian 12.1 notebook, sedangkan pembahasan dan jawabannya ada di bagian 13.
