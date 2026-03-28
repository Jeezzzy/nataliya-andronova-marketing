---
name: nataliya-landing-edits
description: Скилл для правок лендинга проекта Наталья Андронова (nataliya-andronova.ru). Используй когда нужно: изменить тексты на сайте, поправить цены, добавить/убрать секцию, изменить кнопки, поправить стили, обновить фото. Триггеры: "изменить текст на сайте", "поправить лендинг", "обновить заголовок", "изменить цену", "задеплоить сайт", "поправить блок", "добавить секцию".
---

# Скилл: Правки лендинга Натальи Андроновой

## Контекст проекта

**Сайт:** https://nataliya-andronova.ru
**Стек:** React + Vite + Tailwind + framer-motion
**Деплой:** статика на VPS `/var/www/natalia/` через nginx
**SSH:** `ssh -i ~/.ssh/clients_vps root@155.212.128.171`
**Локальный код:** `/Users/user/Documents/CLAUDE FIL AI/CLAUDE Devs/nataliya-andronova/`

---

## Структура лендинга

```
src/
├── content.ts            ← ВСЕ тексты и данные сайта (главный файл правок)
├── App.tsx               ← Корневой компонент, импорт блоков
├── pages/
│   ├── Index.tsx         ← Главная страница (подключает все блоки)
│   ├── Offer.tsx         ← Публичная оферта
│   └── Privacy.tsx       ← Политика конфиденциальности
└── blocks/               ← Секции страницы
    ├── Hero/             ← Заголовок, CTA, авторка
    ├── About/            ← О Наталье
    ├── ForWhom/          ← Для кого (Pain Points)
    ├── Program/          ← Программа курса
    ├── Bonuses/          ← Бонусы
    ├── Cases/            ← Кейсы учениц
    ├── Pricing/          ← Тарифы
    ├── FAQ/              ← Вопросы и ответы
    ├── Footer/           ← Подвал
    ├── CTA/              ← Призыв к действию
    ├── Contact/          ← Контакты
    ├── Payment/          ← Оплата
    ├── Quote/            ← Цитата
    ├── System/           ← Система работы
    └── SuccessFactors/   ← Факторы успеха
```

---

## Главный файл правок: `src/content.ts`

**Всегда редактировать только `content.ts`** — все блоки берут данные оттуда.
Прямо в блоки лезть только если нужна структурная правка (новый элемент, другой порядок).

### Ключевые экспорты

```typescript
export const hero         // Заголовок, подзаголовок, буллеты, CTA-кнопки
export const painPoints   // «Узнаёшь себя?» — 5 карточек ЦА
export const about        // История Натальи, результаты
export const program      // Программа (модули)
export const bonuses      // Бонусы к курсу
export const cases        // Кейсы учениц (НЕ УДАЛЯТЬ без подтверждения)
export const pricing      // Тарифы и цены
export const faq          // FAQ вопросы/ответы
export const footer       // Ссылки, контакты
```

### URL-константы (вверху content.ts)
```typescript
const BOT_URL        = 'https://t.me/nataliya_andronova_bot?start=landing_hero'
const BOT_URL_TARIFF = 'https://t.me/nataliya_andronova_bot?start=tariff_growth'
const CHANNEL_URL    = 'https://t.me/andronova_nata'
```

---

## Дизайн-токены (не менять без согласования)

| Элемент | Значение |
|---------|---------|
| Primary | Терракот `#A0522D` |
| Акцент | Золото `#C4A265` |
| Фон | Крем `#F5EDE4` |
| Заголовки | **Unbounded 900** |
| Подзаголовки | **Playfair Display 500 Italic** |
| Тело | **Montserrat** |

---

## Тарифы (финальные, синхронизировать с ботом)

| Тариф | Цена |
|-------|------|
| Быстрый старт | 1 990 ₽ |
| Система | 7 990 ₽ |
| Рост (ХИТ) | 14 990 ₽ |
| VIP | 24 990 ₽ |

Цены в `src/content.ts` → `export const pricing`.
**Обязательно синхронизировать с `bot/src/text.ts` → `TARIFFS`.**

---

## Workflow правки и деплоя

### 1. Изменить текст / цену / данные
```bash
# Редактируем src/content.ts
# Собираем
cd "/Users/user/Documents/CLAUDE FIL AI/CLAUDE Devs/nataliya-andronova"
npm run build

# Деплоим
rsync -avz --delete -e "ssh -i ~/.ssh/clients_vps" \
  ./dist/ root@155.212.128.171:/var/www/natalia/
```

### 2. Изменить структуру блока (jsx/tsx)
```bash
# Редактируем нужный файл в src/blocks/[BlockName]/
# Потом то же самое: build + rsync dist/
```

### 3. Заменить изображение
```bash
# Копируем новый файл в public/ с тем же именем
# build + rsync
```

---

## Правила по контенту

- **InSTART не упоминается нигде** — ни в текстах, ни в кнопках, ни в meta
- **Гарантии возврата 30 дней НЕТ** — не добавлять нигде
- **Кейсы** (`export const cases`) — не удалять блок без явного «убрать кейсы»
- Все секции лендинга — согласованная воронка из ТЗ. Удалять блок только по явной команде

---

## Статика в `public/`

| Файл | Что |
|------|-----|
| `autor.png` | Фото Натальи (OG-image) |
| `bg-1.jpg` | Фоновое изображение |
| `favicon.svg` | Фавикон SVG (терракот + золото «Н») |
| `favicon.ico` | Фавикон .ico |

---

## Проверка после деплоя

```bash
# Убедиться что файлы обновились
ssh -i ~/.ssh/clients_vps root@155.212.128.171 "ls -la /var/www/natalia/"

# Nginx работает
ssh -i ~/.ssh/clients_vps root@155.212.128.171 "nginx -t"

# Открыть сайт
open https://nataliya-andronova.ru
```

---

## SSL

Сертификат Let's Encrypt, истекает **2026-06-14**.
Обновление: `ssh ... "certbot renew"`
