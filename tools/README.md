# Интерактивные инструменты

Промпты и утилиты для настройки и оптимизации Claude Code.

## Содержание

| Файл | Описание | Использование |
|------|-------------|-------|
| [audit-prompt.md](./audit-prompt.md) | Комплексный аудит настройки с персонализированными рекомендациями (8 направлений, оценка из 100) | `cat audit-prompt.md \| claude` |
| [permissions-audit-prompt.md](./permissions-audit-prompt.md) | Аудит того, всё ли ещё ваши правила разрешений образуют защитную границу: широкие разрешения на выполнение, покрытие правил deny и ask, состояние песочницы (sandbox) (6 этапов, оценка из 100, включая массовую проверку проектов) | `cat permissions-audit-prompt.md \| claude` |
| [context-audit-prompt.md](./context-audit-prompt.md) | Измерение и улучшение архитектуры контекста | `cat context-audit-prompt.md \| claude` |
| [spec-completeness-audit.md](./spec-completeness-audit.md) | Аудит полноты спецификации проекта для безопасного делегирования задач агенту (5 слоёв спецификации, оценка из 100) | `cat spec-completeness-audit.md \| claude` |
| [audit-cheatsheet-prompt.md](./audit-cheatsheet-prompt.md) | Оценка необходимости шпаргалки для проекта и аудит уже существующих | `cat audit-cheatsheet-prompt.md \| claude` |
| [onboarding-prompt.md](./onboarding-prompt.md) | Персонализированный вводный тур с учётом вашего профиля | `cat onboarding-prompt.md \| claude` |
| [mobile-access.md](./mobile-access.md) | Руководство по настройке мобильного доступа через ttyd + Tailscale | Пошагово |

## Какой аудит и когда использовать

| Вопрос | Инструмент |
|----------|------|
| Всё ли в порядке со всей моей настройкой? | `audit-prompt.md` |
| Действительно ли мои правила разрешений что-либо ограничивают? | `permissions-audit-prompt.md` |
| Не трачу ли я контекст впустую? | `context-audit-prompt.md` |
| Можно ли здесь безопасно делегировать работу агенту? | `spec-completeness-audit.md` |
| Есть ли в этом репозитории секреты или поверхности для инъекций? | `/security-audit` (слэш-команда) |

## Быстрый аудит

Для быстрого автоматического сканирования используйте скрипт:

```bash
# Зафиксировано на проверенном коммите: скачайте, прочитайте и только затем запускайте вместо передачи меняющейся ветки напрямую в bash
AUDIT_SCAN_REF=eab8adc215822f67629b6a0f9366f60a1db9b03c
curl -fsSL "https://raw.githubusercontent.com/FlorianBruniaux/claude-code-ultimate-guide/${AUDIT_SCAN_REF}/examples/scripts/audit-scan.sh" -o audit-scan.sh
less audit-scan.sh
bash audit-scan.sh
```

---

*Вернуться к [главному README](../README.md)*
