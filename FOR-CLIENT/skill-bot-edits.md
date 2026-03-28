---
name: nataliya-bot-edits
description: Скилл для работы с Telegram-ботом проекта Наталья Андронова (@nataliya_andronova_bot). Используй когда нужно: изменить тексты прогрева, добавить/удалить голосовые или медиафайлы, поправить логику квиза, изменить расписание рассылок, исправить баг в боте, задеплоить изменения на VPS. Триггеры: "изменить текст бота", "добавить голосовое", "поправить воронку", "задеплоить бот", "бот не работает", "квиз", "прогрев", "scheduler".
---

# Скилл: Редактирование Telegram-бота Натальи Андроновой

## Контекст проекта

**Бот:** @nataliya_andronova_bot
**Стек:** TypeScript + Telegraf + better-sqlite3
**Деплой:** Docker контейнер `na_bot` на VPS `root@155.212.128.171`
**SSH ключ:** `~/.ssh/clients_vps`
**Проект на сервере:** `/opt/natalia/`
**Локальный код:** `/Users/user/Documents/CLAUDE FIL AI/CLAUDE Devs/nataliya-andronova/bot/`

---

## Структура бота

```
bot/
├── src/
│   ├── index.ts          ← Точка входа, регистрация хендлеров
│   ├── text.ts           ← ВСЕ тексты бота (TEXTS, TARIFFS)
│   ├── config.ts         ← Конфиг (токен, admin ID)
│   ├── api.ts            ← REST API для Admin Panel (порт 3000)
│   ├── init_db.ts        ← Инициализация БД при старте
│   ├── database/
│   │   └── index.ts      ← SQLite queries, путь /app/data/bot.db
│   ├── handlers/
│   │   ├── start.ts      ← /start: баннер → текст → фото → голосовые → квиз
│   │   ├── quiz.ts       ← Квиз (3 вопроса) → сегментация → лид-магнит
│   │   ├── callbacks.ts  ← Inline-кнопки (гостевой доступ, тарифы)
│   │   ├── admin.ts      ← Команды /admin, /stats
│   │   ├── consult.ts    ← Запись на консультацию
│   │   ├── guide.ts      ← Отправка гайда
│   │   └── ai.ts         ← AI-ответы (заглушка)
│   └── services/
│       └── scheduler.ts  ← Планировщик прогрева (дни 1-9)
├── assets/               ← Медиафайлы
│   ├── voice/            ← Голосовые: voice_01.ogg, voice_02.ogg, voice_03.ogg
│   ├── *.pdf             ← Лид-магниты (dekret_10k, plan_pobega, after_35, guide)
│   └── img_*.jpg         ← Изображения (welcome, proof, тарифы)
├── schema.sql            ← Схема БД
├── package.json
└── Dockerfile
```

---

## Ключевые файлы для правок

### Тексты → `bot/src/text.ts`
Все тексты бота хранятся в одном файле. Структура:
- `TARIFFS` — цены тарифов (синхронизированы с лендингом)
- `TEXTS.GREETING(name)` — приветствие при /start
- `TEXTS.AFTER_VOICE_INTRO` — подводка после голосовых
- `TEXTS.QUIZ_Q0..Q3` — вопросы квиза
- `TEXTS.QUIZ_A*` — кнопки ответов квиза
- `TEXTS.DAY_*` — тексты дней прогрева (объект по сегментам)

### Голосовые → `bot/assets/voice/`
Текущие файлы: `voice_01.ogg`, `voice_02.ogg`, `voice_03.ogg`
Используются в `handlers/start.ts` массив `VOICE[]`.
При добавлении/удалении файла — обновить массив в `start.ts`.

### Стартовый хендлер → `bot/src/handlers/start.ts`
Последовательность при /start:
1. `img_welcome.jpg` — баннер
2. `TEXTS.GREETING` — текст с историей
3. `img_natasha_proof.jpg` — скрин банка
4. Голосовые из `VOICE[]` с паузами 3 сек
5. `TEXTS.AFTER_VOICE_INTRO` — подводка
6. Кнопка «Да, поехали →» → запускает квиз

### Планировщик → `bot/src/services/scheduler.ts`
Отправляет сообщения по дням прогрева (День 1-9).
Сегменты: `dekret`, `naim`, `age35plus`.

### Гостевой доступ InSTART → `callbacks.ts` + `text.ts`
День 7 воронки отправляет гостевой доступ к платформе InSTART на 48 часов.

**Как работает:**
1. Scheduler отправляет `WARMUP_DAY_7_OFFER` с inline-кнопками
2. Пользователь нажимает «Хочу гостевой доступ» → callback `guest_yes`
3. Бот отправляет 3 сообщения подряд:
   - Фото-карточка `img_guest_details.jpg`
   - Инструкция `WARMUP_DAY_7_GUEST_GIVEN` — видео-урок, регистрация на ooo-instart.ru, что заполнить
   - Ключ `WARMUP_DAY_7_GUEST_KEY(key)` — из переменной `GUEST_KEY` в `.env`

**Ссылки внутри инструкции (зашиты в `text.ts`):**
- Видео-урок: `https://vk.com/video-226069864_456239453`
- Сайт: `https://ooo-instart.ru`

