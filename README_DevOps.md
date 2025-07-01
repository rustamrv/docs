# Общие навыки и DevOps — Теория и Практика

## Git, workflow (GitFlow, trunk-based)
Git — система контроля версий. GitFlow: master, develop, feature, release, hotfix ветки. Trunk-based: одна основная ветка, быстрые интеграции.

**Пример (создание ветки):**
```sh
git checkout -b feature/new-feature
```

## Docker, docker-compose, основы Kubernetes
Docker — контейнеризация приложений. Dockerfile описывает сборку образа. docker-compose — запуск нескольких контейнеров. Kubernetes — оркестрация, масштабирование, обновления.

**Пример (docker-compose.yml):**
```yaml
version: '3'
services:
  app:
    build: .
    ports:
      - "3000:3000"
```

## CI/CD: пайплайны, автоматизация тестов и деплоя
CI/CD — автоматизация сборки, тестирования, доставки кода. Пайплайны (GitHub Actions, Gitlab CI, Jenkins).

**Пример (GitHub Actions):**
```yaml
name: CI
on: [push]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Run tests
        run: npm test
```

## Мониторинг и логирование (Prometheus, Grafana, Sentry)
Prometheus — сбор метрик, Grafana — визуализация, Sentry — отслеживание ошибок.

**Пример (Sentry инициализация):**
```js
Sentry.init({ dsn: 'https://example@sentry.io/123' });
```

## Английский: чтение документации, code review, общение в команде
Английский — ключ к чтению документации, участию в code review, коммуникации в международных командах. 