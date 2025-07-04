# Backend: Node.js и современные практики — Теория и Практика

## Node.js: Асинхронность, Event Loop, Streams, Middleware
Node.js — это среда выполнения JavaScript вне браузера, построенная на движке V8. Она предназначена для создания высокопроизводительных сетевых приложений, особенно серверов и API.

**Асинхронность** — ключевая особенность Node.js. Большинство операций ввода-вывода (чтение файлов, сетевые запросы, работа с БД) выполняются неблокирующе, то есть не останавливают выполнение программы. Это достигается через колбэки, промисы и async/await. Асинхронность позволяет обслуживать тысячи одновременных соединений без создания отдельных потоков для каждого клиента.

**Event Loop** — механизм, который управляет обработкой событий и асинхронных задач. В Node.js есть одна основная нить исполнения, которая последовательно обрабатывает события из очереди. Когда асинхронная операция завершается, её колбэк помещается в очередь событий, и event loop вызывает его, когда основной поток свободен. Это позволяет эффективно использовать ресурсы, но требует аккуратного обращения с CPU-bound задачами (долгие вычисления могут "заморозить" event loop).

**Streams** — абстракция для работы с потоками данных (например, чтение файлов, сетевые соединения). Позволяют обрабатывать данные по частям, не загружая всё в память. Существуют readable, writable, duplex и transform streams. Streams используются для передачи больших файлов, обработки логов, проксирования данных и др. Преимущества: экономия памяти, возможность обработки данных "на лету".

**Middleware** — это промежуточные обработчики HTTP-запросов, которые формируют цепочку обработки в серверных фреймворках (например, Express, Koa, Fastify). Каждый middleware получает на вход объект запроса (req), ответа (res) и функцию next(), которую вызывает для передачи управления следующему обработчику в цепочке.

### Виды middleware:
- **Глобальные** — применяются ко всем маршрутам (например, логирование, CORS, парсинг тела запроса).
- **Маршрутные** — применяются только к определённым маршрутам (например, аутентификация для /admin).
- **Обрабатывающие ошибки** — имеют 4 параметра (err, req, res, next) и вызываются при ошибках в цепочке.
- **Встроенные** — предоставляются фреймворком (например, express.json()).
- **Пользовательские** — реализуются разработчиком для специфических задач.

### Жизненный цикл и порядок выполнения:
- Запрос проходит через цепочку middleware в порядке их подключения (app.use/app.get и т.д.).
- Каждый middleware может:
  - Изменить req/res (например, добавить поле, изменить заголовки).
  - Прервать цепочку (отправить ответ сразу).
  - Передать управление дальше (вызвать next()).
- Если ни один middleware не отправил ответ, запрос "зависнет" — важно всегда вызывать next() или завершать ответ.

### Типичные сценарии применения:
- Аутентификация и авторизация (проверка токенов, прав доступа).
- Логирование запросов и ошибок.
- Парсинг тела запроса (JSON, form-data).
- Кэширование ответов.
- Rate limiting (ограничение частоты запросов).
- Обработка ошибок (единая точка для логирования и возврата ошибок клиенту).

### Best practices:
- Минимизировать логику в middleware, выносить бизнес-логику в сервисы.
- Не забывать вызывать next() или завершать ответ.
- Использовать отдельный middleware для обработки ошибок.
- Сохранять порядок подключения (например, логирование — до роутинга, обработка ошибок — в конце).
- Не хранить состояние между запросами в middleware (использовать req/res или внешние хранилища).

### Типичные ошибки проектирования:
- Забыли вызвать next() — запрос "зависает".
- Слишком много логики в middleware — усложняет поддержку.
- Нарушение порядка подключения — некорректная обработка (например, CORS после роутинга).
- Необработанные ошибки — приложение падает или возвращает неинформативные ответы.

### Роль в Express и других фреймворках:
- В Express middleware — основа архитектуры, позволяет строить расширяемые и поддерживаемые приложения.
- В Koa middleware реализованы через async/await и поддерживают "обратный поток" (downstream/upstream).
- В Fastify middleware называются hooks и имеют схожую концепцию.

## Архитектура и масштабирование

**Чистая архитектура (Clean Architecture)** — подход к проектированию ПО, при котором бизнес-логика отделена от инфраструктуры (БД, UI, внешних сервисов). Основная идея — зависимость направлена внутрь: внешние слои зависят от внутренних, но не наоборот. Это облегчает тестирование, поддержку и масштабирование.

**SOLID** — пять принципов объектно-ориентированного проектирования:
- **S** (Single Responsibility) — каждый модуль/класс отвечает за одну задачу.
- **O** (Open/Closed) — модули открыты для расширения, но закрыты для изменения.
- **L** (Liskov Substitution) — подклассы могут использоваться вместо базовых классов без ошибок.
- **I** (Interface Segregation) — лучше много маленьких интерфейсов, чем один большой.
- **D** (Dependency Inversion) — зависимости строятся через абстракции, а не через конкретные реализации.
SOLID повышает гибкость, расширяемость и тестируемость кода.

