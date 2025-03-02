# 🚀 build-and-release.yml 🚀
### Принудительное обновление кэша
[Актуальная версия workflow](.github/workflows/build-and-release.yml)
Чтобы переустановить Python 2.7 и зависимости:
1. Перед запуском workflow измените переменную в файле `.github/workflows/build-and-release.yml`:
   ```yaml
   env:
     FORCE_CACHE_REFRESH: "true"
   ```

---


# 🚀 cleanup-runs.yml 🚀
# 🧹 Очистка старых запусков Workflow

Автоматически удаляет старые запуски GitHub Actions, сохраняя последние 3 для каждого workflow.

## ⚙️ Параметры

| Параметр            | По умолчанию              | Описание                                  |
|---------------------|---------------------------|-------------------------------------------|
| `dry_run`           | `true`                    | Режим тестирования (без удаления)         |
| `keep_last`         | 3                         | Количество сохраняемых запусков           |
| `max_days`          | 7                         | Удалять всё старше указанных дней         |
| `exclude_branches`  | -                         | Исключить ветки (через запятую)           |

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
    exclude_branches: "dev,test"
```

### 3. Удаление по возрасту
```yaml
- uses: ./.github/workflows/cleanup-runs.yml
  with:
    max_days: 30
```

## ⚠️ Важно
- **Никогда не удаляет**:
  - Активные запуски (`in_progress`)
  - Запуски из исключённых веток
  - Последние `keep_last` запусков
- **Обязательно удаляет**:
  - Все запуски старше `max_days` дней
  - Даже если они попадают в `keep_last`

## 🔍 Пример вывода
```
▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀
 Обработка: CI Tests
░░░░░░░░░░░░░░░░░░░░░░░░░░░
╞════════════════════════════════
 📊 Статистика:
 ├ Всего запусков: 15
 ├ Сохраняем: 3
 └ Удаляем: 12
╘════════════════════════════════
 ┌ ID: 12345
 ├ Статус: completed
 ├ Ветка: main
 ├ Дата: 2025-03-02 14:30
 └ Коммит: Fix critical security vulnerability...
```

[Актуальная версия workflow](cleanup-runs.yml)