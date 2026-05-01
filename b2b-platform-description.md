# Shine Lab — Техническа спецификация

> Сайт-визитка за услуги по детайлинг на автомобили. Single-page, mobile-first, статичен сайт.

---

## Взети решения (не се обсъждат)

| Категория | Избор |
|---|---|
| Framework | Astro 5 |
| CSS | Tailwind CSS v4 |
| Анимации | GSAP |
| Галерия/Слайдер | Embla Carousel |
| Карта | Google Maps Embed |
| Оптимизация снимки | Astro Image (`astro:assets`) |
| Цветова тема | Премиум тъмен |
| Шрифт | Inter (Google Fonts) |
| Иконки | Lucide Icons |
| Хостинг | Cloudflare Pages |
| Домейн регистратор | Cloudflare Registrar |
| Аналитика | Plausible |

---

## 1. Изисквания

**Тип:** Single-page (scroll-to sections), евентуално 2–3 страници по-късно.

**Задължителни функции:**
- Представяне на услугите с цени
- Галерия "преди/след" с drag slider
- Ценоразпис
- Локация с вградена карта
- Контакти — телефон (click-to-call), email, WhatsApp/Viber
- Click-to-call от мобилно устройство

**Целеви резултати:**
- Lighthouse score: 95+ на всички категории
- Зареждане: под 1 секунда (3G)
- Mobile-first — 70%+ трафик от телефони

---

## 2. Технологичен стек

```
Astro 5
├── Tailwind CSS v4
├── GSAP (scroll анимации, parallax)
├── Embla Carousel (галерия преди/след)
├── Lucide Icons
└── astro:assets (оптимизация снимки → WebP)
```

**Защо Astro:** 0 KB JavaScript по подразбиране, статичен HTML, Lighthouse 95–100 е лесно постижим, идеален за content-focused сайтове.

**JavaScript Islands:** Само за галерията и контактната форма. Всичко останало е статичен HTML.

---

## 3. Дизайн система

### Цветова палитра — "Премиум тъмен"

```css
--color-bg:        #0A0A0A   /* основен фон */
--color-surface:   #1A1A1A   /* карти, секции */
--color-border:    #2A2A2A   /* разделители */
--color-accent:    #00D4FF   /* CTA бутони, акценти */
--color-silver:    #C0C0C0   /* вторичен акцент */
--color-text:      #FFFFFF   /* основен текст */
--color-muted:     #9CA3AF   /* вторичен текст */
```

### Типография

- **Шрифт:** Inter (Google Fonts) — поддържа кирилица
- **Заглавия:** `font-bold`, размери: `text-5xl` / `text-4xl` / `text-2xl`
- **Текст:** `font-normal`, `text-base` / `text-lg`

### Анимации

- Scroll-triggered reveal: елементи влизат при скрол (GSAP ScrollTrigger)
- Hover ефекти на карти: lift + subtle glow в `--color-accent`
- Parallax на hero фоновата снимка (умерен — не прекалено)
- Smooth scroll между секциите
- Без loading animation, без custom cursor

---

## 4. Структура на сайта

Секциите в ред отгоре надолу:

### 4.1 Hero
- Fullscreen фонова снимка (блестяща, полирана кола) — `hero-car.webp`
- Заглавие: **"Shine Lab — Връщаме блясъка на твоята кола"**
- Подзаглавие: кратко (1 изречение)
- 2 CTA бутона: `Виж услугите` (scroll-to) и `Обади се сега` (`tel:` link)
- Scroll indicator анимация

### 4.2 Услуги (Services)
Grid с карти. Всяка карта: Lucide икона + заглавие + 1–2 изречения описание.

Услуги:
1. Външно полиране — премахване на драскотини, защитни покрития
2. Пране на седалки и интериор — дълбоко почистване с пара
3. Керамично покритие — дълготрайна защита
4. Почистване на джанти и гуми
5. Цялостен пакет (Full Detailing)
6. Полиране на фарове

Данни в: `src/data/services.json`

### 4.3 Галерия "Преди / След"
- **Drag slider** с вертикален разделител (Embla Carousel)
- Двойки снимки: `before-N.webp` / `after-N.webp`
- Минимум 10 двойки при старт
- Lazy loading за снимките извън viewport

Данни в: `src/data/gallery.json`

### 4.4 Ценоразпис (Pricing)
Три карти с пакети:

| Пакет | Включва | Цена |
|---|---|---|
| Basic Wash | Външно измиване + интериор | от 40 лв |
| Premium Detailing | Полиране + дълбоко вътрешно почистване | от 150 лв |
| Full Package | Всичко + керамично покритие | от 350 лв |

Disclaimer под таблицата: *"Финалната цена се определя след оглед на автомобила."*

Данни в: `src/data/pricing.json`

### 4.5 За нас (About)
- Снимка на собственика
- 2–3 параграфа текст
- Статистики: брой обработени коли, години опит

### 4.6 Отзиви (Testimonials)
- 3–6 отзива: снимка + име + звезди + текст
- Данни в: `src/data/testimonials.json`

### 4.7 Локация (Location)
- Google Maps Embed (iframe)
- Адрес, работно време
- Бутон "Отвори в Google Maps"

### 4.8 Контакти (Contact)
- Телефон (`tel:` link — click-to-call)
- Email (`mailto:` link)
- WhatsApp бутон (`https://wa.me/...`)
- Viber бутон
- Facebook / Instagram линкове
- Контактна форма: Име, Телефон, Тип услуга (dropdown), Съобщение

