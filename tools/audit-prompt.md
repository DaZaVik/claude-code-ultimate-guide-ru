# Аудит вашей настройки Claude Code

> Автономный промпт, который за один проход проводит аудит вашей конфигурации Claude Code — памяти проекта, гигиены правил, скиллов, агентов/команд, безопасности, MCP, команд рабочих процессов и актуальности.

**Автор**: [Florian BRUNIAUX](https://github.com/FlorianBruniaux) | Приглашённый директор по ИИ (Fractional Chief AI Officer)

**Источник**: [Полное руководство по Claude Code (The Ultimate Claude Code Guide)](https://github.com/FlorianBruniaux/claude-code-ultimate-guide/blob/main/guide/ultimate-guide.md)

---

## 1. Что делает этот промпт

Этот промпт превращает Claude в **оркестратор аудита** по 8 взвешенным измерениям (всего 100 баллов). Он выполняет быструю инвентаризацию через bash, а затем делегирует каждую область специализированному скиллу или команде, если они установлены, либо переключается на встроенные проверки в резервном режиме (фолбэк).

| Что проверяется | Как |
|---|---|
| Память и контекст (CLAUDE.md, правила, бюджет токенов) | Делегирует `/token-audit`, если установлен, иначе оценка через bash |
| Гигиена правил (`.claude/rules/`, валидность `paths:`) | Делегирует `/eval-rules`, если установлен, иначе сканирование через bash |
| Качество скиллов (frontmatter, effort, allowed-tools) | Делегирует `/eval-skills`, если установлен, иначе быстрая проверка |
| Качество агентов/команд (16 критериев, оценки A-F) | Делегирует `/audit-agents-skills`, если установлен, иначе базовая проверка |
| Состояние безопасности (разрешения, хуки, песочница) | Делегирует `/security-check`, если установлен, иначе проверка через bash |
| Экосистема MCP (серверы, риски БД, безопасность версий) | Встроенный bash (отдельный скилл не требуется) |
| Команды рабочих процессов (/investigate, /qa, /canary…) | Встроенное сканирование через bash |
| Актуальность и лучшие практики (устаревшие ссылки, баги кэша) | Встроенный bash + проверка паттернов |

**Чего он НЕ делает**: не заменяет глубокие инструменты анализа, которым делегирует задачи. Используйте `/security-audit`, `/token-audit`, `/eval-rules` напрямую, когда вам нужна полная детализация по конкретному измерению.

**Время**: ~5–8 мин, если установлены все скиллы аудита, и ~3–4 мин в резервном режиме.

**Важно**: Claude НЕ будет вносить никаких изменений без вашего явного одобрения.

---

## 2. Для кого это предназначено

| Уровень | Что вы получите |
|-------|-----------------|
| **Начинающий** | Узнаете, чего вам не хватает, и получите стартовые шаблоны |
| **Средний** | Выявите возможности для оптимизации и продвинутые паттерны |
| **Продвинутый пользователь** | Проверите свою конфигурацию и найдёте крайние случаи для доработки |

**Предварительные требования**:
- Установленный и работающий Claude Code
- Директория проекта для анализа (или только глобальная конфигурация)
- Оболочка Bash (нативная в macOS/Linux, WSL в Windows)

**Опционально** (для более детальных результатов): установленные `/token-audit`, `/eval-rules`, `/eval-skills`, `/audit-agents-skills`, `/security-check`. Команды установки см. в разделе 8.

---

## 3. Как использовать

### Шаг 1: Скопируйте промпт

Скопируйте всё содержимое внутри блока кода в [разделе 4](#4-the-prompt) ниже.

### Шаг 2: Запустите Claude Code

```bash
cd your-project-directory
claude
```

### Шаг 3: Вставьте и выполните

Вставьте промпт и нажмите Enter. Чтобы также провести аудит глобальной конфигурации `~/.claude/`, добавьте `--include-global` после вставленного текста.

### Шаг 4: Просмотрите результаты

Claude представит сводную таблицу оценок по 8 измерениям и запросит подтверждение перед внесением каких-либо изменений.

### Примечание по платформам

| Платформа | Путь к глобальной конфигурации |
|----------|-------------------|
| **macOS/Linux** | `~/.claude/` |
| **Windows** | `%USERPROFILE%\.claude\` |

---

## 4. Промпт

````markdown
# Аудит моей настройки Claude Code — v5.0

## Определение области проверки

Проверь, добавил ли пользователь флаг `--include-global` к этому промпту.
- **По умолчанию (только проект)**: проверяй `.` + `.claude/` в текущей директории.
- **С флагом `--include-global`**: также проверяй `~/.claude/` и `~/.claude.json`.

Установи SCOPE соответствующим образом. Во всех bash-блоках ниже указано, какие пути применяются в зависимости от области проверки.

## Инструкции

НЕ изменяй никакие файлы. НЕ вноси никаких правок. Только аудит и отчёт.

Используй эффективные bash-команды для первичного сбора данных. Читай содержимое файлов только тогда, когда это необходимо для выставления оценки.

---

## Фаза 1 — Инвентаризация (30 секунд, только bash)

Выполни этот единый блок, чтобы собрать все структурные данные за один раз:

```bash
bash -c '
echo "=== SCOPE ==="
SCOPE="project"
[[ "$*" == *"--include-global"* ]] && SCOPE="project+global"
echo "Audit scope: $SCOPE"
CURRENT_DIR=$(pwd)

echo ""
echo "=== CONFIG FILES ==="
# Project
for f in ./CLAUDE.md ./.claude/CLAUDE.md ./.claude/settings.json ./.claude/settings.local.json; do
  [ -f "$f" ] && echo "✅ $f" || echo "❌ $f"
done
# Global (always check for context, even in project-only scope)
[ -f ~/.claude/CLAUDE.md ] && echo "✅ ~/.claude/CLAUDE.md (global)" || echo "❌ ~/.claude/CLAUDE.md (global)"
[ -f ~/.claude.json ] && echo "✅ ~/.claude.json (MCP config)" || echo "❌ ~/.claude.json"

echo ""
echo "=== FOLDER STRUCTURE ==="
for d in agents commands skills hooks rules styles; do
  if [ -d "./.claude/$d" ]; then
    count=$(find "./.claude/$d" -maxdepth 2 -type f | wc -l | tr -d " ")
    echo "✅ .claude/$d/ ($count files)"
  else
    echo "❌ .claude/$d/"
  fi
done

echo ""
echo "=== TECH STACK ==="
[ -f package.json ] && grep -o '"name": *"[^"]*"' package.json | head -1 | sed "s/\"name\": /nodejs: /"
[ -f pyproject.toml ] && grep "^name" pyproject.toml | head -1 | sed "s/name/python:/"
[ -f requirements.txt ] && echo "python: requirements.txt"
[ -f go.mod ] && head -1 go.mod | sed "s/module /go: /"
[ -f Cargo.toml ] && grep "^name" Cargo.toml | head -1 | sed "s/name/rust:/"
[ -f composer.json ] && echo "php: detected"
[ -f Gemfile ] && echo "ruby: detected"

echo ""
echo "=== MCP SERVERS ==="
if command -v jq &>/dev/null && [ -f ~/.claude.json ]; then
  MCP=$(jq -r --arg p "$CURRENT_DIR" '.projects[$p].mcpServers // {} | keys[]' ~/.claude.json 2>/dev/null)
  [ -n "$MCP" ] && echo "$MCP" | sed "s/^/  /" || echo "  (none for this project)"
  DB_MCP=$(echo "$MCP" | grep -iE "postgres|neon|supabase|mysql|database" || true)
  [ -n "$DB_MCP" ] && echo "  ⚠️  DB MCPs detected: $DB_MCP (verify not production)"
else
  echo "  (jq not installed or ~/.claude.json absent)"
fi

echo ""
echo "=== RULES INVENTORY ==="
RULES_DIR="./.claude/rules"
if [ -d "$RULES_DIR" ]; then
  count=$(find "$RULES_DIR" -name "*.md" | wc -l | tr -d " ")
  size=$(find "$RULES_DIR" -name "*.md" | xargs wc -c 2>/dev/null | tail -1 | awk "{print \$1}")
  echo "  $count rules files, ~$size total chars"
  echo "  Top 3 by size:"
  find "$RULES_DIR" -name "*.md" | xargs wc -c 2>/dev/null | sort -rn | head -4 | grep -v "total" | awk "{print \"    \" \$0}"
  with_paths=$(grep -rl "^paths:" "$RULES_DIR"/*.md 2>/dev/null | wc -l | tr -d " ")
  always_on=$(( count - with_paths ))
  echo "  path-scoped: $with_paths | always-on: $always_on"
else
  echo "  No .claude/rules/ directory"
fi

echo ""
echo "=== AUDIT SKILLS AVAILABLE ==="
for skill in token-audit eval-rules eval-skills audit-agents-skills; do
  found=false
  [ -f "$HOME/.claude/skills/$skill/SKILL.md" ] && found=true
  [ -f ".claude/skills/$skill/SKILL.md" ] && found=true
  $found && echo "  ✅ /$skill" || echo "  ❌ /$skill (fallback mode)"
done
for cmd in security-check security-audit; do
  found=false
  [ -f "$HOME/.claude/commands/$cmd.md" ] && found=true
  [ -f ".claude/commands/$cmd.md" ] && found=true
  [ -f "$HOME/.claude/skills/$cmd/SKILL.md" ] && found=true
  [ -f ".claude/skills/$cmd/SKILL.md" ] && found=true
  $found && echo "  ✅ /$cmd" || echo "  ❌ /$cmd (fallback mode)"
done

echo ""
echo "=== CACHE BUG INDICATORS ==="
grep -rl "disableSkillShellExecution\|--resume" .claude/ ~/.claude/ 2>/dev/null | head -3 | sed "s/^/  /" || echo "  No cache bug workarounds found"
' "$@"
```

Сохрани весь этот вывод. Используй его для оценки всех измерений ниже.

---

## Фаза 2 — Аудит по измерениям

Оцени каждое измерение. Для измерений с делегируемым скиллом проверь, доступен ли этот скилл (по выводу фазы 1). Если ✅: вызови скилл и используй его вывод для выставления оценки. Если ❌: выполни встроенный резервный bash-скрипт и примени упрощённую эвристику.

### Измерение 1 — Память и контекст (20 баллов)

**Полный аудит** (если доступен `/token-audit`):
Вызови: `/token-audit`
Используй вывод Token Audit:
- Фиксированный контекст <20K токенов → 18–20 баллов
- 20–40K токенов → 12–17 баллов
- 40–60K токенов → 6–11 баллов
- >60K токенов → 0–5 баллов. Вычти 2 балла, если отсутствует CLAUDE.md, и 3 балла, если отсутствует глобальный CLAUDE.md.

**Резервный режим** (если `/token-audit` не установлен):

```bash
GLOBAL=$(cat ~/.claude/CLAUDE.md ~/.claude/*.md 2>/dev/null | wc -c || echo 0)
PROJECT=$(wc -c < CLAUDE.md 2>/dev/null || echo 0)
RULES=$(find .claude/rules -name "*.md" 2>/dev/null | xargs cat 2>/dev/null | wc -c || echo 0)
TOTAL=$(( (GLOBAL + PROJECT + RULES) / 4 + 7500 ))
echo "Estimated fixed context: ~$TOTAL tokens (~$(( TOTAL * 100 / 200000 ))% of 200K window)"
```

Оценка в резервном режиме (максимум 14 баллов):
- Глобальный CLAUDE.md существует и не пуст: 3 балла
- Проектный CLAUDE.md существует: 3 балла
- Разумное количество правил (<15 файлов): 2 балла
- Оценка токенов <20K: 6 баллов | 20–40K: 3 балла | >40K: 0 баллов

### Измерение 2 — Гигиена правил (10 баллов)

**Полный аудит** (если доступен `/eval-rules`):
Вызови: `/eval-rules`
Возьми средний балл по всем файлам правил (из 12 баллов на файл). Пропорционально пересчитай в шкалу до 10 баллов.

**Резервный режим** (если `/eval-rules` не установлен):

```bash
RULES_DIR=".claude/rules"
[ -d "$RULES_DIR" ] || { echo "No rules dir"; exit 0; }
total=$(find "$RULES_DIR" -name "*.md" | wc -l | tr -d " ")
with_front=$(grep -rl "^---" "$RULES_DIR"/*.md 2>/dev/null | wc -l | tr -d " ")
with_paths=$(grep -rl "^paths:" "$RULES_DIR"/*.md 2>/dev/null | wc -l | tr -d " ")
valid_patterns=0
for f in "$RULES_DIR"/*.md; do
  pattern=$(grep -A1 "^paths:" "$f" 2>/dev/null | grep "^\s*-" | head -1 | sed "s/.*- //;s/['\"]//g")
  [ -n "$pattern" ] && ls $pattern 2>/dev/null | head -1 | grep -q . && valid_patterns=$(( valid_patterns + 1 ))
done
echo "Total: $total | With frontmatter: $with_front | With paths: $with_paths | Valid patterns: $valid_patterns"
```

Оценка в резервном режиме (максимум 8 баллов):
- Директория правил существует: 1 балл
- Все файлы содержат YAML frontmatter: 2 балла
- Не менее половины содержат поле `paths:`: 3 балла
- Ни один файл не превышает 150 строк (проверить через `wc -l`): 2 балла

### Измерение 3 — Качество скиллов (10 баллов)

**Полный аудит** (если доступен `/eval-skills`):
Вызови: `/eval-skills`
Возьми средний балл по всем файлам скиллов (из 14 баллов на файл). Пропорционально пересчитай в шкалу до 10 баллов.

**Резервный режим** (если `/eval-skills` не установлен):

```bash
SKILLS_DIR=".claude/skills"
[ -d "$SKILLS_DIR" ] || { echo "No skills dir (0 pts)"; exit 0; }
total=$(find "$SKILLS_DIR" -name "SKILL.md" | wc -l | tr -d " ")
with_effort=$(grep -rl "^effort:" "$SKILLS_DIR"/*/SKILL.md 2>/dev/null | wc -l | tr -d " ")
with_tools=$(grep -rl "^allowed-tools:" "$SKILLS_DIR"/*/SKILL.md 2>/dev/null | wc -l | tr -d " ")
with_desc=$(grep -rl "^description:" "$SKILLS_DIR"/*/SKILL.md 2>/dev/null | wc -l | tr -d " ")
echo "Skills: $total | effort field: $with_effort | allowed-tools: $with_tools | description: $with_desc"
```

Оценка в резервном режиме (максимум 8 баллов):
- Директория скиллов существует: 1 балл
- Все SKILL.md содержат поле `description:`: 2 балла
- Все SKILL.md содержат поле `effort:`: 3 балла
- Все SKILL.md содержат поле `allowed-tools:`: 2 балла

### Измерение 4 — Качество агентов/команд (10 баллов)

**Полный аудит** (если доступен `/audit-agents-skills`):
Вызови: `/audit-agents-skills`
Возьми итоговую оценку из его отчёта (балл/100). Умножь на 0.10, чтобы получить балл по 10-балльной шкале.

**Резервный режим** (если `/audit-agents-skills` не установлен):

```bash
agents=$(find .claude/agents -name "*.md" 2>/dev/null | wc -l | tr -d " ")
commands=$(find .claude/commands -name "*.md" 2>/dev/null | wc -l | tr -d " ")
skills=$(find .claude/skills -name "SKILL.md" 2>/dev/null | wc -l | tr -d " ")
with_front=$(find .claude/agents .claude/commands .claude/skills -name "*.md" 2>/dev/null | xargs grep -l "^---" 2>/dev/null | wc -l | tr -d " ")
with_desc=$(find .claude/agents .claude/commands .claude/skills -name "*.md" 2>/dev/null | xargs grep -l "^description:" 2>/dev/null | wc -l | tr -d " ")
# Check argument-hint on legacy commands still using $ARGUMENTS
uses_args=$(find .claude/commands -name "*.md" 2>/dev/null | xargs grep -l '\$ARGUMENTS' 2>/dev/null | wc -l | tr -d " ")
with_hint=$(find .claude/commands -name "*.md" 2>/dev/null | xargs grep -l 'argument-hint' 2>/dev/null | wc -l | tr -d " ")
echo "Agents: $agents | Commands: $commands | Skills: $skills | With frontmatter: $with_front | With description: $with_desc"
echo "Commands using \$ARGUMENTS: $uses_args | With argument-hint: $with_hint"
```

Оценка в резервном режиме (максимум 8 баллов):
- Есть агенты, команды или скиллы: 2 балла
- Все содержат YAML frontmatter: 2 балла
- Все содержат поле `description:`: 2 балла
- Поле `argument-hint:` присутствует во всех устаревших командах, использующих `$ARGUMENTS`: 2 балла

### Измерение 5 — Состояние безопасности (20 баллов)

**Полный аудит** (если доступен `/security-check`):
Вызови: `/security-check`
Преобразуй его находки в шкалу до 20 баллов:
- Нет критических находок: 18–20 баллов
- 1–2 находки средней критичности: 12–17 баллов
- 3+ находок или любая критическая находка: 0–11 баллов

**Резервный режим** (если `/security-check` не установлен):

```bash
# permissions.deny check
echo "=== Permissions Deny ==="
for setting in ".claude/settings.json" "~/.claude/settings.json"; do
  [ -f "$setting" ] && {
    echo "File: $setting"
    grep -E "\.env|\.pem|credentials|secrets" "$setting" 2>/dev/null && echo "  ✅ Sensitive patterns found" || echo "  ❌ No .env/.pem/credentials blocked"
    grep -i "sandbox\|failIfUnavailable" "$setting" 2>/dev/null | head -3 | sed "s/^/  /"
  }
done

echo ""
echo "=== Hooks ==="
if [ -d ".claude/hooks" ]; then
  hooks=$(ls .claude/hooks/*.sh 2>/dev/null | wc -l | tr -d " ")
  pretool=$(grep -rl "PreToolUse" .claude/hooks/ 2>/dev/null | wc -l | tr -d " ")
  echo "  Hooks: $hooks | PreToolUse: $pretool"
else
  echo "  ❌ No hooks directory"
fi

echo ""
echo "=== Dangerous Patterns ==="
# Check for hardcoded tokens/keys in config
grep -rn "sk-\|ghp_\|xox[baprs]-\|AKIA" .claude/ CLAUDE.md 2>/dev/null | grep -v "example\|sample\|template" | head -5 || echo "  No obvious secrets found"
```

Оценка в резервном режиме (максимум 17 баллов):
- Файлы `.env*` заблокированы в `permissions.deny`: 4 балла
- Файлы `*.pem` и `credentials*` также заблокированы: 3 балла
- Существует хотя бы один хук `PreToolUse`: 4 балла
- Настроена песочница (`failIfUnavailable`): 3 балла
- В конфигурации нет захардкоженных секретов: 3 балла

### Измерение 6 — Экосистема MCP (10 баллов)

Только встроенный bash (отдельного скилла для этого измерения нет):

```bash
CURRENT_DIR=$(pwd)
echo "=== MCP Servers for this project ==="
if command -v jq &>/dev/null && [ -f ~/.claude.json ]; then
  jq -r --arg p "$CURRENT_DIR" '
    .projects[$p].mcpServers // {} | to_entries[] |
    "\(.key): \(.value.command // .value.url // "configured")"
  ' ~/.claude.json 2>/dev/null || echo "  No project-specific MCPs"

  echo ""
  echo "=== DB MCP Risk ==="
  jq -r --arg p "$CURRENT_DIR" '.projects[$p].mcpServers // {} | keys[]' ~/.claude.json 2>/dev/null \
    | grep -iE "postgres|neon|supabase|mysql|database|mongo" \
    | sed "s/^/  ⚠️  /" || echo "  No DB MCPs found"

  echo ""
  echo "=== Guide MCP ==="
  jq -r --arg p "$CURRENT_DIR" '.projects[$p].mcpServers // {} | keys[]' ~/.claude.json 2>/dev/null \
    | grep -iE "claude-code-ultimate-guide|ccguide" \
    | sed "s/^/  ✅ /" || echo "  ❌ Guide MCP not installed"
else
  echo "  (install jq for MCP analysis)"
fi
```

Оценка (максимум 10 баллов):
- Настроен хотя бы 1 MCP: 3 балла
- Присутствует MCP для документации (Context7 или аналогичный): 2 балла
- Отсутствует MCP для БД, либо MCP для БД явно ограничен средами dev/staging: 3 балла
- Установлен Guide MCP: 2 балла

### Измерение 7 — Команды рабочих процессов (10 баллов)

```bash
echo "=== Core Workflow Skills/Commands ==="
for cmd in investigate qa canary land-and-deploy review-pr; do
  found=false
  [ -f ".claude/commands/$cmd.md" ] && found=true
  [ -f "$HOME/.claude/commands/$cmd.md" ] && found=true
  [ -f ".claude/skills/$cmd/SKILL.md" ] && found=true
  [ -f "$HOME/.claude/skills/$cmd/SKILL.md" ] && found=true
  $found && echo "  ✅ /$cmd" || echo "  ❌ /$cmd"
done

echo ""
echo "=== Additional Debug/Deploy Skills/Commands ==="
for cmd in ship commit release-notes diagnose; do
  found=false
  [ -f ".claude/commands/$cmd.md" ] && found=true
  [ -f "$HOME/.claude/commands/$cmd.md" ] && found=true
  [ -f ".claude/skills/$cmd/SKILL.md" ] && found=true
  [ -f "$HOME/.claude/skills/$cmd/SKILL.md" ] && found=true
  $found && echo "  ✅ /$cmd" || echo "  ❌ /$cmd"
done
```

Оценка: по 2 балла за каждую присутствующую базовую команду (`/investigate`, `/qa`, `/canary`, `/land-and-deploy`, `/review-pr`). Максимум 10 баллов.

### Измерение 8 — Актуальность и лучшие практики (10 баллов)

```bash
echo "=== Deprecated Model References ==="
grep -rn "claude-3-haiku\|gpt-3.5\|claude-2\b\|claude-instant\|claude-3-5-sonnet\b" \
  .claude/ CLAUDE.md ~/.claude/CLAUDE.md 2>/dev/null | grep -v ".git" | head -8 \
  || echo "  No deprecated model names found"

echo ""
echo "=== Config Freshness ==="
git log --oneline -1 --format="  Last commit: %ar (%h)" 2>/dev/null || echo "  (not a git repo)"

echo ""
echo "=== Cache Bug Workarounds ==="
# Bug 2 HIGH: --resume causes 87-118K token re-announcement
grep -rn "disableSkillShellExecution" ~/.claude/settings.json .claude/settings.json 2>/dev/null \
  | sed "s/^/  /" || echo "  disableSkillShellExecution: not set"

echo ""
echo "=== argument-hint Coverage (legacy commands) ==="
missing=0
for f in $(find .claude/commands -name "*.md" 2>/dev/null); do
  grep -q '\$ARGUMENTS' "$f" && ! grep -q "argument-hint" "$f" && {
    echo "  ⚠️  Missing argument-hint: $f"
    missing=$(( missing + 1 ))
  }
done
[ $missing -eq 0 ] && echo "  ✅ All commands using \$ARGUMENTS have argument-hint (skills use effort: field instead)"

echo ""
echo "=== Hook Profiles (env vars) ==="
grep -rn "CLAUDE_HOOK_PROFILE\|HOOK_PROFILE" .claude/ CLAUDE.md 2>/dev/null | head -3 | sed "s/^/  /" || echo "  No hook profiles configured"
```

Оценка (максимум 10 баллов):
- Нет упоминаний устаревших названий моделей: 3 балла
- Активность в Git за последние 90 дней (или это не git-репозиторий): 2 балла
- Задано `disableSkillShellExecution: false` ИЛИ паттерн `--resume` не используется: 3 балла
- Все команды, использующие `$ARGUMENTS`, имеют поле `argument-hint:`: 2 балла

---

## Фаза 3 — Единый отчёт

Сформируй отчёт строго в этой структуре:

### Краткое резюме

Укажи:
- **Итоговый балл**: X/100
- **Уровень зрелости**: Начальный (<40) | Развивающийся (40–59) | Устоявшийся (60–79) | Оптимизированный (80+)
- **Обнаруженный стек**: [из фазы 1]
- **Топ-3 быстрых улучшения**: пробелы с наибольшей отдачей, каждый из которых можно исправить менее чем за 15 минут
- **Топ-3 критических пробела**: отсутствующие элементы с наивысшей степенью критичности

### Сводная таблица по измерениям

| # | Измерение | Балл | Макс. | Статус | Ключевая находка |
|---|-----------|-------|-----|--------|-------------|
| 1 | Память и контекст | X | 20 | ✅/⚠️/❌ | вывод в одну строку |
| 2 | Гигиена правил | X | 10 | ✅/⚠️/❌ | вывод в одну строку |
| 3 | Качество скиллов | X | 10 | ✅/⚠️/❌ | вывод в одну строку |
| 4 | Качество агентов/команд | X | 10 | ✅/⚠️/❌ | вывод в одну строку |
| 5 | Состояние безопасности | X | 20 | ✅/⚠️/❌ | вывод в одну строку |
| 6 | Экосистема MCP | X | 10 | ✅/⚠️/❌ | вывод в одну строку |
| 7 | Команды рабочих процессов | X | 10 | ✅/⚠️/❌ | вывод в одну строку |
| 8 | Актуальность и лучшие практики | X | 10 | ✅/⚠️/❌ | вывод в одну строку |
| | **ИТОГО** | **X** | **100** | | |

Пороги статусов: ✅ ≥80% от максимума, ⚠️ 50–79%, ❌ <50%.

### Детальные находки

Сгруппируй по измерениям. Для каждого пробела (❌ или ⚠️):

```
**[Измерение N — Название]**
Пробел: [чего не хватает или что настроено неоптимально]
Влияние: [что ломается или деградирует без этого]
Исправление: [конкретное действие с указанием пути к файлу]
```

### Шаблоны под конкретный стек

Предложи не более 3 шаблонов, выбранных для наиболее значимых пробелов обнаруженного стека. Включи только путь к файлу + стартовое содержимое. Не дублируй уже существующее содержимое.

### Углубление аудита

Перечисли, какие скиллы аудита не установлены и какие возможности они откроют:

```
Неустановленные скиллы — установите для более глубокого анализа:

# token-audit (Измерение 1 — добавляет классификацию правил, анализ накладных расходов хуков)
mkdir -p ~/.claude/skills/token-audit
curl -sL https://raw.githubusercontent.com/FlorianBruniaux/claude-code-ultimate-guide/main/examples/skills/token-audit/SKILL.md \
  > ~/.claude/skills/token-audit/SKILL.md

# eval-rules (Измерение 2 — добавляет валидацию glob-паттернов, интерактивное ревью)
mkdir -p ~/.claude/skills/eval-rules
curl -sL https://raw.githubusercontent.com/FlorianBruniaux/claude-code-ultimate-guide/main/examples/skills/eval-rules/SKILL.md \
  > ~/.claude/skills/eval-rules/SKILL.md

# eval-skills (Измерение 3 — добавляет 14-балльную оценку для каждого скилла)
mkdir -p ~/.claude/skills/eval-skills
curl -sL https://raw.githubusercontent.com/FlorianBruniaux/claude-code-ultimate-guide/main/examples/skills/eval-skills/SKILL.md \
  > ~/.claude/skills/eval-skills/SKILL.md

# audit-agents-skills (Измерение 4 — добавляет оценки A-F, сравнительный анализ)
mkdir -p ~/.claude/skills/audit-agents-skills
curl -sL https://raw.githubusercontent.com/FlorianBruniaux/claude-code-ultimate-guide/main/examples/skills/audit-agents-skills/SKILL.md \
  > ~/.claude/skills/audit-agents-skills/SKILL.md

# security-check (Измерение 5 — сканирование по threat-db, 55 CVE, 24 техникам)
mkdir -p ~/.claude/skills/security-check
curl -sL https://raw.githubusercontent.com/FlorianBruniaux/claude-code-ultimate-guide/main/examples/skills/security-check/SKILL.md \
  > ~/.claude/skills/security-check/SKILL.md

# Альтернатива для измерения 1 — context-evaluator.ai
# LLM-нативный аудит без установки: 17 ИИ-оценщиков для CLAUDE.md/AGENTS.md,
# автоматические исправления в формате .patch. Дополняет /token-audit более глубоким анализом правил.
# Сайт: https://context-evaluator.ai
```

---

## Фаза 4 — Запрос подтверждения

После представления отчёта спроси:

«Реализовать топ-3 быстрых улучшения? Ответьте:
- **yes** → я реализую все три
- **high** → только критические пробелы (измерения 5 и 1, если они отмечены ❌)
- **1, 3** → конкретные пункты по номерам из списка находок
- **none** → оставить отчёт без изменений»

Дождись явного ответа пользователя, прежде чем предпринимать какие-либо действия.
````

---

## 5. Чего ожидать

### Пример краткого резюме (Executive Summary)

```
## Краткое резюме (Executive Summary)

Итоговая оценка: 52/100 — Развивающийся (Growing)

Обнаруженный стек: TypeScript + Next.js + Prisma

Топ-3 быстрых улучшения (Quick Wins):
- Добавить permissions.deny для .env* (15 мин) → закрывает критический пробел по измерению 5
- Установить команды /investigate и /qa (5 мин) → +4 балла по измерению 7
- Добавить frontmatter paths: в 3 постоянно загружаемых правила (20 мин) → сокращает фиксированный контекст на ~3K токенов

Топ-3 критических пробела:
1. ❌ Безопасность — нет permissions.deny, нет хуков PreToolUse (0/20)
2. ⚠️ Память — отсутствует проектный CLAUDE.md, глобальный занимает 22K токенов (8/20)
3. ❌ Рабочий процесс — отсутствуют 3 из 5 основных команд (4/10)
```

### Пример оценочной таблицы по измерениям

| # | Измерение | Балл | Макс. | Статус | Ключевая находка |
|---|-----------|------|-------|--------|------------------|
| 1 | Память и контекст (Memory & Context) | 8 | 20 | ⚠️ | 22K фиксированных токенов, нет проектного CLAUDE.md |
| 2 | Гигиена правил (Rules Hygiene) | 7 | 10 | ⚠️ | 4 правила, ни в одном нет поля paths: |
| 3 | Качество скиллов (Skills Quality) | 8 | 10 | ✅ | 3 скилла, у всех указаны effort + allowed-tools |
| 4 | Качество агентов и команд (Agents/Commands Quality) | 6 | 10 | ⚠️ | 8 команд, у 2 отсутствует argument-hint |
| 5 | Состояние безопасности (Security Posture) | 0 | 20 | ❌ | Нет правил deny, нет хуков |
| 6 | Экосистема MCP (MCP Ecosystem) | 7 | 10 | ✅ | Настроены Context7 + Sequential |
| 7 | Команды рабочего процесса (Workflow Commands) | 4 | 10 | ⚠️ | /investigate ✅ /qa ❌ /canary ❌ |
| 8 | Актуальность и лучшие практики (Freshness & Best Practices) | 12 | 10 | — | ограничено максимумом |
| | **ИТОГО** | **52** | **100** | ⚠️ | |

---

## 6. Как интерпретировать результаты

### Глоссарий

| Термин | Определение |
|--------|-------------|
| **Файлы памяти (Memory Files)** | Файлы CLAUDE.md, обеспечивающие постоянный контекст для Claude между сессиями |
| **Бюджет контекста (Context Budget)** | Суммарный постоянный расход токенов до начала любой задачи. Пороги: зелёный <20K, жёлтый 20–40K, красный >40K |
| **Правила (автозагружаемые / Rules)** | Файлы `.claude/rules/*.md`, загружаемые при каждом запуске сессии. Файлы с `paths:` загружаются только при чтении подходящего файла |
| **Frontmatter paths:** | Поле в YAML-заголовке правила, ограничивающее область его действия конкретными шаблонами файлов — снижает постоянный расход токенов |
| **Скилл оценки (Eval Skill)** | Специализированный скилл для аудита одной области: `eval-skills`, `eval-rules`, `token-audit`, `audit-agents-skills` |
| **Единый источник истины (Single Source of Truth)** | Паттерн, при котором соглашения документируются в одном месте и подключаются через `@path` |
| **Tool SEO** | Написание описаний агентов и команд так, чтобы Claude автоматически выбирал нужный инструмент |
| **MCP-серверы (MCP Servers)** | Model Context Protocol — внешние инструменты, расширяющие возможности Claude. Конфигурация хранится в `~/.claude.json` для каждого проекта |
| **Профили хуков (Hook Profiles)** | Уровни безопасности minimal/standard/strict для хуков, переключаемые через переменную окружения (добавлено в v3.38.0) |
| **PreToolUse** | Хук, срабатывающий ДО того, как Claude выполнит инструмент — используется для проверок безопасности и порогов подтверждения (approval gates) |
| **Поле effort:** | Поле в frontmatter скилла, задающее сигнал сложности low/medium/high — используется Claude для выделения бюджета на рассуждения (thinking budget) |
| **argument-hint** | Поле frontmatter, отображающее текст-подсказку в меню слэш-команд для команд, использующих `$ARGUMENTS` |
| **База угроз (Threat Database)** | `examples/commands/resources/threat-db.yaml` — версионированные CVE, техники атак, записи IOC и минимальные безопасные версии |
| **Баг кэша #40524 (Cache Bug #40524)** | Баг 2 (HIGH): `--resume` вызывает полное повторное объявление контекста (87–118K токенов пересобирается при каждом возобновлении) |
| **Дрейф области изменений (Scope Drift)** | Ситуация, когда PR изменяет файлы за пределами заявленного плана. Выявляется сравнением `~/.claude/plans/` с `git diff --stat` |
| **Эвристика Fix-First (Fix-First Heuristic)** | Паттерн ревью: автоматическое исправление механических проблем и запрос решения человека по вопросам безопасности и дизайна |
| **Граница доверия к выводу LLM (LLM Output Trust Boundary)** | Категория ревью для сгенерированных ИИ значений, записываемых в БД без валидации формата |
| **managed-settings.d/** | Корпоративная drop-in директория для правил управления (governance), переопределяющих пользовательские настройки (добавлено в v2.1.83) |
| **Routines** | Облачные задачи по расписанию с 3 типами триггеров: расписание, API, события GitHub (запущены в апреле 2026 года) |
| **Зоны контекста (Context Zones)** | <70% — оптимально, 75% — триггер автокомпакции, 85% — рекомендуется передача контекста (handoff) |
| **Песочница (Sandbox)** | Изоляция на уровне ОС (контейнер Docker или нативная изоляция на уровне процессов). Настраивается в settings.json |
| **Железный закон (Iron Law)** | Принцип отладки: никаких исправлений без предварительного поиска первопричины. См. `/investigate` |

### Пороги оценок

| Баллы | Уровень | Что это означает |
|-------|---------|------------------|
| 80–100 | Оптимизированный (Optimized) | Конфигурация надёжна. Сосредоточьтесь на актуальности (Freshness) и пограничных случаях |
| 60–79 | Устоявшийся (Established) | Хорошая база. Закройте пробелы в измерениях со статусом ⚠️ |
| 40–59 | Развивающийся (Growing) | Основные элементы есть, но остаётся ряд пробелов. Начните с быстрых улучшений (Quick Wins) |
| <40 | Начальный (Starter) | Начните с измерения 5 (Безопасность) и измерения 1 (Память) |

### Значки статусов

| Значок | Значение |
|--------|----------|
| ✅ | ≥80% от максимума баллов по этому измерению |
| ⚠️ | 50–79% от максимума баллов |
| ❌ | <50% от максимума баллов |

---

## 7. Частые проблемы

### «Скиллы аудита не установлены» ("Audit skills not installed")

**Причина**: специализированные скиллы являются опциональными и по умолчанию не доступны глобально.

**Что происходит**: промпт запускается в резервном режиме (fallback) для этого измерения. Максимальные баллы ограничиваются ниже (8 баллов вместо 10 для некоторых измерений). Результаты всё равно практичны и применимы, просто менее детализированы.

**Решение**: используйте команды установки из раздела «Deepen Your Audit» («Углублённый аудит») в отчёте. Установка каждого скилла занимает ~1 минуту и сразу повышает точность последующих аудитов.

### «Claude не нашёл мои файлы» ("Claude didn't find my files")

**Причина**: неверная рабочая директория или различия в путях между платформами.

**Решение**:
- Убедитесь, что запускаете `claude` из корня проекта
- В Windows используются пути `%USERPROFILE%\.claude\`, а не `~/.claude/`

### «Оценка кажется неточной» ("Score seems off")

**Причина**: оценка в резервном режиме (fallback) упрощена — она не может проверить валидность glob-шаблонов, выполнить 14-балльную проверку скиллов или просканировать конфигурацию по базе угроз.

**Решение**: установите соответствующие скиллы аудита (см. «Deepen Your Audit»). Запустите аудит повторно, чтобы получить точные оценки по измерениям.

### «Слишком много рекомендаций» ("Too many recommendations")

**Причина**: первый аудит проекта без конфигурации Claude Code.

**Решение**: возьмите быстрые улучшения (Quick Wins) из краткого резюме (Executive Summary). Реализуйте эти три пункта. Проведите аудит повторно. Улучшайте конфигурацию постепенно.

### «Claude внёс изменения без спроса» ("Claude made changes without asking")

**Причина**: фаза 4 (валидация) не была достигнута или была пропущена.

**Решение**: убедитесь, что вы скопировали полный промпт, включая фазу 4. Перед вставкой промпта переключитесь в Plan Mode (`Shift+Tab` дважды) для дополнительной безопасности.

---

## 8. Связанные ресурсы

**Дополнительные инструменты аудита** (для более глубокого анализа отдельных измерений):

| Инструмент | Измерение | Установка |
|------------|-----------|-----------|
| `/token-audit` | Память и контекст (Memory & Context) | `mkdir -p ~/.claude/skills/token-audit && curl -sL .../examples/skills/token-audit/SKILL.md > ...` |
| `/eval-rules` | Гигиена правил (Rules Hygiene) | Тот же шаблон |
| `/eval-skills` | Качество скиллов (Skills Quality) | Тот же шаблон |
| `/audit-agents-skills` | Агенты и команды (Agents/Commands) | Тот же шаблон |
| `/security-check` | Состояние безопасности (быстрая проверка, ~30 с) | `mkdir -p ~/.claude/skills/security-check && curl -sL ...` |
| `/security-audit` | Состояние безопасности (полный аудит, 2–5 мин, оценка /100) | Тот же шаблон |
| [`tools/context-audit-prompt.md`](context-audit-prompt.md) | Глубокий разбор инженерии контекста | Автономный промпт, установка не требуется |
| [`tools/onboarding-prompt.md`](onboarding-prompt.md) | Настройка с нуля | Автономный промпт, установка не требуется |
| [context-evaluator.ai](https://context-evaluator.ai) | Память и контекст (альтернатива) — LLM-native, 17 оценщиков, авто-`.patch` | Веб-инструмент без установки |

**Справочная документация**:
- [Полное руководство по Claude Code](../guide/ultimate-guide.md) — полный справочник
- [Шпаргалка](../guide/cheatsheet.md) — краткий справочник на каждый день
- [Усиление безопасности (Security Hardening)](../guide/security/security-hardening.md) — паттерны безопасности для продакшена
- [Инженерия контекста](../guide/core/architecture.md) — стратегии управления бюджетом токенов
- [Официальная документация Claude Code](https://docs.anthropic.com/en/docs/claude-code) — документация Anthropic

**Для интеграции в CI/CD** (вывод в JSON, пакетный режим): [`examples/scripts/audit-scan.sh`](../examples/scripts/audit-scan.sh)

---

*Версия 5.2 (руководство v3.41.0+) | v5.2: обнаружение скиллов обновлено под унификацию скиллов и команд в CC 2.1.3 — bash-скрипты для измерений 4/7/8 теперь проверяют и `.claude/skills/`, и `.claude/commands/`; путь установки security-check исправлен на канонический SKILL.md. v5.1: добавлен context-evaluator.ai. v5.0: переработан из чек-листа в оркестратор с 8 взвешенными измерениями.*
