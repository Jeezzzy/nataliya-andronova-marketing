# CLAUDE.md — Фабрика Контента: Наталья Андронова

> Этот файл читается автоматически. Содержит данные клиента + правила проекта.
> Движок фабрики — в плагине content-dept-fil-ai (v5.3.3).

---

## КЛИЕНТ

```
CLIENT_NAME: Наталья Андронова
PROJECT_SLUG: andronova
TIMEZONE: Europe/Moscow
PRIMARY_PLATFORM: Telegram
ONBOARDING_DATE: 2026-03-19
```

---

## ТАРИФЫ

| Тариф | Цена |
|---|---|
| Старт (базовый) | 1 990 ₽ |
| Основной | ~8 000 ₽ |
| VIP / личное сопровождение | 24 990 ₽ |

> CTA единый: t.me/andronova_nata_bot | Гарантий нет — позиция «я даю инструменты, результат зависит от тебя»

---

## ПРАВИЛА КОНТЕНТА

- CTA: t.me/andronova_nata_bot (написать СТАРТ) | Директ / ЛС
- Тон: см. brand/voice-style.md
- Аватары: см. brand/audience.md
- ТАБУ: слово «inSTART» — не упоминать публично
- Кейсы: ТОЛЬКО из brand/social-proof.md, не выдумывать

---

## АКТИВНЫЕ ПАКЕТЫ

- [x] Core (Telegram, Threads — всегда)
- [ ] Визуал (Instagram карусели)
- [ ] Видео (Reels, YouTube Shorts)
- [ ] SEO (статьи, GEO-контент)
- [ ] Прогрев (серии, офферы, CTA)

---

## КУДА СОХРАНЯТЬ (единые правила)

> ВСЕ результаты — ТОЛЬКО в папки этого проекта. Никаких внешних путей.

| Что | Куда | Формат имени |
|-----|------|-------------|
| Готовый контент | `output/content/[platform]/` | `YYYY-MM-DD_[slug].md` |
| Визуал-промпты | `output/visuals/` | `YYYY-MM-DD_[тип]_[slug].md` |
| HTML-дашборды | `output/dashboards/` | `content-YYYY-MM-DD.html` |
| Ресёрч-отчёты | `output/research/` | `[тип]-research-YYYY-MM-DD.md` |
| Аудит-отчёты | `output/audits/` | `audit-[канал]-YYYY-MM-DD.md` |
| Стратегия, планы | `strategy/` | `[тип]-YYYY-MM-DD.md` |
| Контент на ревью | `learning/pending/` | `YYYY-MM-DD_[platform]_[slug].md` |
| Коррекции клиента | `learning/corrections.md` | Дописывать в конец |
| Контекст сессии | `memory/active-context.md` | Перезаписывать |

### Запрещено:
- ❌ Сохранять в ~/SECOND-BRAIN/, ~/DASHBOARDS/ или любые внешние папки
- ❌ Сохранять в /tmp/ или системные директории
- ❌ Дублировать один контент в несколько папок

---

## ЛОГИРОВАНИЕ (обязательно)

> Каждое действие агента фиксируется в лог-файле текущей сессии.

- Лог-файл: `logs/SESSION-LOG-[YYYY-MM-DD].md`
- **Создаётся автоматически** при первом действии дня
- **Обновляется** после каждого завершённого шага
- Формат записи:

```
### [HH:MM] — [Что сделано]
- Файлы: [список]
- Решения: [если есть]
- Флаги: [если есть]
```

**Правило:** Нельзя завершить задачу без записи в лог.

---

## РАСПИСАНИЕ

```
morning_check: true
research_interval: weekly
content_plan_day: monday
audit_memory_day: friday
learning_review_day: friday
```

### Утренний чек (при каждом запуске):
```
1. READ memory/active-context.md
2. READ schedule.md
3. CHECK learning/pending/
4. CHECK learning/corrections.md
5. Предложить задачи дня
```

---

## БЫСТРЫЕ КОМАНДЫ

| Команда | Что делает |
|---------|-----------|
| `/onboarding` | Полная распаковка (40-60 мин) |
| `/status` | Статус brand/ и пакеты |
| `/telegram [тема]` | Пост для Telegram |
| `/threads [тема]` | Пост для Threads |
| `/reels [тема]` | Сценарий Reels / Shorts |
| `/article [тема]` | Статья / GEO-статья |
| `/carousel [тема]` | Карусель для Instagram |
| `/hooks [тема]` | 5 вариантов хуков |
| `/plan` | Контент-план на неделю |
| `/dashboard` | HTML-дашборд сессии |
| `/audit` | Ревизия памяти и brand/ |
| `/learning` | Управление обучением |

---

*Фабрика Контента v5.3.3 | Fil AI Hub | 2026-03-27*
