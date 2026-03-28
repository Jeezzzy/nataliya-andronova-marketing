# Session Anchor — fabrika-kontenta-v4 v4.3.0

## Plugin State
- **Плагин:** fabrika-kontenta-v4 **v4.3.0**
- **Путь:** `/Users/user/Library/Application Support/Claude/local-agent-mode-sessions/725ee1ca-a43d-4af0-b766-1ea61b398abd/202d6211-2c8c-4566-a6e5-8c3a5d683f4b/cowork_plugins/marketplaces/local-desktop-app-uploads/fabrika-kontenta-v4/`
- **Патчи P1-P14** применены

## ЖЕЛЕЗНОЕ ПРАВИЛО
- Патчить ТОЛЬКО через DC start_process + python3 (assert-based)
- НИКОГДА repackaging / .plugin / present_files
- ВСЕГДА обновлять ОБА plugin.json (корневой + .claude-plugin/)
- DC read_file на .md → метаданные. Использовать cat через start_process

## Что сделано (P13-P14)
- `skills/designer/SKILL.md` — ПОЛНАЯ ЗАМЕНА на Visual Prompt Director
- 9 references в `skills/designer/references/`:
  tpl-carousel, tpl-post, tpl-illustration, tpl-presentation, tpl-cover, tpl-avatar,
  archetypes, slide-techniques, anti-gpt-visual
- Оба plugin.json + CHANGELOG → 4.3.0

## Pending
Нет задач — плагин обновлён
