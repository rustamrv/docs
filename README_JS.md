# Must have знания по JS и TS

## JavaScript (JS)
- **Прототипное наследование**: цепочка прототипов, отличие классов ES6 от функций-конструкторов
- **Замыкания**: область видимости, лексическое окружение
- **Асинхронность**: event loop, micro/macro tasks, промисы, async/await, обработка ошибок
- **Работа с this**: bind/call/apply, потеря контекста
- **Модули**: import/export, отличие от CommonJS
- **Современный синтаксис (ES6+)**: деструктуризация, spread/rest, стрелочные функции, let/const
- **Работа с массивами**: map, filter, reduce, find, every, some
- **Работа с объектами**: копирование, сравнение, Object.assign, spread
- **Линтинг, форматирование, строгий режим ('use strict')**
- **Типичные ошибки**: забыли обработать ошибку в промисе, неправильное использование this, дублирование кода, неэффективная работа с коллекциями
- **Best practices**: чистые функции, минимизация побочных эффектов, избегать глобальных переменных, писать читаемый и поддерживаемый код

## TypeScript (TS)
- **Явное объявление типов**: переменных, параметров, возвращаемых значений
- **Интерфейсы и типы**: отличие, расширение, объединение, alias
- **Generics**: универсальные функции и классы
- **Type guards**: пользовательские проверки типов
- **Strict-режимы**: strict, noImplicitAny, strictNullChecks
- **Utility types**: Partial, Pick, Omit, Readonly и др.
- **Работа с union/intersection types**
- **Типизация массивов, кортежей, enum**
- **Работа с any, unknown, never, void**
- **Интеграция с JS-библиотеками, типы DefinitelyTyped**
- **Best practices**: избегать any, явно типизировать публичные API, поддерживать актуальность tsconfig.json, использовать readonly для неизменяемых структур
- **Типичные ошибки**: чрезмерное использование any, игнорирование ошибок компилятора, неправильное сужение типов, отсутствие строгих режимов

---

# JavaScript / TypeScript: Теория и Практика

## Прототипы
**Теория:** Прототипное наследование — фундамент JS. Каждый объект имеет скрытое свойство [[Prototype]], по которому строится цепочка поиска свойств. ES6-классы — синтаксический сахар над прототипами.

**Пример:**
```js
function Animal(name) { this.name = name; }
Animal.prototype.sayHi = function() { return `Hi, I'm ${this.name}`; };
const dog = new Animal('Rex');
dog.sayHi(); // 'Hi, I'm Rex'
```

**Типичные ошибки:**
- Определение методов внутри конструктора (дублирование)
- Потеря цепочки прототипов при наследовании

**Вопросы для самопроверки:**
- Как работает цепочка прототипов?
- Чем отличается класс ES6 от функции-конструктора?

**Ресурсы:** [MDN Prototypes](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/Object_prototypes)

---

## Замыкания
**Теория:** Замыкание — функция, "запоминающая" область видимости, в которой была создана. Используется для приватных переменных, модулей, итераторов.

**Пример:**
```js
function counter() { let count = 0; return () => ++count; }
const inc = counter(); inc(); // 1
```

**Типичные ошибки:**
- Утечки памяти из-за замыкания больших объектов
- Неожиданное поведение в циклах (var vs let)

**Вопросы для самопроверки:**
- Как замыкания влияют на сборку мусора?
- Как реализовать приватные переменные через замыкание?

**Ресурсы:** [MDN Closures](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures)

---

## Асинхронность
**Теория:** Асинхронность реализуется через event loop, очереди micro/macro tasks, промисы, async/await. Важно различать порядок выполнения, уметь обрабатывать ошибки.

**Пример:**
```js
setTimeout(() => console.log('timeout'), 0);
Promise.resolve().then(() => console.log('promise'));
console.log('sync'); // sync -> promise -> timeout
```

**Типичные ошибки:**
- Необработанные ошибки в промисах
- Путаница между micro/macro tasks
- Забыли await для async-функции

**Вопросы для самопроверки:**
- Как работает event loop?
- Чем отличаются microtasks и macrotasks?
- Как ловить ошибки в async/await?

**Ресурсы:** [MDN Event Loop](https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop)

---

## Современные возможности языка (ES6+)
**Теория:** Деструктуризация, spread/rest, стрелочные функции, let/const, модули, новые коллекции (Map, Set), optional chaining, nullish coalescing.

**Пример:**
```js
const {a, ...rest} = {a: 1, b: 2};
const arr = [1, 2, 3];
const [first, ...others] = arr;
```

**Типичные ошибки:**
- Использование var вместо let/const
- Ошибки при деструктуризации undefined/null

**Вопросы для самопроверки:**
- Как работает деструктуризация?
- В чём разница между import/export и require/module.exports?

**Ресурсы:** [MDN ES6 Features](https://developer.mozilla.org/en-US/docs/Web/JavaScript)

---

## TypeScript: основы и примеры
**Теория:** TS — надстройка над JS, добавляющая статическую типизацию, интерфейсы, generics, строгие режимы, utility types.

**Примеры:**
```ts
// Типизация переменных и функций
let age: number = 30;
function greet(name: string): string { return `Hello, ${name}`; }

