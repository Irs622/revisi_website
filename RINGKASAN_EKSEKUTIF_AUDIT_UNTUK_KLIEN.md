# LAPORAN AUDIT WEBSITE & PROPOSAL REKOMENDASI REVISI
**Untuk Manajemen / Klien:** PT Inpartner Optima Integra (`https://inpartner.id/`)  
**Penyusun:** Tim Konsultan & Auditor SEO Independen  
**Tanggal:** 28 September 2026  
**Status Audit:** Selesai (Final Proposal & Handover Package)  

---

## 1. Surat Pengantar & Ringkasan untuk Manajemen

Kepada Yth.  
**Manajemen PT Inpartner Optima Integra**,

Kami telah menyelesaikan audit independen dan menyeluruh terhadap performa website resmi **Inpartner (`https://inpartner.id/`)**, mencakup aspek teknis web (*Next.js architecture*), visibilitas mesin pencari (*Google & Naver*), kesiapan pasar internasional (*versi Bahasa Inggris & Bahasa Korea*), serta data *benchmark* industri dari crawler pihak ketiga (**Semrush Site Audit per 25 September 2026**).

Karena kami bertindak sebagai pihak auditor eksternal tanpa akses langsung ke repositori kode sumber (*source code*), seluruh hasil temuan audit ini telah kami formulasikan menjadi **Paket Proposal Rekomendasi Revisi Siap Eksekusi**. Dokumen teknis dan aset pendukungnya telah kami siapkan secara spesifik agar manajemen Inpartner dapat **langsung meneruskannya kepada tim web developer lama/eksisting** untuk dikerjakan tanpa perlu perdebatan teknis.

---

## 2. Tiga Temuan Kritis yang Perlu Diketahui Manajemen

```
+-----------------------------------------------------------------------------------------+
|                                KONDISI KESEHATAN WEBSITE SAAT INI                       |
+--------------------------+---------------------+----------------------------------------+
| Parameter Audit          | Skor Kesehatan      | Dampak Nyata terhadap Bisnis Inpartner |
+--------------------------+---------------------+----------------------------------------+
| Versi Bahasa Korea (KO)  | 15 / 100 (Kritis)   | 0% Terindeks di Google Korea & Naver   |
| Versi Bahasa Inggris (EN)| 32 / 100 (Tinggi)   | Bocoran Kredibilitas & Lead B2B        |
| Semrush Site Health      | 74% (203 Errors)    | 95% Halaman Memiliki Masalah Teknis    |
+--------------------------+---------------------+----------------------------------------+
```

### 1. Masalah Fatal Versi Korea (0% Visibilitas Mesin Pencari)
* **Kondisi Riil:** Tombol "KR" pada navigasi website Inpartner saat ini hanya berupa pemantik widget penerjemah otomatis **Google Translate** di peramban pengguna. Tidak ada halaman fisik berbahasa Korea (tidak ada rute `/ko`).
* **Kerugian Bisnis:** Robot mesin pencari (**Google Korea** dan **Naver** yang menguasai lebih dari 60% pasar Korea) **tidak membaca hasil terjemahan widget tersebut**. Akibatnya, website Inpartner **100% tidak ada (invisible)** dalam hasil pencarian di Korea Selatan. Padahal, minat investor dan perusahaan Korea untuk masuk ke pasar Indonesia (FDI) di sektor hilirisasi industri, energi, dan infrastruktur sangat tinggi.

### 2. Typo Fatal & Bahasa Non-Formal yang Merusak Citra B2B
* **Kondisi Riil:** Pada kartu layanan konsultasi bisnis utama di halaman `/services`, terdapat salah ketik mencolok: **`"Busines and Management Consulting"`** (kurang huruf 's'). 
* Pada nama legal entitas resmi di halaman About terdapat typo: **`"PT Inpartrner Optima Integra"`** (kelebihan huruf 'r').
* Terdapat penggunaan istilah slang olahraga bisbol: **`"give you a home run"`** pada halaman muka dan About Us, serta salah ketik wilayah **`"East Jave"`** alih-alih *East Java*.
* **Kerugian Bisnis:** Klien korporasi multinasional dan investor asing melakukan *due diligence* ketat sebelum menunjuk konsultan manajemen. Kesalahan ketik pada nama layanan dan entitas resmi menurunkan impresi profesionalisme firma.

### 3. Portofolio Proyek Masih Berbahasa Indonesia di Halaman Inggris (`/project`)
* **Kondisi Riil:** Saat investor luar negeri membuka halaman rekam jejak `inpartner.id/project`, 90% judul proyek masih tertulis dalam bahasa Indonesia mentah (misal: *"Penyusunan Laporan Sektor Riil pada Badan Usaha Jalan Tol (BUJT)"*, *"Jasa Pembuatan Website"*).
* **Kerugian Bisnis:** Calon klien asing tidak dapat memahami skala keahlian dan nilai strategis dari proyek-proyek prestisius yang pernah diselesaikan Inpartner.

