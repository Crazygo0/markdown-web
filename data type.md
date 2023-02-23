## Динамическая типизация

JavaScript является слабо типизированным или динамическим языком. Это значит, что вам не нужно определять тип переменной 🔔 заранее.

![Dinamics](https://media.giphy.com/media/26uf759LlDftqZNVm/giphy.gif)

Тип определится автоматически во время выполнения программы. Также это значит, что вы можете использовать одну переменную 🔔 для хранения 📦 данных различных типов 👇 :

```jsx live
function learnJavaScript() {
  let foo = 42 // сейчас foo типа number
  foo = 'bar' // а теперь foo типа string
  return typeof foo
}
```

## Видео

<YouTube videoId="1zXZCVbNbkQ" />

## typeof

Для того чтобы понять тип данных содержащийся в переменной, используется оператор `typeof`. Оператор `typeof` возвращает тип аргумента.
У него есть два синтаксиса: со скобками и без:

- Синтаксис оператора: `typeof x`

- Синтаксис функции: `typeof(x)`

Работают они одинаково, но первый синтаксис короче.

Результатом `typeof` является строка, содержащая тип.

```jsx live
function learnJavaScript() {
  let num = 9
  return typeof num
}
```

## Типы данных

![Data types](https://media.giphy.com/media/NPXkCN2FutVO1Nt4P9/giphy.gif)

Стандарт JavaScript определяет 9 типов данных. Познакомьтесь с каждым из них делая вывод в консоль и после я расскажу 🗣️ о каждом из них подробнее.

```javascript
let one = { firstName: 'John', lastName: 'Smith' } // object

let two = () => {} // function

let three = 'bar' // string

let four = 42 // number

let five = 19241924124n // bigint

let six = true // boolean

let seven = null // null

let eight // undefined

let nine = Symbol() // symbol
```

## Объекты

![cupboard](https://media.giphy.com/media/l2Sq0NFJlJC5Dqb7y/giphy.gif)

В компьютерной терминологии, тип объект `object` — это значение в памяти, на которое возможно сослаться с помощью идентификатора. В JavaScript объект может расцениваться как набор свойств. Это как шкаф 🗄️ для хранения 📦 других типов данных.

## Функции

![Function](https://media.giphy.com/media/FuSJ5C7SSHlZCxjC6q/giphy.gif)

Функции⚙️ `function` — это обычные объекты, имеющие дополнительную возможность быть вызванными для исполнения.

## Примитивные значения

![Primitive](https://media.giphy.com/media/rBdWc61BPFVYc/giphy.gif)

Все типы данных в JavaScript, кроме объектов, являются иммутабельными (значения не могут быть модифицированы, а только перезаписаны новым полным значением). Например, в отличии от языка👅 C, где строку можно посимвольно корректировать, в JavaScript строки пересоздаются🏗️ только полностью. Значения таких типов называются "примитивными значениями".

## Текстовые строки

![text](https://media.giphy.com/media/26n6AaCcCajAyZx04/giphy.gif)

В JavaScript для представления текстовых 📜 данных служит тип `string`.

## Числа

![Numbers](https://media.giphy.com/media/xT5LMMneIRG1UJquOI/giphy.gif)

Числовой тип данных `number` представляет как целочисленные значения, так и числа с плавающей точкой.

## BigInt

![giant](https://media.giphy.com/media/LZGipmRpX6uwE/giphy.gif)

В JavaScript тип `number` не может содержать числа больше, чем (253-1) (т. е. 9007199254740991), или меньше, чем -(253-1) для отрицательных чисел. Это техническое ограничение вызвано их внутренним представлением.

Для большинства случаев этого достаточно. Но иногда нам нужны действительно гигантские числа, например, в криптографии или при использовании метки времени ("timestamp") с микросекундами.

Тип `bigInt` был добавлен в JavaScript, чтобы дать возможность работать с целыми числами произвольной длины.

## Булевый тип данных

Булевый тип `boolean` представляет логическую сущность и имеет два 2️⃣ значения: `true` ✅ (истина)

![true](https://media.giphy.com/media/ap6wcjRyi8HoA/giphy.gif)

и `false` ❎ (ложь).

![False](https://media.giphy.com/media/HNOVuT5AvCK1fgvp1m/giphy.gif)

Такой тип, как правило, используется для хранения 📦 значений да/нет: true ✅ значит «да, правильно», а false ❎ значит «нет, не правильно».

## Null

![Null](https://media.giphy.com/media/26hkhPJ5hmdD87HYA/giphy.gif)

Этот тип данных имеет всего одно значение: `null`. Это значение, специально обозначенное как примитив, так как по поведению это в самом деле видимый примитив. Но при этом от `null` унаследованы все остальные Объекты, поэтому, несмотря на то, что `null` возвращает🔄 примитивное значение, его тип это объект.
Например можно присвоить его значению по умолчанию.

## Undefined

![Unndefined](https://media.giphy.com/media/PkKzNQjwPy7GvxZbfe/giphy.gif)

Переменная 🔔 , которой не было присвоено значение, будет иметь значение `undefined`.

### Отличия между null и undefined

![Spiderman](https://media.giphy.com/media/l36kU80xPf0ojG0Erg/giphy.gif)

`null` является определенным значением отсутствия объекта, тогда как `undefined` обозначает неопределенность. Например вы можете это проверить в консоле браузера:

```javascript
let TestVar
console.log(TestVar) // undefined
console.log(typeof TestVar) // undefined
```

`null` - это значение присваивания. Он может быть присвоен переменной 🔔 как представление без значения:

```javascript
let TestVar = null
console.log(TestVar) // null
console.log(typeof TestVar) // object
```

Из предыдущих примеров ясно, что `undefined` и `null` - это два 2️⃣ различных типа: `undefined` - это сам тип (неопределенный), а `null` - объект.

```javascript
null === undefined // false
null == undefined // true
null === null // true
```

## Тип данных Символ (Symbol)

![Symbol](https://media.giphy.com/media/QvSGhHq8CrVzq/giphy.gif)

Тип символ `Symbol` — это уникальное и иммутабельное примитивное значение, которое может быть использовано как ключ для свойства объекта. Этот тип на столько редко используется в реальной работе, что мы даже не будем рассматривать его в рамках этого курса.