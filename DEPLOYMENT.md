# Деплой на GitHub Pages

Этот проект настроен для автоматического деплоя на GitHub Pages через GitHub Actions.

## Настройка GitHub Pages

1. **Перейдите в настройки репозитория:**
   - Откройте ваш репозиторий на GitHub
   - Перейдите в Settings → Pages

2. **Настройте источник деплоя:**
   - В разделе "Source" выберите "GitHub Actions"
   - Сохраните настройки

3. **Проверьте права доступа:**
   - Убедитесь, что у GitHub Actions есть права на запись в Pages
   - В Settings → Actions → General → Workflow permissions выберите "Read and write permissions"

## Локальная сборка

Для тестирования сборки локально:

### Обычная сборка (без basePath):
```bash
cd main
pnpm install
pnpm run export
```

### Сборка для GitHub Pages (с basePath):
```bash
cd main
pnpm install
NEXT_PUBLIC_GH_PAGES=true pnpm run export
```

Собранные файлы будут в папке `main/out/`

## Настройка для подпапки репозитория

Репозиторий настроен для работы в подпапке `/polly-strat/` на GitHub Pages.

Конфигурация в `next.config.ts` использует переменную окружения `NEXT_PUBLIC_GH_PAGES`:
- Если `NEXT_PUBLIC_GH_PAGES=true`, то используется `basePath: '/polly-strat'` и `assetPrefix: '/polly-strat/'`
- Если переменная не установлена, приложение работает без basePath (для локальной разработки)

## Автоматический деплой

После настройки GitHub Pages, каждый push в ветку `main` будет автоматически:
1. Собирать Next.js приложение с `NEXT_PUBLIC_GH_PAGES=true`
2. Деплоить его на GitHub Pages

**Важно**: При сборке для GitHub Pages обязательно должна быть установлена переменная окружения `NEXT_PUBLIC_GH_PAGES=true`, чтобы правильно настроились пути к ресурсам.

URL вашего сайта будет доступен по адресу:
- `https://ruddch.github.io/polly-strat/` (текущая настройка)
