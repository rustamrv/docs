# JavaScript / TypeScript: Теория и Практика

## Прототипы
Прототипное наследование — основа объектной модели JS. Каждый объект имеет внутреннее свойство [[Prototype]], указывающее на другой объект. Это позволяет реализовывать наследование и делиться методами между объектами.

**Пример:**
```js
function Animal(name) {
  this.name = name;
}
Animal.prototype.sayHi = function() {
  return `Hi, I'm ${this.name}`;
};
const dog = new Animal('Rex');
dog.sayHi(); // 'Hi, I\'m Rex'
```

## Замыкания
Замыкание — функция, которая запоминает область видимости, в которой была создана. Используется для инкапсуляции состояния и создания приватных переменных.

**Пример:**
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

## Асинхронность
Асинхронное программирование реализуется через колбэки, промисы, async/await. Event loop управляет очередями задач (microtask, macrotask).

**Пример:**
```js
setTimeout(() => console.log('timeout'), 0);
Promise.resolve().then(() => console.log('promise'));
console.log('sync');
// sync -> promise -> timeout
```

## Современные возможности языка (ES6+)
- Деструктуризация, spread/rest, модули (import/export), работа с npm/yarn/pnpm, линтинг и форматирование.

**Пример (деструктуризация):**
```js
const user = {name: 'Ann', age: 25};
const {name, ...rest} = user;
```

## TypeScript
TypeScript добавляет статическую типизацию, интерфейсы, generics, строгие режимы, type guards.

**Пример:**
```ts
function isString(val: unknown): val is string {
  return typeof val === 'string';
}
```

## Тестирование
- Юнит-тесты (Jest/Mocha), TDD/BDD, тестирование асинхронного кода.

**Пример (Jest):**
```js
test('sum', () => {
  expect(1 + 2).toBe(3);
});
``` 