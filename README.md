<div align="center">

# 🔍 ListLens

**Turn a few product photos into polished Etsy & eBay listings in seconds.**

[![Live Demo](https://img.shields.io/badge/demo-live-brightgreen)](https://your-vercel-url.vercel.app)
[![Next.js](https://img.shields.io/badge/Next.js-15-black)](https://nextjs.org)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Hacktoberfest](https://img.shields.io/badge/Hacktoberfest-2026-orange)](https://hacktoberfest.com)

[Live Demo](https://your-vercel-url.vercel.app) · [Report Bug](https://github.com/itsomg134/ListLens/issues) · [Request Feature](https://github.com/itsomg134/ListLens/issues)

</div>

---

## 📸 What is ListLens?

ListLens is an AI listing writer for Etsy and eBay sellers. Upload 1–8 product photos, and it generates a complete, platform-optimized listing — **title, description, tags, and category** — in about 15 seconds.

Writing good listings is tedious. Etsy lives or dies on SEO tags. eBay lives or dies on title keywords. Most makers and resellers either skip it (and lose visibility) or spend 15–20 minutes per item. ListLens handles the boring part so you can focus on sourcing and photographing.

---

## ✨ Features

- 📷 **Multi-photo upload** — drag-and-drop up to 8 images, auto-resized to 1024px to cut token cost
- 🎯 **Platform-aware** — tuned for Etsy, eBay, Shopify, and Depop
- 🎨 **Tone selection** — Friendly, Minimal, Vintage, or Luxury
- 🧠 **Two-stage AI pipeline** — vision model extracts attributes, language model writes copy
- 🛡️ **Hallucination guard** — prompt forces the vision model to describe *only what is clearly visible*
- 📋 **One-click copy** — copy individual fields or the full listing
- 🌙 **Dark mode** — follows your system theme
- ⚡ **Open-weight models** — runs on Llama via Groq, not a closed API

---

## 🖼️ Demo

> Live: **[your-vercel-url.vercel.app](https://your-vercel-url.vercel.app)**

*(Add a screenshot or GIF here — drag one into the GitHub README editor and it uploads automatically.)*

---

## 🧠 How It Works

ListLens uses a **two-stage pipeline** instead of one giant prompt. This matters:

```
┌─────────────────┐
│  Product Photos │
└────────┬────────┘
         │
         ▼
┌──────────────────────────────────────┐
│  Stage 1: Vision (Llama 3.2 90B V)   │
│  Extract only visible attributes:    │
│  category, colors, materials, style, │
│  visible_text, condition             │
└────────┬─────────────────────────────┘
         │  JSON
         ▼
┌──────────────────────────────────────┐
│  Stage 2: Copy (Llama 3.3 70B)       │
│  Generate platform-optimized:        │
│  title, description, tags, category  │
└────────┬─────────────────────────────┘
         │
         ▼
┌─────────────────┐
│  Ready Listing  │
└─────────────────┘
```

**Why two calls instead of one:**

1. **Cheaper** — the vision call is the expensive one, and it never regenerates when you tweak the copy tone
2. **Tunable** — when the vision model started inventing leather textures, we tightened only that prompt; the writer prompt stayed stable
3. **Testable** — you can swap either model independently without touching the other

The vision prompt includes a strict constraint:

> *"Only describe what is CLEARLY VISIBLE. Never invent brands, materials, or origins."*

This is non-negotiable. Vision models hallucinate product details, and Etsy/eBay penalize sellers for inaccurate authenticity claims.

---

## 🛠️ Tech Stack

| Layer | Choice |
|-------|--------|
| Framework | [Next.js 15](https://nextjs.org) (App Router) |
| Styling | [Tailwind CSS](https://tailwindcss.com) |
| Vision model | `llama-3.2-90b-vision-preview` (open-weight) |
| Copy model | `llama-3.3-70b-versatile` (open-weight) |
| Inference | [Groq](https://groq.com) |
| Hosting | [Vercel](https://vercel.com) |

---

## 🚀 Getting Started

### Prerequisites

- Node.js 18.17 or later
- A free [Groq API key](https://console.groq.com/keys)

### Installation

```bash
git clone https://github.com/itsomg134/ListLens.git
cd ListLens
npm install
```

### Environment setup

Create a `.env.local` file in the project root:

```bash
GROQ_API_KEY=gsk_your_key_here
```

### Run locally

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000).

---

## 📖 Usage

1. **Upload** — drag 1–8 product photos into the drop zone
2. **Pick a platform** — Etsy, eBay, Shopify, or Depop
3. **Pick a tone** — Friendly, Minimal, Vintage, or Luxury
4. **Click Generate** — wait ~15 seconds
5. **Copy** — grab the title, description, or tags individually, or copy the full listing

---

## 📁 Project Structure

```
ListLens/
├── app/
│   ├── api/
│   │   └── generate/
│   │       └── route.ts        # Two-stage AI pipeline
│   ├── components/
│   │   └── ListingResult.tsx   # Result cards with copy buttons
│   ├── globals.css             # Theme tokens, dark mode, animations
│   ├── layout.tsx              # Root layout + metadata
│   └── page.tsx                # Main UI
├── public/
├── .env.local                  # (gitignored) API key
├── package.json
└── README.md
```

---

## 🗺️ Roadmap

- [x] Core vision → copy pipeline
- [x] Multi-photo upload with client-side resize
- [x] Platform + tone selection
- [x] Dark mode
- [ ] User accounts (Supabase auth) + saved listings
- [ ] Stripe paywall (5 free, then $9/mo)
- [ ] Browser extension for form auto-fill on Etsy
- [ ] Fine-tune on seller-provided listing data
- [ ] Self-host option (Ollama + local Llama)

---

## 🤝 Contributing

Contributions are welcome. For major changes, please open an issue first to discuss what you'd like to change.

```bash
# Fork the repo, then:
git checkout -b feature/your-feature
git commit -m "Add your feature"
git push origin feature/your-feature
# Open a Pull Request
```

---

## 🏆 Hacktoberfest 2026

Built for the [Hacktoberfest Open-Source AI Challenge — Week 2: Side Hustle](https://dev.to/challenges/hacktoberfest-week2-2026-10-12).

---

## 📄 License

MIT — see [LICENSE](LICENSE) for details.

---

<div align="center">

**Built with open-weight AI because tiny-margin side hustles deserve tools too.**

⭐ If this helped you, star the repo — it helps others find it.

</div>
```

---

## Save and push

```powershell
code README.md
# paste the content, save with Ctrl+S
git add README.md
git commit -m "Add comprehensive README"
git push
```

---

## Two things to update before pushing

1. **Replace `your-vercel-url.vercel.app`** with your actual Vercel URL (it appears 3 times in the file)
2. **Add a screenshot** — drag a PNG into the README editor on GitHub (or commit it to `public/` and reference it), then replace the "Add a screenshot or GIF here" line with:

```markdown
![ListLens demo](./public/demo.png)
```

---

## Optional badges to add

If you create these, add them under the title:
