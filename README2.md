# Code used to build the website

All source and config files used to build the Thái Sport homepage.

---

## app/page.tsx

```tsx
"use client";

import React, { useState, useEffect } from "react";
import Image from "next/image";

// Logo URLs: Wikimedia Commons (Babolat, Wilson, Head, Dunlop) + Simple Icons (Nike, Adidas)
const BRAND_LOGOS = [
  { name: "Babolat", logoUrl: "https://commons.wikimedia.org/wiki/Special:FilePath/Babolat_logo.svg", fallbackUrl: "" },
  { name: "Wilson", logoUrl: "https://commons.wikimedia.org/wiki/Special:FilePath/Wilson-logo.svg", fallbackUrl: "" },
  { name: "Head", logoUrl: "https://commons.wikimedia.org/wiki/Special:FilePath/HEAD.svg", fallbackUrl: "" },
  { name: "Dunlop", logoUrl: "https://commons.wikimedia.org/wiki/Special:FilePath/Dunlop_sport_logo.png", fallbackUrl: "" },
  { name: "Adidas", logoUrl: "https://cdn.simpleicons.org/adidas/FFFFFF", fallbackUrl: "https://upload.wikimedia.org/wikipedia/commons/2/20/Adidas_Logo.svg" },
  { name: "Nike", logoUrl: "https://cdn.simpleicons.org/nike/FFFFFF", fallbackUrl: "https://upload.wikimedia.org/wikipedia/commons/a/a6/Logo_NIKE.svg" },
];

function BrandLogoButton({ name, logoUrl, fallbackUrl }: { name: string; logoUrl: string; fallbackUrl: string }) {
  const [src, setSrc] = useState(logoUrl);
  const [failed, setFailed] = useState(false);
  const onError = () => {
    if (src === logoUrl && fallbackUrl) {
      setSrc(fallbackUrl);
    } else {
      setFailed(true);
    }
  };
  return (
    <button
      type="button"
      className="flex h-12 w-24 items-center justify-center rounded bg-gray-700 border border-gray-600 px-3 py-2 hover:bg-gray-600"
    >
      {failed ? (
        <span className="text-xs font-medium text-white">{name}</span>
      ) : (
        // eslint-disable-next-line @next/next/no-img-element
        <img
          src={src}
          alt={name}
          referrerPolicy="no-referrer"
          className="max-h-8 w-auto object-contain"
          style={src.includes("wikimedia") ? { filter: "brightness(0) invert(1)" } : undefined}
          onError={onError}
        />
      )}
    </button>
  );
}

// 3 tennis + 3 pickleball (local images in /public)
const CAROUSEL_IMAGES = [
  { src: "/carousel-1.png", alt: "Professional tennis player during match" },
  { src: "/carousel-2.png", alt: "Tennis rackets" },
  { src: "/carousel-3.png", alt: "Tennis shoes" },
  { src: "/carousel-4.png", alt: "Professional pickleball player during match" },
  { src: "/carousel-5.png", alt: "Pickleball shoes" },
  { src: "/carousel-6.png", alt: "Pickleball rackets and balls" },
];

type Category = {
  name: string;
  children?: string[];
};

type Product = {
  name: string;
  price: string;
  tag?: string;
};

const categories: Category[] = [
  {
    name: "BÓNG TENNIS",
    children: ["Bóng Head", "Bóng Dunlop", "Bóng Penn", "Bóng Print", "Bóng Wilson"],
  },
  {
    name: "GIÀY DÁN ĐỀ ÉP NHIỆT",
  },
  {
    name: "GIẦY TENNIS",
    children: ["Giầy Adidas", "Giầy Asics", "Giầy Babolat", "Giầy Head", "Giầy Nike"],
  },
  {
    name: "HÀNG MỚI VỀ",
  },
  {
    name: "HÀNG SALE OFF",
    children: ["Giày", "Hàng khác", "Quần, áo", "Vợt"],
  },
  {
    name: "PHỤ KIỆN TENNIS",
    children: [
      "Các phụ kiện khác",
      "Chắn mồ hôi Trán & Tay",
      "Cước Tennis",
      "Dunlop",
      "GOSEN",
      "Hang Signum Pro",
      "HEAD",
      "Pacific",
      "Pro s pro",
      "Star",
      "Tecnifibre",
      "Cuốn cán mỏng & Cốt",
      "Hỗ trợ & Giảm rung",
      "Mũ Tennis",
      "Nước uống thể thao",
      "Tất Tennis",
    ],
  },
  {
    name: "QUẦN ÁO TENNIS",
    children: ["Adidas", "Dunlop", "Nike", "Puma", "Sịp Freeman"],
  },
  {
    name: "TÚI, BALO TENNIS",
    children: ["Adidas", "Babolat", "Dunlop", "HEAD", "Nike", "Wilson"],
  },
  {
    name: "VỢT PICKLEBALL",
    children: ["Vợt Bamboo", "Vợt CRBN", "Vợt HEAD", "Vợt JOOLA", "Vợt SELKIRK"],
  },
  {
    name: "VỢT TENNIS",
    children: ["Vợt BabolaT", "Vợt Dunlop", "Vợt Head", "Vợt Print", "Vợt Tecnifibre", "Vợt Wilson"],
  },
];

// Different product names and prices to avoid copyright
const featuredProducts: Product[] = [
  {
    name: "Pro Racket Elite 2024",
    price: "3 850.000VND",
    tag: "New",
  },
  {
    name: "Champion Series 300G Pro",
    price: "3 450.000VND",
  },
  {
    name: "Performance Plus 310G (2024)",
    price: "3 650.000VND",
    tag: "Hot",
  },
  {
    name: "Ultra Light 300G Edition",
    price: "3 250.000VND",
  },
  {
    name: "Pro Blade 100UL V9.5 (265GR)",
    price: "3 550.000VND",
  },
  {
    name: "Elite Blade V9 285G",
    price: "3 950.000VND",
  },
  {
    name: "Power Drive MP 2024",
    price: "4 150.000VND",
  },
  {
    name: "Speed Master 300G Pro",
    price: "3 750.000VND",
  },
];

export default function HomePage() {
  const [carouselIndex, setCarouselIndex] = useState(0);

  // Auto-advance every 3 seconds, loop after image 6
  useEffect(() => {
    const id = setInterval(() => {
      setCarouselIndex((i) => (i === 5 ? 0 : i + 1));
    }, 3000);
    return () => clearInterval(id);
  }, []);

  return (
    <main className="min-h-screen bg-gray-100">
      {/* Blue Header Bar */}
      <div className="bg-blue-600 text-white">
        <div className="mx-auto flex max-w-7xl items-center justify-between px-4 py-4">
          <div className="flex items-center gap-4">
            <div className="flex h-14 w-14 items-center justify-center rounded-full bg-white text-blue-600 text-xl font-bold">
              TS
            </div>
            <div>
              <div className="text-2xl font-bold">THÁI SPORT</div>
              <div className="text-xs mt-1">CUNG CẤP SẢN PHẨM TENNIS CHÍNH HÃNG</div>
            </div>
          </div>
          <div className="hidden text-sm sm:block">
            <div className="mb-1">- DUNLOP</div>
            <div className="mb-1">- HEAD, WILSON</div>
            <div className="mb-1">- NIKE, ADIDAS</div>
            <div>- BABOLAT</div>
          </div>
        </div>
      </div>

      {/* Navigation Bar */}
      <nav className="bg-gray-700 border-b border-gray-600">
        <div className="mx-auto flex max-w-7xl items-center justify-start gap-8 px-4 py-3">
          <a href="#" className="text-white hover:text-blue-300 font-medium text-sm">
            TRANG CHỦ
          </a>
          <a href="#" className="text-white hover:text-blue-300 font-medium text-sm">
            TIN TỨC
          </a>
          <a href="#" className="text-white hover:text-blue-300 font-medium text-sm">
            TƯ VẤN
          </a>
          <a href="#" className="text-white hover:text-blue-300 font-medium text-sm">
            LIÊN HỆ
          </a>
        </div>
      </nav>

      {/* Search and Contact Bar */}
      <div className="bg-gray-700 border-b border-gray-600">
        <div className="mx-auto flex max-w-7xl flex-col gap-4 px-4 py-3 sm:flex-row sm:items-center sm:justify-between">
          <div className="flex items-center gap-2">
            <input
              type="text"
              placeholder="tìm kiếm..."
              className="rounded bg-gray-600 border border-gray-500 px-4 py-2 text-white placeholder-gray-400 focus:outline-none focus:ring-1 focus:ring-blue-400 w-64"
            />
            <button className="rounded bg-blue-600 px-4 py-2 text-white hover:bg-blue-700">
              🔍
            </button>
          </div>
          <div className="text-sm text-gray-200">
            Tel: 0904002122 - 0984746641 - 0466703988 Email: quocthaiphan73@yahoo.com
          </div>
        </div>
      </div>

      {/* Image Carousel Area - Large banner section */}
      <section className="bg-gray-800 border-b border-gray-700">
        <div className="relative mx-auto max-w-7xl px-4 py-6">
          <div className="relative h-96 overflow-hidden bg-gray-700">
            <div key={carouselIndex} className="carousel-slide absolute inset-0">
              <Image
                src={CAROUSEL_IMAGES[carouselIndex].src}
                alt={CAROUSEL_IMAGES[carouselIndex].alt}
                fill
                className="object-cover"
                sizes="(max-width: 1280px) 100vw, 1280px"
                priority
              />
            </div>

            {/* Left navigation arrow */}
            <button
              type="button"
              onClick={() => setCarouselIndex((i) => (i === 0 ? 5 : i - 1))}
              className="absolute left-4 top-1/2 -translate-y-1/2 rounded-full bg-amber-700/80 p-3 text-white hover:bg-amber-700 shadow-lg z-10"
            >
              <span className="text-xl font-bold">←</span>
            </button>

            {/* Right navigation arrow */}
            <button
              type="button"
              onClick={() => setCarouselIndex((i) => (i === 5 ? 0 : i + 1))}
              className="absolute right-4 top-1/2 -translate-y-1/2 rounded-full bg-amber-700/80 p-3 text-white hover:bg-amber-700 shadow-lg z-10"
            >
              <span className="text-xl font-bold">→</span>
            </button>
          </div>

          {/* Six slots: 3 tennis + 3 pickleball */}
          <div className="mt-4 flex justify-center gap-2 bg-gray-800 px-4 py-3 rounded">
            {CAROUSEL_IMAGES.map((img, i) => (
              <button
                key={img.alt}
                type="button"
                onClick={() => setCarouselIndex(i)}
                className={`relative h-16 w-16 rounded border-2 overflow-hidden flex-shrink-0 ${
                  carouselIndex === i ? "border-amber-500 ring-2 ring-amber-400" : "border-gray-600 hover:border-gray-500"
                }`}
              >
                <Image
                  src={img.src}
                  alt={img.alt}
                  fill
                  className="object-cover"
                  sizes="64px"
                />
              </button>
            ))}
          </div>
        </div>
      </section>

      {/* Main Content: Sidebar + Products */}
      <section className="bg-gray-100 py-6">
        <div className="mx-auto max-w-7xl px-4">
          {/* 6 brand logos - above Danh Mục Sản Phẩm */}
          <div className="mb-4 flex flex-wrap items-center justify-center gap-3 border-b border-gray-300 bg-gray-800 px-4 py-3 rounded-t">
            {BRAND_LOGOS.map((brand) => (
              <BrandLogoButton key={brand.name} name={brand.name} logoUrl={brand.logoUrl} fallbackUrl={brand.fallbackUrl} />
            ))}
          </div>
          <div className="grid gap-6 lg:grid-cols-[240px,1fr]">
            {/* Left Sidebar - Dark grey */}
            <aside className="bg-gray-800 rounded border border-gray-700 p-4 h-fit">
              <h2 className="mb-4 text-sm font-bold uppercase text-white border-b border-gray-700 pb-2">
                DANH MỤC SẢN PHẨM
              </h2>
              <nav className="space-y-1 text-sm">
                {categories.map((category) => (
                  <div key={category.name} className="space-y-0.5">
                    <button className="w-full text-left text-xs font-semibold text-white hover:text-blue-400 py-1">
                      {category.name}
                    </button>
                    {category.children && (
                      <ul className="ml-2 space-y-0.5 border-l border-gray-700 pl-2">
                        {category.children.map((child) => (
                          <li key={child}>
                            <button className="text-xs text-gray-300 hover:text-blue-400 py-0.5">
                              {child}
                            </button>
                          </li>
                        ))}
                      </ul>
                    )}
                  </div>
                ))}
              </nav>
            </aside>

            {/* Products Grid - Light background */}
            <div className="space-y-4">
              <div>
                <h1 className="mb-1 text-xl font-bold text-gray-900">Tennis Chính hãng ThaiSports</h1>
                <p className="text-sm text-gray-600">
                  Khám phá bộ sưu tập vợt tennis và phụ kiện chính hãng
                </p>
              </div>

              <div className="grid gap-4 sm:grid-cols-2 lg:grid-cols-4">
                {featuredProducts.map((product) => (
                  <article
                    key={product.name}
                    className="group flex flex-col overflow-hidden rounded border border-gray-300 bg-white shadow-sm transition hover:shadow-md"
                  >
                    <div className="relative h-48 bg-gray-200">
                      <div className="flex h-full items-center justify-center">
                        <div className="text-center text-gray-400">
                          <div className="mb-2 text-4xl">🎾</div>
                          <div className="text-xs">Racket Image</div>
                        </div>
                      </div>
                      {product.tag && (
                        <span className="absolute left-2 top-2 rounded bg-red-600 px-2 py-1 text-xs font-semibold text-white">
                          {product.tag}
                        </span>
                      )}
                    </div>
                    <div className="flex flex-1 flex-col gap-1 p-3">
                      <h3 className="text-sm font-semibold text-gray-900 line-clamp-2 min-h-[2.5rem]">
                        {product.name}
                      </h3>
                      <p className="text-sm font-bold text-red-600 mt-auto">{product.price}</p>
                    </div>
                  </article>
                ))}
              </div>
            </div>
          </div>
        </div>
      </section>

      {/* Footer */}
      <footer className="bg-gray-800 border-t border-gray-700">
        <div className="mx-auto max-w-7xl px-4 py-4">
          <div className="flex flex-col gap-4 text-sm sm:flex-row sm:items-center sm:justify-between">
            <div className="flex flex-wrap items-center gap-2 text-white font-semibold">
              <span className="text-white">•</span>
              <a href="#" className="text-white hover:text-blue-300">Site map</a>
              <span className="text-white">|</span>
              <span className="text-white">•</span>
              <a href="#" className="text-white hover:text-blue-300">Giới thiệu</a>
              <span className="text-white">|</span>
              <span className="text-white">•</span>
              <a href="#" className="text-white hover:text-blue-300">Liên hệ</a>
              <span className="text-white">|</span>
            </div>
            <div className="text-right text-white text-xs sm:text-sm">
              <p>© {new Date().getFullYear()} ThaiSport.vn – All rights reserved.</p>
            </div>
          </div>
        </div>
      </footer>
    </main>
  );
}
```

