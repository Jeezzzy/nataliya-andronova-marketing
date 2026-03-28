# ВИЗУАЛЬНЫЙ СТИЛЬ И ДИЗАЙН-СИСТЕМА
> Проект: НАТАЛЬЯ | ФРИЛАНС С 0
> Обновлено: 2026-03-20
> Источник: готовый сайт nataliya-andronova

---

## Цветовая палитра

> Авторитетный источник: `CLAUDE Devs/nataliya-andronova/src/App.css` + `src/config/theme.ts`

| Роль | Цвет | HEX | HSL | Использование |
|------|------|-----|-----|--------------|
| **Primary / Accent** | Terracotta | `#A0522D` | `19 56% 40%` | CTA-кнопки, акценты, иконки |
| **Gold** | Gold | `#C4A265` | `24 70% 70%` | Градиенты, выделение смыслов |
| **Background** | Cream | `#F5EDE4` | `33 43% 93%` | Основной фон, hero-секция |
| **Secondary** | Powder Pink | `#E8D4C4` | `27 41% 84%` | Вторичные блоки, подложки |
| **Muted / Border** | Beige | `#D4B8A0` | `28 38% 73%` | Бордеры, поля ввода, разделители |
| **Cards** | White | `#FFFFFF` | `0 0% 100%` | Карточки тарифов, блоки контента |
| **Foreground** | Graphite | `#3D3D3D` | `0 0% 24%` | Основной текст |

### Градиенты (зафиксированы на лендинге)

**Hero-фон:**
```css
background: linear-gradient(135deg, #F5EDE4 0%, #EDE0D4 30%, #E8D4C4 60%, #F0E6DC 100%);
```

**Текст-градиент (заголовки):**
```css
background: linear-gradient(180deg, #1a1a1a 0%, #3D2B1F 40%, #7A3E20 70%, #A0522D 100%);
```

---

## Типографика

| Уровень | Шрифт | Стиль | Аналоги для ИИ |
|---------|-------|-------|----------------|
| **H1, H2** | `Unbounded` (900) | Широкий, геометрический, Extra Bold | Benzin, Impact, Bold Sans-serif |
| **Подзаголовки** | `Playfair Display` (Italic) | Элегантная антиква с наклоном | Classic Serif, Fashion Editorial |
| **Текст** | `Montserrat` | Чистый современный гротеск | —  |

Google Fonts:
```
https://fonts.googleapis.com/css2?family=Unbounded:wght@700;900&family=Playfair+Display:ital,wght@1,500;1,600;1,700&family=Montserrat:ital,wght@0,100..900;1,100..900&display=swap
```

---

## Визуальные эффекты

- **Градиенты:** мягкие переходы Cream → Powder Pink; текст Graphite → Terracotta
- **Скругления:** `1rem` (16px) — мягкие, дружелюбные
- **Эффекты:** Glassmorphism (матовое стекло), лёгкие тени, чистый минимализм, «воздух»

---

## Промпты для генерации изображений

### Ключевые слова (всегда включать):
`Terracotta and cream color palette, minimalist workspace, premium aesthetic, feminine professional, warm natural lighting, elegant textures, glassmorphism elements, high-end editorial style`

### Шаблоны промптов:

**Рабочее место:**
> Premium minimalist workspace with a laptop on a cream-colored wooden desk, a terracotta clay vase with dried flowers, golden sunlight streaming through a window, soft powder pink background, 8k resolution, elegant and clean aesthetic, editorial photography style.

**Абстракция для фона:**
> Abstract flowing liquid shapes in terracotta, gold, and cream colors, smooth gradients, soft organic forms, glassmorphism overlays, high-end luxury feel, clean and professional, 4k, macro photography.

**Портрет / аватар (vibe):**
> Modern professional woman in a terracotta blazer, smiling confidently, blurred cream-colored office background with minimalist decor, warm soft lighting, high-end commercial photography, sophisticated and approachable vibe.

**Для Reels обложек:**
> Bold text overlay on terracotta gradient background, Unbounded font style, cream colored accent elements, minimal clean design, social media story format 9:16, premium feel.

**Для Telegram постов:**
> Clean card design with cream background, terracotta accent bar on left side, elegant typography, one powerful quote in center, minimalist premium style, 1:1 square format.

---

## Эталонные ассеты (скопированы с лендинга и бота)

> Папка: `brand/assets/`

| Файл | Что это | Использование |
|------|---------|--------------|
| `natalia-photo.png` | Основное фото Натальи | OG-image, обложки, карусели |
| `natalia-welcome.jpg` | Приветственное фото | Первый пост, знакомство |
| `natalia-proof.jpg` | Фото-доказательство | Посты с результатами |
| `consultation.jpg` | Фото консультации | Продающие посты |
| `result.jpg` | Результат/достижение | Кейсовые посты |
| `bg-hero.jpg` | Фоновое изображение | Сторис-фоны, обложки |
| `logo.svg` | Логотип (SVG, «Н») | Подписи, водяные знаки |
| `review-support.jpg` | Скрин поддержки | Посты про сопровождение |
| `review-valentina.jpg` | Отзыв Валентины | Социальные доказательства |
| `cases/case1-13.png` | Скрины кейсов учениц | Посты с результатами |
| `tariffs/tariff-start.jpg` | Тариф «Быстрый старт» | Ценовые посты |
| `tariffs/tariff-system.jpg` | Тариф «Система» | Ценовые посты |
| `tariffs/tariff-growth.jpg` | Тариф «Рост» ⭐ хит | Ценовые посты |
| `tariffs/tariff-premium.jpg` | Тариф «Премиум» | Ценовые посты |
| `tariffs/tariff-table.jpg` | Таблица всех тарифов | Сравнительные посты |

**FaceID-якорь для AI-генерации:** см. `natalia-photo.png` — эталон внешности для всех промптов.

## Рекомендации по композиции

- Больше свободного пространства (negative space)
- Природные материалы: дерево, глина, текстиль
- Освещение: мягкое, «золотой час», без резких теней
- Настроение: уютная уверенность, не пафос
- Фото: живые, не студийные — за ноутбуком, с телефоном, с чашкой кофе

---

*Дизайн-система синхронизирована с лендингом nataliya-andronova.ru. Версия 1.1 | 2026-03-28*
