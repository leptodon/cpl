# Routine Checks

Рутинные проверки и задачи, запускаемые через `/cpl:verify` или вручную.

## Lint & Format

| Стек | Lint | Format |
|------|------|--------|
| Kotlin/Android | `./gradlew detekt` | `./gradlew ktlintFormat` |
| TypeScript/JS | `npm run lint` | `npm run format` / `npx prettier --write .` |
| Python | `ruff check .` | `ruff format .` |
| Rust | `cargo clippy` | `cargo fmt` |
| Go | `golangci-lint run` | `gofmt -w .` |

## Commit Hygiene

- Conventional commits: `feat:`, `fix:`, `refactor:`, `test:`, `docs:`, `chore:`
- Один логический change = один коммит
- Не коммить: `.env`, credentials, IDE-специфичные файлы

## Commit Trailers (опционально, для нетривиальных решений)

Добавляй трейлеры когда решение требует контекста для будущих агентов:

```
feat: краткое описание изменения

Тело коммита (если нужно).

Rejected: <альтернатива> | <причина отклонения>
Directive: <предупреждение для будущих разработчиков>
Constraint: <ограничение, которое повлияло на решение>
Confidence: high | medium | low
Scope-risk: narrow | moderate | broad
Not-tested: <кейс, не покрытый тестами>
```

Пример:

```
fix(auth): перехватывать все 4xx для инлайн-обновления токена

Сервис auth не поддерживает introspection, поэтому
interceptor ловит все 4xx и сразу рефрешит токен.

Rejected: продлить TTL токена до 24h | нарушение security policy
Rejected: фоновый refresh по таймеру | race condition при параллельных запросах
Constraint: Auth service не поддерживает token introspection
Directive: обработка намеренно широкая (все 4xx) — не сужай без проверки upstream
Confidence: high
Scope-risk: narrow
Not-tested: cold-start latency Auth service >500ms
```

Трейлеры можно пропускать для мелких изменений (typo, форматирование, тривиальные фиксы).

## Import Cleanup

- Удали неиспользуемые imports
- Сортируй imports по конвенции проекта
- Не добавляй wildcard imports

## Naming Conventions

- Следуй конвенциям языка (camelCase для Kotlin/Java, snake_case для Python/Rust)
- Имена переменных/функций — по смыслу, не по типу
- Тестовые методы: `should_<behavior>_when_<condition>` или проектная конвенция
