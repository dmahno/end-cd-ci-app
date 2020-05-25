### Для запуска серверной части в prod (c поддержкой SSR)

- Добавить в файл `.env` API_TOKEN - ключ авторизации к API
- Запустить `npm run start`
- Перейти по адресу `http://127.0.0.1:3000/`

### Для сборки клиенсткой части в prod (с поддержкой SSR)

- Запустить сборку коммандой `npm run build:client`

## Development

### Для запуска серверной части проекта в development режиме

- Добавить в файл `.env` API_TOKEN - ключ авторизации к API
- Запустить сервер `npm run start:server`
- Перейти по адресу `http://127.0.0.1:3000/`

### Для запуска клиенсткой части проекта в development режиме

- Запустить webpack-dev-server `npm run start:client`
- Перейти по адресу `http://127.0.0.1:3000/`

## Тестирование

### e2e тесты

- Установить [selenium-standalone](https://github.com/vvo/selenium-standalone#install--run)
- Запустить selenium сервер `npm run test:selenium`
- Запустить приложение `npm run start`
- Запустить e2e тесты `npm run test:e2e`

### unit тесты

- Запустить unit тесты для сервера `npm run test:server`

### Cценарии проверяемые интеграционными тестами

Главная страница (`http://127.0.0.1:3000/settings`)
Страница настроек (`http://127.0.0.1:3000/settings`):
Страница сборки (`http://127.0.0.1:3000/build/{buildId}`):

## Типизация

- Какие в процессе перевода были найдены ошибки.

  Проверки на возможные значения `undefined`.

- Решили ли вы вливать данный PR, или предпочитаете работать с JavaScript? Почему?

  В процессе

## Локализация

Для локализации использовалась библиотека [i18next](https://www.i18next.com) с расширениями для определения используемой пользователем локализации.

- Как приложение узнает, какой язык выбран у пользователя?
  Модуль [i18next-browser-languageDetector](https://github.com/i18next/i18next-browser-languageDetector) определяет выбранную локализацию по следующим принципам:

  - проверка ключа `i18next` в `cookie`, или
  - проверка ключа `i18nextLng` в `localStorage`, или;
  - обращается к объекту `navigator`

  При изменении языка выбранная пользователем локализация кэшируется в `cookie` / `localStorage`.

- Какие типы контента поддерживают переключение языка и как вы это реализовали?

  Локализация строк и дат. Локализация строк происходит в рантайме по принципу поиска по ключу сроки с учетом выбранной пользователем локализации (Для локализации используется хук [useTranslate](https://react.i18next.com/latest/usetranslation-hook)). Для локализации дат используется [date-fns](https://date-fns.org/v1.30.1/docs/format) с передачей соответствующей локализации функции форматирования дат.

- Как переводы попадают на клиент? как изменилась сборка приложения?

  Переводы хранятся на сервере в виде статических ресурсов (директория `locales`) и подгружаются в рантайме по требованию модулем [i18next-http-backend](https://github.com/i18next/i18next-http-backend) в зависимости от выбранной локали или при переключении языка приложения.