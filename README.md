# Полное руководство по Claude Code (Claude Code Ultimate Guide)

> [!NOTE]
> **Русская редакция:** Это полный неофициальный перевод на русский язык — форк репозитория [FlorianBruniaux/claude-code-ultimate-guide](https://github.com/FlorianBruniaux/claude-code-ultimate-guide) (версия `v3.46.0`, базовый коммит `3fd3e805`). Автор оригинала — Florian Bruniaux. Лицензия руководства — [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/).

<table>
  <tr>
    <td width="64">
      <a href="https://www.florian.bruniaux.com/about/?utm_source=github&amp;utm_medium=readme&amp;utm_campaign=claude-code-ultimate-guide"><img src="https://cc.bruniaux.com/author.png" width="56" height="56" alt="Florian Bruniaux" /></a>
    </td>
    <td>
      <strong><a href="https://www.florian.bruniaux.com/about/?utm_source=github&amp;utm_medium=readme&amp;utm_campaign=claude-code-ultimate-guide">Florian BRUNIAUX</a></strong> &middot; Практикующий Fractional Chief AI Officer (CAIO)<br />
      Около 15 лет в разработке ПО, из них 8–10 лет в техническом лидерстве &middot; <a href="https://www.florian.bruniaux.com/blog/?utm_source=github&amp;utm_medium=readme&amp;utm_campaign=claude-code-ultimate-guide">Блог &#8599;</a> &middot; <a href="https://www.florian.bruniaux.com/projects/?utm_source=github&amp;utm_medium=readme&amp;utm_campaign=claude-code-ultimate-guide">Проекты &#8599;</a>
      <br /><strong><a href="https://clauders.com/leaders/florian-bruniaux/">Официальный амбассадор сообщества Claude &middot; Париж &#8599;</a></strong>
    </td>
  </tr>
</table>

<p align="center">
  <a href="https://cc.bruniaux.com/"><img src="https://img.shields.io/badge/Interactive_Guide-cc.bruniaux.com-ff6b35?style=for-the-badge" alt="Открыть интерактивное руководство" /></a>
</p>

<p align="center">
  <a href="./CHANGELOG.md"><img src="https://img.shields.io/badge/Guide-v3.46.0-brightgreen?style=flat-square" alt="Версия руководства 3.46.0" /></a>
  <a href="./CHANGELOG.md"><img src="https://img.shields.io/badge/Updated-Nov_22,_2026_·_v3.46.0-brightgreen?style=flat-square" alt="Обновлено 17 октября 2026, версия руководства 3.46.0" /></a>
  <a href="https://creativecommons.org/licenses/by-sa/4.0/"><img src="https://img.shields.io/badge/Guide-CC_BY--SA_4.0-blue?style=flat-square" alt="Лицензия руководства: CC BY-SA 4.0" /></a>
  <a href="https://cc.bruniaux.com/mcp/"><img src="https://img.shields.io/badge/MCP-npx_ready-blueviolet?style=flat-square" alt="MCP-сервер доступен через npx" /></a>
  <a href="https://deepwiki.com/FlorianBruniaux/claude-code-ultimate-guide"><img src="https://deepwiki.com/badge.svg" alt="Спросить DeepWiki" /></a>
</p>

Изучите Claude Code, научитесь строить надёжных агентов и безопасно масштабировать их применение. Сайт служит основным интерфейсом для чтения и навигации. В этом репозитории хранятся канонические исходники в Markdown, переиспользуемые файлы, машиночитаемые индексы и история изменений.

**С чего начать:** [выполнить первую задачу онлайн](https://cc.bruniaux.com/guide/ultimate-guide/01-quick-start/) · [открыть портал руководства](https://cc.bruniaux.com/guide/) · [посмотреть полную карту сайта](https://cc.bruniaux.com/sitemap/) · [читать исходник в Markdown](./guide/ultimate-guide.md)

## Выберите следующий шаг

Таблица ниже генерируется из [`machine-readable/navigation.json`](./machine-readable/navigation.json). Этот же контракт используется для публичной карты сайта, поэтому репозиторий и веб-сайт отражают единую модель навигации по задачам.

<!-- BEGIN GENERATED INTENT NAVIGATION -->
| Задача | Читать онлайн |
|---|---|
| **Старт** | [Портал руководства](https://cc.bruniaux.com/guide/) · [Быстрый старт](https://cc.bruniaux.com/guide/ultimate-guide/01-quick-start/) · [Маршруты обучения](https://cc.bruniaux.com/learning/) · [Краткий справочник](https://cc.bruniaux.com/cheatsheet/) · [AI-роли](https://cc.bruniaux.com/roles/) |
| **Разработка** | [Проектирование обвязки агента](https://cc.bruniaux.com/guide/agent-harness/) · [Проектирование циклов и графов](https://cc.bruniaux.com/guide/loop-graph-engineering/) · [Паттерны проектирования ИИ](https://cc.bruniaux.com/ai-design-patterns/) · [Инженерия контекста](https://cc.bruniaux.com/context-engineering/) · [Системы памяти](https://cc.bruniaux.com/memory-systems/) · [Рабочие процессы](https://cc.bruniaux.com/guide/workflows/) · [Методологии](https://cc.bruniaux.com/methodologies/) · [MCP или CLI?](https://cc.bruniaux.com/mcp-or-cli/) · [Примеры](https://cc.bruniaux.com/examples/) |
| **Масштабирование** | [Безопасность](https://cc.bruniaux.com/security/) · [Корпоративное управление](https://cc.bruniaux.com/guide/enterprise-governance/) · [Наблюдаемость](https://cc.bruniaux.com/guide/observability/) · [Командные метрики](https://cc.bruniaux.com/team-metrics/) · [Внедрение в команде](https://cc.bruniaux.com/guide/adoption-approaches/) · [AI FinOps](https://cc.bruniaux.com/finops/) · [Срез рынка LLM](https://cc.bruniaux.com/guide/llm-market-snapshot/) · [Стратегия подписок](https://cc.bruniaux.com/guide/subscription-strategy/) · [AI юнит-экономика](https://cc.bruniaux.com/guide/ai-unit-economics/) · [База знаний команды](https://cc.bruniaux.com/guide/team-knowledge-base/) · [API-шлюз](https://cc.bruniaux.com/guide/api-gateway/) |
| **Ресурсы** | [Центр ресурсов](https://cc.bruniaux.com/resources/) · [Загрузки](https://cc.bruniaux.com/downloads/) · [Шпаргалки](https://cc.bruniaux.com/cheatsheets/) · [Электронные книги](https://cc.bruniaux.com/whitepapers/) · [Диаграммы](https://cc.bruniaux.com/diagrams/) · [Экосистема](https://cc.bruniaux.com/ecosystem/) · [Сравнения](https://cc.bruniaux.com/compare/) · [Глоссарий](https://cc.bruniaux.com/guide/glossary/) · [FAQ](https://cc.bruniaux.com/faq/) · [MCP-сервер руководства](https://cc.bruniaux.com/mcp/) · [Связанные проекты](https://cc.bruniaux.com/projects/) |
| **Обновления** | [История изменений руководства](https://cc.bruniaux.com/changelog/) · [Релизы Claude Code](https://cc.bruniaux.com/releases/) · [RSS-лента](https://cc.bruniaux.com/rss.xml) |
<!-- END GENERATED INTENT NAVIGATION -->

## Зачем нужно это руководство

Официальная документация Claude Code объясняет устройство продукта. Это руководство связывает поведение продукта с инженерными решениями: что должно попадать в контекст, когда использовать агента вместо скилла (skill), как проверять сгенерированный результат и какие механизмы контроля важны при выходе за рамки одного разработчика.

| Потребность | С чего начать |
|---|---|
| Понять внутреннее устройство Claude Code | [Архитектура](./guide/core/architecture.md) и [Справочник инструментов](./guide/core/tools-reference.md) |
| Проектировать агентные системы | [Проектирование обвязки агента (agent harness)](./guide/core/agent-harness.md), [Проектирование циклов и графов](./guide/core/loop-graph-engineering.md) и [Паттерны проектирования ИИ](./guide/core/ai-design-patterns.md) |
| Выстроить процесс разработки с ИИ | [Методологии](./guide/core/methodologies.md) и [Руководства по рабочим процессам](./guide/workflows/) |
| Выстроить периметр безопасности | [Усиление безопасности](./guide/security/security-hardening.md) и [Изоляция в песочнице](./guide/security/sandbox-isolation.md) |
| Проверить понимание | [Тест знаний](https://cc.bruniaux.com/quiz/) и [Карточки-памятки](https://cc.bruniaux.com/cheatsheets/) |

Руководство делает упор на явные компромиссы и проверяемые процедуры. Там, где доказательная база неполна, соответствующая страница сохраняет эти ограничения, а не выдаёт один рабочий процесс за универсальный.

## Старт

### Установите Claude Code

Anthropic рекомендует нативный установщик, который обновляется автоматически:

```bash
# macOS, Linux, WSL
curl -fsSL https://claude.ai/install.sh | bash
```

```powershell
# Windows PowerShell
irm https://claude.ai/install.ps1 | iex
```

Альтернативы без автообновления: `brew install --cask claude-code`, `winget install Anthropic.ClaudeCode` или `npm install -g @anthropic-ai/claude-code` (Node.js 22+). Подробнее — на [официальной странице установки](https://code.claude.com/docs/en/setup).

Проверьте установку и пройдите аутентификацию:

```bash
claude --version
claude doctor
claude auth login
```

В главе [Быстрый старт](./guide/ultimate-guide.md#1-quick-start-day-1) описаны альтернативные способы установки, аутентификация, обновления, режимы прав доступа и типичные проблемы первого дня.

### Выполните первую задачу

Откройте небольшой репозиторий с чистым или понятным состоянием Git и запустите Claude Code:

```bash
cd your-project
claude
```

Дайте Claude ограниченный по области запрос с ожидаемым результатом и способом проверки:

```text
Объясни, как в этом проекте запускаются тесты. Файлы не изменяй.
Назови нужные команды и укажи файлы, в которых они определены.
```

Прежде чем просить Claude редактировать код, добавьте файл `CLAUDE.md` на уровне проекта с командами и ограничениями, которым Claude должен следовать:

```markdown
# Инструкции проекта

## Команды
- Тесты: `npm test`
- Линтер: `npm run lint`

## Границы
- Не редактируй сгенерированные файлы.
- Не меняй зависимости без согласования.
- Запускай релевантные тесты перед тем, как сообщить о завершении.
```

Переходите к разделу [Первый рабочий процесс](./guide/ultimate-guide.md#12-first-workflow) или воспользуйтесь [стартовыми шаблонами CLAUDE.md](./examples/claude-md/).

### Выберите маршрут обучения

| Ситуация | Рекомендуемый маршрут |
|---|---|
| Новичок в Claude Code | [Курс обучения из семи модулей](./guide/learning-path/README.md) |
| Уже пользуетесь CLI | [Базовые концепции](./guide/ultimate-guide.md#2-core-concepts), затем [Инженерия контекста](./guide/core/context-engineering.md) |
| Старший разработчик или техлид | [Методологии](./guide/core/methodologies.md), [Проектирование обвязки агента](./guide/core/agent-harness.md), затем [Безопасность в продакшене](./guide/security/production-safety.md) |
| Engineering Manager или CTO | [Подходы к внедрению](./guide/roles/adoption-approaches.md), [Командные метрики](./guide/ops/team-metrics.md), затем [Стратегия подписок](./guide/ops/subscription-strategy.md) |
| Специалист по безопасности или платформенный инженер | [Усиление безопасности](./guide/security/security-hardening.md), [Корпоративное управление](./guide/security/enterprise-governance.md), затем [Наблюдаемость](./guide/ops/observability.md) |
| Продакт-менеджер или дизайнер | [Руководство для продакт-менеджеров](./docs/for-product-managers.md) или [Воркфлоу Design-to-Code](./guide/workflows/design-to-code.md) |
| Специалист умственного труда (не разработчик) | [Руководство по Claude Cowork](https://github.com/FlorianBruniaux/claude-cowork-guide) |

Для персонального маршрута используйте онбординг-промпт из репозитория:

```bash
claude "Fetch and follow the onboarding instructions from: https://raw.githubusercontent.com/FlorianBruniaux/claude-code-ultimate-guide/main/tools/onboarding-prompt.md"
```

## Разработка

### Инженерия агентов

Агент — лишь один компонент более крупной системы. Окружающая его обвязка агента (харнесс) управляет контекстом, инструментами, правами доступа, состоянием, условиями остановки, восстановлением после сбоев и оценкой (eval).

| Ресурс | Какое решение поддерживает |
|---|---|
| [Проектирование обвязки агента](./guide/core/agent-harness.md) | Определить механизмы контроля, необходимые вокруг цикла агента |
| [Минимальная обвязка (The minimal harness)](https://www.florian.bruniaux.com/resources/minimal-harness/?utm_source=github&utm_medium=readme&utm_campaign=harness-minimal&utm_content=readme) | Разобрать три версии сервиса регистрации, чтобы найти ложное срабатывание. Интерактивный PDF по email. |
| [Проектирование циклов и графов](./guide/core/loop-graph-engineering.md) | Выбрать между ограниченными циклами обратной связи и явными графами рабочих процессов |
| [Паттерны проектирования ИИ](./guide/core/ai-design-patterns.md) | Объяснить архитектуру агента через знакомые разработчикам паттерны GoF, интеграционные паттерны и паттерны отказоустойчивости |
| [Карта обвязок агентов](./guide/ecosystem/agent-harness-landscape.md) | Разграничить рантаймы, оркестраторы, фреймворки, плоскости управления и вспомогательные инструменты |
| [Агентные инструменты](./guide/ecosystem/agentic-tools.md) | Сравнить выбранных кодинг-агентов и продукты оркестрации |
| [Оценка агентов](./guide/roles/agent-evaluation.md) | Проверять поведение, регрессии и результаты на уровне задач |
| [Глоссарий обвязок агентов](./guide/core/glossary.md) | Синхронизировать терминологию при проектировании и ревью |
| [Границы понятий в ИИ](./guide/core/ai-concept-boundaries.md) | Устранить семь распространённых источников путаницы с примерами из репозитория и проверочными вопросами |

### Контекст и память

Качество контекста влияет на каждый вызов инструмента и каждое решение. Начните с инструкций проекта, добавляйте специализированный контекст только тогда, когда этого требует повторяющаяся задача, и проверяйте, действительно ли дополнительный материал меняет поведение.

| Ресурс | Фокус |
|---|---|
| [Инженерия контекста](./guide/core/context-engineering.md) | Бюджет контекста, модульные инструкции, сборка и измерение |
| [Системы памяти](./guide/core/memory-systems.md) | Встроенная память, межсессионные системы, совместное использование в команде и риски хранения |
| [Инструменты инженерии контекста](./guide/ecosystem/context-engineering-tools.md) | Сжатие вывода, поиск и извлечение, шлюзы и инспекция контекста |
| [Аудит контекста](./tools/context-audit-prompt.md) | Оценка архитектуры контекста в проекте |
| [Командные инструкции для ИИ](./guide/workflows/team-ai-instructions.md) | Поддержка общих инструкций в команде разработки |

### Рабочие процессы

| Цель | Рабочий процесс |
|---|---|
| Разработка через тестирование | [TDD с Claude](./guide/workflows/tdd-with-claude.md) |
| Описать поведение до реализации | [Разработка от спецификации (Spec-First)](./guide/workflows/spec-first.md) |
| Отделить планирование от исполнения | [Разработка по плану (Plan-Driven)](./guide/workflows/plan-driven.md) |
| Сравнить независимых кандидатов | [Выбор лучшего из N (Best-of-N)](./guide/workflows/best-of-n.md) |
| Координировать нескольких агентов | [Команды агентов (Agent Teams)](./guide/workflows/agent-teams.md) |
| Строить ограниченные автономные циклы | [Агентные фабрики ПО](./guide/workflows/agentic-software-factories.md) |
| Системно проводить код-ревью | [Код-ревью](./guide/workflows/code-review.md) |
| Делать изменения агента удобными для ревью | [Проверяемые изменения агента](./guide/workflows/reviewable-agent-changes.md) |
| Подготовить вклад, который сможет проверить другая команда | [Open Source вклад с помощью ИИ](./guide/workflows/ai-assisted-open-source-contributions.md) |
| Разбираться в незнакомых репозиториях | [Воркфлоу исследования](./guide/workflows/exploration-workflow.md) |

[Просмотреть все рабочие процессы](./guide/workflows/): управление задачами, GitHub Actions, надёжность в продакшене, событийно-управляемые агенты, design-to-code, генерация PDF, поиск и командные инструкции.

### Выбирайте минимальный интерфейс

Claude Code умеет вызывать локальные команды, скиллы, агентов, хуки, плагины и MCP-серверы. Чем сложнее инфраструктура, тем больше настройка, права доступа, режимы отказов и затраты на сопровождение.

| Если задаче требуется | Предпочитайте |
|---|---|
| Детерминированная локальная команда | CLI или скрипт |
| Переиспользуемые инструкции и вспомогательные файлы | Скилл |
| Отдельный контекст и роль | Агент |
| Реакция на событие жизненного цикла | Хук |
| Упакованный набор возможностей | Плагин |
| Типизированный интерфейс к удалённому сервису | MCP-сервер |

Используйте [руководство по выбору между MCP и CLI](./guide/ecosystem/mcp-vs-cli.md) и [матрицу компромиссов](./guide/ultimate-guide.md#when-to-use-what), прежде чем добавлять ещё одну интеграцию.

## Масштабирование

### Надёжность и безопасность

| Область риска | Основной ресурс | Операционное дополнение |
|---|---|---|
| Права доступа и промпт-инъекции | [Усиление безопасности](./guide/security/security-hardening.md) | [Аудит прав доступа](./tools/permissions-audit-prompt.md) |
| Изоляция недоверенного исполнения | [Изоляция в песочнице (sandbox)](./guide/security/sandbox-isolation.md) | [Нативная песочница](./guide/security/sandbox-native.md) |
| Изменения в продакшене и откат | [Безопасность в продакшене](./guide/security/production-safety.md) | [Надёжность в продакшене](./guide/workflows/production-reliability.md) |
| Конфиденциальные данные и хранение | [Конфиденциальность данных](./guide/security/data-privacy.md) | [Корпоративное управление](./guide/security/enterprise-governance.md) |
| Активное тестирование авторизованных приложений | [Агентный пентестинг](./guide/security/agentic-pentesting.md) | [Оценка DarkMoon и Strix](./docs/resource-evaluations/darkmoon-strix-agentic-pentesting.md) |
| Цепочка поставок MCP и расширений | [Экосистема MCP](./guide/ecosystem/mcp-servers-ecosystem.md) | [База угроз](./examples/commands/resources/threat-db.yaml) |
| Готовность к делегированию | [Аудит полноты спецификации](./tools/spec-completeness-audit.md) | [Оценка агентов](./guide/roles/agent-evaluation.md) |

Утверждения по безопасности и количество угроз меняются по мере добавления или уточнения источников. Используйте связанные базу угроз и руководства как актуальный источник вместо копирования их чисел в документацию проекта.

### Оценка и эксплуатация

| Потребность | Ресурс |
|---|---|
| Отслеживать поведение агента и сбои | [Наблюдаемость (observability)](./guide/ops/observability.md) |
| Атрибутировать изменения, выполненные с ИИ | [Прослеживаемость (traceability) ИИ](./guide/ops/ai-traceability.md) |
| Оценивать результаты команды | [Командные метрики](./guide/ops/team-metrics.md) |
| Рассчитывать стоимость на уровне задачи | [AI юнит-экономика](./guide/ops/ai-unit-economics.md) |
| Эксплуатировать инфраструктурные рабочие процессы | [DevOps и SRE](./guide/ops/devops-sre.md) |
| Маршрутизировать управляемый API-трафик | [API-шлюзы](./guide/ops/api-gateway.md) |

Успешная структурная проверка доказывает лишь то, что она непосредственно проверяла. Поведение во время выполнения, приёмка задачи, границы безопасности и бизнес-результаты требуют отдельных доказательств.

### Организация и экономика

| Решение | Ресурс |
|---|---|
| Внедрить Claude Code в команде | [Подходы к внедрению](./guide/roles/adoption-approaches.md) |
| Определить уровни использования и согласования | [Корпоративное управление](./guide/security/enterprise-governance.md) |
| Сохранять командные знания | [База знаний команды](./guide/ecosystem/team-knowledge-base.md) |
| Сравнить подписки, API и шлюзы | [Стратегия подписок](./guide/ops/subscription-strategy.md) |
| Сравнить облачный и локальный инференс | [Локальный и облачный инференс](./guide/ecosystem/local-vs-cloud-inference.md) |
| Описать меняющиеся AI-роли | [AI-роли](./guide/roles/ai-roles.md) |

Страницы по экономике отделяют фактически наблюдаемые расходы от оценок и сценариев. Пересчитывайте их с учётом вашей нагрузки, критериев приёмки, трудозатрат на ревью и ограничений по рискам.

## Выберите формат под задачу

| Формат | Для чего использовать | Читать онлайн | Исходники или загрузка |
|---|---|---|---|
| Полный справочник | Глубокие разборы и связанные разделы | [Полное руководство](https://cc.bruniaux.com/guide/ultimate-guide/) | [Markdown](./guide/ultimate-guide.md) |
| Ежедневный справочник | Команды, горячие клавиши и проверки | [Краткий справочник](https://cc.bruniaux.com/cheatsheet/) | [Markdown](./guide/cheatsheet.md) |
| Пошаговый курс | Последовательные упражнения с фиксацией результатов | [Маршруты обучения](https://cc.bruniaux.com/learning/) | [Исходники курса](./guide/learning-path/) |
| Исполняемые материалы | Агенты, скиллы, хуки, воркфлоу и скрипты | [Примеры](https://cc.bruniaux.com/examples/) | [Файлы](./examples/) |
| Визуальные схемы | Карты архитектуры, контекста, безопасности и воркфлоу | [Диаграммы](https://cc.bruniaux.com/diagrams/) | [Исходники диаграмм](./guide/diagrams/) |
| Проверка знаний | Вопросы со ссылками на документацию | [Тест знаний](https://cc.bruniaux.com/quiz/) | [Исходники вопросов](./quiz/) |
| Справочник для печати | Одна концепция на страницу (на французском и английском) | [Шпаргалки](https://cc.bruniaux.com/cheatsheets/) | [Исходники карточек](./whitepapers/recap-cards/) |
| Длинноформатное издание | Офлайн PDF и EPUB | [Электронные книги](https://cc.bruniaux.com/whitepapers/) | [Загрузки](https://cc.bruniaux.com/downloads/) |
| Машиночитаемый индекс | Поиск и извлечение для ИИ-ассистентов | [MCP руководства](https://cc.bruniaux.com/mcp/) | [llms.txt](./machine-readable/llms.txt) и [reference.yaml](./machine-readable/reference.yaml) |

## MCP-сервер: используйте руководство из любого кодинг-клиента

<!-- mcp-product:start -->
Установите руководство как stdio MCP-сервер и обращайтесь к нему из Claude Code, Codex, Cursor, VS Code или любого другого MCP-клиента.

```bash
claude mcp add --scope user claude-code-guide -- npx -y claude-code-ultimate-guide-mcp@1.3.8
codex mcp add claude-code-guide -- npx -y claude-code-ultimate-guide-mcp@1.3.8
```

Конфигурация Claude Code на уровне проекта размещается в `.mcp.json`:

```json
{
  "mcpServers": {
    "claude-code-guide": {
      "type": "stdio",
      "command": "npx",
      "args": ["-y", "claude-code-ultimate-guide-mcp@1.3.8"]
    }
  }
}
```

| Возможность | Кол-во | Имена |
| --- | ---: | --- |
| Инструменты (Tools) | 17 | `compare_versions`, `diff_official_docs`, `get_changelog`, `get_cheatsheet`, `get_digest`, `get_example`, `get_release`, `get_threat`, `init_official_docs`, `list_examples`, `list_threats`, `list_topics`, `read_section`, `refresh_official_docs`, `search_examples`, `search_guide`, `search_official_docs` |
| Ресурсы (Resources) | 7 | `claude-code-guide://agent-harnesses`, `claude-code-guide://ai-design-patterns`, `claude-code-guide://distribution-channels`, `claude-code-guide://llms`, `claude-code-guide://reference`, `claude-code-guide://releases`, `claude-code-guide://translations` |
| Промпты (Prompts) | 1 | `claude-code-expert` |
| Сопутствующие команды | 5 | `/ccguide:daily`, `/ccguide:diff-docs`, `/ccguide:init-docs`, `/ccguide:refresh-docs`, `/ccguide:search-docs` |

Операции списков и поисковый индекс используют встроенный контент. Инструменты для разделов, примеров, шпаргалок, журнала изменений, дайджеста (`get_digest`) и угроз могут загружать содержимое с GitHub и сохранять локальный кэш на 24 часа. Инструменты инициализации и обновления официальной документации загружают документацию Anthropic и сохраняют отдельные локальные снимки.

[Каноническое техническое руководство: установка, приватность, ограничения и датированная статистика](./guide/ecosystem/claude-code-guide-mcp.md)

[README пакета и диагностика](./mcp-server/README.md)

Сопутствующие команды, генерируемые из репозитория: `/ccguide:daily`, `/ccguide:diff-docs`, `/ccguide:init-docs`, `/ccguide:refresh-docs`, `/ccguide:search-docs`.
<!-- mcp-product:end -->

### Загрузите руководство в другой ассистент

Используйте компактный индекс для первичной навигации:

```bash
curl -sL https://raw.githubusercontent.com/FlorianBruniaux/claude-code-ultimate-guide/main/machine-readable/llms.txt
```

Используйте [reference.yaml](./machine-readable/reference.yaml), когда ассистенту нужны структурированные маршруты по темам и ссылки на полное руководство. Инструкции по сопровождению находятся в [машиночитаемой документации](./machine-readable/README.md), а не в этом README.

## Смежная экосистема

Ни один репозиторий не обязан одновременно охватывать обучение, установку, подборки, справочные материалы и каждый специализированный интерфейс. Выбирайте ресурс, подходящий под текущую задачу.

| Потребность | Ресурс | Что предоставляет |
|---|---|---|
| Проверить поведение Claude Code | [Официальная документация Claude Code](https://code.claude.com/docs) | Первичная документация продукта |
| Изучить архитектуру, компромиссы, безопасность и рабочие процессы | [Claude Code Guide](https://cc.bruniaux.com/guide/) | Объяснения, руководства по выбору решений, операционные проверки и примеры |
| Найти проекты сообщества | [awesome-claude-code](https://github.com/hesreallyhim/awesome-claude-code) | Кураторский список ссылок по экосистеме |
| Установить набор конфигураций | [everything-claude-code](https://github.com/affaan-m/everything-claude-code) | Упакованные агенты, скиллы, хуки и конфигурации |
| Подобрать устанавливаемые шаблоны | [claude-code-templates](https://github.com/davila7/claude-code-templates) | Каталог шаблонов и распространение через CLI |
| Начать с официальных примеров скиллов | [anthropics/skills](https://github.com/anthropics/skills) | Примеры скиллов, поддерживаемые Anthropic |
| Просмотреть маркетплейс скиллов | [skills.sh](https://skills.sh/) | Поиск и маршруты установки опубликованных скиллов |
| Подобрать хуки для Claude Code | [awesome-claude-code-hooks](https://github.com/loqimean/awesome-claude-code-hooks) | Кураторский список хуков Claude Code |
| Работать вне разработки ПО | [Claude Cowork Guide](https://github.com/FlorianBruniaux/claude-cowork-guide) | Рабочие процессы для специалистов умственного труда |
| Сравнить возможности кодинг-агентов | [AI Coding Agents Matrix](https://coding-agents-matrix.dev) | Межпродуктовое сравнение функций агентов |

Этот краткий список проверялся 2026-08-31. Активность проектов, способы установки и область охвата могут меняться. Сначала посмотрите публичные страницы [Экосистема](https://cc.bruniaux.com/ecosystem/) и [Сравнения](https://cc.bruniaux.com/compare/). Более подробные данные сохранены в исходниках [Экосистема ИИ](./guide/ecosystem/ai-ecosystem.md), [Сторонние инструменты](./guide/ecosystem/third-party-tools.md) и [Оценки ресурсов](./docs/resource-evaluations/).

По десктопным рабочим пространствам поверх существующих агентных CLI см. [сравнение рабочих пространств за октябрь 2026](./guide/ecosystem/third-party-tools.md#desktop-agent-workspace-comparison), включая локальный/облачный воркфлоу Conductor и заметку о статусе сопровождения Vibe Kanban.

## Обновления

Изменения руководства и релизы самого продукта Claude Code отвечают на разные вопросы:

| Лента | Что отслеживает | Источник |
|---|---|---|
| [История изменений руководства](https://cc.bruniaux.com/changelog/) | Новые страницы, исправления и крупные ревизии репозитория | [CHANGELOG.md](./CHANGELOG.md) |
| [Релизы Claude Code](https://cc.bruniaux.com/releases/) | Версии продукта Claude Code и их операционное влияние | [Исходник релизов](./guide/core/claude-code-releases.md) |
| [RSS-лента](https://cc.bruniaux.com/rss.xml) | Опубликованные обновления руководства и продукта в RSS-ридере | Генерируется сайтом |

Среди недавних дополнений руководства:

- [Оценка Mistral Large 4](./docs/resource-evaluations/mistral-large-4.md): данные запуска от 6 октября, промо-цены, независимые результаты, региональный инференс и ожидаемая публикация весов; интегрировано в [срез рынка](./guide/ops/llm-market-snapshot.md) и [экосистему ИИ](./guide/ecosystem/ai-ecosystem.md#21-mistral-large-4-multimodal-api-candidate).
- [Проектирование циклов и графов](https://cc.bruniaux.com/guide/loop-graph-engineering/) ([исходник](./guide/core/loop-graph-engineering.md)): ограниченная обратная связь, состояние рабочего процесса, правила остановки, восстановление и распределение ответственности за суждения.
- [Паттерны проектирования ИИ](https://cc.bruniaux.com/ai-design-patterns/) ([исходник](./guide/core/ai-design-patterns.md)): классические паттерны в проекции на механизмы Claude Code, границы применимости каждой аналогии, нативные агентные паттерны и антипаттерны.
- [Стратегия подписок](https://cc.bruniaux.com/guide/subscription-strategy/) ([исходник](./guide/ops/subscription-strategy.md)): пользовательские места, API, шлюзы, сценарии самостоятельного хостинга и критерии принятия решений при масштабировании команды.
- [Межсессионный обмен сообщениями](https://cc.bruniaux.com/guide/workflows/cross-session-messaging/) ([исходник](./guide/workflows/cross-session-messaging.md)): обнаружение узлов, доставка сообщений, границы безопасности и контроль скоррелированного дрейфа.

Полную историю смотрите в журнале изменений. README содержит лишь небольшую актуальную подборку.

## Языки и переводы

Английская версия является канонической. Французская версия поддерживается в этом репозитории. Упрощённый китайский, украинский и латиноамериканский испанский — независимые редакции сообщества с собственными графиками обновлений.

| Язык | Редакция |
|---|---|
| English | [Каноническое руководство](./guide/ultimate-guide.md) |
| Français | [Французское руководство, поддерживаемое в этом репозитории](./guide/ultimate-guide.fr.md) |
| 简体中文 | [Редакция сообщества от JAYcodr](https://github.com/JAYcodr/claude-code-ultimate-guide-zh) |
| Українська | [Редакция сообщества от gerasimsergey](https://github.com/gerasimsergey/claude-code-ultimate-guide-ua) |
| Español latinoamericano | [Редакция сообщества от Richardls](https://github.com/Richardls/claude-code-ultimate-guide-es) |

На странице [статуса переводов](./guide/core/translations.md) фиксируются мейнтейнеры, исходные коммиты, полнота охвата, измеренное отставание и статус ревью.

## Карта репозитория

```text
guide/
├── ultimate-guide.md       Полный справочник
├── learning-path/          Пошаговый курс
├── core/                   Архитектура, инструменты, контекст, методологии
├── security/               Усиление безопасности, изоляция, приватность, управление
├── ecosystem/              Агенты, MCP, инструменты, инференс, знания
├── roles/                  Внедрение, обучение, оценка, карьера
├── ops/                    Наблюдаемость, метрики, экономика, шлюзы
├── workflows/              Практические руководства по рабочим процессам
└── diagrams/               Диаграммы Mermaid с текстовыми фолбэками

examples/                   Переиспользуемые агенты, скиллы, хуки и воркфлоу
machine-readable/           Структурированные индексы и данные о релизах
mcp-server/                 Упакованный доступ к руководству для MCP-клиентов
quiz/                       Локальная проверка знаний
docs/resource-evaluations/  Оценённые внешние ресурсы
whitepapers/                Длинноформатные исходники на французском и английском
```

Подробный [индекс руководства](./guide/README.md), [каталог примеров](./examples/README.md) и [индекс инструментов](./tools/README.md) служат каноническими страницами навигации для соответствующих каталогов.

## Участие в развитии

Приветствуются исправления, недостающие подтверждения, починка битых ссылок, примеры, вопросы для тестов и улучшения документации. Прочитайте [CONTRIBUTING.md](./CONTRIBUTING.md), прежде чем открывать pull request.

Полезные направления вклада:

- Сообщайте о неточных или устаревших утверждениях через [GitHub Issues](https://github.com/FlorianBruniaux/claude-code-ultimate-guide/issues).
- Предлагайте внешние ресурсы через [процесс оценки ресурсов](./docs/resource-evaluations/README.md).
- Предлагайте сфокусированное руководство или рабочий процесс с указанием источников, границ применимости и способа проверки.
- Улучшайте примеры, не ослабляя существующие проверки безопасности.

## Мейнтейнер

Это руководство поддерживает Florian Bruniaux.

[GitHub](https://github.com/FlorianBruniaux) · [LinkedIn](https://www.linkedin.com/in/florian-bruniaux-43408b83/) · [Портфолио](https://www.florian.bruniaux.com/)

<!-- BEGIN GENERATED RELATED PROJECTS -->
<!-- Source: https://github.com/FlorianBruniaux/FlorianBruniaux/blob/main/ecosystem/projects.json; project: claude-code-guide -->
## Исследуйте экосистему

Эти проекты расширяют рабочий процесс, не дублируя этот инструмент:

- **Устанавливайте с [claude-code-plugins](https://github.com/FlorianBruniaux/claude-code-plugins)**: переходите от объяснений к устанавливаемым шаблонам.
- **Проверяйте с [ctxharness](https://github.com/FlorianBruniaux/ctxharness)**: тестируйте, по-прежнему ли задокументированный контекст и инструкции соответствуют репозиторию.
- **Защищайте с [agentsec-triage](https://github.com/FlorianBruniaux/agentsec-triage)**: связывайте рекомендации по безопасности с версионируемой операционной лентой.
- **Продолжайте с [Claude Cowork Guide](https://github.com/FlorianBruniaux/claude-cowork-guide)**: переходите к рабочим процессам, созданным для специалистов умственного труда и неразработчиков.

[Открыть всю open-source экосистему](https://github.com/FlorianBruniaux#open-source-galaxy)
<!-- END GENERATED RELATED PROJECTS -->

## Лицензия

Руководство распространяется под лицензией [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/). Переиспользуемые шаблоны распространяются под лицензией [CC0 1.0](https://creativecommons.org/publicdomain/zero/1.0/). Перед повторным распространением смешанного контента проверьте файлы лицензий в репозитории.

Следите за [GitHub Releases](https://github.com/FlorianBruniaux/claude-code-ultimate-guide/releases) или подпишитесь на [RSS-ленту](https://cc.bruniaux.com/rss.xml), чтобы получать обновления.

---

*Версия 3.46.0 | Обновляется ежедневно · 22 ноября 2026*