// Интерфейсы и типы
interface User { id: number; name: string; }
type Status = 'active' | 'inactive';
const user: User = { id: 1, name: 'Ann' };

// Generics
function identity<T>(value: T): T { return value; }
const num = identity<number>(42);

// Type guards
function isString(val: unknown): val is string { return typeof val === 'string'; }

// Utility types
interface Task { id: number; title: string; completed: boolean; }
const update: Partial<Task> = { completed: true };
```

**Типичные ошибки:**
- Чрезмерное использование any
- Игнорирование ошибок компилятора
- Неправильное сужение типов

**Вопросы для самопроверки:**
- Чем отличается interface от type?
- Как работают generics?
- Как включить strict-режимы?

**Ресурсы:** [TypeScript Handbook](https://www.typescriptlang.org/docs/)

---

## Оглавление

- [Базовые понятия JS](#базовые-понятия-js)
- [Прототипы и ООП](#прототипы-и-ооп)
- [Функции и замыкания](#функции-и-замыкания)
- [Асинхронность: Event Loop, Promise, async/await](#асинхронность-event-loop-promise-asyncawait)
- [Модули и сборка](#модули-и-сборка)
- [Современные возможности языка (ES6+)](#современные-возможности-языка-es6)
- [Типизация: TypeScript](#типизация-typescript)
- [Тестирование](#тестирование)

---

## Базовые понятия JS

- **Динамическая типизация:** переменные могут менять тип во время выполнения.
- **Типы данных:**
  - Примитивы: `string`, `number`, `boolean`, `null`, `undefined`, `symbol`, `bigint`
  - Объекты: `Object`, `Array`, функции, классы и др.
- **Сравнение:**  
  - `==` — нестрогое сравнение (приводит типы)
  - `===` — строгое сравнение (без преобразования типов)

**Пример:**
```js
typeof null // 'object'
typeof []   // 'object'
typeof (() => {}) // 'function'
```

---

## Прототипы и ООП

JavaScript использует прототипное наследование. Каждый объект имеет внутреннюю ссылку на прототип (`[[Prototype]]`), что позволяет наследовать свойства и методы.

**Пример:**
```js
function Animal(name) {
  this.name = name;
}
Animal.prototype.sayHi = function() {
  return `Hi, I'm ${this.name}`;
};
const dog = new Animal('Rex');
dog.sayHi(); // 'Hi, I'm Rex'
```

**ES6 Классы:**
```js
class Animal {
  constructor(name) {
    this.name = name;
  }
  sayHi() {
    return `Hi, I'm ${this.name}`;
  }
}
```

## Замыкания
Замыкание — это функция, которая "запоминает" область видимости, в которой была создана, даже после выхода из неё. Используются для инкапсуляции состояния, создания приватных переменных, реализации модулей, итераторов, функций обратного вызова. Замыкания лежат в основе асинхронного программирования (setTimeout, обработчики событий). Важно понимать, как замыкания влияют на сборку мусора и могут приводить к утечкам памяти (например, если замкнуты большие объекты).

**Пример замыкания:**
```js
function counter() {
  let count = 0;
  return function() {
    return ++count;
  };
}
const inc = counter();
inc(); // 1
inc(); // 2
```

- **Стрелочные функции:** не имеют своего `this`, `arguments`, нельзя использовать как конструктор.

**Пример:**
```js
const sum = (a, b) => a + b;
```

---

## Асинхронность: Event Loop, Promise, async/await

- **Event Loop:** обеспечивает неблокирующее выполнение кода.
- **Callback-функции:** первый способ работы с асинхронностью, но приводят к "callback hell".
- **Promise:** объект для работы с будущими результатами асинхронных операций.
- **async/await:** синтаксический сахар для работы с Promise.

**Пример:**
```js
setTimeout(() => console.log('timeout'), 0);
Promise.resolve().then(() => console.log('promise'));
console.log('sync');
// sync -> promise -> timeout
```

**Promise:**
```js
function fetchData() {
  return new Promise((resolve, reject) => {
    setTimeout(() => resolve('data'), 1000);
  });
}
fetchData().then(console.log);
```

**async/await:**
```js
async function main() {
  const data = await fetchData();
  console.log(data);
}
main();
```

---

## Модули и сборка

- **Модули (import/export):**
  - `import { foo } from './module.js'`
  - `export function foo() {}`
  - `export default ...`
- **Сборщики:** Webpack, Vite, Parcel — для объединения и оптимизации кода.
- **Менеджеры пакетов:** npm, yarn, pnpm.

---

## Современные возможности языка (ES6+)

- **Деструктуризация:**
  ```js
  const user = { name: 'Ann', age: 25 };
  const { name, ...rest } = user;
  ```

- **Spread/Rest:**
  ```js
  const arr = [1,2,3];
  const newArr = [...arr, 4];
  function sum(...args) { return args.reduce((a,b) => a+b); }
  ```

- **let/const:** блочная область видимости.
- **Шаблонные строки:**  
  ```js
  const str = `Hello, ${user.name}!`;
  ```

- **Map/Set, Symbol, итераторы и генераторы**
- **Optional chaining (`?.`) и Nullish coalescing (`??`)**

## Современные возможности языка (ES6+)
- **Модули (import/export)**: модульная система ES6 позволяет разделять код на независимые части, поддерживает статический анализ, tree-shaking, оптимизацию сборки. Отличие от CommonJS — статичность, невозможность динамического импорта без import().
- **Работа с npm/yarn/pnpm**: современные менеджеры пакетов обеспечивают управление зависимостями, автоматизацию сборки, публикацию собственных пакетов. Важно знать работу с lock-файлами, настройку скриптов, семантическое версионирование.
- **Линтинг и форматирование**: инструменты (ESLint, Prettier) поддерживают чистоту и единообразие кода, выявляют ошибки и потенциальные баги до запуска приложения. Best practices: использовать строгие правила, интегрировать линтеры в CI/CD.
- **Best practices**: избегать глобальных переменных, использовать строгий режим ('use strict'), писать чистые функции, минимизировать побочные эффекты, использовать const/let вместо var, отдавать предпочтение современным синтаксическим конструкциям.
- **Типичные ошибки**: неправильное использование this, потеря контекста, забыли обработать ошибку в промисе, дублирование кода, неэффективная работа с массивами и объектами.

---

## Типизация: TypeScript

TypeScript — статически типизированное надмножество JS.

- **Типы:**
  - Примитивы: `string`, `number`, `boolean`
  - Массивы: `number[]` или `Array<number>`
  - Кортежи: `[string, number]`
  - Enum, union, intersection, literal types
  - Типы функций: `(a: number, b: number) => number`
- **Интерфейсы и типы:**
  ```ts
  interface User { name: string; age: number }
  type UserType = { name: string; age: number }
  ```
- **Generics:**
  ```ts
  function identity<T>(arg: T): T { return arg; }
  ```
- **Утилиты:**
  - Partial, Pick, Omit, Record, ReturnType и др.
- **Type Guards:**
  ```ts
  function isString(val: unknown): val is string {
    return typeof val === 'string';
  }
  ```
- **Конфигурация (tsconfig.json):**
  - strict, noImplicitAny, strictNullChecks

## TypeScript
TypeScript — надстройка над JavaScript, добавляющая статическую типизацию и расширенные возможности для крупных проектов.

- **Типизация**: позволяет явно указывать типы переменных, параметров, возвращаемых значений. Типизация предотвращает ошибки на этапе компиляции, облегчает рефакторинг, улучшает автодополнение.

**Пример:**
```ts
let age: number = 30;
function greet(name: string): string {
  return `Hello, ${name}`;
}
```

- **Интерфейсы и типы**: интерфейсы описывают структуру объектов, могут расширяться и объединяться. Типы (type) позволяют создавать сложные объединения (union, intersection), алиасы для примитивов и объектов.

**Пример интерфейса и типа:**
```ts
interface User {
  id: number;
  name: string;
}
type Status = 'active' | 'inactive';
const user: User = { id: 1, name: 'Ann' };
```

- **Generics**: обобщённые типы позволяют писать универсальные функции и классы, которые работают с разными типами данных, сохраняя типовую безопасность.

**Пример generic-функции:**
```ts
function identity<T>(value: T): T {
  return value;
}
const num = identity<number>(42);
const str = identity<string>('hello');
```

- **Type guards**: пользовательские функции для сужения типов, обеспечивают безопасность при работе с unknown/any, позволяют строить надёжные проверки и избегать ошибок рантайма.

**Пример type guard:**
```ts
function isString(val: unknown): val is string {
  return typeof val === 'string';
}
function print(val: unknown) {
  if (isString(val)) {
    console.log(val.toUpperCase());
  }
}
```

- **Strict-режимы**: строгие настройки компилятора (strict, noImplicitAny, strictNullChecks и др.) минимизируют ошибки, делают код надёжнее и предсказуемее.

**Пример ошибки без strictNullChecks:**
```ts
function getLength(str?: string) {
  // Ошибка: Object is possibly 'undefined'
  return str.length;
}
```

- **Utility types**: встроенные типы для трансформации других типов (Partial, Pick, Omit, Readonly и др.).

**Пример использования Partial:**
```ts
interface Task {
  id: number;
  title: string;
  completed: boolean;
}
const update: Partial<Task> = { completed: true };
```

---

## Тестирование

- **Юнит-тесты:** проверяют отдельные функции и модули.
- **Инструменты:** Jest, Mocha, Jasmine, AVA.
- **Мока объектов, тестирование асинхронного кода, snapshot-тесты.**
- **TDD/BDD:** Test Driven Development / Behavior Driven Development

**Пример (Jest):**
```js
test('sum', () => {
  expect(1 + 2).toBe(3);
});
```

---

## Рекомендуемые темы для углубленного изучения

- Внутреннее устройство JS-движка (V8, интерпретация, оптимизация)
- WeakMap/WeakSet, Proxy, Reflect API
- Работа с датой и временем (Date, Intl)
- Регулярные выражения
- Безопасность JS: XSS, CSP, защита от утечек памяти
- Локализация и интернационализация

---

## Полезные ресурсы

- [MDN JavaScript Guide](https://developer.mozilla.org/ru/docs/Web/JavaScript/Guide)
- [TypeScript Handbook](https://www.typescriptlang.org/docs/handbook/intro.html)
- [You Don't Know JS (book series)](https://github.com/getify/You-Dont-Know-JS)
- [Exploring ES6](https://exploringjs.com/es6/)

---
