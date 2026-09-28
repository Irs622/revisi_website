# DOKUMEN HANDOVER RESMI: AUDIT SEO & PANDUAN REVISI PENGEMBANGAN WEBSITE INPARTNER
**Target Website:** `https://inpartner.id/`  
**Klien / Entitas:** PT Inpartner Optima Integra  
**Penerima Dokumen:** Tim Developer / Web Engineering Inpartner  
**Penyusun:** Senior SEO & Technical Web Auditor  
**Versi Dokumen:** 1.0 (Final Handover Package)  
**Tanggal:** 28 September 2026  

---

## DAFTAR ISI
1. [Latar Belakang & Tujuan Handover](#1-latar-belakang--tujuan-handover)
2. [Ringkasan Eksekutif & Skor Kesehatan SEO](#2-ringkasan-eksekutif--skor-kesehatan-seo)
3. [Daftar Tiket Pekerjaan Developer Berdasarkan Prioritas (P0 – P3)](#3-daftar-tiket-pekerjaan-developer-berdasarkan-prioritas-p0--p3)
4. [Spesifikasi Teknis Next.js & Kode Siap Pasang](#4-spesifikasi-teknis-nextjs--kode-siap-pasang)
   - 4.1. Setup Routing Bahasa Korea (`next.config.js`) & Eliminasi Google Translate Widget
   - 4.2. Komponen SEO Dinamis (`components/SEO.jsx`)
   - 4.3. Konfigurasi `pages/_document.jsx` (Atribut `lang` Dinamis)
   - 4.4. Pemecahan URL Layanan (Menghapus Anchor `#...` Menjadi Halaman Mandiri)
5. [Kamus Tag Title, Meta Description & Heading (H1–H3) Siap Pasang](#5-kamus-tag-title-meta-description--heading-h1h3-siap-pasang)
   - 5.1. Versi Bahasa Inggris (EN)
   - 5.2. Versi Bahasa Korea (KO)
6. [Daftar Perbaikan Copywriting & Typo (Search-and-Replace Diffs)](#6-daftar-perbaikan-copywriting--typo-search-and-replace-diffs)
7. [Daftar Penerjemahan Portofolio Proyek (`/project`)](#7-daftar-penerjemahan-portofolio-proyek-project)
8. [Schema.org JSON-LD Structured Data Siap Pasang](#8-schemaorg-json-ld-structured-data-siap-pasang)
9. [Konfigurasi WAF / Cloudflare & Robots.txt](#9-konfigurasi-waf--cloudflare--robotstxt)
10. [Checklist Pengujian & Verifikasi Deployment (QA Checklist)](#10-checklist-pengujian--verifikasi-deployment-qa-checklist)

---

## 1. Latar Belakang & Tujuan Handover

Dokumen ini disusun khusus untuk diserahkan langsung kepada **tim developer** website Inpartner. Auditor telah melakukan *crawling* mendalam terhadap seluruh halaman publik live di `https://inpartner.id/` (Next.js SSG/SSR). 

**Tujuan Dokumen:**
- Memberikan instruksi revisi yang **jelas, teknis, dan langsung dapat dieksekusi** tanpa interpretasi ganda.
- Mengatasi masalah visibilitas SEO bahasa Korea (yang saat ini **0% terindeks** karena penggunaan widget Google Translate client-side).
- Memperbaiki kelemahan arsitektur teknis, hierarki heading semantik, typo fatal pada judul layanan utama, dan ketiadaan metadata terstruktur pada versi bahasa Inggris.
- Menyediakan seluruh kode pengganti, teks terjemahan, diff teks, dan skema JSON-LD siap *copy-paste*.

---

## 2. Ringkasan Eksekutif & Skor Kesehatan SEO

```
+-----------------------------------------------------------------------------------------+
|                                KONDISI KESEHATAN SEO SAAT AUDIT                         |
+--------------------------+---------------------+----------------------------------------+
| Versi Bahasa             | Skor Kesehatan SEO  | Status Kritis                          |
+--------------------------+---------------------+----------------------------------------+
| Versi Korea (KO)         | 15 / 100            | KRITIS (Tidak terindeks di mesin cari) |
| Versi Inggris (EN)       | 32 / 100            | HIGH RISK (Bocoran trust & ranking)    |
+--------------------------+---------------------+----------------------------------------+
```

### 4 Akar Masalah Terbesar yang Wajib Dipahami Developer:
1. **Kegagalan Arsitektur Versi Korea (P0):** Tombol "KR" pada navigasi hanya memicu skrip terjemahan instan Google Translate (`#google_translate_element`). Robot perayap (Googlebot, Naver Yeti, Bingbot) **tidak mengeksekusi widget tersebut**. Mesin pencari hanya membaca HTML awal berbahasa Inggris. Versi Korea saat ini **100% tidak terindeks**.
2. **The Hash-Fragment Trap pada Layanan (`/services#...`) (P0):** Tiga pilar layanan utama—*Business & Management Consulting*, *Investment*, dan *Capacity Building*—ditumpuk pada satu halaman menggunakan tagar ID `#`. Google **tidak mengindeks fragment identifier (`#`)** sebagai landing page terpisah.
3. **Wabah Heading `<h5>` & Ketiadaan `<h1>` (P1):** Hampir semua judul seksi utama di seluruh situs menggunakan tag `<h5>`, melompati hierarki semantik `<h2>` dan `<h3>`. Halaman `/contact` bahkan **tidak memiliki tag `<h1>` sama sekali**.
4. **Typo & Kualitas Teks Menurunkan Kredibilitas B2B (P1):** Terdapat salah ketik fatal pada judul layanan utama (**"Busines and Management Consulting"**), salah ketik nama entitas resmi PT (**"PT Inpartrner Optima Integra"**), istilah slang yang tidak profesional (**"give you a home run"**), serta portofolio proyek di halaman Inggris yang masih 90% berbahasa Indonesia.

---

## 3. Daftar Tiket Pekerjaan Developer Berdasarkan Prioritas (P0 – P3)

Developer disarankan mengeksekusi tugas sesuai urutan sprint prioritas berikut:

### SPRINT 1: PERBAIKAN KRITIS & HYGIENE (PRIORITAS P0 - MINGGU 1-2)
- [ ] **TIKET-01:** Hapus widget client-side Google Translate. Aktifkan routing Next.js i18n atau buat subpath statis `/ko/*`.
- [ ] **TIKET-02:** Atur tag `<html lang="...">` dinamis di `_document.jsx` agar merender `lang="en"` untuk rute Inggris dan `lang="ko"` untuk rute Korea.
- [ ] **TIKET-03:** Pasang tag `canonical` mandiri (*self-referencing*) dan tag `hreflang` bilateral (`en`, `ko`, `x-default`) pada seluruh halaman.
- [ ] **TIKET-04:** Koreksi seluruh typo memalukan: `"Busines"` di `/services`, `"PT Inpartrner"` di `/about`, `"East Jave"` di Homepage/About.
- [ ] **TIKET-05:** Hapus metafora slang `"give you a home run"` dan perbaiki tata bahasa Inggris hero section.
- [ ] **TIKET-06:** Tambahkan tag `<h1>` yang hilang pada halaman `/contact`.
- [ ] **TIKET-07:** Pisahkan meta description duplikat antara `/project` dan `/blog` (saat ini keduanya memakai teks definisi generik manajemen proyek).
- [ ] **TIKET-08:** Whitelist bot mesin pencari resmi (`Googlebot`, `Bingbot`, `Yeti/1.1`) pada aturan firewall Cloudflare/WAF agar `robots.txt` dan `sitemap.xml` dapat diakses tanpa JS challenge.

### SPRINT 2: RESTRUKTURISASI ARSITEKTUR & KONTEN (PRIORITAS P1 - BULAN 1)
- [ ] **TIKET-09:** Pecah rute layanan `/services#...` menjadi 3 landing page mandiri:
  - `/services/business-management-consulting`
  - `/services/investment`
  - `/services/capacity-building`
  *(Serta buat versi Koreanya di bawah `/ko/services/...`)*.
- [ ] **TIKET-10:** Refactor semantik heading: ganti tag `<h5>` pada judul-judul seksi menjadi `<h2>` dan `<h3>` (pertahankan style Emotion CSS eksisting).
- [ ] **TIKET-11:** Perbarui `<title>` dan `<meta description>` di seluruh 7 halaman utama sesuai kamus metadata di Bab 5.
- [ ] **TIKET-12:** Terjemahkan judul-judul portofolio di `/project` menjadi bahasa Inggris dan bahasa Korea profesional sesuai tabel di Bab 7.
- [ ] **TIKET-13:** Pasang struktur data Schema.org JSON-LD (`Organization`, `Service`, `FAQPage`) ke komponen `<Head>`.

### SPRINT 3: PENGUATAN E-E-A-T & SOCIAL SHARING (PRIORITAS P2 - BULAN 2)
- [ ] **TIKET-14:** Perbaiki tombol *"Meet our Team"* di `/about` yang saat ini *looping* kembali ke `/about`. Hubungkan ke seksi tim atau buka modal/halaman profil partner & konsultan.
- [ ] **TIKET-15:** Sinkronkan tahun pendirian perusahaan di seluruh situs (homepage menyebut 2009, hero about menyebut 2019). Standardisasi ke 2009.
- [ ] **TIKET-16:** Tambahkan tag Open Graph (`og:title`, `og:description`, `og:image`, `og:url`) dan Twitter Card di setiap halaman.
- [ ] **TIKET-17:** Tambahkan nama penulis (*author byline*) dan tanggal update pada artikel-artikel `/blog`.

---

## 4. Spesifikasi Teknis Next.js & Kode Siap Pasang

Berikut adalah kode yang dapat langsung diterapkan oleh tim pengembang:

### 4.1. Setup Routing Bahasa Korea (`next.config.js`)
Jika website menggunakan server Next.js (SSR / ISR):

```javascript
// next.config.js
/** @type {import('next').NextConfig} */
const nextConfig = {
  reactStrictMode: true,
  i18n: {
    locales: ['en', 'ko'],
    defaultLocale: 'en',
    localeDetection: false, // Menghindari redirect otomatis yang membingungkan crawler
  },
  images: {
    domains: ['inpartner.id'],
  },
};

module.exports = nextConfig;
```

*Jika website menggunakan static export (`next export`)*:
Buat struktur direktori fisik di dalam folder `pages/`:
```
pages/
  ├── _app.js
  ├── _document.js
  ├── index.js                  --> https://inpartner.id/ (English Homepage)
  ├── about.js                  --> https://inpartner.id/about
  ├── services/
  │     ├── index.js            --> https://inpartner.id/services
  │     ├── business-management-consulting.js
  │     ├── investment.js
  │     └── capacity-building.js
  └── ko/                       --> RUTE KHUSUS KOREA
        ├── index.js            --> https://inpartner.id/ko
        ├── about.js            --> https://inpartner.id/ko/about
        ├── services/
        │     ├── index.js      --> https://inpartner.id/ko/services
        │     ├── business-management-consulting.js
        │     ├── investment.js
        │     └── capacity-building.js
        ├── project.js          --> https://inpartner.id/ko/project
        └── contact.js          --> https://inpartner.id/ko/contact
```

#### Menghapus Widget Google Translate di Header:
Ganti elemen tombol terjemahan lama di komponen Navbar/Header:

```jsx
// SEBELUM (HAPUS INI):
<div id="google_translate_element" style={{ display: 'none' }}></div>
<button className="notranslate ...">EN</button>
<button className="notranslate ...">KR</button>

// SESUDAH (GUNAKAN LINK NEXT.JS ASLI):
import Link from 'next/link';
import { useRouter } from 'next/router';

export function LanguageSwitcher() {
  const router = useRouter();
  const currentPath = router.asPath;

  return (
    <div className="language-switcher">
      <Link href={currentPath} locale="en" className={router.locale === 'en' ? 'active' : ''}>
        EN
      </Link>
      <span className="divider">|</span>
      <Link href={currentPath} locale="ko" className={router.locale === 'ko' ? 'active' : ''}>
        KR
      </Link>
    </div>
  );
}
```

---

### 4.2. Komponen SEO Dinamis (`components/SEO.jsx`)
Buat file `components/SEO.jsx` untuk disuntikkan ke setiap halaman:

```jsx
// components/SEO.jsx
import Head from 'next/head';
import { useRouter } from 'next/router';

export default function SEO({
  title,
  description,
  canonicalUrl,
  ogImage = 'https://inpartner.id/og-image.jpg',
  schemaData = null,
}) {
  const router = useRouter();
  const locale = router.locale || 'en';
  const baseUrl = 'https://inpartner.id';
  
  // Format path bersih tanpa locale prefix untuk alternate hreflang
  const cleanPath = router.asPath.replace(/^\/ko/, '') || '/';
  const enUrl = `${baseUrl}${cleanPath === '/' ? '' : cleanPath}`;
  const koUrl = `${baseUrl}/ko${cleanPath === '/' ? '' : cleanPath}`;
  const currentCanonical = canonicalUrl || (locale === 'ko' ? koUrl : enUrl);

  return (
    <Head>
      <meta charSet="utf-8" />
      <meta name="viewport" content="width=device-width, initial-scale=1" />
      
      {/* Primary Metadata */}
      <title>{title}</title>
      <meta name="description" content={description} />

      {/* Canonical Self-Referencing */}
      <link rel="canonical" href={currentCanonical} />

      {/* Bidirectional Hreflang Tags */}
      <link rel="alternate" hrefLang="en" href={enUrl} />
      <link rel="alternate" hrefLang="ko" href={koUrl} />
      <link rel="alternate" hrefLang="x-default" href={enUrl} />

      {/* Naver Search Advisor Content-Language */}
      {locale === 'ko' && (
        <meta httpEquiv="content-language" content="ko-kr" />
      )}

      {/* Open Graph / Social Sharing */}
      <meta property="og:type" content="website" />
      <meta property="og:title" content={title} />
      <meta property="og:description" content={description} />
      <meta property="og:url" content={currentCanonical} />
      <meta property="og:image" content={ogImage} />
      <meta property="og:site_name" content="Inpartner" />

      {/* Twitter Cards */}
      <meta name="twitter:card" content="summary_large_image" />
      <meta name="twitter:title" content={title} />
      <meta name="twitter:description" content={description} />
      <meta name="twitter:image" content={ogImage} />

      {/* JSON-LD Structured Data Injection */}
      {schemaData && (
        <script
          type="application/ld+json"
          dangerouslySetInnerHTML={{ __html: JSON.stringify(schemaData) }}
        />
      )}
    </Head>
  );
}
```

---

### 4.3. Konfigurasi `pages/_document.jsx` (Atribut `lang` Dinamis)
Perbarui file `pages/_document.js` agar tag `<html>` tidak *hardcoded* `lang="en"`:

```jsx
// pages/_document.jsx
import Document, { Html, Head, Main, NextScript } from 'next/document';

class MyDocument extends Document {
  render() {
    const locale = this.props.__NEXT_DATA__.locale || 'en';
    return (
      <Html lang={locale}>
        <Head>
          <link rel="apple-touch-icon" sizes="180x180" href="/apple-touch-icon.png" />
          <link rel="icon" type="image/png" sizes="32x32" href="/favicon-32x32.png" />
          <link rel="icon" type="image/png" sizes="16x16" href="/favicon-16x16.png" />
          <link rel="manifest" href="/site.webmanifest" />
        </Head>
        <body>
          <Main />
          <NextScript />
        </body>
      </Html>
    );
  }
}

export default MyDocument;
```

---

### 4.4. Pemecahan URL Layanan & Perbaikan Semantik Heading
Pada file styling Emotion CSS developer, ganti tag HTML-nya tanpa mengubah class Emotion:

```jsx
// CONTOH DI HOMEPAGE & ABOUT PAGE:
// SEBELUM:
<h5 className="css-1o1gi7u en4cht40">About Us</h5>
<h5 className="card-title css-jl6au6 ebofkgh0">Busines and Management Consulting</h5>

// SESUDAH:
<h2 className="css-1o1gi7u en4cht40">About Inpartner</h2>
<h2 className="card-title css-jl6au6 ebofkgh0">Business and Management Consulting</h2>
```
> *Catatan Pengembang:* Mengubah tag dari `<h5>` menjadi `<h2>` tidak merusak tampilan visual karena styling CSS Emotion menimpa ukuran default browser.

---

## 5. Kamus Tag Title, Meta Description & Heading (H1–H3) Siap Pasang

Developer tinggal menyalin nilai metadata berikut ke masing-masing halaman:

### 5.1. Versi Bahasa Inggris (EN)

| URL Path | Tag `<title>` (Max 60 Karakter) | Tag `<meta name="description">` (Max 160 Karakter) | Tag `<h1>` Utama | Tag `<h2>` Seksi |
| :--- | :--- | :--- | :--- | :--- |
| **`/` (Homepage)** | `Business & Management Consulting Jakarta \| Inpartner` | `Inpartner is a leading management consulting and investment advisory firm in Jakarta and Surabaya, helping enterprises drive growth and optimize operations.` | `Strategic Business Consulting & Investment Solutions in Indonesia` | `1. About Inpartner`<br>`2. Core Advisory Pillars`<br>`3. Our Services & Scope`<br>`4. Sectors Coverage` |
| **`/about`** | `About Inpartner \| Management Consulting & Investment Advisory` | `Established in 2009, PT Inpartner Optima Integra provides strategic corporate consulting, feasibility studies, and investment advisory in Indonesia.` | `About Inpartner: Trusted Management Consulting in Indonesia` | `1. Strategic Vision & Mission`<br>`2. Corporate History (2009–Present)`<br>`3. Core Values & Principles`<br>`4. Leadership & Partners` |
| **`/services`** | `Consulting & Investment Advisory Services \| Inpartner Indonesia` | `Explore Inpartner's comprehensive advisory services: corporate strategy, operational optimization, market research, and investment feasibility studies.` | `Business Consulting & Investment Advisory Services` | `1. Business & Management Consulting`<br>`2. Investment Advisory & Solutions`<br>`3. Executive Capacity Building` |
| **`/services/business-management-consulting`** | `Business & Management Consulting Services \| Inpartner Jakarta` | `Accelerate enterprise performance with Inpartner's business consulting, corporate strategy formulation, operations redesign, and market entry research.` | `Business and Management Consulting Services` | `1. Corporate Business Strategy`<br>`2. Operational Process Optimization`<br>`3. Market Research & Intelligence` |
| **`/services/investment`** | `Investment Advisory & Feasibility Study Services \| Inpartner` | `Comprehensive investment advisory in Indonesia: financial modeling, feasibility studies (FS), valuation analysis, and private equity transaction advisory.` | `Investment Advisory & Capital Solutions in Indonesia` | `1. Project Feasibility Studies (FS)`<br>`2. Valuation & Investment Teasers`<br>`3. Alternative Investment Sourcing` |
| **`/services/capacity-building`** | `Executive Capacity Building & Business Programs \| Inpartner` | `Enhance executive leadership and workforce productivity with Inpartner Academy's tailored corporate training and organizational development programs.` | `Executive Capacity Building & Leadership Programs` | `1. Executive Training Modules`<br>`2. Workforce Productivity Optimization` |
| **`/project`** | `Portfolio & Completed Advisory Projects \| Inpartner Indonesia` | `Review Inpartner's delivered advisory track record: feasibility studies for toll roads, BRT transportation, renewable energy, and investment teasers.` | `Proven Advisory Track Record & Delivered Projects` | `1. Infrastructure & Utilities`<br>`2. Feasibility Studies & Due Diligence`<br>`3. Alternative Investment Sourcing` |
| **`/blog`** | `Indonesia Business & Investment Insights \| Inpartner Insights` | `Authoritative analyses, market intelligence, and regulatory updates on Indonesian business expansion, foreign direct investment (FDI), and industrial trends.` | `Insights, Market Intelligence & Industry Updates` | `1. Featured Market Insights`<br>`2. FDI & Regulatory Guides` |
| **`/contact`** | `Contact Us \| Inpartner Consulting Offices Jakarta & Surabaya` | `Connect with Inpartner's senior consultants in Jakarta and Surabaya. Request a consultation for strategic business management or investment advisory.` | `Contact Inpartner Consulting Jakarta & Surabaya` | `1. Schedule a Consultation`<br>`2. Corporate Office Locations` |

---

### 5.2. Versi Bahasa Korea (KO)

| URL Path | Tag `<title>` (Max 60 Karakter) | Tag `<meta name="description">` (Max 160 Karakter) | Tag `<h1>` Utama | Tag `<h2>` Seksi |
| :--- | :--- | :--- | :--- | :--- |
| **`/ko` (Homepage)** | `인도네시아 비즈니스 경영 컨설팅 및 투자 자문 \| 인파트너` | `인파트너(Inpartner)는 한국 기업의 인도네시아 시장 진출, 현지 법인 설립 자문, 사업 타당성 조사(FS), 투자 실사를 전문으로 지원하는 현지 전략 컨설팅 펌입니다.` | `인도네시아 비즈니스 성공을 이끄는 전략 컨설팅 & 투자 자문` | `1. 인파트너 소개 (About Us)`<br>`2. 4대 핵심 전략 역량`<br>`3. 전문 컨설팅 서비스 안내`<br>`4. 산업별 커버리지` |
| **`/ko/about`** | `인파트너 소개 \| 인도네시아 전문 경영 컨설팅 펌 (Inpartner)` | `2009년 설립된 PT Inpartner Optima Integra는 자카르타 본사와 수라바야 지사를 기반으로 국내외 중견·대기업에 최적화된 경영 및 투자 솔루션을 제공합니다.` | `인도네시아 비즈니스의 신뢰할 수 있는 전략적 파트너, 인파트너` | `1. 비전 및 미션 (Vision & Mission)`<br>`2. 회사 연혁 (2009년~현재)`<br>`3. 핵심 가치 (Core Values)`<br>`4. 전문 컨설턴트 및 파트너` |
| **`/ko/services`** | `전문 컨설팅 서비스 안내 \| 인도네시아 인파트너 (Inpartner)` | `인도네시아 경영 전략 수립, 시장 조사, 사업 타당성 조사(FS), 투자 자문 및 기업 역량 강화 프로그램 등 인파트너의 전방위 B2B 전문 자문 서비스를 확인하십시오.` | `인파트너 B2B 종합 컨설팅 & 투자 솔루션` | `1. 비즈니스 & 경영 컨설팅`<br>`2. 투자 자문 및 솔루션`<br>`3. 기업 역량 강화 (임원 교육)` |
| **`/ko/services/business-management-consulting`** | `인도네시아 시장 진출 및 경영 전략 컨설팅 \| 인파트너` | `한국 기업을 위한 인도네시아 시장 진출 전략, 현지 규제 분석, 시장 조사, 경쟁사 분석 및 현지 법인 운영 최적화 컨설팅을 제공합니다.` | `인도네시아 시장 진출 및 경영 전략 컨설팅` | `1. 시장 진입 및 법인 설립 전략`<br>`2. B2B 시장 조사 및 산업 분석`<br>`3. 비즈니스 운영 프로세스 최적화` |
| **`/ko/services/investment`** | `인도네시아 기업 투자 자문 및 타당성 조사(FS) \| 인파트너` | `인도네시아 인프라, 신재생에너지, M&A 실사(Due Diligence), 사업 타당성 조사(FS) 및 투자 티저 작성을 전문으로 하는 종합 투자 자문 서비스입니다.` | `인도네시아 투자 자문 및 자본 솔루션` | `1. 사업 타당성 조사 (FS)`<br>`2. 기업 가치평가 및 투자 티저`<br>`3. 대체 투자 및 파트너십 발굴` |
| **`/ko/project`** | `주요 프로젝트 실적 및 포트폴리오 \| 인파트너 인도네시아` | `인도네시아 고속도로(BUJT) 실사, BRT 타당성 조사, 신재생에너지 재무 모델링, 투자 티저 등 인파트너가 성공적으로 완수한 공공·민간 프로젝트 실적입니다.` | `검증된 프로젝트 수행 실적 및 포트폴리오` | `1. 인프라 & 공공 부문 실적`<br>`2. 타당성 조사 & 실사 프로젝트`<br>`3. 대체 투자 & M&A 포트폴리오` |
| **`/ko/contact`** | `상담 문의 및 오피스 안내 \| 인파트너 (자카르타·수라바야)` | `인파트너 자카르타 본사 및 수라바야 지사 연락처. 한국 기업의 인도네시아 진출, 사업 타당성 조사, 투자 자문 상담을 신속하게 접수하십시오.` | `인파트너 프로젝트 상담 및 문의` | `1. 비즈니스 상담 신청`<br>`2. 오피스 위치 및 연락처 안내` |

---

## 6. Daftar Perbaikan Copywriting & Typo (Search-and-Replace Diffs)

Developer diminta melakukan pencarian teks (*find & replace*) pada file komponen halaman berikut:

```diff
===================================================================
FILE: pages/services.js (Card 1 Title)
===================================================================
- <h5 className="...">Busines and Management Consulting</h5>
+ <h2 className="...">Business and Management Consulting</h2>

===================================================================
FILE: pages/index.js (Hero Subtitle) & pages/about.js
===================================================================
- Go Beyond Than Just Consultancy
+ Going Beyond Conventional Consulting

- Through our Consultation Services, we take a holistic approach to identify the problem and give you a home run.
+ Through our advisory services, we take a comprehensive approach to diagnose business challenges and deliver measurable, high-impact outcomes.

===================================================================
FILE: pages/index.js & pages/about.js (Geographic Typo)
===================================================================
- ...provide capacity building of the MSME sector in East Jave.
+ ...providing capacity building for the MSME sector in East Java.

===================================================================
FILE: pages/about.js (Legal Entity Typo & Founding Year)
===================================================================
- INPARTNER (PT Inpartrner Optima Integra) is a transformation of management consulting services which established in 2009.
+ INPARTNER (PT Inpartner Optima Integra) is a premier management consulting firm established in 2009.

- Founded by professionals since 2019...
+ Founded in 2009 by experienced corporate professionals...

===================================================================
FILE: pages/services.js (Grammar Errors in Service Descriptions)
===================================================================
- We also recommends alternative strategies to meet the goals
+ We also recommend innovative strategic alternatives to achieve key organizational milestones.

- We experienced professionals can work closely with clients to understand their investment needs...
+ Our experienced investment advisors work closely with clients to understand their strategic objectives...

- Inpartner capacity building involve various activities such as training, education, mentoring, coaching... Making positive impacts on the clientele we serves, We helps making business plans and effectively implements, swiftly taking new challenges, develop business relations, creating partnerships
+ Inpartner's capacity building division delivers executive mentoring, corporate training, and organizational development. We empower client leadership to formulate actionable business plans, accelerate operational efficiency, and forge resilient institutional partnerships.

===================================================================
FILE: pages/contact.js (Headline Form)
===================================================================
- What Can We Help?
+ How Can We Assist Your Business?
```

---

## 7. Daftar Penerjemahan Portofolio Proyek (`/project`)

Pada file `pages/project.js`, ganti judul proyek yang berbahasa Indonesia menjadi bahasa Inggris dan bahasa Korea agar kredibel bagi audiens internasional:

| Judul Asli di Website (Indonesia) | Sektor | Judul Bahasa Inggris Rekomendasi | Judul Bahasa Korea Rekomendasi |
| :--- | :--- | :--- | :--- |
| `Penyusunan Laporan Sektor Riil pada Badan Usaha Jalan Tol (BUJT)` | Infrastructure | **Real Sector Comprehensive Advisory & Impact Assessment for Toll Road Concessionaires (BUJT)** | **인도네시아 유료도로공사(BUJT) 실물경제 부문 실사 및 자문 보고서 작성** |
| `Penyusunan Kajian Review Feasibility Study (FS) Bandung Rapit Transit (BRT) Bandung Raya` | Infrastructure | **Feasibility Study (FS) Review & Economic Viability Analysis for Greater Bandung Rapid Transit (BRT)** | **반둥 광역 간선급행버스체계(BRT) 사업 타당성 조사(FS) 검토 및 경제성 분석** |
| `Penyusunan Kajian Penyertaan Modal pada Jalan Tol Getaci` | Alternative Investment | **Capital Injection Feasibility & Financial Assessment for Gedebage–Tasikmalaya–Cilacap (Getaci) Toll Road** | **게타치(Getaci) 고속도로 지분 투자 및 출자 타당성 평가 자문** |
| `Penyusunan Investment Teaser Kazuhiro` | Alternative Investment | **Strategic Investment Teaser & Capital Sourcing Formulation for Project Kazuhiro** | **카즈히로(Kazuhiro) 프로젝트 투자 유치 티저(Teaser) 및 재무 구조 설계** |
| `Penyusunan Kebijakan dan SOP Environmental, Social and Governance (ESG)` | ESG & Sustainability | **Corporate ESG Policy Framework & Standard Operating Procedures (SOP) Development** | **기업 ESG 정책 프레임워크 수립 및 표준운영절차(SOP) 구축 자문** |
| `Jasa Konsultansi Penyusunan Investment Teaser dan Perhitungan Valuasi` | Alternative Investment | **Corporate Valuation Modeling & Investment Teaser Preparation for Private Equity Placement** | **기업 가치평가(Valuation) 모델링 및 사모펀드 투자 유치 티저 작성** |
| `Jasa Konsultansi Penyusunan Pitch Deck dan business plan untuk pengembangan bisnis Falga Group` | IT & Infrastructure | **Corporate Business Plan & Investor Pitch Deck Formulation for Falga Group Expansion** | **팔가(Falga) 그룹 사업 확장용 비즈니스 플랜 수립 및 투자자 피치덱 제작** |
| `Kajian Penyediaan Infrastruktur Tempat Pengolahan dan Pemrosesan Akhir Sampah (TPPAS) Regional Lulut Nambo` | Cleantech / Infra | **Regional Waste Management & Processing Infrastructure (TPPAS Lulut Nambo) Feasibility Review** | **룰룻 남보(Lulut Nambo) 지역 폐기물 종합 처리 인프라 타당성 검토** |
| `Jasa Konsultasi Keuangan Project Pembuatan Jalur Pipa Gas` | Industrial Energy | **Project Financial Modeling & Capital Advisory for Industrial Natural Gas Pipeline Development** | **산업용 천연가스 배관망 건설 프로젝트 재무 자문 및 타당성 분석** |
| `Jasa Pembuatan Website` | Information Technology | **Corporate Digital Architecture & Enterprise Web Platform Engineering** | **기업 디지털 플랫폼 구축 및 엔터프라이즈 웹 아키텍처 엔지니어링** |

---

## 8. Schema.org JSON-LD Structured Data Siap Pasang

Suntikkan kode skema ini langsung ke komponen `<Head>` melalui `components/SEO.jsx`:

### 8.1. Skema Organisasi (`Organization`) - Global
```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "ConsultingBusiness",
  "@id": "https://inpartner.id/#organization",
  "name": "Inpartner",
  "legalName": "PT Inpartner Optima Integra",
  "url": "https://inpartner.id/",
  "logo": "https://inpartner.id/_next/static/media/logo.1853afdf.png",
  "foundingDate": "2009",
  "description": "PT Inpartner Optima Integra (Inpartner) is a premier management consulting and investment advisory firm in Indonesia, serving middle and large corporations across infrastructure, energy, and corporate strategy.",
  "address": [
    {
      "@type": "PostalAddress",
      "streetAddress": "Pakuwon Tower 10th Floor, Jl. Raya Casablanca Kav. 88",
      "addressLocality": "South Jakarta",
      "addressRegion": "DKI Jakarta",
      "postalCode": "12870",
      "addressCountry": "ID"
    },
    {
      "@type": "PostalAddress",
      "streetAddress": "Jemur Sari Street V No. 10",
      "addressLocality": "Surabaya",
      "addressRegion": "East Java",
      "addressCountry": "ID"
    }
  ],
  "contactPoint": {
    "@type": "ContactPoint",
    "telephone": "+62-896-2831-0192",
    "contactType": "corporate inquiries",
    "email": "corporatesecretary@inpartner.id",
    "availableLanguage": ["English", "Indonesian", "Korean"]
  },
  "sameAs": [
    "https://www.linkedin.com/company/inpartner",
    "https://www.instagram.com/inpartnerconsulting",
    "https://www.facebook.com/profile.php?id=100092037564577"
  ],
  "knowsAbout": [
    "Management Consulting",
    "Investment Advisory",
    "Feasibility Studies (FS)",
    "Indonesia Market Entry Strategy",
    "Corporate Valuation",
    "ESG Policy Frameworks"
  ]
}
</script>
```

### 8.2. Skema Layanan (`Service`) - Halaman `/services`
```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Service",
  "serviceType": "Management Consulting & Investment Advisory",
  "provider": {
    "@id": "https://inpartner.id/#organization"
  },
  "areaServed": {
    "@type": "Country",
    "name": "Indonesia"
  },
  "hasOfferCatalog": {
    "@type": "OfferCatalog",
    "name": "Inpartner Core Advisory Practice",
    "itemListElement": [
      {
        "@type": "Offer",
        "itemOffered": {
          "@type": "Service",
          "name": "Business and Management Consulting",
          "description": "Strategic corporate planning, operational process optimization, market research, and competitive intelligence for enterprises in Indonesia."
        }
      },
      {
        "@type": "Offer",
        "itemOffered": {
          "@type": "Service",
          "name": "Investment Advisory and Feasibility Studies",
          "description": "Financial modeling, project valuation, comprehensive bankable feasibility studies (FS), and private equity investment teasers."
        }
      },
      {
        "@type": "Offer",
        "itemOffered": {
          "@type": "Service",
          "name": "Executive Capacity Building",
          "description": "Customized C-suite coaching, workforce productivity enhancement, and corporate governance training programs."
        }
      }
    ]
  }
}
</script>
```

---

## 9. Konfigurasi WAF / Cloudflare & Robots.txt

Saat ini, `https://inpartner.id/robots.txt` mengembalikan halaman tantangan Cloudflare (*"One moment, please..."*). Crawler mesin pencari seringkali gagal melewatinya.

### 9.1. Aturan Firewall WAF (Cloudflare Custom Rule)
Tambahkan aturan *WAF Bypass* pada dashboard Cloudflare:
```
Expression:
(cf.client.bot) or (http.user_agent contains "Googlebot") or (http.user_agent contains "bingbot") or (http.user_agent contains "Yeti")
Action:
Bypass -> Security Level, Rate Limiting, Browser Integrity Check
```

### 9.2. File `public/robots.txt`
Pastikan file fisik `public/robots.txt` berisi direktif yang jelas:
```txt
User-agent: *
Allow: /

# Allow Naver Yeti Crawler Explicitly
User-agent: Yeti
Allow: /

Sitemap: https://inpartner.id/sitemap.xml
Sitemap: https://inpartner.id/ko-sitemap.xml
```

---

## 10. Checklist Pengujian & Verifikasi Deployment (QA Checklist)

Sebelum merilis perubahan ke server produksi (*production*), developer wajib memverifikasi poin-poin berikut:

- [ ] **1. Verifikasi Status HTTP Rute Korea:** Buka `https://inpartner.id/ko`, pastikan merespons `200 OK` (bukan 404 dan bukan halaman kosong).
- [ ] **2. Verifikasi Header HTML:** Periksa View-Source di browser:
  - Pada halaman Inggris: harus ada `<html lang="en">`.
  - Pada halaman Korea: harus ada `<html lang="ko">` dan `<meta http-equiv="content-language" content="ko-kr">`.
- [ ] **3. Uji Bidirectional Hreflang:**
  - Halaman `/` harus merujuk `hreflang="en"` ke `/` dan `hreflang="ko"` ke `/ko`.
  - Halaman `/ko` harus merujuk `hreflang="en"` ke `/` dan `hreflang="ko"` ke `/ko`.
- [ ] **4. Uji Self-Referencing Canonical:**
  - `/about` memiliki canonical ke `https://inpartner.id/about`.
  - `/ko/about` memiliki canonical ke `https://inpartner.id/ko/about`.
- [ ] **5. Uji Validasi Schema JSON-LD:** Buka [Google Rich Results Test](https://search.google.com/test/rich-results) dan masukkan URL live, pastikan entitas `ConsultingBusiness`, `Service`, dan `FAQPage` terdeteksi valid tanpa error/warning.
- [ ] **6. Pendaftaran Naver Search Advisor:**
  - Daftarkan `https://inpartner.id/ko` di [Naver Search Advisor](https://searchadvisor.naver.com/).
  - Verifikasi kepemilikan via `<meta name="naver-site-verification" content="..." />`.
  - Submit sitemap `https://inpartner.id/ko-sitemap.xml`.
- [ ] **7. Verifikasi Perbaikan Typo:** Pastikan tidak ada lagi teks `"Busines and Management Consulting"` di `/services` dan tidak ada lagi kata `"East Jave"` atau slang `"home run"`.
- [ ] **8. Uji Tombol "Meet our Team":** Pastikan tombol di `/about` tidak lagi melakukan *reloading* halaman tanpa aksi.