---

## 3. Hasil Validasi Tool Audit Pihak Ketiga (Semrush - 25 September 2026)

Audit kami diperkuat oleh hasil pemindaian independen software SEO global, **Semrush**, yang mendeteksi **203 Errors** dan **154 Warnings** pada domain `inpartner.id`:

* **72 Masalah Judul Halaman Duplikat (*Duplicate Title Tags*):** Disebabkan karena judul halaman utama terbawa ke seluruh sub-halaman tanpa diganti secara dinamis.
* **72 Masalah Konten Duplikat (*Duplicate Content*):** Disebabkan karena website **tidak memiliki tag Canonical** sama sekali, sehingga URL dengan parameter dianggap sebagai puluhan halaman kembar.
* **56 Deskripsi Meta Duplikat:** Halaman `/project` dan `/blog` memiliki teks deskripsi meta yang sama persis (berupa definisi kamus tentang manajemen proyek).
* **3 Halaman Rusak (*Broken Links 404*):** Ada tautan internal yang mengarah ke halaman mati.

---

## 4. Solusi & Dokumen yang Telah Kami Siapkan untuk Klien

Agar manajemen Inpartner tidak perlu pusing memikirkan teknis kodingnya, kami telah menyiapkan **Paket Handover Lengkap** yang disimpan di repository GitHub:  
👉 **`git@github.com:Irs622/revisi_website.git`**

### Isi Paket yang Siap Diteruskan ke Developer:
1. **Panduan Tiket Developer ([`SEO_AUDIT_DAN_PANDUAN_REVISI_DEVELOPER.md`](./SEO_AUDIT_DAN_PANDUAN_REVISI_DEVELOPER.md)):**  
   Berisi 18 tiket kerja prioritas (P0 hingga P3), potongan kode Next.js siap salin (`next.config.js`, `_document.jsx`, `components/SEO.jsx`), tabel *find-and-replace* untuk memperbaiki typo, dan checklist uji coba.
2. **Kamus Data Metadata ([`developer_handover_final.json`](./developer_handover_final.json)):**  
   Daftar judul halaman (`<title>`), deskripsi (`<meta description>`), dan heading (`<h1>` & `<h2>`) baru dalam bahasa Inggris dan bahasa Korea.
3. **Penerjemahan Portofolio Proyek:**  
   Judul-judul proyek lama Inpartner telah diterjemahkan ke bahasa Inggris dan bahasa Korea formal yang berbobot (*bankable*).
4. **File Sitemap XML Siap Pakai ([`sitemap.xml`](./sitemap.xml) & [`ko-sitemap.xml`](./ko-sitemap.xml)):**  
   Developer tinggal menyalin kedua file ini ke folder `public/` website.

---

## 5. Proyeksi Dampak Setelah Revisi Diterapkan

| Indikator Kinerja | Kondisi Saat Ini | Target Setelah Revisi Selesai (90 Hari) |
| :--- | :---: | :---: |
| **Indeks Halaman Bahasa Korea** | 0% (Tidak terindeks) | **100% Terindeks** di Naver & Google Korea |
| **Skor Semrush Site Health** | 74% (203 Errors) | **> 92% (Errors turun mendekati 0)** |
| **Error Duplicate Content & Title** | 144 Kasus | **0 Kasus (Teratasi via Canonical & Metadata)** |
| **Impresi & Click-Through-Rate (CTR)**| Rendah / Terfragmentasi | **Peningkatan CTR 35% – 50% di Google** |
| **Kredibilitas B2B & Konversi Lead** | Terhambat typo & slang | **Meningkat signifikan bagi investor asing** |

---

## 6. Langkah Tindak Lanjut yang Direkomendasikan bagi Klien

1. **Teruskan Repository ke Tim Developer:**  
   Kirimkan tautan repository `git@github.com:Irs622/revisi_website.git` kepada tim developer lama Inpartner.
2. **Instruksikan Pengerjaan Sprint P0 (Minggu 1–2):**  
   Minta developer memprioritaskan Tiket P0 (perbaikan routing Korea `/ko/`, perbaikan typo `"Busines"`, penghapusan slang `"home run"`, dan pemasangan tag canonical).
3. **Siapkan 1 Aset Internal (Profil Tim):**  
   Siapkan foto dan bio singkat 3–4 konsultan/partner Inpartner untuk mengisi tombol *"Meet our Team"* di halaman About yang saat ini masih kosong.
