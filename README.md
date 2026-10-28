# Awesome MCP Servers на русском

> Курированный список Model Context Protocol (MCP) серверов с описаниями на русском языке. Обновляется в 2026.

[MCP](https://modelcontextprotocol.io/) — открытый протокол от Anthropic, который позволяет LLM-клиентам (Claude Desktop, Claude Code, Cursor, VS Code, Continue, Cline) подключаться к внешним инструментам и данным единообразно.

## Содержание

- [Что такое MCP](#что-такое-mcp)
- [Официальные серверы](#официальные-серверы)
- [Файловая система и инструменты ОС](#файловая-система-и-инструменты-ос)
- [Поиск и веб](#поиск-и-веб)
- [Базы данных](#базы-данных)
- [Git и GitHub](#git-и-github)
- [Браузер и автоматизация](#браузер-и-автоматизация)
- [Память и заметки](#память-и-заметки)
- [AI и генерация](#ai-и-генерация)
- [Devtools](#devtools)
- [Клиенты MCP](#клиенты-mcp)
- [Как добавить свой MCP-сервер](#как-добавить-свой-mcp-сервер)

## Что такое MCP

MCP — это **стандартизированный способ**, которым LLM получает доступ к:

- **Tools** — функциям, которые модель может вызвать (например, прочитать файл, сделать HTTP-запрос).
- **Resources** — данным, которые модель может прочитать (файлы, документы, записи БД).
- **Prompts** — переиспользуемым шаблонам промптов.

Сервер MCP — это процесс (обычно stdio или SSE), который реализует этот протокол. Клиент (Claude Desktop, Cursor, VS Code) подключается к нему и автоматически предоставляет модели его tools.

## Официальные серверы

| Сервер | Что делает | Ссылка |
|--------|------------|--------|
| `filesystem` | Чтение, запись, поиск по локальной ФС с whitelist директорий | [modelcontextprotocol/servers](https://github.com/modelcontextprotocol/servers/tree/main/src/filesystem) |
| `git` | git status/log/diff/blame/branch и другие безопасные операции | [modelcontextprotocol/servers](https://github.com/modelcontextprotocol/servers/tree/main/src/git) |
| `github` | Issues, PR, search, file operations через GitHub API | [github/github-mcp-server](https://github.com/github/github-mcp-server) |
| `memory` | Граф знаний (entities + relations + observations) | [modelcontextprotocol/servers](https://github.com/modelcontextprotocol/servers/tree/main/src/memory) |
| `fetch` | HTTP GET с конвертацией HTML → Markdown | [modelcontextprotocol/servers](https://github.com/modelcontextprotocol/servers/tree/main/src/fetch) |
| `time` | Текущее время + конвертация таймзон | [modelcontextprotocol/servers](https://github.com/modelcontextprotocol/servers/tree/main/src/time) |
| `sequentialthinking` | Поэтапное рассуждение модели через явный tool | [modelcontextprotocol/servers](https://github.com/modelcontextprotocol/servers/tree/main/src/sequentialthinking) |
| `everything` | Полнотекстовый поиск файлов на Windows через Everything | [modelcontextprotocol/servers](https://github.com/modelcontextprotocol/servers) |

## Файловая система и инструменты ОС

- **filesystem** (официальный) — чтение/запись с whitelist директорий.
- **everything-search** — интеграция Everything (Windows) для мгновенного поиска по имени файла.
- **shell** — выполнение shell-команд (используй с осторожностью, только в sandboxed окружении).

## Поиск и веб

- **fetch** (официальный) — `fetch_url` с автоконвертацией в Markdown.
- **duckduckgo-mcp** — веб-поиск без API-ключа.
- **brave-search** — поиск через Brave Search API.
- **firecrawl** — продвинутый scraping и краулинг сайтов.
- **markitdown** — конвертация PDF/DOCX/PPTX/HTML/изображений в Markdown.

## Базы данных

- **sqlite-mcp** — query, schema, write для SQLite.
- **postgres-mcp** — read-only запросы к PostgreSQL.
- **mongodb-mcp** — официальный сервер MongoDB.
- **redis-mcp** — операции с Redis.

## Git и GitHub

- **git** (официальный) — локальные git-операции.
- **github** (от GitHub) — issues, PR, search, файлы через GitHub API.
- **gitlab-mcp** — то же для GitLab.
- **gitkraken-mcp** — расширенные git-операции через GitKraken.

## Браузер и автоматизация

- **playwright-mcp** — управление Playwright из LLM (открывать страницы, кликать, заполнять формы).
- **puppeteer-mcp** — то же на Puppeteer.
- **browser-use** — высокоуровневая автоматизация браузера для агентов.

## Память и заметки

- **memory** (официальный) — knowledge graph: entities + relations + observations.
- **obsidian-mcp** — чтение и поиск по vault Obsidian.
- **notion-mcp** — операции с Notion API.

## AI и генерация

- **openai-mcp** — proxy на OpenAI API как tool.
- **pollinations-mcp** — бесплатная генерация изображений через pollinations.ai.
- **replicate-mcp** — запуск моделей с Replicate.

## Devtools

- **coding-tools-mcp** — настольный сервер для кодинг-агентов: каркас проекта, поиск по коду, зависимости и сборка. [GitHub](https://github.com/mybolide/coding-tools-mcp)
- **pylance-mcp** — type checking, refactoring, syntax errors для Python.
- **context7** — актуальная документация по библиотекам и фреймворкам.
- **mcp-probe-kit** — самопроверка MCP-серверов: прогоняет все tools, resources и prompts, показывает здоровье, задержки и дрейф схем. [GitHub](https://github.com/mybolide/mcp-probe-kit)
- **sentry-mcp** — issues и performance из Sentry.
- **sqlite-mcp** — для отладки локальных БД.

## Клиенты MCP

| Клиент | Платформа | Конфиг |
|--------|-----------|--------|
| Claude Desktop | macOS, Windows | `~/Library/Application Support/Claude/claude_desktop_config.json` |
| Claude Code | CLI | `~/.config/claude/mcp.json` |
| Cursor | macOS, Windows, Linux | Settings → Features → MCP |
| VS Code (Copilot Chat) | Все | `.vscode/mcp.json` или Settings |
| Continue | VS Code, JetBrains | `.continue/config.json` |
| Cline | VS Code | Cline settings |

## Как добавить свой MCP-сервер

1. Форкни этот репо.
2. Добавь сервер в нужную секцию по алфавиту в формате:
   ```
   - **имя-сервера** — короткое описание на русском. [GitHub](https://github.com/owner/repo)
   ```
3. Открой PR.

**Критерии включения**:
- Открытый исходный код.
- Реально работает (мейнтейнится в последние 6 месяцев).
- Не дубликат уже включённого.

## Лицензия

[MIT](LICENSE)
