# Studio Proyek 3 — Fine-Tuning Transformer Pretrained untuk NLP

**Mata Kuliah:** Pembelajaran Mendalam (IF25-40401) · **Kelas:** Deep Learning RA
**Program Studi:** Teknik Informatika, Institut Teknologi Sumatera (ITERA)

**Kelompok 15**

| No | Nama Lengkap | NIM |
|:-:|---|---|
| 1 | Muhammad Fadhilah Akbar | 123140003 |
| 2 | Muhammad Fajri Firdaus | 123140050 |

## Isi repositori

- `Studio_Proyek_3_FineTuning_SmSA.ipynb` — notebook utama (satu berkas, berisi seluruh eksperimen).

## Ringkasan tugas

Klasifikasi sentimen teks Bahasa Indonesia (negatif / netral / positif) pada dataset **SmSA (IndoNLU; Wilie dkk., 2020)** dengan cara *fine-tuning* Transformer pretrained lewat HuggingFace.

Rancangan eksperimen: **3 backbone × 3 strategi × 3 seed = 27 run**, protokol identik di semua run.

- Backbone: mBERT (`bert-base-multilingual-cased`), DistilmBERT (`distilbert-base-multilingual-cased`), IndoBERT (`indobenchmark/indobert-base-p1`). Model English-only tidak dipakai karena datasetnya Bahasa Indonesia.
- Strategi: full fine-tuning (baseline), partial freezing (embedding + separuh lapis awal), linear probing (hanya head).
- Head replacement ke 3 kelas berlaku di semua run. Evaluasi memakai pembagian validasi resmi karena label uji resmi disembunyikan.

Metrik per run: akurasi, F1 makro, waktu latih, waktu inferensi (ms/kalimat), parameter total dan yang dilatih, serta memori puncak. Hasil dilaporkan sebagai **rata-rata ± simpangan baku antar-seed**.

## Cara menjalankan

1. Buka notebook di Google Colab atau Kaggle, lalu aktifkan GPU T4 (Kaggle: nyalakan juga Internet).
2. **Uji jalan sekali:** set `UJI_JALAN = True` (bagian 2), lalu *Run all*. Notebook memakai subset kecil, 1 seed, 1 epoch, dan menyimpan hasil ke berkas `*_uji_*` supaya berkas resmi tidak tercampur.
3. **Eksperimen resmi:** set `UJI_JALAN = False`, tinjau bagian **Rancangan** (bagian 3), set `RANCANGAN_DIKONFIRMASI = True`, lalu *Run all*.
4. Notebook menolak mode `"penuh"` selama Rancangan belum lengkap/dikonfirmasi. Setiap run langsung disimpan ke CSV, jadi sesi yang terputus bisa dilanjutkan tanpa mengulang run yang sudah selesai.

## Keluaran

- `hasil_smsa_<kode>.csv` — semua run.
- `rekap_agregat_smsa_<kode>.csv` — rata-rata ± simpangan baku antar-seed.
- Grafik PNG (performa, trade-off, sebaran antar-seed, confusion matrix) dan arsip zip dari bagian 14.

## Catatan

Teks resmi **3 Pertanyaan Riset Wajib** tidak termuat di PDF spesifikasi. Pertanyaan tersebut dimintakan ke dosen, lalu jawabannya diisi pada bagian 13.3 notebook.

## Batas waktu

Notebook & berkas hasil: **20 November 2026**. Slide dan laporan singkat dikumpulkan saat hari presentasi.
