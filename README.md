# Shine Lab

Сайт-визитка за услуги по детайлинг на автомобили.

## Стек

- **Astro 5** — статичен сайт generator (0 KB JS по подразбиране)
- **Tailwind CSS v4** — utility-first CSS
- **GSAP** — scroll анимации
- **Embla Carousel** — листане между snimки в галерията
- **img-comparison-slider** — drag handle за преди/след
- **Lucide Icons** — иконки

## Команди

```bash
npm install        # инсталиране на зависимости
npm run dev        # dev сървър на localhost:4321
npm run build      # production build → dist/
npm run preview    # преглед на build-а локално
```

## Структура

Виж [b2b-platform-description.md](./b2b-platform-description.md) за пълна спецификация.

```
src/
├── components/   # .astro компоненти за всяка секция
├── layouts/      # BaseLayout с SEO meta
├── pages/        # index.astro
├── styles/       # global.css с Tailwind + theme
└── data/         # JSON файлове с услуги, цени, снимки

public/
└── images/       # снимки (hero, gallery, services)
```

## Deploy

Cloudflare Pages, свързан с GitHub repo. Build command: `npm run build`, output: `dist/`.
