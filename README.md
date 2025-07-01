# 🧭 Fullstack Developer Knowledge Map

Этот репозиторий — структурированная шпаргалка для подготовки к техническим заданиям и собеседованиям на middle/senior позиции: frontend, backend, DevOps.

---

## 🔗 Быстрая навигация

- [1. JavaScript / TypeScript](#1-javascript--typescript)
- [2. Frontend: React / Next.js](#2-frontend-react--nextjs)
- [3. Backend: Node.js и современные практики](#3-backend-nodejs--современные-практики)
- [4. Общие навыки и DevOps](#4-общие-навыки-и-devops)
- [5. Как пользоваться репозиторием](#5-как-пользоваться-репозиторием)
- [6. Внесение вклада (Contributing)](#6-внесение-вклада-contributing)

---

## 1. JavaScript / TypeScript

- **Прототипы:**  
  Понимание цепочки прототипов, отличие от классов, пример:
  ```js
  function A() {}
  A.prototype.sayHi = () => console.log('hi');
  ```
- **Замыкания:**  
  Что такое лексическая область видимости, пример инкремента:
  ```js
  function makeCounter() { let n=0; return ()=>++n; }
  ```
- **Асинхронность:**  
  Promise, async/await, event loop, разница между micro/macro-task.
- **Модули (import/export):**  
  Когда использовать default export, когда именованный.
- **Современные возможности ES6+:**  
  Деструктуризация, spread/rest, стрелочные функции.
- **TypeScript:**  
  Типы, interface vs type, generics, utility types (`Partial`, `Pick`).
- **Type Guards:**  
  Проверка и сужение типа, пример:
  ```ts
  function isString(val: unknown): val is string { return typeof val === 'string'; }
  ```
- **Тестирование:**  
  Юнит-тесты (Jest), TDD/BDD, тестирование асинхронного кода.

---

## 2. Frontend: React / Next.js

- **React (хуки, архитектура):**
  - useState, useEffect, useCallback, useMemo, useContext, useRef.
  - Оптимизация: React.memo, Suspense, lazy loading.
  - Архитектурные паттерны: HOC, render props, контейнерные/презентационные компоненты.
- **Жизненный цикл:**
  - Side-effects, очищение эффектов, Error Boundaries.
- **Next.js (SSR / CSR / ISR / SSG):**
  - SSR (getServerSideProps), SSG (getStaticProps), ISR (revalidate), динамический роутинг.
- **Работа с формами:**  
  Formik/React Hook Form, yup/zod для валидации, контролируемые/неконтролируемые компоненты.
- **Управление состоянием:**  
  Context API, Redux Toolkit, Zustand, middleware (redux-thunk, saga).
- **Адаптивная вёрстка:**  
  CSS/SCSS, styled-components/Emotion, Tailwind, mobile-first, media queries.
- **Взаимодействие с backend:**  
  REST/GraphQL, axios/fetch/Apollo, авторизация (JWT, httpOnly cookies), кэширование (SWR, React Query).
- **Тестирование:**  
  Jest, Testing Library, Cypress/Playwright, msw (mock сервисы).

---

## 3. Backend: Node.js и современные практики

- **Node.js (экосистема, паттерны):**
  - Асинхронность, event loop, streams, buffer.
  - Express/Fastify/Koa, middleware, REST API.
  - JWT, OAuth, session/cookie, refresh-токены.
  - Централизованный error handling, логирование (winston/pino).
- **Архитектура и масштабирование:**
  - SOLID, CQRS, DDD, сервисный слой, микросервисы, очереди (RabbitMQ, Kafka), WebSocket.
- **Базы данных:**
  - Реляционные (PostgreSQL/MySQL), NoSQL (MongoDB/Redis), ORM/ODM (Prisma, TypeORM, Mongoose), транзакции, миграции.
- **Тестирование и CI/CD:**
  - Модульные, интеграционные, контрактные тесты, mock-данные, Testcontainers, CI/CD (GitHub Actions, Docker, Kubernetes).
- **Безопасность:**
  - Валидация данных, XSS, CSRF, SQL/NoSQL injection, HTTPS, CORS, security headers, rate limiting.

---

## 4. Общие навыки и DevOps

- **Git, workflow:**  
  GitFlow, trunk-based, code review, мерж-конфликты.
- **Docker, docker-compose, основы Kubernetes:**  
  Контейнеризация, написание Dockerfile, деплой, оркестрация.
- **CI/CD:**  
  Автоматизация тестов и деплоя, пайплайны.
- **Мониторинг и логирование:**  
  Prometheus, Grafana, Sentry.
 

---

## 5. Как пользоваться репозиторием

- Изучайте разделы последовательно или по интересующим темам.
- В каждом разделе ищите примеры, best practices, вопросы для самопроверки.
- Используйте шпаргалку перед собеседованиями, ревью или планированием обучения.

---

## 6. Внесение вклада (Contributing)

- Форкайте репозиторий, создавайте pull request с пояснением изменений.
- Добавляйте новые темы, примеры, тестовые задания.
- Участвуйте в обсуждениях и обновлении содержания.

