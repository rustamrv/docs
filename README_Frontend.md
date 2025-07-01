# Frontend: React / Next.js — Теория и Практика

## React: Хуки, Архитектура, Оптимизация
**Хуки** позволяют использовать состояние и другие возможности React без классов. Основные: useState (состояние), useEffect (эффекты), useCallback/useMemo (оптимизация), useRef (доступ к DOM), useContext (глобальные данные).

**Пример (useState):**
```js
const [count, setCount] = useState(0);
```

**Архитектурные паттерны**: HOC, render props, контейнерные/презентационные компоненты — для разделения ответственности и переиспользования логики.

**Оптимизация**: React.memo, Suspense, lazy loading, code splitting — для повышения производительности и уменьшения времени загрузки.

## Жизненный цикл компонента
В функциональных компонентах жизненный цикл реализуется через useEffect. Важно очищать ресурсы (например, слушатели событий) для предотвращения утечек памяти.

**Пример:**
```js
useEffect(() => {
  window.addEventListener('resize', handler);
  return () => window.removeEventListener('resize', handler);
}, []);
```

## Next.js: SSR, CSR, ISR, SSG
- **SSR** (Server-Side Rendering): серверный рендеринг для SEO и быстрой загрузки. Используется getServerSideProps.
- **CSR** (Client-Side Rendering): рендеринг на клиенте, подходит для динамических интерфейсов.
- **ISR** (Incremental Static Regeneration): обновление статических страниц по таймеру (revalidate).
- **SSG** (Static Site Generation): генерация статических страниц на этапе сборки (getStaticProps).

**Пример (getServerSideProps):**
```js
export async function getServerSideProps() {
  return { props: { time: Date.now() } };
}
```

## Работа с формами
Formik, React Hook Form — для управления состоянием и валидацией форм. Контролируемые компоненты используют state, неконтролируемые — ref.

**Пример (React Hook Form):**
```js
const { register, handleSubmit } = useForm();
<form onSubmit={handleSubmit(data => console.log(data))}>
  <input {...register('name')} />
</form>
```

## Управление состоянием
Context API, Redux Toolkit, Zustand — для глобального состояния. Middleware (redux-thunk, redux-saga) — для асинхронных действий и логирования.

**Пример (Context):**
```js
const ThemeContext = React.createContext('light');
```

## Адаптивная и современная вёрстка
CSS/SCSS, CSS-in-JS (styled-components, Emotion), Tailwind. Mobile-first подход: сначала стили для мобильных, затем media queries для десктопа.

**Пример (styled-components):**
```js
import styled from 'styled-components';
const Button = styled.button`
  color: white;
`;
```

## Взаимодействие с backend
REST/GraphQL (axios, fetch, Apollo Client), авторизация (JWT, OAuth), кэширование (SWR, React Query).

**Пример (fetch):**
```js
fetch('/api/data').then(res => res.json());
```

## Тестирование
Unit (Jest, Testing Library), E2E (Cypress, Playwright), mock-сервисы (msw).

**Пример (Testing Library):**
```js
import { render, screen } from '@testing-library/react';
render(<button>Click</button>);
expect(screen.getByText('Click')).toBeInTheDocument();
``` 