---

## app/layout.tsx

```tsx
import React from "react";
import "./globals.css";

export const metadata = {
  title: "Tennis Chính hãng ThaiSports",
  description: "Cửa hàng tennis chính hãng tại Hà Nội, chuyên vợt và phụ kiện chính hãng.",
};

export default function RootLayout({
  children,
}: {
  // Use 'any' here to avoid depending on React type declarations
  children: any;
}) {
  return (
    <html lang="vi">
      <body className="bg-gray-100 text-gray-900 antialiased">
        {children}
      </body>
    </html>
  );
}
```

---

## app/globals.css

```css
@tailwind base;
@tailwind components;
@tailwind utilities;

html,
body {
  height: 100%;
}

body {
  @apply bg-slate-100 text-slate-900 antialiased;
}

a {
  @apply text-brand-700 hover:text-brand-600;
}

/* Carousel fade-in when slide changes */
@keyframes carousel-fade-in {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

.carousel-slide {
  animation: carousel-fade-in 2s ease-out;
}
```

---

## next.config.mjs

```js
/** @type {import('next').NextConfig} */
const nextConfig = {
  images: {
    remotePatterns: [
      { protocol: "https", hostname: "images.unsplash.com", pathname: "/**" },
      { protocol: "https", hostname: "logo.clearbit.com", pathname: "/**" },
      { protocol: "https", hostname: "cdn.simpleicons.org", pathname: "/**" },
      { protocol: "https", hostname: "upload.wikimedia.org", pathname: "/**" }
    ],
    dangerouslyAllowSVG: true,
    contentSecurityPolicy: "default-src 'self'; script-src 'none'; sandbox;"
  }
};

export default nextConfig;
```

