# UASDL - Struktur Proyek

Dokumentasi singkat yang menjelaskan seluruh struktur folder di proyek ini.

## Ikhtisar

Proyek ini berisi beberapa tugas/eksperimen yang dikelompokkan dalam folder `task1`, `task2`, dan `task3`.
Setiap `task` biasanya memiliki subfolder untuk laporan (`LAPORAN`) dan notebook/hasil eksperimen (`NOTEBOOK`).

---

## Struktur Utama

- **task1/**: Koleksi eksperimen terkait beberapa dataset dan model (agnews, goemotions, mnli).
  - **agnews/**
    - **LAPORAN/**: Dokumentasi laporan, berisi `README.md` yang menjelaskan eksperimen AGNews.
    - **NOTEBOOK/**: Notebook Jupyter untuk eksperimen (`test.ipynb`) dan folder `fine-tuned-bert-agnews/` yang berisi artifact model hasil fine-tune:
      - `config.json`, `model.safetensors`, `tokenizer.json`, `vocab.txt`, dsb.
      - `results/`: Hasil evaluasi, metrik, atau file keluaran lain.

  - **goemotions/**
    - **LAPORAN/**: Laporan eksperimen GoEmotions.
    - **NOTEBOOK/**: Notebook (`testing.ipynb`) dan direktori model `goemotions-bert/` yang menyimpan beberapa checkpoint (`checkpoint-2714/`, `checkpoint-5428/`, `checkpoint-8142/`).

  - **mnli/**
    - **LAPORAN/**: Laporan eksperimen MNLI.
    - **NOTEBOOK/**: Notebook (`test.ipynb`) dan folder `mnli-bert-finetuned/` yang berisi model fine-tuned dan checkpoint (`checkpoint-49088/`).

  - **virtualenvdl/**: Virtual environment Python yang digunakan untuk menjalankan eksperimen.
    - `bin/`: Berisi executable seperti `python`, `pip`, `transformers`, `accelerate`, `jupyter`, dsb.
    - `lib/`, `include/`, dan `pyvenv.cfg`.

- **task2/**: Eksperimen lain yang terpisah dari `task1`.
  - **LAPORAN/**: Menyimpan laporan dan file terkait (`test.ipynb`, `t5-finetuned-squad/`).
  - **NOTEBOOK/**: README atau notebook ringkasan eksperimen.

- **task3/**: Eksperimen lanjutan (mis. fine-tuning model untuk tugas ringkasan).
  - **LAPORAN/**: Dokumentasi hasil eksperimen.
  - **NOTEBOOK/**: Notebook `fine_tune_phi2.ipynb` dan beberapa model/folder hasil fine-tune seperti `phi2-xsum-final/` dan `phi2-xsum-finetuned/`.
    - `phi2-xsum-final/` berisi adapter, tokenizer, dan file model (`adapter_model.safetensors`, `tokenizer.json`, `vocab.json`, dll.).
    - `phi2-xsum-finetuned/` berisi checkpoint-checkpoint (mis. `checkpoint-500/`, `checkpoint-625/`) dan file terkait.

## Penjelasan Umum Isi Folder

- `LAPORAN/`: Materi tertulis yang menjelaskan metodologi, hasil, dan analisis. Biasanya berformat Markdown atau notebook.
- `NOTEBOOK/`: Notebook Jupyter yang digunakan untuk eksperimen, pelatihan, dan evaluasi.
- Folder model (mis. `*-bert-finetuned/`, `*-final/`, `checkpoint-*`): Menyimpan konfigurasi model (`config.json`), bobot model (`*.safetensors`), tokenizer (`tokenizer.json`, `vocab.txt`), dan file tambahan seperti `special_tokens_map.json`.
- `virtualenvdl/`: Virtual environment lokal yang berisi dependensi untuk menjalankan notebook dan skrip dalam proyek ini.


Jika Anda ingin, saya dapat:
- Menambahkan penjelasan lebih rinci untuk salah satu `task` tertentu.
- Menyusun daftar per-file artifact dan ukuran file untuk tiap model.

