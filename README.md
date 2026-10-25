# ai-code-quality

Принципы качества кода (Agent Skills), которые устанавливаются как плагин в **Claude Code** и **Codex**.
Один и тот же каталог `skills/` используется обоими агентами.

## Структура

```
ai-code-quality/
├── .claude-plugin/
│   ├── plugin.json        # манифест плагина Claude Code
│   └── marketplace.json   # маркетплейс Claude Code
├── .codex-plugin/
│   └── plugin.json        # манифест плагина Codex
├── .agents/plugins/
│   └── marketplace.json   # маркетплейс Codex
└── skills/
    └── <skill-name>/
        └── SKILL.md
```

## Установка

### Claude Code

```
/plugin marketplace add grind-t/ai-code-quality
/plugin install code-quality@code-quality
```

Локально: `/plugin marketplace add ./ai-code-quality`.

### Codex

```bash
codex plugin marketplace add grind-t/ai-code-quality
```

Затем установите `code-quality` из каталога плагинов (`/plugins` в Codex).
Локально: `codex plugin marketplace add ./ai-code-quality`.

Навыки доступны с префиксом плагина: `/code-quality:<skill-name>`, например `/code-quality:principles`.

## Добавление навыка

1. Создайте `skills/<skill-name>/SKILL.md`.
2. Во frontmatter укажите `name` (kebab-case, совпадает с именем папки) и `description` — что делает навык и когда его применять.
3. Поднимите `version` в обоих `plugin.json`.

```markdown
---
name: my-skill
description: Что делает навык и когда его использовать.
---

# Инструкции
...
```

## Навыки

| Навык | Описание |
|---|---|
| `principles` | Принципы дизайна кода и именования |
| `defects` | Описание дефектов качества кода по схеме на основе ISO/IEC 25010:2023 (вызывается вручную) |
