# Торговые стратегии на основе "Debut ™ / Community Edition"

Debut - это экосистема для разработки и запуска торговых стратегий. Аналог известного `ZenBot`, но с гораздо более гибкими возможностями для конструирования стратегий. Все что вам нужно сделать, это придумать и описать точки входа в рынок и подключить нужные [плагины](https://github.com/debut-js/Plugins) для работы. Все остальное - дело техники: **генетические алгоритмы** - помогут подобрать самые эффективные параметры для стратегии (период, стопы, и другие), **модуль подбора тикеров** - поможет найти подходящий для стратегии актив (токен или акцию), на котором она будет работать лучше всего.

В основе Debut лежит архитектура ядра и надстраиваемых плагинов, позволяющих гибко кастомизировать любые решения. Оснвной целью всей экосистемы Debut, является упрощение процесса создания и запуска рабочих торговых роботов на различные биржи. На данный момент поддерживаются: **Тинькофф Инвестици** и **Binance**.

В проекте есть две стартовые торговые стратегии "Для примера" как нужно работать с системой.

Пример работы стратегии [SpikesG](/src/strategies/spikes-grid/ReadMe.md) за 200 дней. Оптимизация проводилась за 180 дней и 20 дней свободной работы на необученных данных.
Использовался стартовый депозит в размере *500$*

<p align="center"><img src="/src/strategies/spikes-grid/img/BATUSDT.png" width="800"></p>

Статистика стратегии собиралась на основе плагина [статистики](https://github.com/debut-js/Plugins/tree/master/packages/stats), по ссылке можно подробнее узнать о значении некоторых статистических данных.

Визуализация выполнена с помощью плагина [Report](https://github.com/debut-js/Plugins/tree/master/packages/report).

## Community edition
Мы верим в силу сообщества! Именно поэтому решили опубликовать проект. Комьюнити версия бесплатная, но имеет некоторые ограничения в коммерческом использовании (доход от торговли стартегий не является коммерцией), а также технические отличия в тестировании стратегий. Присоединяйтесь к комьюнити, вступайте в **[чат разработчиков](https://t.me/joinchat/Acu2sbLIy_c0OWIy)**

## Enterprise edition
Энтерпрайз версия - это готовый набор инструментария для "больших дядек", для тех, кто занимается услугами торговли или создания стратегий профессионально. Здесь есть всё! И это всё уже готово работать на вас и на повышение скорости вашей разработки.


|         Функционал                  |            Community                |                              Enterprise                             |
| ----------------------------------- | ----------------------------------- | ------------------------------------------------------------------- |
| Тестер стратегий | ✅ | ✅ |
| Эмуляция OHLC тиков в тестере | ✅ | ✅ |
| Моудль поиска (finder) подходящих под стратегию активов | ✅ | ✅ |
| Набор плагинов из [коллекции](https://github.com/debut-js/Plugins) | ✅ | ✅ |
| Базовый набор готовых торговых стратегий | ✅  | ✅ |
| Данные свеч м1 для эмуляция тиков | ❌ | ✅ |
| Синтетическая эмуляция тиков в тестере (размер тика не более 0.75%) | ❌ | ✅ |
| Система управления рисками | ❌ | ✅ |
| Отчеты о работе в [мессенджер](https://t.me/debutjs) | ❌ | ✅ |
| Готовые решения для запуска на VPS/VDS и Cloud серверах | ❌ | ✅ |
| Техническая поддержка | ❌ | ✅ |
| Не ограниченое кол-во подключений TCP на Тинькофф API ([о лимитах](https://tinkoffcreditsystems.github.io/invest-openapi/marketdata/)) | ❌ | ✅ |

Мы ведем прямой эфир сделок на основе Enterprise решения в нашем [телеграмм канале](https://t.me/debutjs)
**Узнайте цену, отправив запрос на [sales@debutjs.io](mailto:sales@debutjs.io)**

# Начало работы
Все что нужно знать, для запуска и разработки собственных решений на основе Debut.

## Системные требования
Для работы вам потребуется [NodeJS 14.x.x / npm 7.x.x](https://nodejs.org/en/) ([инструкция по установке](https://htmlacademy.ru/blog/boost/tools/installing-nodejs))

## Файловая структура проекта

```
|-- .tokens.json - пользовательские токены доступа для работы с биржей
|-- schema.json - описание расположения файлов запуска
|-- public/ - папка для отчетов finder (создается при запуске finder)
|-- src/
    |-- strategies/
        |-- strategy1/ - директория стратегий
            |-- bot.ts - Реализация стратегии
            |-- meta.ts - Мета данные, для запуска и для оптимизации
            |-- cfgs.ts - Конфигурации, для запуска в tester и genetic
        |-- strategy2/
        ...

```

# Установка и настройка

### Получение токенов API

[Инструкция Binance](https://www.binance.com/ru/support/faq/360002502072)

[Инструкция Tinkoff](https://tinkoffcreditsystems.github.io/invest-openapi/auth/#_2)

### Установка токенов
Для работы необходимо создать файл .tokens.json, в него добавить токен для работы.

Для Тинькофф:

```json
{
    "tinkoff": "YOU_TOKEN"
}
```

Для Binance:
```json
{
    "binance": "YOU_TOKEN",
    "binanceSecret": "YOU_SECRET
}
```

Можно использовать любое название поля для токена, подробнее в разделе [документации о настройках токенов]().

## Установка npm пакетов
Для установки пакетов выполните:
```bash
npm install
```

## Сборка проекта
```bash
npm run compile
```

*Рекомендуется выполнять сборку перед каждым запуском тестирования*

`npm run compile && npm run ...`
## Запуск тестирования на исторических данных
Исторические данные будут загружаться автоматически при запуске. Все загружаемые данные сохраняются в папку `history` в корне проекта, затем переиспользуются.

**Перед запуском стоит убедиться:**
* В файле `cfgs.ts` есть нужный вам тикер
* Для получения истории в файле `.tokens.json` может требоваться токен
* История акции или токена существует в запрашиваемом количестве дней

Для запуска выполните команду:
```bash
npm run testing -- --bot=FTBot --ticker=CRVUSDT --days=200 --gap=20 --amount=500
```

Для просмотра результатов тестирования в браузере выполните
```bash
npm run serve
```

Результаты будут доступны для просмотра на `http://localhost:5000/`

Подробрее о параметраз запуска тестирования можно прочитать в [документации]()

## Запуск генетической оптимизации

Выполните команду:
```bash
npm run genetic -- --bot=FTBot --ticker=CRVUSDT --days=200 --gap=30 --gen=12 --pop=2000 --log
```

Подробрее о параметрах запуска генетика можно прочитать в [документации]()

После запуска с параметром --log, генетик будет выдавать данные в консоль

```bash
Binance history loading from Wed Nov 18 2020 03:00:00 GMT+0300 (Moscow Standard Time)...

----- Genetic Start with 17314 candles -----

Generation:  0
Generation time:  5.15 s
Stats:  {
  population: 100,
  maximum: 20.8,
  minimum: -1.24,
  mean: 2.5174,
  stdev: 3.8101996325652054
}
Generation:  1
...
```

## Запуск генетической оптимизации с перебором тикеров/токенов
Выполните команду:
```bash
npm run finder -- --bot=FTBot --ticker=CRVUSDT --days=200 --gap=30 --gen=12 --pop=2000 --log
```
Используйте опцию `--crypt`, чтобы брать крипто-пары из файла `./crypt.json` (По умаолчанию там актуальные кросс-маржинальные пары Binance)

По умолчанию для потоковой оптимизации используется набор тикеров акций из файла `stocks.json`

Подробрее о параметрах запуска потокового генетика можно прочитать в [документации]()

## Запуск стратегии

Установите любой процесс менеджер для NodeJS, например PM2

```bash
npm install -g pm2
```

Выполните команду запуска, путь к файлу запуска стратегии в директории `./out`.
Пример такого файла можно найти здесь `/src/bootstrap.ts`

```bash
pm2 start ./out/bootstrap.js
```

Далее для работы и мониторинга можно использовать набор команд `pm2`

`pm2 list` - список активных процессов
`pm2 delete $pid` - остановка процесса
и другие команды, о которых можно прочитать в документации процесс менеджера
