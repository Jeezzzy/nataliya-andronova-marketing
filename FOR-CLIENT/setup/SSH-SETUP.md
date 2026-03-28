# Настройка SSH-доступа к серверу

Без SSH-ключа невозможно задеплоить изменения бота и лендинга на VPS.

---

## Данные сервера

| Параметр | Значение |
|----------|---------|
| IP | `155.212.128.171` |
| Пользователь | `root` |
| Хостинг | Beget VPS |
| Ключ | `clients_vps` |

---

## Шаг 1 — Получить ключ

Ключ `clients_vps` хранится у Олега (Fil AI Hub). Запроси файл `clients_vps` (без расширения).

---

## Шаг 2 — Разместить ключ

```bash
# Создать папку если нет
mkdir -p ~/.ssh

# Скопировать ключ
cp /путь/к/clients_vps ~/.ssh/clients_vps

# Установить правильные права (ОБЯЗАТЕЛЬНО)
chmod 600 ~/.ssh/clients_vps
chmod 700 ~/.ssh
```

---

## Шаг 3 — Проверить подключение

```bash
ssh -i ~/.ssh/clients_vps root@155.212.128.171 "echo Подключение работает"
```

Если видишь `Подключение работает` — всё настроено.

---

## Шаг 4 — Добавить в ~/.ssh/config (удобно)

```bash
cat >> ~/.ssh/config << 'EOF'
Host natalia-vps
    HostName 155.212.128.171
    User root
    IdentityFile ~/.ssh/clients_vps
EOF
```

После этого можно подключаться короче:
```bash
ssh natalia-vps
```

---

## Частые проблемы

**`Permission denied (publickey)`**
→ Проверь права на ключ: `chmod 600 ~/.ssh/clients_vps`

**`Connection refused`**
→ Сервер недоступен. Проверь IP или статус VPS в панели Beget.

**`WARNING: UNPROTECTED PRIVATE KEY FILE`**
→ Права слишком широкие: `chmod 600 ~/.ssh/clients_vps`
