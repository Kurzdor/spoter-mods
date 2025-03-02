### Принудительное обновление кэша
Чтобы переустановить Python 2.7 и зависимости:
1. Перед запуском workflow измените переменную в файле `.github/workflows/build-and-release__in_work.yml`:
   ```yaml
   env:
     FORCE_CACHE_REFRESH: "true"


# 🧹 Очистка старых запусков Workflow

Автоматически удаляет старые запуски GitHub Actions, сохраняя последние 3 для каждого workflow.

## ⚙️ Параметры

| Параметр            | По умолчанию              | Описание                                 |
|---------------------|---------------------------|------------------------------------------|
| `dry_run`           | `true`                    | Режим тестирования (без удаления)        |
| `target_statuses`   | `completed,failure,cancelled` | Удалять только эти статусы          |
| `exclude_workflows` | -                         | Исключить workflow по названиям через запятую |

## 🚀 Примеры использования

### 1. Тестовый запуск
```yaml
- uses: ./.github/workflows/cleanup-runs.yml
  with:
    dry_run: true
```

### 2. Реальное удаление
```yaml
- uses: ./.github/workflows/cleanup-runs.yml
  with:
    dry_run: false
    exclude_workflows: "deploy.prod,ci-tests"
```

### 3. Кастомные статусы
```yaml
- uses: ./.github/workflows/cleanup-runs.yml
  with:
    target_statuses: "failure,timed_out"
```

## 📋 Список статусов
- `completed` – Завершен
- `failure` – Ошибка
- `cancelled` – Отменен
- `timed_out` – Таймаут
- `in_progress` – **Не удаляется!** (активные запуски)

## 🔍 Логирование
Пример вывода:
```
🔍 Обработка: CI Tests (ID: 123)
📊 Статистика:
  Всего запусков: 15
  Сохраняем: 3
  Удаляем: 12
🚮 Удаление: ID 1001 (статус: failure, дата: 2025-03-01T12:00:00Z)
```

## ⚠️ Важно
- Активные запуски (`in_progress`) **никогда** не удаляются
- Для критически важных процессов добавьте их в `exclude_workflows`
- Расписание: ежедневно в 07:00 МСК (`cron: "0 4 * * *"`)

[Ссылка на файл workflow](cleanup-runs.yml)
