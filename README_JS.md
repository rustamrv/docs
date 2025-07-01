# JavaScript / TypeScript: Теория и Практика

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

---

## Функции и замыкания

- **Функции — объекты первого класса:** можно присваивать переменным, передавать аргументом, возвращать из других функций.
- **Замыкания (Closures):** функция запоминает область видимости, в которой была создана.

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
