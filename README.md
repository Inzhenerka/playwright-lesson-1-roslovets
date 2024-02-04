# Урок 1 "Создание проекта Playwright"

## Введение

Добро пожаловать в первый урок курса "Тестирование с Playwright"! Playwright — это мощный инструмент для автоматизации тестирования веб-приложений, который поддерживает все современные веб-браузеры. В этом уроке мы рассмотрим, как создать новый проект с Playwright, настроить окружение и подготовить всё необходимое для начала тестирования.

## Пошаговая инструкция по созданию нового проекта

### Шаг 1: Установка Node.js

Перед началом работы убедитесь, что у вас установлен Node.js. Скачать и установить его можно с официального сайта [Node.js](https://nodejs.org/).

### Шаг 2: Инициализация нового проекта

1. Откройте терминал в папке проекта
2. Инициализируйте новый проект Node.js:

```
npm init -y
```

### Шаг 3: Установка Playwright

Установите Playwright с помощью npm, что также автоматически установит браузеры, необходимые для тестирования:

```
npm i -D @types/node playwright @playwright/test
```

### Шаг 4: Создание тестового файла

1. Создайте файл с тестами `tests/basic.spec.ts`.
2. Откройте этот файл в вашем любимом редакторе кода и добавьте следующий тест:

```ts
import { test, expect } from '@playwright/test';

test('has title', async ({ page }) => {
  await page.goto('https://playwright.dev/');

  // Expect a title "to contain" a substring.
  await expect(page).toHaveTitle(/Playwright/);
});

test('get started link', async ({ page }) => {
  await page.goto('https://playwright.dev/');

  // Click the get started link.
  await page.getByRole('link', { name: 'Get started' }).click();

  // Expects page to have a heading with the name of Installation.
  await expect(page.getByRole('heading', { name: 'Installation' })).toBeVisible();
});
```

### Шаг 5: Создание тестовой конфигурации

Создайте файл конфигурации для тестов `playwright.config.ts`:

```ts
import { defineConfig, devices } from '@playwright/test';

export default defineConfig({
  testDir: './tests',
  /* Run tests in files in parallel */
  fullyParallel: true,
  /* Fail the build on CI if you accidentally left test.only in the source code. */
  forbidOnly: !!process.env.CI,
  /* Retry on CI only */
  retries: process.env.CI ? 2 : 0,
  /* Opt out of parallel tests on CI. */
  workers: process.env.CI ? 1 : undefined,
  /* Reporter to use. See https://playwright.dev/docs/test-reporters */
  reporter: 'html',
  /* Shared settings for all the projects below. See https://playwright.dev/docs/api/class-testoptions. */
  use: {
    trace: 'on-first-retry',
  },
  /* Configure projects for major browsers */
  projects: [
    {
      name: 'chromium',
      use: { ...devices['Desktop Chrome'] },
    },
    {
      name: 'firefox',
      use: { ...devices['Desktop Firefox'] },
    },
    {
      name: 'webkit',
      use: { ...devices['Desktop Safari'] },
    },
  ],
});
```

### Шаг 6: Запуск тестов

Запустите тест:

```
npx playwright test
```

После выполнения скрипта в директории проекта появится файл `playwright-report/index.html`.

## Дополнительные материалы

-   [Официальная документация Playwright](https://playwright.dev/) предлагает глубокое понимание возможностей инструмента
-   [Playwright GitHub репозиторий](https://github.com/microsoft/playwright) содержит примеры кода и ответы на часто задаваемые вопросы

## Заключение

Поздравляем с созданием вашего первого проекта на Playwright! Вы успешно установили окружение и запустили свой первый тест. Это важный первый шаг в изучении автоматизации тестирования веб-приложений с помощью Playwright. Продолжайте изучать возможности Playwright, экспериментируйте с различными типами тестов и улучшайте свои навыки автоматизации.

## НАСТРОЙКА ТЕСТА

Установка

```
npm i && npx playwright install && npx playwright install-deps > /dev/null
```

Запуск

```
PW_TEST_HTML_REPORT_OPEN=never npx playwright test
```
