# SnapCard Brand Assets

Complete asset library for web and mobile apps. All assets follow the **Playful** design system DNA — sticker-style stacked flashcards, hard ink stroke, yellow + coral palette.

---

## Folder structure

```
assets/
├── README.md              ← you are here
├── preview.html           ← visual reference of all logo variants
│
├── svg/                   ← master vector files (edit these, regenerate PNGs)
│   ├── icon.svg                 Primary 512×512 icon (cream bg + 2 cards)
│   ├── icon-transparent.svg     Same icon, no background — for compositing
│   ├── icon-mono-ink.svg        Single-color dark variant
│   ├── icon-mono-white.svg      Single-color light variant
│   ├── icon-admin.svg           Admin app variant (ink + yellow)
│   ├── wordmark.svg             Icon + "SnapCard" text
│   ├── wordmark-mono.svg        Single-color dark wordmark
│   └── wordmark-white.svg       White wordmark for dark bg
│
├── web/                   ← drop these into your Next.js /public folder
│   ├── favicon.ico              Multi-resolution (16/32/48)
│   ├── favicon-16.png           ← also exposed individually
│   ├── favicon-32.png
│   ├── favicon-48.png
│   ├── apple-touch-icon.png     180×180, iOS Safari home-screen
│   ├── icon-192.png             PWA icon (any purpose)
│   ├── icon-512.png             PWA icon (any purpose)
│   ├── icon-maskable-512.png    PWA maskable icon
│   ├── manifest.json            Web app manifest
│   ├── head-snippet.html        Copy-paste <head> tags
│   ├── og-image.png             1200×630 — Open Graph / social
│   ├── wordmark.png             1× wordmark for emails / footer
│   ├── wordmark-2x.png          2× retina
│   ├── wordmark-mono.png        1-color dark version
│   └── wordmark-white.png       For dark backgrounds
│
├── ios/                   ← drop these into AppIcon.appiconset/
│   ├── Contents.json            Xcode AppIcon manifest
│   ├── icon-1024.png            App Store
│   ├── icon-180.png             iPhone @3x
│   ├── icon-167.png             iPad Pro
│   ├── icon-152.png             iPad
│   ├── icon-120.png             iPhone @2x
│   ├── icon-87.png              Settings @3x
│   ├── icon-80.png              Spotlight @2x
│   ├── icon-76.png              iPad
│   ├── icon-60.png              Notification @3x
│   ├── icon-58.png              Settings @2x
│   ├── icon-40.png              Spotlight @1x
│   ├── icon-29.png              Settings @1x
│   └── icon-20.png              Notification @1x
│
└── android/               ← drop into android/app/src/main/res/
    ├── playstore-icon-512.png         Play Store listing (separate upload)
    ├── ic_launcher.xml                 → res/mipmap-anydpi-v26/
    ├── ic_launcher_foreground.png      → res/drawable/ (adaptive fg, 432×432)
    ├── ic_launcher_background.png      → res/drawable/ (paper bg, 512×512)
    ├── colors.xml                      → res/values/ (brand color tokens)
    ├── mipmap-mdpi/ic_launcher.png     48px
    ├── mipmap-hdpi/ic_launcher.png     72px
    ├── mipmap-xhdpi/ic_launcher.png    96px
    ├── mipmap-xxhdpi/ic_launcher.png   144px
    └── mipmap-xxxhdpi/ic_launcher.png  192px
```

---

## Web — installation

Copy `assets/web/*` into your Next.js `public/` directory:

```bash
cp -r playful-latest/assets/web/* packages/web/public/
```

Then paste the contents of `web/head-snippet.html` into your root `<head>`. In Next.js 14+:

```tsx
// app/layout.tsx
export const metadata = {
  title: 'SnapCard — AI flashcards for NEET 2027 Biology.',
  description: 'Take a photo of any NCERT Biology page. Get a NEET-tested flashcard deck in 30 seconds.',
  manifest: '/manifest.json',
  themeColor: '#FB7185',
  icons: {
    icon: [
      { url: '/favicon-16.png', sizes: '16x16', type: 'image/png' },
      { url: '/favicon-32.png', sizes: '32x32', type: 'image/png' },
    ],
    apple: '/apple-touch-icon.png',
  },
  openGraph: {
    title: 'SnapCard — AI flashcards for NEET 2027 Biology.',
    description: 'Take a photo of any NCERT Biology page. Get a NEET-tested flashcard deck in 30 seconds.',
    images: ['/og-image.png'],
    url: 'https://snapcard.app',
  },
  twitter: {
    card: 'summary_large_image',
    images: ['/og-image.png'],
  },
};
```

---

## iOS — installation

1. Drag `assets/ios/` into your Xcode project, dropping it inside `Assets.xcassets/AppIcon.appiconset/`.
2. Xcode will read `Contents.json` and link every size automatically.
3. Verify in Xcode → Project → Assets → AppIcon — every slot should be filled.

**Note:** iOS strips alpha from app icons. Our PNGs ship with the cream background baked in, so they're App-Store-compliant.

---

## Android — installation

```bash
# Adaptive icon (Android 8.0+, recommended)
cp playful-latest/assets/android/ic_launcher.xml \
   android/app/src/main/res/mipmap-anydpi-v26/

cp playful-latest/assets/android/ic_launcher_foreground.png \
   android/app/src/main/res/drawable/
cp playful-latest/assets/android/ic_launcher_background.png \
   android/app/src/main/res/drawable/

# Legacy launcher (Android 7.x and below)
cp -r playful-latest/assets/android/mipmap-* \
      android/app/src/main/res/

# Brand color tokens
cp playful-latest/assets/android/colors.xml \
   android/app/src/main/res/values/
```

For the Play Store listing, upload `playstore-icon-512.png` separately via the Play Console (it's not bundled with the APK).

---

## Regenerating PNGs from SVG

If you edit the SVG masters in `svg/`, regenerate all PNGs by running the generation script. The script uses a headless canvas to rasterize each SVG at the required sizes — no external tooling needed.

The full script lives in this project's `playful-latest/` history; ping the design team if you need it re-extracted.

---

## Brand rules

### Do
- Use the colored icon (`icon.svg`) on `--p-paper` (#FFFBEB), white, or any sticker background that isn't yellow or coral.
- Use the admin variant (`icon-admin.svg`) for internal admin tooling so it's visually distinct.
- Use `wordmark-white.svg` on ink (#0F172A) backgrounds.
- Maintain ½ logo-height clear space on every side.

### Don't
- Don't recolor the logo, add gradients, or apply drop shadows beyond the built-in ink stroke.
- Don't rotate the entire logo (the inner cards are already at -6° / +4° — that's the brand).
- Don't place the colored logo on saturated yellow or coral backgrounds — use mono-ink or admin variant.
- Don't use the wordmark below 140×32px — use the icon alone in tight spaces.
- Don't crop the icon's ink stroke — it's load-bearing.

---

## Dimensions reference

| Surface | Asset | Dimensions |
|---|---|---|
| Browser tab | `favicon.ico` | 16/32/48 (multi) |
| Browser tab (modern) | `favicon-32.png` | 32×32 |
| iOS Safari home | `apple-touch-icon.png` | 180×180 |
| PWA install | `icon-192.png` | 192×192 |
| PWA splash / Android Chrome | `icon-512.png` | 512×512 |
| PWA maskable | `icon-maskable-512.png` | 512×512 |
| OG / Twitter card | `og-image.png` | 1200×630 |
| iOS App Store | `ios/icon-1024.png` | 1024×1024 |
| iOS app (largest) | `ios/icon-180.png` | 180×180 |
| Android Play Store | `android/playstore-icon-512.png` | 512×512 |
| Android adaptive fg | `ic_launcher_foreground.png` | 432×432 |
| Android adaptive bg | `ic_launcher_background.png` | 512×512 |

---

## Quick visual reference

Open `preview.html` in a browser to see every logo variant rendered side-by-side on light and dark backgrounds.
