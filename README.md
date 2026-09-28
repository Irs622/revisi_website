# Inpartner Website SEO Audit & Developer Handover Repository

Repository ini berisi hasil audit komprehensif, panduan revisi teknis, kamus metadata, dan spesifikasi implementasi SEO (Bahasa Inggris dan Bahasa Korea) untuk website **[Inpartner (PT Inpartner Optima Integra)](https://inpartner.id/)**.

---

## 📌 Panduan Navigasi Dokumen

Repository ini dibagi menjadi 2 pandangan utama: untuk **Manajemen Klien** dan untuk **Tim Developer**:

| Target Pembaca | Nama File Rekomendasi | Format | Deskripsi & Kegunaan |
| :--- | :--- | :---: | :--- |
| **Untuk Manajemen / Klien** | **[`RINGKASAN_EKSEKUTIF_AUDIT_UNTUK_KLIEN.md`](./RINGKASAN_EKSEKUTIF_AUDIT_UNTUK_KLIEN.md)** | `Markdown` | **Proposal & Laporan Eksekutif:** Menjelaskan masalah bisnis (kenapa traffic Korea 0, dampak 203 error Semrush, risiko typo terhadap klien asing), ringkasan solusi, dan proyeksi ROI tanpa bahasa koding rumit. |
| **Untuk Tim Developer** | **[`SEO_AUDIT_DAN_PANDUAN_REVISI_DEVELOPER.md`](./SEO_AUDIT_DAN_PANDUAN_REVISI_DEVELOPER.md)** | `Markdown` | **DOKUMEN TEKNIS UTAMA:** Berisi 18 tiket kerja (P0–P3), kode Next.js siap pakai (`next.config.js`, `_document.jsx`, `components/SEO.jsx`), tabel *find & replace* typo/slang, penerjemahan portofolio proyek, Schema JSON-LD, dan QA checklist. |
| **Untuk Tim Developer** | **[`developer_handover_final.json`](./developer_handover_final.json)** | `JSON` | **Kamus Data & Metadata:** Kamus tag `<title>`, `<meta description>`, `<h1>`, `<h2>`, dan teks revisi terstruktur siap pakai secara programatik. |
| **Aset Siap Salin** | **[`sitemap.xml`](./sitemap.xml)** & **[`ko-sitemap.xml`](./ko-sitemap.xml)** | `XML` | File XML sitemap bahasa Inggris dan bahasa Korea siap salin ke folder `public/`. |
| **Arsip Riset Internal** | **[`seo.json`](./seo.json)** & **[`seo_ko.json`](./seo_ko.json)** | `JSON` | Master database riset keyword dan taksonomi (Inggris & Korea) untuk tim konten/marketing. |

---

## 🎯 4 Fokus Revisi Paling Mendesak (Sprint P0)

1. **Routing Versi Korea:** Hapus widget client-side Google Translate (`#google_translate_element`), ganti dengan subpath statis `/ko/*` agar dapat diindeks mesin pencari.
2. **Koreksi Typo Fatal:** Perbaiki kata `"Busines"` pada kartu layanan utama di `pages/services.js` dan hapus slang informal `"give you a home run"`.
3. **Canonical & Hreflang:** Pasang tag `canonical` mandiri dan `hreflang` bilateral (`en`, `ko`, `x-default`) di seluruh halaman.
4. **Pecah Layanan Hash (`#`):** Buat URL mandiri untuk `/services/business-management-consulting`, `/services/investment`, dan `/services/capacity-building`.

---

## 👨‍💻 Kontak & Verifikasi

Jika ada pertanyaan teknis terkait implementasi atau penyesuaian kode, silakan merujuk pada checklist di **Bab 10** file [`SEO_AUDIT_DAN_PANDUAN_REVISI_DEVELOPER.md`](./SEO_AUDIT_DAN_PANDUAN_REVISI_DEVELOPER.md).