**CQRS (Command Query Responsibility Segregation)** — разделение операций чтения (Query) и записи (Command) в системе. Позволяет оптимизировать производительность, масштабировать чтение и запись независимо, использовать разные модели данных для чтения и записи. Применяется в сложных бизнес-системах, микросервисах.

**DDD (Domain-Driven Design)** — подход, при котором архитектура строится вокруг бизнес-домена (предметной области). Включает понятия: сущности, агрегаты, value objects, репозитории, сервисы домена. DDD помогает создавать гибкие, масштабируемые и понятные системы, но требует тесного взаимодействия с экспертами предметной области.

**DTO (Data Transfer Object)** — объекты для передачи данных между слоями приложения или между сервисами. DTO не содержат бизнес-логики, только данные. Используются для оптимизации передачи данных, обеспечения безопасности (скрытие лишних полей), сериализации.

**Сервисный слой (Service Layer)** — слой, реализующий бизнес-логику приложения. Отделяет бизнес-логику от контроллеров и инфраструктуры, облегчает тестирование и повторное использование кода.

**Репозитории (Repository Pattern)** — абстракция для доступа к данным. Репозиторий инкапсулирует логику хранения, поиска, обновления и удаления данных, позволяя менять источник данных (БД, API) без изменения бизнес-логики.

**Микросервисы** — архитектурный стиль, при котором приложение состоит из набора независимых сервисов, каждый из которых реализует отдельную бизнес-функцию. Сервисы общаются по сети (обычно через HTTP/gRPC, очереди). Плюсы: независимое масштабирование, изоляция ошибок, гибкость в выборе технологий. Минусы: сложность в развертывании, мониторинге, межсервисных коммуникациях.

**Очереди (RabbitMQ, Kafka)** — системы обмена сообщениями между сервисами. Позволяют реализовать асинхронную обработку задач, балансировку нагрузки, надёжную доставку сообщений. RabbitMQ — брокер сообщений с поддержкой различных шаблонов маршрутизации. Kafka — распределённый лог событий, оптимизирован для высокой пропускной способности и хранения больших объёмов данных.

**WebSocket** — протокол для двусторонней связи между клиентом и сервером в реальном времени. Используется для чатов, онлайн-игр, уведомлений. Позволяет серверу отправлять данные клиенту без запроса.

**Фоновые задачи (background jobs)** — задачи, которые выполняются вне основного потока обработки запросов (например, отправка email, обработка изображений, интеграция с внешними сервисами). Реализуются через очереди, worker-процессы, планировщики (cron). Позволяют разгрузить основной поток и повысить отзывчивость приложения.

**Пример (слой сервисов):**
```js
class UserService {
  getUser(id) { /* ... */ }
}
```

## Базы данных: виды, нормализация, оптимизация
### Виды баз данных
- **Реляционные БД (SQL):** Структурированные таблицы, поддержка транзакций, строгая схема (PostgreSQL, MySQL, Oracle, MS SQL Server).
- **NoSQL БД:** Гибкая схема, горизонтальное масштабирование, разные типы хранения (документные — MongoDB, ключ-значение — Redis, графовые — Neo4j, колоночные — Cassandra).
- **NewSQL:** Совмещают преимущества реляционных и NoSQL (Google Spanner, CockroachDB).
- **Графовые БД:** Для хранения и обработки графовых структур (Neo4j, ArangoDB).
- **In-memory БД:** Для сверхбыстрого доступа к данным (Redis, Memcached).

### Теория нормализации
- **1NF (Первая нормальная форма):** Все значения в таблице атомарны, нет повторяющихся групп и массивов.
- **2NF (Вторая нормальная форма):** Таблица в 1NF, все неключевые атрибуты зависят от всего первичного ключа (актуально для составных ключей).
- **3NF (Третья нормальная форма):** Таблица в 2NF, нет транзитивных зависимостей между неключевыми атрибутами.
- **BCNF (Форма Бойса-Кодда):** Более строгая версия 3NF, каждая детерминирующая зависимость — ключ.
- **4NF (Четвёртая нормальная форма):** Нет многозначных зависимостей, таблица в BCNF.
- **Денормализация:** Иногда используется для ускорения чтения, но увеличивает избыточность.

### Индексация и оптимизация
- **Индексы** ускоряют поиск, но замедляют вставку/обновление. Важно индексировать только часто используемые поля.
- **Составные индексы** — для сложных запросов с несколькими условиями.
- **Покрывающие индексы** — содержат все поля, необходимые для запроса.
- **Анализировать планы выполнения** (EXPLAIN) для поиска узких мест.
- **Кэширование** результатов запросов для ускорения повторных обращений.
- **Шардирование** — горизонтальное разделение данных для масштабирования.
- **Репликация** — копирование данных для отказоустойчивости и масштабирования чтения.

### Best practices и типичные ошибки
- Проектировать схему под реальные запросы, а не только под предметную область.
- Не использовать SELECT * в production.
- Следить за размером транзакций и блокировками.
- Регулярно проводить аудит индексов и запросов.
- Не хранить большие бинарные данные (файлы) в БД без необходимости.
- Для NoSQL: внимательно относиться к денормализации и размеру документов.
- Для реляционных: избегать избыточных связей и циклических зависимостей.

