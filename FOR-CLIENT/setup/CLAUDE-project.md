# CLAUDE.md — Наталья Андронова (рабочий контекст)

> Скопируй этот файл как `CLAUDE.md` в папку проекта если нужна чистая версия.
> Актуальный CLAUDE.md уже лежит в корне проекта — этот файл как резервная копия.

---

## О ПРОЕКТЕ

**Клиент:** Наталья Андронова
**Бренд:** «НАТАЛЬЯ | ФРИЛАНС С 0»
**Сайт:** https://nataliya-andronova.ru
**Бот:** @nataliya_andronova_bot
**Описание:** Воронка продаж — Telegram-бот прогрева (9 дней) + Admin Panel + лендинг

---

## СТЕК

| Компонент | Технология |
|-----------|-----------|
| Лендинг | React + Vite + Tailwind |
| Telegram Bot | TypeScript + Telegraf |
| Admin Backend | FastAPI + SQLAlchemy |
| Admin Frontend | Next.js 16 + shadcn/ui |
| База данных | SQLite (`/app/data/bot.db`) |
| Деплой | Docker на VPS (Beget) |
| Nginx + SSL | Let's Encrypt (до 2026-06-14) |

---

## СЕРВЕР

```
IP:     155.212.128.171
SSH:    ssh -i ~/.ssh/clients_vps root@155.212.128.171
Проект: /opt/natalia/
Сайт:   /var/www/natalia/
```

---

## КЛЮЧЕВЫЕ ПРАВИЛА

1. **Тексты бота** — только в `bot/src/text.ts`
2. **Тексты лендинга** — только в `src/content.ts`
3. **После правок бота** — rsync src/ + docker compose build bot + up
4. **После правок лендинга** — npm run build + rsync dist/
5. **InSTART** — нигде в публичных материалах не упоминать
6. **Гарантия возврата** — НЕТ, не добавлять
7. **Голосовые** — `bot/assets/voice/voice_01.ogg`, `voice_02.ogg`, `voice_03.ogg`

---

## СКИЛЛЫ ПРОЕКТА

- `skill-bot-edits.md` — полный гайд по боту (деплой, структура, workflow)
- `skill-landing-edits.md` — полный гайд по лендингу

При любой задаче по боту или лендингу — сначала прочитай соответствующий скилл.

---

## ТАРИФЫ (финальные)

| Тариф | Цена |
|-------|------|
| Быстрый старт | 1 990 ₽ |
| Система | 7 990 ₽ |
| Рост (ХИТ) | 14 990 ₽ |
| VIP | 24 990 ₽ |

---

## ДИЗАЙН-ТОКЕНЫ

Терракот `#A0522D` · Золото `#C4A265` · Крем `#F5EDE4`
Шрифты: Unbounded 900 · Playfair Display Italic · Montserrat