---

## tailwind.config.ts

```ts
const config = {
  content: [
    "./app/**/*.{ts,tsx}",
    "./components/**/*.{ts,tsx}",
    "./data/**/*.{ts,tsx}"
  ],
  theme: {
    extend: {
      colors: {
        brand: {
          50: "#e8f2ff",
          100: "#d4e6ff",
          600: "#2563eb",
          700: "#1d4ed8"
        }
      }
    }
  },
  plugins: []
};

export default config;
```

---

## postcss.config.mjs

```js
export default {
  plugins: {
    tailwindcss: {},
    autoprefixer: {}
  }
};
```

---

## tsconfig.json

```json
{
  "compilerOptions": {
    "target": "ES2017",
    "lib": ["dom", "dom.iterable", "esnext"],
    "allowJs": true,
    "skipLibCheck": true,
    "strict": false,
    "noEmit": true,
    "incremental": true,
    "module": "esnext",
    "esModuleInterop": true,
    "moduleResolution": "node",
    "resolveJsonModule": true,
    "isolatedModules": true,
    "jsx": "react-jsx",
    "plugins": [{ "name": "next" }]
  },
  "include": [
    "next-env.d.ts",
    ".next/types/**/*.ts",
    ".next/dev/types/**/*.ts",
    "**/*.mts",
    "**/*.ts",
    "**/*.tsx"
  ],
  "exclude": ["node_modules"]
}
```

---

## package.json

```json
{
  "name": "thaisport-homepage-clone",
  "private": true,
  "version": "0.1.0",
  "type": "module",
  "scripts": {
    "dev": "next dev -H localhost -p 3003 --webpack",
    "build": "next build",
    "start": "next start -p 3003",
    "lint": "next lint"
  },
  "dependencies": {
    "next": "latest",
    "react": "latest",
    "react-dom": "latest",
    "tailwindcss": "^3.4.19"
  },
  "devDependencies": {
    "@types/node": "latest",
    "@types/react": "latest",
    "@types/react-dom": "latest",
    "autoprefixer": "^10.4.24",
    "eslint": "latest",
    "eslint-config-next": "latest",
    "postcss": "^8.5.6",
    "typescript": "latest"
  }
}
```

---

## .eslintrc.json

```json
{
  "extends": ["next/core-web-vitals"]
}
```

---

## Assets

- **public/carousel-1.png** … **public/carousel-6.png** – Carousel images (place in `public/`).