### 4.9 Footer
- Лого + слоган
- Бързи линкове към секциите
- Социални икони
- Copyright

---

## 5. Файлова структура

```
shine-lab/
├── public/
│   ├── images/
│   │   ├── hero/
│   │   │   └── hero-car.webp
│   │   ├── gallery/
│   │   │   ├── before-1.webp
│   │   │   ├── after-1.webp
│   │   │   └── ... (двойки)
│   │   ├── services/
│   │   └── team/
│   ├── favicon.ico
│   └── robots.txt
├── src/
│   ├── components/
│   │   ├── Hero.astro
│   │   ├── Services.astro
│   │   ├── ServiceCard.astro
│   │   ├── Gallery.astro
│   │   ├── BeforeAfterSlider.astro   ← Embla, client:load
│   │   ├── Pricing.astro
│   │   ├── PricingCard.astro
│   │   ├── About.astro
│   │   ├── Testimonials.astro
│   │   ├── Location.astro
│   │   ├── Contact.astro
│   │   ├── ContactForm.astro         ← client:load
│   │   ├── Navbar.astro
│   │   └── Footer.astro
│   ├── layouts/
│   │   └── BaseLayout.astro          ← SEO meta, fonts, global styles
│   ├── pages/
│   │   └── index.astro
│   ├── styles/
│   │   └── global.css                ← CSS custom properties, base styles
│   └── data/
│       ├── services.json
│       ├── pricing.json
│       ├── gallery.json
│       └── testimonials.json
├── astro.config.mjs
├── tailwind.config.mjs
└── package.json
```

---

## 6. SEO

### Задължително в BaseLayout.astro
```html
<title>Shine Lab — Полиране и Детайлинг на Автомобили в [Град]</title>
<meta name="description" content="Професионален детайлинг, полиране и пране на седалки. [Град]. Обадете се за оглед и оферта.">
<meta name="viewport" content="width=device-width, initial-scale=1">
<link rel="canonical" href="https://shinelab.bg">

<!-- Open Graph -->
<meta property="og:title" content="Shine Lab">
<meta property="og:image" content="/images/hero/hero-car.webp">

<!-- Schema.org LocalBusiness -->
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "AutoRepair",
  "name": "Shine Lab",
  "address": { ... },
  "telephone": "...",
  "openingHours": "..."
}
</script>
```

### Извън сайта (ръчно)
- [ ] Google Business Profile — създаден преди deploy
- [ ] Google Search Console — submit след deploy
- [ ] Plausible Analytics — вграден в BaseLayout

---

## 7. Хостинг и Deploy

**Хостинг:** Cloudflare Pages (безплатен план — неограничен трафик, глобален CDN)

**Workflow:**
```
git push → GitHub → Cloudflare Pages (auto-deploy)
```

**Setup стъпки:**
1. `npm run build` → `dist/` папка (статичен HTML)
2. Cloudflare Pages свързан с GitHub repo
3. Build command: `npm run build`
4. Output directory: `dist`
5. Custom домейн: `shinelab.bg` (или `.com`)
6. SSL: автоматично от Cloudflare

**Домейн:** Регистриран от Cloudflare Registrar (най-евтино, без markup).

---

## 8. Roadmap

### Фаза 1: Съдържание (преди да се пише код)
- [ ] 10–15 двойки снимки преди/след (висококачествени, добро осветление)
- [ ] Текстове: описания на услугите, "За нас", цени
- [ ] Лого (Canva или AI инструмент)
- [ ] Google Business Profile — регистриран и попълнен
- [ ] Домейн — купен

### Фаза 2: Setup
- [ ] `npm create astro@latest shine-lab`
- [ ] Tailwind CSS интеграция
- [ ] GSAP инсталация
- [ ] Lucide Icons
- [ ] Git repo + Cloudflare Pages свързване

### Фаза 3: Разработка (компонент по компонент)
- [ ] BaseLayout (fonts, meta, global CSS)
- [ ] Navbar
- [ ] Hero
- [ ] Services + ServiceCard
- [ ] Gallery + BeforeAfterSlider
- [ ] Pricing + PricingCard
- [ ] About
- [ ] Testimonials
- [ ] Location (Google Maps embed)
- [ ] Contact + ContactForm
- [ ] Footer

### Фаза 4: Полиране
- [ ] GSAP scroll анимации на всяка секция
- [ ] Hover ефекти
- [ ] Оптимизация на снимките (WebP, lazy loading)
- [ ] SEO мета тагове + Schema.org
- [ ] Lighthouse audit → цел 95+

### Фаза 5: Deploy
- [ ] Push към GitHub
- [ ] Cloudflare Pages build
- [ ] Custom домейн + SSL
- [ ] Google Search Console submit

### Фаза 6: Разширения (по-късно)
- Booking система: Cal.com embed (open source) или Calendly
- Блог секция за SEO съдържание

---

## 9. Бюджет

| Позиция | Цена |
|---|---|
| Домейн (`.bg` или `.com`) | ~25–50 лв/година |
| Хостинг (Cloudflare Pages) | 0 лв |
| Шрифтове (Google Fonts) | 0 лв |
| Иконки (Lucide) | 0 лв |
| Plausible Analytics | 9 €/месец или self-hosted безплатно |
| **Минимум** | **~25–50 лв/година** |

---

*Спецификацията е финализирана на 30 април 2026. Всички технологични избори са направени — не се преразглеждат освен при основателна причина.*
