---
title: "Документация руководства"
description: "Указатель всех основных файлов документации для освоения Claude Code"
tags: [guide, reference]
---

# Документация руководства

Основная документация для освоения Claude Code, организованная по темам.

---

## Начало работы

| Файл | Описание | Время |
|------|----------|-------|
| [**learning-path/**](./learning-path/README.md) | **Структурированный учебный путь из 7 модулей** для начинающих: установка, основной цикл, память, агенты, скиллы, хуки, продвинутые паттерны | 8–11 часов |
| [core/ai-concept-boundaries.md](./core/ai-concept-boundaries.md) | Семь практических разграничений понятий, примеры из репозитория и семь сценариев для проверки понимания; выборочная адаптация Lexigraph с указанием авторства | В своём темпе |
| [learning-path/01-installation.md](./learning-path/01-installation.md) | Модуль 01: установка Claude Code и проверка его работы | 15 мин |
| [learning-path/02-core-loop.md](./learning-path/02-core-loop.md) | Модуль 02: понимание цикла взаимодействия и контекста | 45 мин |
| [learning-path/03-memory.md](./learning-path/03-memory.md) | Модуль 03: создание `CLAUDE.md` и настройка памяти | 1 час |
| [learning-path/04-agents.md](./learning-path/04-agents.md) | Модуль 04: создание специализированных агентов | 1,5 часа |
| [learning-path/05-skills.md](./learning-path/05-skills.md) | Модуль 05: создание переиспользуемых скиллов | 1,5 часа |
| [learning-path/06-hooks.md](./learning-path/06-hooks.md) | Модуль 06: создание хуков автоматизации | 1 час |
| [learning-path/07-advanced.md](./learning-path/07-advanced.md) | Модуль 07: оркестрация нескольких агентов | 2–3 часа |

---

## Основной справочник

| Файл | Описание | Время |
|------|----------|-------|
| [ultimate-guide.md](./ultimate-guide.md) | Полный справочник по всем возможностям Claude Code | ~3 часа |
| [ultimate-guide.fr.md](./ultimate-guide.fr.md) | Французский перевод полного справочного руководства | ~3 часа |
| [core/translations.md](./core/translations.md) | **Переводы и управление языковыми версиями**: проверенное указание авторства, исходные коммиты, измеренная задержка и официальный либо общественный статус | 5 мин |
| [cowork.md](./cowork.md) | Claude Cowork: обзор агентного настольного приложения для нетехнических специалистов, работающих со знаниями | 10 мин |
| [cheatsheet.md](./cheatsheet.md) | Одностраничная краткая справка для печати | 5 мин |
| [core/architecture.md](./core/architecture.md) | Внутреннее устройство Claude Code (главный цикл, инструменты, контекст) | 25 мин |
| [core/computer-use.md](./core/computer-use.md) | **Управление компьютером**: границы разрешений, порядок резервных вариантов, безопасная рабочая процедура и ограничения проверки | 12 мин |
| [core/agent-harness.md](./core/agent-harness.md) | **Инженерия обвязки агента (Agent Harness Engineering)**: компоненты среды выполнения, горизонты циклов, безопасность, оценка и оптимизация харнесса внешнего цикла | 35 мин |
| [core/loop-graph-engineering.md](./core/loop-graph-engineering.md) | **Инженерия циклов и графов**: ограниченная обратная связь, исполняемые графы рабочих процессов, устойчивое состояние, восстановление и распределение задач, требующих суждения | 25 мин |
| [core/ai-design-patterns.md](./core/ai-design-patterns.md) | **Паттерны проектирования ИИ**: паттерны GoF, интеграции и отказоустойчивости, сопоставленные с механизмами Claude Code, включая режимы отказа, проверки, нативные агентные паттерны и антипаттерны | 20 мин |
| [core/tools-reference.md](./core/tools-reference.md) | **Полный справочник инструментов**: все 40 встроенных инструментов, форматы правил разрешений, особенности отдельных инструментов (тайм-ауты Bash, чтение перед редактированием в Edit, ограничение Glob, потеря данных в WebFetch) и инструкции по использованию Monitor, Workflow, команд агентов, Cron и Tasks API | 20 мин |
| [core/hooks-events-reference.md](./core/hooks-events-reference.md) | **Полный справочник хуков**: все 33 события хуков, поля сопоставления, входные схемы, форматы управления решениями и стандартные тайм-ауты, а также готовые для копирования примеры JSON | 15 мин |
| [core/settings-reference.md](./core/settings-reference.md) | **Полный справочник по `settings.json`**: все подтверждённые настройки и переменные окружения | 15 мин |
| [core/methodologies.md](./core/methodologies.md) | Справочник по 15 методологиям разработки (TDD, SDD, BDD и т. д.) | 20 мин |
| [core/visual-reference.md](./core/visual-reference.md) | Визуальная шпаргалка: ASCII-диаграммы основных понятий | 5 мин |
| [core/claude-code-releases.md](./core/claude-code-releases.md) | Официальная история выпусков (сокращённая) | 10 мин |
| [core/known-issues.md](./core/known-issues.md) | **Трекер критических ошибок**: проблемы безопасности, расход токенов, проверенные сообщения сообщества | 15 мин |
| [core/context-engineering.md](./core/context-engineering.md) | **Инженерия контекста**: бюджет токенов, модульная архитектура, формирование команды, конвейер ACE, измерение качества | 25 мин |
| [core/memory-systems.md](./core/memory-systems.md) | **Системы памяти**: нативный стек (`CLAUDE.md`, Auto Memory, Auto Dream), межсессионные инструменты (claude-mem, agentmemory, ICM), совместное использование в команде, мультиагентные паттерны, архитектура, риски и блок-схема принятия решений | 30 мин |
| [core/glossary.md](./core/glossary.md) | **Глоссарий**: терминология Claude Code и смежные понятия об агентах (41 термин в формате абзацев, со ссылками на разделы руководства) | 5 мин |
| [core/community-patterns.md](./core/community-patterns.md) | **Паттерны сообщества**: около 130 созданных сообществом паттернов, терминов рабочих процессов, понятий инженерии ИИ и кратких определений | 10 мин |
| [core/skill-design-patterns.md](./core/skill-design-patterns.md) | **Паттерны проектирования скиллов**: архитектурные паттерны для надёжных и экономных по токенам скиллов с мультиагентными конвейерами | 20 мин |
| [core/credits.md](./core/credits.md) | Проекты с открытым исходным кодом и инженерные команды, чья работа послужила основой для конкретных паттернов этого руководства | 5 мин |
| [diagrams/](./diagrams/) | **Серия визуальных диаграмм**: 41 интерактивная диаграмма Mermaid по выбору модели, жизненному циклу агента, безопасности и мультиагентным паттернам | 15 мин |

---

## Визуальные диаграммы

**48 интерактивных диаграмм Mermaid** в 12 тематических файлах, с нативным отображением Mermaid на GitHub и резервным вариантом в ASCII для каждой диаграммы. Полный навигационный указатель и руководства по вариантам использования см. в [diagrams/README.md](./diagrams/README.md).

| Файл | Диаграммы | Темы |
|------|-----------|------|
| [diagrams/01-foundations.md](./diagrams/01-foundations.md) | 4 | Четырёхуровневая модель, конвейер рабочего процесса, дерево решений, режимы разрешений |
| [diagrams/02-context-and-sessions.md](./diagrams/02-context-and-sessions.md) | 4 | Зоны контекста, иерархия памяти, перенос между сессиями, свежий контекст |
| [diagrams/03-configuration-system.md](./diagrams/03-configuration-system.md) | 4 | Приоритет конфигураций, скиллы и команды и агенты, жизненный цикл агента, хуки |
| [diagrams/04-architecture-internals.md](./diagrams/04-architecture-internals.md) | 4 | Главный цикл, категории инструментов, сборка системного промпта, изоляция субагентов |
| [diagrams/05-mcp-ecosystem.md](./diagrams/05-mcp-ecosystem.md) | 4 | Карта экосистемы MCP, архитектура MCP, атака с внезапной подменой, иерархия конфигураций |
| [diagrams/06-development-workflows.md](./diagrams/06-development-workflows.md) | 5 | Цикл TDD, конвейер «сначала спецификация», разработка на основе плана, итеративное улучшение, пути освоения ИИ |
| [diagrams/07-multi-agent-patterns.md](./diagrams/07-multi-agent-patterns.md) | 5 | Топологии агентов, worktree, два экземпляра, горизонтальное масштабирование, матрица решений |
| [diagrams/08-security-and-production.md](./diagrams/08-security-and-production.md) | 4 | Трёхуровневая защита, решение об использовании песочницы, парадокс проверки, конвейер CI/CD |
| [diagrams/09-cost-and-optimization.md](./diagrams/09-cost-and-optimization.md) | 4 | Выбор модели, оптимизация затрат, уровни подписки, сокращение токенов |
| [diagrams/10-adoption-and-learning.md](./diagrams/10-adoption-and-learning.md) | 3 | Пути адаптации, протокол UVAL, калибровка доверия |
| [diagrams/11-context-engineering.md](./diagrams/11-context-engineering.md) | 4 | Трёхуровневая система контекста, ухудшение соблюдения инструкций, модульная архитектура, размещение правил |
| [diagrams/12-enterprise-governance.md](./diagrams/12-enterprise-governance.md) | 3 | Уровни риска в управлении, рабочий процесс утверждения MCP, классификация данных |

---

## Безопасность

| Файл | Описание | Время |
|------|----------|-------|
| [security/security-hardening.md](./security/security-hardening.md) | Угрозы безопасности, проверка MCP, защита от инъекций | 25 мин |
| [security/sandbox-isolation.md](./security/sandbox-isolation.md) | Песочницы Docker, облачные альтернативы, рабочие процессы безопасной автономной работы | 10 мин |
| [security/sandbox-native.md](./security/sandbox-native.md) | Нативная песочница Claude Code: конфигурация и модель безопасности | 10 мин |
| [security/production-safety.md](./security/production-safety.md) | Безопасность в продакшене: защитные ограничения, этапы проверки, стратегии отката | 15 мин |
| [security/data-privacy.md](./security/data-privacy.md) | Руководство по хранению данных и конфиденциальности | 10 мин |
| [security/agentic-pentesting.md](./security/agentic-pentesting.md) | DarkMoon и Strix: область выполнения, доказательства эксплуатации, раскрытие данных модели и протокол оценки | Справочник |
| [security/enterprise-governance.md](./security/enterprise-governance.md) | **Управление на уровне организации**: регламенты использования, рабочий процесс утверждения MCP, уровни защитных ограничений (Starter/Standard/Strict/Regulated), соответствие требованиям | 25 мин |

---

## Экосистема

| Файл | Описание | Время |
|------|----------|-------|
| [ecosystem/ai-ecosystem.md](./ecosystem/ai-ecosystem.md) | Дополняющие инструменты ИИ (Perplexity, Gemini, Kimi, NotebookLM, TTS), а также кандидат Mistral Large 4 API | 30 мин |
| [ecosystem/plugin-distribution.md](./ecosystem/plugin-distribution.md) | **Распространение плагинов**: границы пакетов, доверие к маркетплейсу, подсказки для рекомендаций и проверки выпусков | 15 мин |
| [ecosystem/agentic-tools.md](./ecosystem/agentic-tools.md) | **Сравнение агентных инструментов**: Hermes Agent, Codex CLI, Aider, Devin, SWE-agent, CrewAI, LangGraph, AutoGen и система принятия решений | 20 мин |
| [ecosystem/mcp-vs-cli.md](./ecosystem/mcp-vs-cli.md) | **Руководство по выбору между MCP и CLI**: когда в рабочих процессах Claude Code использовать MCP-серверы, а когда инструменты CLI, включая компромиссы и критерии выбора | 15 мин |
| [ecosystem/claude-code-guide-mcp.md](./ecosystem/claude-code-guide-mcp.md) | **Технический справочник по MCP руководства**: установка для разных клиентов, опубликованные и кандидатные возможности, архитектура, границы сети и конфиденциальности, автономная работа, устранение неполадок и датированные метрики | 12 мин |
| [ecosystem/agent-harness-landscape.md](./ecosystem/agent-harness-landscape.md) | **Карта обвязок агентов**: строгие среды выполнения, оркестраторы, смежные проекты и основанный на источниках исследовательский слой для оптимизаторов харнессов и метахарнессов | 10 мин |
| [ecosystem/mcp-servers-ecosystem.md](./ecosystem/mcp-servers-ecosystem.md) | **MCP-серверы сообщества**: 8 проверенных серверов (Playwright, Semgrep, Kubernetes и другие) с конфигурациями для продакшена | 25 мин |
| [ecosystem/third-party-tools.md](./ecosystem/third-party-tools.md) | **Инструменты сообщества**: GUI, TUI, менеджеры конфигураций, трекеры токенов; [сравнение настольных рабочих пространств для агентов](./ecosystem/third-party-tools.md#desktop-agent-workspace-comparison) | 15 мин |
| [ecosystem/context-engineering-tools.md](./ecosystem/context-engineering-tools.md) | **Оптимизация контекста и токенов**: сжатие вывода (RTK, в ранней разработке которого участвовал автор руководства; Headroom), сжатие промптов (LLMLingua), шлюзы ИИ (Edgee, Portkey), RAG, LLMOps | 20 мин |
| [ecosystem/remarkable-ai.md](./ecosystem/remarkable-ai.md) | Паттерны использования Remarkable AI и приёмы для опытных пользователей | 10 мин |
| [ecosystem/practitioner-insights.md](./ecosystem/practitioner-insights.md) | **Практические отчёты специалистов**: 75 перефразированных выводов из IFTTD, Devoxx, Dev With AI Meetup, ByteByteGo, Stanford Online и корпуса видео Pavan Belagatti за 2026 год, сгруппированных по темам (инженерия контекста, агентные паттерны, оценка LLM, безопасность агентов, DevX и внедрение) | 20 мин |
| [ecosystem/team-knowledge-base.md](./ecosystem/team-knowledge-base.md) | **Командная инфраструктура знаний**: трёхуровневая система (статическое хранилище Markdown, MCP-коннекторы для действующих систем, RAG в масштабе), порог RAG (~100–1000 документов), MCP для Atlassian/Notion/GitBook, Onyx/LlamaCloud/Ragie, распространение плагинов, связка Code+Cowork | 18 мин |
| [ecosystem/local-vs-cloud-inference.md](./ecosystem/local-vs-cloud-inference.md) | **Экономика локального и облачного инференса**: 10 сопоставимых конфигураций оборудования (размерности llmfit), цены аренды GPU в OVH/AWS/Lambda/RunPod, прогнозы совокупной стоимости владения за один год, пропускная способность Claude и GPT-5.6 в облаке, система принятия решений | 20 мин |
| [ecosystem/ai-executive-agents.md](./ecosystem/ai-executive-agents.md) | **ИИ-агенты руководителей**: подробный разбор OpenExecutive, альтернативы с открытым исходным кодом (Become CEO, OneManCompany, crewAI) с проверенной статистикой GitHub, таблица маршрутизации по ролям (CFO, CMO, CHRO, главный юрисконсульт, совет директоров), соотношение усиления и замены, а также аспект управления Synthetic Director | 12 мин |

---

## Роли и внедрение

| Файл | Описание | Время |
|------|----------|-------|
| [roles/ai-roles.md](./roles/ai-roles.md) | Ограниченная доказательствами карта семейств ролей ИИ, специализаций, сближения ролей в небольших командах и карьерных траекторий | 25 мин |
| [roles/adoption-approaches.md](./roles/adoption-approaches.md) | Стратегии внедрения для команд | 15 мин |
| [roles/learning-with-ai.md](./roles/learning-with-ai.md) | Руководство для начинающих специалистов по использованию ИИ без утраты навыков | 15 мин |
| [roles/agent-evaluation.md](./roles/agent-evaluation.md) | **Метрики качества агентов**: измерение эффективности пользовательских агентов с помощью хуков, тестов и циклов обратной связи | 20 мин |

---

## Эксплуатация

| Файл | Описание | Время |
|------|----------|-------|
| [ops/devops-sre.md](./ops/devops-sre.md) | Система FIRE для диагностики инфраструктуры и реагирования на инциденты | 30 мин |
| [ops/observability.md](./ops/observability.md) | Мониторинг сессий и отслеживание затрат | 15 мин |
| [ops/api-gateway.md](./ops/api-gateway.md) | **Шлюзы API**: отделение поведения шлюзов приложений Claude от средств управления сторонних прокси, таких как LiteLLM и Portkey | 15 мин |
| [ops/ai-traceability.md](./ops/ai-traceability.md) | Указание вклада ИИ, политики раскрытия информации, git-ai, соответствие требованиям | 20 мин |
| [ops/team-metrics.md](./ops/team-metrics.md) | **Командные метрики для разработки с применением ИИ**: DORA, SPACE, DX Core 4, специфичные для ИИ сигналы с разбивкой по размеру команды (5–25 человек) | 20 мин |
| [ops/ai-unit-economics.md](./ops/ai-unit-economics.md) | **Юнит-экономика ИИ**: разложение стоимости каждой задачи, реальные рычаги управления затратами (маршрутизация, изоляция субагентов, критерии завершения), точка безубыточности автономного агента, управление командным бюджетом | 15 мин |
| [ops/subscription-strategy.md](./ops/subscription-strategy.md) | **Стратегия подписок в масштабе команды**: упражнение по формированию портфеля Claude, Codex, Copilot, Gemini, Cursor и Mistral; средства управления шлюзом API; пробелы в договорах персональных тарифов; экономика самостоятельного хостинга на основе сценариев | 20 мин |
| [ops/ai-finops.md](./ops/ai-finops.md) | **AI FinOps (точка входа в раздел)**: три режима затрат (квота подписки, тарифицируемые токены, собственные мощности), цикл Inform-Optimize-Operate применительно к агентам и карта всех рычагов управления затратами с указанием того, какие проблемы они не решают | 12 мин |
| [ops/llm-market-snapshot.md](./ops/llm-market-snapshot.md) | **Обзор рынка LLM (30.09.2026, Mistral Large 4 добавлена 06.10.2026)**: цены, проверенные по источникам, квоты подписок, региональная обработка, бенчмарки и одна гипотетическая агентная рабочая нагрузка | 20 мин |

---

## Рабочие процессы

Практические руководства по эффективным паттернам разработки:

| Файл | Описание |
|------|----------|
| [workflows/tdd-with-claude.md](./workflows/tdd-with-claude.md) | Разработка через тестирование с Claude |
| [workflows/spec-first.md](./workflows/spec-first.md) | Разработка «сначала спецификация» (SDD) |
| [workflows/plan-driven.md](./workflows/plan-driven.md) | Эффективное использование режима `/plan` |
| [workflows/iterative-refinement.md](./workflows/iterative-refinement.md) | Циклы итеративного улучшения |
| [workflows/best-of-n.md](./workflows/best-of-n.md) | Создание независимых вариантов, выбор по зафиксированной системе критериев, проверка и сохранение журнала доказательств |
| [workflows/tts-setup.md](./workflows/tts-setup.md) | Добавление голосового воспроизведения текста в Claude Code (18 мин) |
| [workflows/task-management.md](./workflows/task-management.md) | Отслеживание задач между сессиями, миграция TodoWrite |
| [workflows/agent-teams.md](./workflows/agent-teams.md) | Оркестрация мультиагентных команд для сложных задач |
| [workflows/agent-teams-quick-start.md](./workflows/agent-teams-quick-start.md) | Краткое руководство по началу работы с паттернами команд агентов |
| [workflows/agentic-software-factories.md](./workflows/agentic-software-factories.md) | Ориентировочная карта: от одной сессии до фабрики программного обеспечения и условия, при которых закрытая платформа действительно выигрывает |
| [../examples/workflows/bounded-loop-contract.md](../examples/workflows/bounded-loop-contract.md) | Исполняемый контракт ограниченного цикла с отдельным интерфейсом проверяющего, бюджетом попыток, доказательствами и эскалацией |
| [workflows/dynamic-workflows.md](./workflows/dynamic-workflows.md) | Мультиагентные конвейеры под оркестрацией JavaScript: детерминированный поток управления, параллельное разветвление, автоматическое возобновление |
| [workflows/dual-instance-planning.md](./workflows/dual-instance-planning.md) | Планирование с двумя экземплярами: Opus планирует, Sonnet выполняет |
| [workflows/event-driven-agents.md](./workflows/event-driven-agents.md) | Паттерны событийной координации агентов |
| [workflows/monitor-event-delegation.md](./workflows/monitor-event-delegation.md) | Команда Monitor/WebSocket, мониторы плагинов, Channels, Routines и безопасное делегирование Codex |
| [workflows/github-actions.md](./workflows/github-actions.md) | Пошаговая настройка claude-code-action: проверка PR по упоминанию, автоматическая проверка при отправке изменений, сортировка задач |
| [workflows/reviewable-agent-changes.md](./workflows/reviewable-agent-changes.md) | Обоснование рядом с изменениями: что записывает примечание агента для каждого фрагмента, хранение и перезапись git notes, устаревшие примечания, обратная связь в виде вопроса или изменения, протестированный шаблон | 15 мин |
| [workflows/code-review.md](./workflows/code-review.md) | Автоматизированная мультиагентная проверка PR для Teams и Enterprise: настройка, триггеры, конфигурация `REVIEW.md`, управление затратами |
| [workflows/ai-assisted-open-source-contributions.md](./workflows/ai-assisted-open-source-contributions.md) | Политика внесения вклада, воспроизведение, понимание автором, доказательства проверки и последующая коммуникация с сопровождающими |
| [workflows/production-reliability.md](./workflows/production-reliability.md) | Паттерны надёжности в продакшене: проектирование эскалации, автоматические выключатели, структурированная передача ошибок, плавная деградация |
| [workflows/support-csm-agent.md](./workflows/support-csm-agent.md) | Внутренний агент поддержки/CSM: сортировка обращений, диагностика БД, работа с CRM через MCP |
| [workflows/plan-pipeline.md](./workflows/plan-pipeline.md) | Сквозной конвейер плана: запуск, проверка, выполнение |
| [workflows/design-to-code.md](./workflows/design-to-code.md) | Преобразование макетов Figma и вайрфреймов в работающий код |
| [workflows/exploration-workflow.md](./workflows/exploration-workflow.md) | Систематическое изучение незнакомых кодовых баз |
| [workflows/pdf-generation.md](./workflows/pdf-generation.md) | Создание профессиональных PDF с помощью Quarto/Typst |
| [workflows/search-tools-mastery.md](./workflows/search-tools-mastery.md) | Освоение комбинированных рабочих процессов с rg, grepai, Serena и ast-grep |
| [workflows/skeleton-projects.md](./workflows/skeleton-projects.md) | Использование проверенных в работе репозиториев как основы для новых проектов |
| [workflows/talk-pipeline.md](./workflows/talk-pipeline.md) | Шесть этапов подготовки выступления: от исходного материала до слайдов |
| [workflows/team-ai-instructions.md](./workflows/team-ai-instructions.md) | Масштабирование `CLAUDE.md` на команды из нескольких разработчиков |

---

## Документация Cowork

Для специалистов, работающих со знаниями и использующих Claude Cowork (агентное настольное приложение):

| Ресурс | Описание |
|--------|----------|
| **[Центр Cowork](https://github.com/FlorianBruniaux/claude-cowork-guide/blob/main/README.md)** | Полная документация Cowork |
| [Начало работы](https://github.com/FlorianBruniaux/claude-cowork-guide/blob/main/guide/01-getting-started.md) | Настройка и первый рабочий процесс |
| [Возможности](https://github.com/FlorianBruniaux/claude-cowork-guide/blob/main/guide/02-capabilities.md) | Что Cowork может и чего не может делать |
| [Руководство по безопасности](https://github.com/FlorianBruniaux/claude-cowork-guide/blob/main/guide/03-security.md) | Практики безопасного использования |
| [Библиотека промптов](https://github.com/FlorianBruniaux/claude-cowork-guide/tree/main/prompts) | Более 50 готовых к использованию промптов |
| [Шпаргалка](https://github.com/FlorianBruniaux/claude-cowork-guide/blob/main/reference/cheatsheet.md) | Одностраничная краткая справка |

---

## Рекомендуемый порядок чтения

1. **Новые пользователи**: начните с раздела «Быстрый старт» в `ultimate-guide.md`
2. **Справочник на каждый день**: распечатайте `cheatsheet.md`
3. **Руководители команд**: прочитайте `roles/adoption-approaches.md`, чтобы ознакомиться со стратегиями внедрения
4. **Акцент на безопасности**: сначала `security/security-hardening.md`, затем `security/sandbox-isolation.md`
5. **Глубокое изучение архитектуры**: сначала `core/architecture.md`, затем `diagrams/`

---

*Вернуться к [основному README](../README.md)*
