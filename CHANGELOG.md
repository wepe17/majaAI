# 📝 Changelog

All notable changes to MAJA.AI will be documented in this file.

---

## [3.0.0] - 2024-12-20

### 🎨 **Major UI Redesign: Dark Theme + High Readability**

#### Added
- **Proper dark theme** dengan background #0a0a0f (deep black)
- **High contrast text colors** untuk readability maksimal:
  - Primary text: #ffffff (pure white)
  - Secondary text: #e0e0e5 (light gray)
  - Tertiary text: #c0c0c8 (medium gray)
  - Muted text: #a0a0ab (dark gray)
- **4-level color gradation** untuk hierarchy yang jelas
- **Custom dark scrollbar** (#3a3a48) yang konsisten dengan theme
- **Dark card backgrounds** (#1a1a24) dengan borders (#2a2a38)
- **Gold accent color** (#fbbf24) untuk Majapahit identity

### 💬 **Conversational AI Output**

#### Changed
- **AI sekarang menjawab pertanyaan user terlebih dahulu** dalam dedicated "Jawaban Langsung" box
- **Struktur output baru**:
  1. Jawaban langsung & kesimpulan (kotak kuning)
  2. Grafik interaktif (mendukung jawaban)
  3. Tabel data detail
  4. Rekomendasi & strategi
- **Bahasa yang lebih natural** dan storytelling-based
- **Highlight angka penting** dengan bold formatting
- **Pointer ke detail section** dengan emoji arrows (⬇️)

#### Examples:
**Before (v2.0):**
```
[Langsung tampilkan grafik dan tabel]
```

**After (v3.0):**
```
🤖 Jawaban Langsung dari MAJA.AI

Berdasarkan analisis data yang Anda upload, skor IPD daerah 
Anda saat ini adalah 72.5 dari 100. Ini menempatkan daerah 
Anda pada kategori "Baik"...

3 indikator paling lemah yang perlu segera diperbaiki adalah:
1️⃣ Keamanan Siber (skor 45)
2️⃣ Interoperabilitas Sistem (skor 52)
3️⃣ Kompetensi Digital ASN (skor 58)

Detail lengkap ada di bawah ⬇️

[Grafik, Tabel, Rekomendasi...]
```

### 🎨 **Visual Improvements**

#### Changed
- **Card styling** dengan border #2a2a38 untuk subtle separation
- **Table hover effects** dengan background #1a1a24
- **Button hover** dengan shadow dan translateY animation
- **Badge system** dengan background colors yang lebih readable:
  - HIGH: #991b1b / #fecaca
  - MEDIUM: #92400e / #fed7aa
  - LOW: #1e3a8a / #bfdbfe
- **Chart colors** disesuaikan untuk dark theme:
  - Grid lines: #2a2a38
  - Tick labels: #a0a0ab
  - Legend text: #e0e0e5

### 📊 **Chart Enhancements**

#### Changed
- **Chart backgrounds** sekarang #0a0a0f untuk kontras maksimal
- **Grid lines** lebih subtle (#2a2a38)
- **Label colors** #e0e0e5 untuk readability
- **Tooltip backgrounds** dark theme compatible

### 🔧 **Technical Changes**

#### Added
- CSS variables untuk consistent color management
- `.text-primary`, `.text-secondary`, `.text-tertiary`, `.text-muted` classes
- `.bg-dark-1`, `.bg-dark-2`, `.bg-dark-3`, `.bg-dark-4` classes
- `.answer-box` component untuk direct AI answers

#### Changed
- Base font color: #f5f5f7 (was #e5e7eb)
- Card backgrounds: #1a1a24 (was #1f2937)
- Border colors: #2a2a38 (was #374151)
- Hover states dengan proper dark colors

### 📱 **Responsive Improvements**

#### Changed
- Better text sizing untuk mobile screens
- Improved scroll containers dengan proper max-heights
- Touch-friendly button sizes

---

## [2.0.0] - 2024-12-19

### 🎯 **3-Column Layout + Charts**

#### Added
- **3-column professional layout**:
  - Left: Upload + Chat (320px)
  - Center: Output (flexible)
  - Right: Analysis type (300px)
- **Multi-file upload** (up to 5 files)
- **Chart.js v4 integration** with 4 chart types:
  - Radar charts (6 dimensions)
  - Bar charts (horizontal & vertical)
  - Line charts (5-year predictions)
  - Pie/Doughnut charts (distribution)
- **Professional data tables** with color-coded cells
- **5-year prediction visualizations**
- **Priority-based recommendations** with badges
- **Visual timeline** component

#### Changed
- Layout dari 2-column menjadi 3-column
- Output area sekarang di tengah (bukan kanan)
- Analysis type selector di kanan (bukan di kiri)

---

## [1.0.0] - 2024-12-18

### 🎉 **Initial Release**

#### Added
- Basic 2-column layout (Input | Output)
- Single file upload support
- 3 analysis types:
  - 📊 Analisis 47 Indikator IPD
  - 🗺️ Roadmap Smart City
  - ⚡ Demo Pemerintahan Digital
- Demo mode (no API key required)
- 3 demo responses (33,000+ words total)
- Example prompts per analysis type
- Markdown rendering
- Copy & download hasil analisis
- Glass morphism UI
- Batik pattern background
- Majapahit gold accent colors

#### Technical Stack
- HTML5 + CSS3
- Vanilla JavaScript (ES6+)
- Tailwind CSS via CDN
- Font Awesome 6
- Google Fonts (Inter)

---

## [Unreleased] - Roadmap

### v3.1 (Planned)
- [ ] Real OpenAI API integration (optional)
- [ ] PDF export with charts
- [ ] Excel data export
- [ ] Comparison mode (2+ regions)
- [ ] Advanced filtering & sorting tables

### v3.2 (Future)
- [ ] Analysis history & saved sessions
- [ ] Custom report templates
- [ ] Multi-language support (EN)
- [ ] Advanced chart types (heatmap, treemap)
- [ ] Real-time collaboration features

### v4.0 (Vision)
- [ ] Full backend with RAG pipeline
- [ ] Document parsing & embeddings
- [ ] Vector database (ChromaDB)
- [ ] User authentication
- [ ] Multi-user workspaces
- [ ] API endpoints for integrations

---

## Version Naming

We follow [Semantic Versioning](https://semver.org/):

- **MAJOR** version (X.0.0): Breaking changes, major redesigns
- **MINOR** version (0.X.0): New features, backwards compatible
- **PATCH** version (0.0.X): Bug fixes, minor improvements

---

## Breaking Changes

### v3.0.0
- ⚠️ Complete color scheme redesign → custom colors may need adjustment
- ⚠️ Output structure changed → may affect custom integrations
- ⚠️ CSS class names updated → `.text-white` → `.text-primary`

### v2.0.0
- ⚠️ Layout structure changed from 2-col to 3-col
- ⚠️ Added Chart.js dependency (requires internet for CDN)
- ⚠️ DOM element IDs changed for output sections

### v1.0.0
- Initial release, no breaking changes

---

## Contributors

- **Main Developer**: AI Assistant
- **Design Inspiration**: Majapahit Kingdom Visual Identity
- **Target Users**: Indonesian Local Government (Pemda)

---

## License

MIT License - See LICENSE file for details

---

<div align="center">

**📝 Keep this changelog updated with every release**

[View on GitHub](#) | [Report Bug](#) | [Request Feature](#)

</div>