**Гостевой ключ:**
- Хранится в `/opt/natalia/.env` → `GUEST_KEY=...`
- Текущий: `NEFRLXGNGU86AU0EDLXGN069R62IJP7MD85NXH5C4ZAA4APFIG8ASFTHL55O48S4`
- Действует 48 часов после активации на сайте
- При смене ключа: обновить `GUEST_KEY` в `.env` → `docker compose restart bot`

```bash
# Обновить ключ
ssh -i ~/.ssh/clients_vps root@155.212.128.171 \
  "sed -i 's/GUEST_KEY=.*/GUEST_KEY=НОВЫЙ_КЛЮЧ/' /opt/natalia/.env && cd /opt/natalia && docker compose restart bot"
```

---

## КРИТИЧЕСКОЕ ПРАВИЛО ДЕПЛОЯ

> ⛔ Docker собирает образ ИЗ ФАЙЛОВ НА СЕРВЕРЕ, не с Mac.
> Если изменить файл локально и не скопировать через `scp`/`rsync` — изменение потеряется.

### Workflow изменения кода бота

```bash
# 1. Редактируешь файл локально (Mac)

# 2. Синхронизируешь на сервер (для src/ файлов)
rsync -avz -e "ssh -i ~/.ssh/clients_vps" \
  "/Users/user/Documents/CLAUDE FIL AI/CLAUDE Devs/nataliya-andronova/bot/src/" \
  root@155.212.128.171:/opt/natalia/bot/src/

# 3. Для медиафайлов (assets)
rsync -avz -e "ssh -i ~/.ssh/clients_vps" \
  "/Users/user/Documents/CLAUDE FIL AI/CLAUDE Devs/nataliya-andronova/bot/assets/" \
  root@155.212.128.171:/opt/natalia/bot/assets/

# 4. Пересборка и рестарт
ssh -i ~/.ssh/clients_vps root@155.212.128.171 \
  "cd /opt/natalia && docker compose build bot && docker compose up -d bot"

# 5. Проверка логов
ssh -i ~/.ssh/clients_vps root@155.212.128.171 \
  "docker logs na_bot --tail=15"
```

### Быстрый рестарт (без изменений)
```bash
ssh -i ~/.ssh/clients_vps root@155.212.128.171 \
  "cd /opt/natalia && docker compose restart bot"
```

---

## Замена медиафайлов

Голосовые: скопировать новые `.ogg` в `bot/assets/voice/`, обновить массив `VOICE[]` в `start.ts` если файлов стало больше/меньше, затем rsync + build.

Изображения: скопировать новый файл с тем же именем в `bot/assets/`, затем rsync + build.

PDF лид-магниты: `dekret_10k.pdf`, `plan_pobega.pdf`, `after_35.pdf`, `guide.pdf` — скопировать с тем же именем, rsync + build.

---

## Воронка прогрева (9 дней)

| День | Что происходит |
|------|---------------|
| 0 | /start → квиз → лид-магнит по сегменту |
| 1–6 | Прогревающие сообщения из scheduler.ts |
| 7 | Гостевой доступ InSTART на 48 часов |
| 8–9 | Дожим / CTA |

**Сегменты:** `dekret` / `naim` / `age35plus`
**⚠️ InSTART нигде в публичных материалах не упоминается — только внутри бота.**

---

## Тарифы (финальные, не менять без согласования)

| Тариф | Цена |
|-------|------|
| Быстрый старт | 1 990 ₽ |
| Система | 7 990 ₽ |
| Рост (ХИТ) | 14 990 ₽ |
| VIP | 24 990 ₽ |

Цены и ссылки на оплату хранятся в `bot/src/text.ts` → `TARIFFS`.

**Ссылки на оплату (YooKassa):**

| Тариф | Ссылка |
|-------|--------|
| Быстрый старт | `https://yookassa.ru/my/i/acfCY58woYwU/l` |
| Система | `https://yookassa.ru/my/i/acfDnoJW9Aqh/l` |
| Рост | `https://yookassa.ru/my/i/acfEGpxv6dsm/l` |
| VIP | `https://yookassa.ru/my/i/acfEmguzqvqw/l` |

Ссылки показываются в: День 4, День 9, callback `want_start`, callback `see_tariffs`.
**Обязательно синхронизировать цены с `src/content.ts` на лендинге.**

---

## Диагностика проблем

```bash
# Контейнер упал?
ssh -i ~/.ssh/clients_vps root@155.212.128.171 "docker compose -f /opt/natalia/docker-compose.yml ps"

# Ошибки в логах
ssh -i ~/.ssh/clients_vps root@155.212.128.171 "docker logs na_bot --tail=50"

# Проверить файл попал ли в контейнер
ssh -i ~/.ssh/clients_vps root@155.212.128.171 "docker exec na_bot ls /app/assets/voice/"

# БД
ssh -i ~/.ssh/clients_vps root@155.212.128.171 "docker exec na_bot ls /app/data/"
```

---

## Известные проблемы (технический долг)

| Проблема | Приоритет | Статус |
|----------|-----------|--------|
| Scheduler день 1: отправляет пустую строку | 🔴 Critical | Открыт |
| /start payload UTM не обрабатывается | 🔴 Critical | Открыт |
| Inline-кнопки День 7 (гостевой) | ✅ Решено | 2026-03-28 |
| www поддомен — DNS не настроен | 🟡 Medium | Открыт |
