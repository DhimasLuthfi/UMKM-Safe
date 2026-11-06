# UMKM-Safe (Automated Contract Risk Assessment & Legal Compliance Agent)

UMKM-Safe adalah agen AI interaktif berbasis multimodal yang dibangun menggunakan IBM Langflow Desktop. Proyek ini bertindak sebagai konsultan hukum dan negosiator digital pribadi bagi pelaku Usaha Mikro, Kecil, dan Menengah (UMKM) di Indonesia untuk mendeteksi klausul berbahaya (red flags) dalam dokumen perjanjian bisnis secara otomatis.

## Latar Belakang & Masalah (Problem Statement)

Sebagian besar pelaku UMKM dan pengusaha pemula di Indonesia sering menandatangani surat perjanjian kerja sama, konsinyasi, atau pasokan barang tanpa melalui proses peninjauan hukum (legal review). Faktor utama meliputi:

* Tingginya Biaya: Tidak adanya anggaran untuk menyewa jasa pengacara profesional.
* Kerumitan Bahasa Hukum: Istilah legal jargon yang kaku sulit dipahami oleh orang awam.

### Risiko & Klausul Berbahaya (Red Flags) yang Dideteksi:

1. Tempo Pembayaran Konsinyasi Sepihak: Pembayaran ditunda hingga 120 hari setelah laporan rekapitulasi.
2. Pemotongan Komisi & Promosi Mencekik: Potongan sepihak hingga 60% dari total penjualan kotor.
3. Pengambilalihan Hak Cipta & Resep Rahasia: Penyerahan formula/resep tanpa hak royalti.
4. Pelepasan Tanggung Jawab Barang: Pembebanan ganti rugi barang hilang/rusak di toko mitra sepenuhnya kepada UMKM.

## Fitur Utama & Keunggulan

* Native Multimodal Processing: Pengguna cukup memfoto lembar fisik kontrak (.png / .jpg) tanpa perlu mengetik ulang isi teks atau menggunakan pustaka parser eksternal.
* Klasifikasi Risk Level: Menilai tingkat risiko dokumen secara instan (High Risk, Medium Risk, atau Low Risk).
* Drafting Assistant (Kalimat Tandingan): Menghasilkan usulan contoh pasal revisi yang seimbang dan aman untuk diajukan UMKM saat negosiasi ulang.
* Bahasa Indonesia Ramah Awam: Menerjemahkan pasal-pasal hukum yang kaku menjadi poin tindakan praktis.

## Arsitektur & Alur Sistem (6-Node Pipeline)

Proyek ini dirancang menggunakan pendekatan Multi-Stage Pipeline (2-Stage LLM Process) untuk memisahkan fokus identifikasi risiko dan pembuatan draf solusi.

```text
[ Chat Input ] 
      │ (Foto / Berkas Gambar Kontrak)
      ▼
[ Prompt Template 1 ] ─── (Instruksi Identifikasi Risiko + Variabel {image_input})
      │
      ▼
[ Language Model 1 ] ──── (Evaluasi Risiko Hukum & Penentuan Risk Level)
      │
      │ (Output Tahap 1: Evaluasi & Risk Summary)
      ▼
[ Prompt Template 2 ] ─── (Instruksi Penyusunan Solusi + Variabel {risk_summary})
      │
      ▼
[ Language Model 2 ] ──── (Penyusunan Draf Kalimat Tandingan & Rekomendasi)
      │
      ▼
[ Chat Output ] ───────── (Laporan Interaktif di Playground)
```

### Rincian Fungsi Node:

1. Chat Input: Menerima unggahan foto/gambar dokumen perjanjian dari pengguna di Playground.
2. Prompt Template 1: Membungkus variabel {image_input} dengan panduan analisis evaluasi pasal bermasalah.
3. Language Model 1: Memproses gambar secara multimodal native untuk menghasilkan narasi risiko dan klasifikasi tingkat bahaya.
4. Prompt Template 2: Meneruskan hasil analisis dari LM 1 melalui variabel {risk_summary} ke tahap pembuatan solusi.
5. Language Model 2: Menerjemahkan risiko menjadi draf pasal tandingan dan rekomendasi tindakan praktis.
6. Chat Output: Menampilkan laporan evaluasi akhir secara terstruktur pada jendela percakapan.

## Spesifikasi Teknologi (Tech Stack)

* Orchestration Platform: IBM Langflow Desktop
* Pipeline Nodes: Chat Input, Prompt Template, Language Model, Chat Output
* Input Format: Image (.png, .jpg, .jpeg) / Document Scan

## Cara Menggunakan Proyek di Langflow

1. Clone Repository

2. Impor Flow ke Langflow Desktop:
   * Buka aplikasi IBM Langflow Desktop.
   * Klik Import di halaman utama canvas.
   * Pilih berkas `UMKM-Safe_Flow.json` yang ada di dalam repositori ini.

3. Konfigurasi Node Model:
   * Buka node Language Model 1 dan Language Model 2.
   * Masukkan API Key model Generative AI yang Anda gunakan pada masing-masing node.

4. Jalankan di Playground:
   * Buka Playground di pojok kanan atas canvas.
   * Unggah foto dokumen kontrak.
   * Tekan Enter dan lihat hasil analisis risiko serta draf kalimat tandingannya.
