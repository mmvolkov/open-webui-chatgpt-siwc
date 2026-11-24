# Участие в разработке

[English](CONTRIBUTING.md) | **Русский**

Благодарим за улучшение Open WebUI ChatGPT SIWC.

## Перед созданием Pull Request

- Для крупных изменений сначала откройте issue и обсудите объем работ.
- Не добавляйте в репозиторий конфигурации конкретной инсталляции, `.env`, секреты, ID аккаунтов, приватные хосты, снимки продуктивной среды и журналы развертывания.
- Сохраняйте проект адаптером официальных SIWC и Responses API. Не добавляйте вторую API-шлюзовую систему, базу данных, scheduler, агентный runtime или сторонние службы.
- В тестах применяйте только синтетические данные. Не используйте настоящий аккаунт ChatGPT или живую OAuth-сессию в автоматических тестах.
- Для изменений поведения добавляйте тесты: OAuth, pairing, шифрование, refresh, streaming, обнаружение моделей, reasoning и инструменты.

## Локальные проверки

```sh
python -m venv .venv
. .venv/bin/activate
pip install -r requirements-dev.txt
python -m compileall -q app tests tools
ruff check app tests tools
python -m pytest -q
npm --prefix tools ci
node --check tools/authorize.mjs
node --check tools/web_connect.mjs
node --test tools/test_oauth_flow.test.mjs
node tools/test_companion_flow.mjs
docker build -t open-webui-chatgpt-siwc:local .
git diff --check
```

Приложение companion компилируется и проверяется в CI на macOS. Реальное подтверждение SIWC в браузере - отдельный ручной этап приемки; результаты синтетических тестов нельзя выдавать за успешную живую авторизацию.

## Pull Requests

Используйте шаблон PR. Делайте изменения обозримыми, описывайте совместимость и последствия для безопасности, связывайте изменения с issue. Сопровождающие проекта могут запросить исправления до слияния.