## Работа с БД
Реляционные базы данных (PostgreSQL, MySQL) — это системы управления данными, основанные на таблицах с чётко определённой схемой, поддержкой транзакций (ACID), связями между таблицами (foreign keys) и мощным языком запросов SQL. Они обеспечивают целостность данных, позволяют реализовывать сложные связи и обеспечивают высокую надёжность при работе с критичными бизнес-данными.

NoSQL базы данных (MongoDB, Redis) — это класс СУБД, ориентированных на гибкость схемы, горизонтальное масштабирование и высокую производительность при работе с большими объёмами данных. Документные БД (MongoDB) хранят данные в формате JSON-подобных документов, что удобно для хранения вложенных структур. Ключ-значение БД (Redis) обеспечивают сверхбыстрый доступ к данным и часто используются для кэширования и хранения сессий.

Транзакции — это механизм, гарантирующий, что группа операций с данными будет выполнена полностью или не выполнится вовсе (атомарность). В реляционных БД транзакции реализуют свойства ACID (Atomicity, Consistency, Isolation, Durability), что критично для финансовых и других чувствительных систем. В NoSQL поддержка транзакций ограничена или реализована иначе (например, только на уровне документа).

Индексация — способ ускорения поиска и выборки данных за счёт создания специальных структур (индексов) по ключевым полям таблиц или коллекций. Индексы повышают скорость чтения, но могут замедлять операции записи и требуют дополнительного места на диске. Важно анализировать, какие поля индексировать, чтобы не перегружать систему.

Оптимизация запросов включает в себя анализ и переписывание SQL-запросов для уменьшения времени выполнения, использование индексов, минимизацию количества обращений к БД, отказ от SELECT * в пользу выборки только нужных полей, а также анализ планов выполнения запросов (EXPLAIN). Для NoSQL — проектирование структуры документов под реальные сценарии чтения.

Миграции — это управляемый процесс изменения схемы базы данных (создание, изменение, удаление таблиц, полей, индексов) с сохранением целостности и истории изменений. Миграции позволяют синхронизировать структуру БД между разными средами (разработка, тест, продакшн) и обеспечивают воспроизводимость инфраструктуры данных.

## Тестирование и CI/CD

**Модульные тесты (unit tests)** — проверяют отдельные функции, классы или модули в изоляции от остальной системы. Цель — убедиться, что каждый компонент работает корректно независимо от других. Плюсы: быстрое выполнение, простота локализации ошибок, поддержка рефакторинга. Минусы: не выявляют ошибки интеграции между модулями.

**Интеграционные тесты (integration tests)** — проверяют взаимодействие между несколькими модулями или компонентами (например, контроллер + сервис + БД). Цель — убедиться, что компоненты корректно работают вместе. Плюсы: выявляют ошибки на стыке модулей, ближе к реальным сценариям. Минусы: сложнее поддерживать, медленнее выполняются.

**Контрактные тесты (contract tests)** — проверяют соответствие взаимодействия между сервисами (например, frontend и backend, микросервисы) заранее согласованному контракту (API, формат данных). Используются для предотвращения ошибок интеграции при независимой разработке сервисов. Плюсы: повышают надёжность интеграций, позволяют разрабатывать сервисы независимо. Минусы: требуют поддержки контрактов, сложнее автоматизировать.

**Mock-данные** — искусственно созданные данные, которые подставляются вместо реальных зависимостей (БД, внешние сервисы) для изоляции тестов. Используются для ускорения тестирования, проверки крайних случаев, эмуляции ошибок.

**Testcontainers** — инструмент для запуска реальных зависимостей (БД, брокеров сообщений) в изолированных контейнерах во время тестов. Позволяет проводить интеграционные тесты в условиях, максимально приближённых к production, без необходимости ручной настройки окружения.

**CI/CD (Continuous Integration / Continuous Delivery/Deployment)** — автоматизация процессов сборки, тестирования и доставки кода. CI запускает тесты и проверки при каждом коммите, предотвращая попадание ошибок в основную ветку. CD автоматизирует выкладку приложения на серверы или в облако. Плюсы: ускоряет выпуск новых версий, снижает количество ошибок, обеспечивает воспроизводимость. Минусы: требует настройки пайплайнов, инфраструктуры, мониторинга.

### Примеры сценариев применения:
- Unit: тестирование бизнес-логики (например, расчёт скидки).
- Integration: проверка работы API с реальной БД.
- Contract: проверка, что backend возвращает данные в ожидаемом формате для frontend.
- Mock: тестирование обработки ошибок внешнего сервиса без реального вызова.
- Testcontainers: запуск PostgreSQL в контейнере для интеграционных тестов.
- CI/CD: автоматический запуск тестов и деплой после каждого pull request.

## Безопасность
Валидация входных данных, защита от XSS, CSRF, SQL/NoSQL injection, HTTPS, CORS, security headers, rate limiting.

 