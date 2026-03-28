# Система обучения (3 уровня)

## Структура
- `corrections.md` — коррекции от клиента (применяются всегда)
- `patterns.md` — работающие паттерны
- `anti-patterns.md` — что не работает
- `pending/` — контент на проверку (после публикации → approved или rejected)
- `approved/` — работающие тексты с метриками (высокий CTR/отклик)
- `rejected/` — что не сработало + пометка почему

## Флоу
1. Контент создан → копия автоматически в `pending/`
2. После публикации + замер метрики:
   - Зашло (CTR/отклик/репосты) → `/learning approve` → `approved/`
   - Слабый охват / не в голосе → `/learning reject` → `rejected/`
3. `corrections.md` пополняется при каждом «не так» от клиента
4. `patterns.md` обновляется по approved/ — что работает
5. `anti-patterns.md` обновляется по rejected/ — чего избегать

## Команды
- `/learning status` — показать pending контент
- `/learning approve [файл]` — переместить в approved, записать паттерн
- `/learning reject [файл]` — переместить в rejected, записать антипаттерн
- `/learning correct [текст]` — записать коррекцию
- `/learning patterns` — показать все паттерны и антипаттерны
