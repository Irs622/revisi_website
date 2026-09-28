# Inpartner Website SEO Audit & Developer Handover Repository

Repository ini berisi hasil audit komprehensif, panduan revisi teknis, kamus metadata, dan spesifikasi implementasi SEO (Bahasa Inggris dan Bahasa Korea) untuk website **[Inpartner (PT Inpartner Optima Integra)](https://inpartner.id/)**.

> [!NOTE]
> Seluruh panduan, potongan kode Next.js, kamus JSON, dan sitemap XML dalam repository ini disusun oleh tim auditor eksternal untuk **langsung diserahkan kepada tim web developer lama/eksisting** dan **manajemen Inpartner** tanpa memerlukan akses langsung ke server produksi.

---

## 📌 Panduan Navigasi Dokumen

Repository ini dibagi menjadi 2 pandangan utama: untuk **Manajemen Klien** dan untuk **Tim Developer**:

| Target Pembaca | Nama File Rekomendasi | Format | Deskripsi & Kegunaan |
| :--- | :--- | :---: | :--- |
| **Untuk Manajemen / Klien** | **[`RINGKASAN_EKSEKUTIF_AUDIT_UNTUK_KLIEN.md`](./RINGKASAN_EKSEKUTIF_AUDIT_UNTUK_KLIEN.md)** | `Markdown` | **Proposal & Laporan Eksekutif:** Menjelaskan masalah bisnis (kenapa traffic Korea 0, dampak 203 error Semrush, risiko typo terhadap klien asing), ringkasan solusi, dan proyeksi ROI tanpa bahasa koding rumit. |
| **Untuk Tim Developer** | **[`SEO_AUDIT_DAN_PANDUAN_REVISI_DEVELOPER.md`](./SEO_AUDIT_DAN_PANDUAN_REVISI_DEVELOPER.md)** | `Markdown` | **DOKUMEN TEKNIS UTAMA:** Berisi 18 tiket kerja (P0–P3), kode Next.js siap pakai (`next.config.js`, `_document.jsx`, `components/SEO.jsx`), tabel *find & replace* typo/slang, penerjemahan portofolio proyek, Schema JSON-LD, dan QA checklist. |
| **Untuk Tim Developer** | **[`developer_handover_final.json`](./developer_handover_final.json)** | `JSON` | **Kamus Data & Metadata:** Kamus tag `<title>`, `<meta description>`, `<h1>`, `<h2>`, dan teks revisi terstruktur siap pakai secara programatik. |
| **Aset Siap Salin** | **[`sitemap.xml`](./sitemap.xml)** & **[`ko-sitemap.xml`](./ko-sitemap.xml)** | `XML` | File XML sitemap bahasa Inggris dan bahasa Korea siap salin ke folder `public/`. |
| **Arsip Riset Internal** | **[`english_seo.json`](./english_seo.json)** & **[`korean_seo.json`](./korean_seo.json)** | `JSON` | Database audit teknis lengkap per halaman untuk versi Inggris dan Korea. |
| **Arsip Riset Keyword** | **[`seo.json`](./seo.json)** & **[`seo_ko.json`](./seo_ko.json)** | `JSON` | Master database riset keyword dan taksonomi (Inggris & Korea) untuk tim konten/marketing. |

---

## 📊 Benchmark Audit Pihak Ketiga (Semrush Site Audit - 25 Sept 2026)

* **Skor Kesehatan Situs (Site Health):** `74%` | **AI Search Health:** `83%`
* **Total Halaman Dirayapi:** 80 halaman (76 halaman memiliki isu teknis, 3 broken link 404, hanya 1 halaman sehat).
* **Total Isu Terdeteksi:** **203 Errors** dan **154 Warnings**.
* **5 Masalah Terbesar yang Diselesaikan di Repo Ini:**
  1. **72 Duplicate Title Tags:** Terbawa dari judul layout statis &rarr; diselesaikan via `metadata_dictionary` & `components/SEO.jsx` (TIKET-03, TIKET-11).
  2. **72 Duplicate Content Issues:** Tidak adanya canonical tag &rarr; diselesaikan via self-referencing canonical (TIKET-03).
  3. **56 Duplicate Meta Descriptions:** Definisi kamus umum bocor ke semua sub-halaman &rarr; diselesaikan via kamus metadata dinamis (TIKET-07, TIKET-11).
  4. **16 Missing Meta Descriptions:** Halaman artikel `/blog` tanpa deskripsi &rarr; diselesaikan via dynamic excerpt (TIKET-17).
  5. **3 Broken Pages (404):** Tautan mati internal &rarr; diselesaikan via 301 permanent redirect di `next.config.js` (TIKET-18).

---

## 🎯 4 Fokus Revisi Paling Mendesak (Sprint P0)

1. **Routing Versi Korea:** Hapus widget client-side Google Translate (`#google_translate_element`), ganti dengan subpath statis `/ko/*` agar dapat diindeks mesin pencari.
2. **Koreksi Typo Fatal:** Perbaiki kata `"Busines"` pada kartu layanan utama di `pages/services.js` dan hapus slang informal `"give you a home run"`.
3. **Canonical & Hreflang:** Pasang tag `canonical` mandiri dan `hreflang` bilateral (`en`, `ko`, `x-default`) di seluruh halaman.
4. **Pecah Layanan Hash (`#`):** Buat URL mandiri untuk `/services/business-management-consulting`, `/services/investment`, dan `/services/capacity-building`.

---

## 🗂️ Struktur File Repositori

```text
seoo/
├── README.md                                  # Panduan navigasi utama repositori
├── RINGKASAN_EKSEKUTIF_AUDIT_UNTUK_KLIEN.md   # Laporan & proposal bisnis untuk Direksi Inpartner
├── SEO_AUDIT_DAN_PANDUAN_REVISI_DEVELOPER.md  # Dokumen teknis 18 tiket & kode Next.js developer
├── developer_handover_final.json              # Kamus data metadata, diffs, & schema JSON-LD
├── sitemap.xml                                # Sitemap XML versi Bahasa Inggris
├── ko-sitemap.xml                             # Sitemap XML versi Bahasa Korea
├── english_seo.json                           # Audit teknis & spesifikasi halaman Inggris
├── korean_seo.json                            # Audit teknis & spesifikasi halaman Korea
├── seo.json                                   # Riset kata kunci & taksonomi Bahasa Inggris
└── seo_ko.json                                # Riset kata kunci & taksonomi Bahasa Korea
```

---

## 👨‍💻 Verifikasi & Kontribusi

* **Author / Auditor:** `irsalshydiq` (`ichalprov@gmail.com`)
* **Remote Repository:** [GitHub - Irs622/revisi_website](https://github.com/Irs622/revisi_website)
* Untuk checklist pengujian sebelum deployment rilis ke produksi, lihat **Bab 10 QA Checklist** di [`SEO_AUDIT_DAN_PANDUAN_REVISI_DEVELOPER.md`](./SEO_AUDIT_DAN_PANDUAN_REVISI_DEVELOPER.md).
