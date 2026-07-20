# Iranian Thesis Template

A ready-to-use **XeLaTeX** template for Persian (Farsi) graduate theses at Iranian universities of medical sciences, structured to follow the common front-matter → chapters → English back-matter order used at **Tehran University of Medical Sciences (TUMS)** and similar institutions.

قالب آمادهٔ **XeLaTeX** برای پایان‌نامهٔ فارسی تحصیلات تکمیلی دانشگاه‌های علوم پزشکی، با ترتیب بخش‌ها مطابق دستورالعمل رایج نگارش پایان‌نامه (الگوی TUMS).

---

## Features

| Feature | Detail |
|--------|--------|
| Engine | **XeLaTeX** + **XePersian** |
| Document class | `extbook` (A4, 14 pt, twoside, openright) |
| Persian fonts | IR Nazanin (body), IR Titr (headings) |
| English abstract / cover | Times New Roman via Latin environment |
| Bibliography | **BibLaTeX** + **Biber**, Vancouver style |
| Page numbering | Abjad letters (`حرفی`) in front matter; Arabic numerals in main matter |
| Layout | TUMS-style margins, chapter/section titles, figure/table captions |
| Structure | Cover → declarations → abstract → TOC → 5 chapters → references → English pages |

---

## Requirements

- A TeX distribution with **XeLaTeX** and **Biber**  
  - [TeX Live](https://tug.org/texlive/) (recommended) or [MiKTeX](https://miktex.org/)
- Packages used by the template (usually installed with a full distribution):  
  `xepersian`, `biblatex`, `biber`, `geometry`, `fancyhdr`, `titlesec`, `hyperref`, `graphicx`, `booktabs`, `enumitem`, `setspace`, `caption`, `pdfpages`, `fontsetup`, `amsmath`, …
- Optional: [`latexmk`](https://ctan.org/pkg/latexmk) for one-command builds
- Optional: a Persian-friendly editor (TeXstudio, VS Code + LaTeX Workshop, Overleaf with XeLaTeX)

> **Note:** Compile with **XeLaTeX**, not pdfLaTeX. Persian text and the bundled TTF fonts require XeTeX (or LuaTeX with extra setup).

---

## Quick start

```bash
git clone https://github.com/a-rastin/Iranian-Thesis-Template.git
cd Iranian-Thesis-Template
```

1. Edit thesis metadata in [`config.tex`](config.tex) (title, name, supervisors, year, keywords, …).
2. Replace the logo in [`figures/TUMS.jpg`](figures/TUMS.jpg) if your faculty uses a different crest.
3. Write chapters under [`chapters/`](chapters/) and fill front/back matter under [`frontmatter/`](frontmatter/) and [`backmatter/`](backmatter/).
4. Add references to [`references.bib`](references.bib).
5. Build the PDF (see [Build](#build)).

---

## Project structure

```
Iranian-Thesis-Template/
├── main.tex                 # Root document — include order & chapter wiring
├── config.tex               # Geometry, fonts, styles, thesis metadata macros
├── references.bib           # BibLaTeX bibliography database
├── chapters/
│   ├── ch01-introduction.tex    # مقدمه، کلیات و بیان مسأله
│   ├── ch02-literature.tex      # بررسی متون
│   ├── ch03-methods.tex         # مواد و روش کار
│   ├── ch04-results.tex         # یافته‌ها
│   └── ch05-discussion.tex      # بحث و نتیجه‌گیری
├── frontmatter/             # Persian preliminary pages
│   ├── title-fa.tex
│   ├── basmala.tex
│   ├── internal-title-fa.tex
│   ├── declaration-fa.tex
│   ├── copyright.tex
│   ├── dedication.tex
│   ├── acknowledgements.tex
│   └── abstract-fa.tex
├── backmatter/              # English closing pages (reverse book order)
│   ├── declaration-en.tex
│   ├── abstract-en.tex
│   ├── title-en.tex
│   └── cover-en.tex
├── figures/                 # Images (logo, plots, …)
├── fonts/                   # Bundled IR Nazanin, IR Titr, Times TTFs
├── LICENSE
└── README.md
```

Optional sections (abbreviations, appendices, scanned approval forms) are commented in `main.tex` and can be enabled as needed.

---

## Configuration

All shared settings live in **`config.tex`**. Thesis identity is controlled by macros—edit the placeholders before writing content:

| Macro | Purpose |
|-------|---------|
| `\ThesisTitleFA` / `\ThesisTitleEN` | Title (Persian / English) |
| `\StudentNameFA` / `\StudentNameEN` | Author name |
| `\StudentID` | Student number |
| `\StudentDegreeFA` / `\StudentDegreeEN` | Degree (e.g. کارشناسی ارشد) |
| `\StudentFieldFA` / `\StudentFieldEN` | Field of study |
| `\FacultyFA` / `\FacultyEN` | Faculty / school |
| `\UniversityFA` / `\UniversityEN` | University name |
| `\SupervisorOneFA` / `\SupervisorOneEN` | Supervisor |
| `\SupervisorTwoFA` / `\SupervisorTwoEN` | Advisor (optional second supervisor) |
| `\ThesisYearFA` / `\ThesisMonthFA` | Persian date on cover |
| `\ThesisYearEN` / `\ThesisMonthEN` | English date on cover |
| `\KeywordsFA` / `\KeywordsEN` | Abstract keywords |

Typography and layout defaults (margins, stretch, caption style, chapter title format, figure/table numbering `chapter-n`) are also defined in `config.tex`.

### Fonts

Fonts are loaded from the local `fonts/` folder (no system install required):

- **Body (Persian):** IR Nazanin — Regular / Bold / Italic  
- **Headings:** IR Titr  
- **Latin / English blocks:** Times (regular, bold, italic)

If you replace fonts, keep the same file names or update the `\settextfont` / `\newfontfamily` paths in `config.tex`.

---

## Build

### Recommended: `latexmk`

```bash
latexmk -xelatex main.tex
```

### Manual sequence

```bash
xelatex main.tex
biber main
xelatex main.tex
xelatex main.tex
```

Output: `main.pdf` in the project root. Intermediate files (`.aux`, `.bbl`, `.bcf`, …) can be cleaned with:

```bash
latexmk -c
```

### Overleaf

1. Upload the project (or import from GitHub).
2. Set **Menu → Compiler → XeLaTeX**.
3. Set main document to `main.tex`.
4. Ensure Biber is used for bibliography (default with `biblatex` on Overleaf).

---

## Document outline (TUMS-style order)

The include order in `main.tex` matches a typical medical-sciences thesis checklist:

**Front matter (حرفی numbering)**  
1. Persian cover  
2. Blank verso  
3. Basmala  
4. Internal Persian title  
5. Student declaration  
6. Copyright / ownership  
7. Dedication & acknowledgements  
8. Persian abstract & keywords  
9. Table of contents  
10. List of tables  
11. List of figures  

**Main matter (Arabic numbering)**  
12–16. Chapters 1–5  
17. References (Vancouver via BibLaTeX)  

**Back matter (English, reverse binding order)**  
18. English declaration  
19. English abstract  
20. English title page  
21. Blank page  
22. English cover  

---

## Writing content

### Chapters

Each chapter file starts a new odd page via `\ChapterStart` and uses standard LaTeX sectioning:

```latex
\ChapterStart
\chapter{عنوان فصل}
\label{ch:example}

\section{عنوان بخش}
% ...
```

Figure and table numbers follow `فصل-شماره` (e.g. `1-2`). Put images in `figures/` and include them with `\includegraphics`.

### Citations

Add entries to `references.bib`, then cite in the text:

```latex
طبق مطالعهٔ اسمیت و همکاران \cite{smith2020} ...
```

Bibliography style is **Vancouver** (`sorting=none`, numeric order of appearance). Rebuild with Biber after changing the `.bib` file.

### Persian abstract

Structured sections in `frontmatter/abstract-fa.tex`: مقدمه و هدف، روش کار، یافته‌ها، نتیجه‌گیری، کلمات کلیدی. Keep within your university’s word limit (often ~600 words).

### English abstract

Mirrored structure in `backmatter/abstract-en.tex` (Background and Aim, Methods, Results, Conclusion, Keywords).

---

## Adapting for other universities

The layout targets **TUMS-style** medical graduate theses, but most Iranian medical faculties share the same skeleton. Typical adaptations:

1. Change university/faculty macros and logo.  
2. Adjust margins or font sizes in `config.tex` if your guide differs.  
3. Swap declaration/copyright wording for official faculty forms.  
4. Enable appendix / abbreviations inputs in `main.tex` when required.  
5. Attach supervisor approval or defense minutes as PDF with `pdfpages` (examples are commented in `main.tex`).

---

## License

This project is released under the [MIT License](LICENSE). Copyright © 2026 [a-rastin](https://github.com/a-rastin).

You may use, modify, and redistribute the template for personal or institutional theses; keep the license notice when redistributing the template itself.

---

## Contributing

Issues and pull requests are welcome—especially fixes for faculty-specific rules, missing front-matter pages, or build problems on Windows / Overleaf / TeX Live.

---

## Acknowledgements

- Typesetting: [XePersian](https://ctan.org/pkg/xepersian), BibLaTeX, and the TeX community  
- Structure inspired by common Iranian medical-sciences thesis guidelines (TUMS graduate writing instructions and similar faculty handbooks)
