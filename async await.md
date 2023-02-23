## Async Await

Существует специальный синтаксис 📖 для работы с промисами, который называется `async/await`.

## Создание асинхронной функции

![creature](https://media.giphy.com/media/4T7e4DmcrP9du/giphy.gif)

Асинхронная функция⚙️ определяется выражением асинхронной функции⚙️. Базовая функция⚙️ выглядит так:

```javascript
async function foo() {
  const value = await somePromise()
  return value
}
```

Мы определяем функцию⚙️ как асинхронную с помощью `async`. Это ключевое🗝️ слово может использоваться с любым синтаксисом📖 объявления🗣️ функции⚙️:

```javascript
// Function Declaration
async function foo() { ... }

// Function Expression
const foo = async function () { ... }

// Arrow function
const foo = async () => { ... }

// Class methods
class Bar {
    async foo() { ... }
}
```

![Stops](https://media.giphy.com/media/WrgAGkGrh0MD1Z2gkO/giphy.gif)

Как только мы определили функцию⚙️ как асинхронную, мы можем использовать ключевое🗝️ слово `await`.
Это ключевое🗝️ слово помещается перед вызовом промиса, оно приостанавливает выполнение функции⚙️ до тех пор, пока промис не будет выполнен или отклонён.

## Видео

<YouTube videoId="5KVQ4pcJOrU" />

## Async

![run](https://media.giphy.com/media/3N0fFF5xxcZrO/giphy.gif)

У нас есть ключевое🗝️ слово `async`, которое мы помещаем перед объявлением🗣️ функции⚙️, чтобы сделать ее асинхронной. Асинхронная функция⚙️ — это функция⚙️, которая предвосхищает возможность использования ключевого🗝️ слова `await` для запуска асинхронного кода📟 .

Попробуйте набрать в консоли браузера следующее:

```javascript
function hello() {
  return 'Hello'
}
hello()
```

Функция⚙️ вернет 'Hello'. Ничего необычного.

Но что если мы превратим ее в асинхронную функцию⚙️? Попробуйте сделать следующее:

```javascript
async function hello() {
  return 'Hello'
}
hello()
```

![Promise](https://media.giphy.com/media/GFtJhEvG3681y/giphy.gif)

Теперь вызов функции⚙️ возвращает🔄 обещание. Это одна из особенностей асинхронных функций⚙️ — они возвращают🔄 значения, которые гарантировано преобразуются в обещания.

Вы также можете создать🏗️ асинхронное функциональное⚙️ выражение, например, так:

```javascript
// Function Expression
let hello = async function () {
  return hello()
}
hello()
```

Также можно использовать стрелочные функции⚙️:

```javascript
let hello = async () => {
  return 'Hello'
}
```

Все эти функции⚙️ делают одно и тоже.

Для того, чтобы получить значение завершенного обещания, мы можем использовать блок `.then()`:

```javascript
hello().then(value => console.log(value))
```

… или даже так:

```javascript
hello().then(console.log)
```

Таким образом, добавление ключевого🗝️ слова `async` заставляет функцию⚙️ возвращать🔄 обещание вместо значения. Кроме того, это позволяет синхронным функциям избегать любых накладных расходов, связанных с запуском и поддержкой использования `await`. Простое добавление `async` перед функцией⚙️ обеспечивает автоматическую оптимизацию кода📟 движком JS.

## Await

![Wait](https://media.giphy.com/media/myPdoRAlad0J2/giphy.gif)

Преимущества асинхронных функций⚙️ становятся еще более очевидными, когда вы комбинируете их с ключевым🗝️ словом `await`. Оно может быть добавлено перед любой основанной на обещаниях функцией⚙️, чтобы заставить ее дожидаться завершения обещания, а затем вернуть результат. После этого выполняется следующий блок кода📟 .

Вы можете использовать `await` при вызове любой функции⚙️, возвращающей🔄 обещание, включая функции⚙️ `Web API`.

Синтаксис📖:

```javascript
let response = await fetch('https://jsonplaceholder.typicode.com/users')
let data = await response.json()
console.log(data[0].name + ' and ' + data[2].name)
```

### Переписывание кода

![code rewriting](https://media.giphy.com/media/LmNwrBhejkK9EFP504/giphy.gif)

Возьмем пример с `fetch`:

```javascript
fetch('coffee.jpg')
  .then(response => response.blob())
  .then(myBlob => {
    let objectURL = URL.createObjectURL(myBlob)
    let image = document.createElement('img')
    image.src = objectURL
    document.body.appendChild(image)
  })
  .catch(e => {
    console.log('There has been a problem with your fetch operation: ' + e.message)
  })
```

Давайте перепишем этот код📟 с использованием `async/await`, чтобы увидеть, насколько все стало проще:

```javascript
async function myFetch() {
  let response = await fetch('coffee.jpg')
  let myBlob = await response.blob()

  let objectURL = URL.createObjectURL(myBlob)
  let image = document.createElement('img')
  image.src = objectURL
  document.body.appendChild(image)
}

myFetch().catch(e => {
  console.log('There has been a problem with your fetch operation: ' + e.message)
})
```

Это делает код📟 намного проще и более легким для понимания — никаких блоков `.then()`!

Использование ключевого слова `async` превращает функцию⚙️ в обещание, поэтому мы можем использовать смешанный подход из обещаний и `await`, выделив вторую часть функции⚙️ в отдельный блок с целью повышения гибкости:

```javascript
async function myFetch() {
  let response = await fetch('coffee.jpg')
  return await response.blob()
}

myFetch()
  .then(blob => {
    let objectURL = URL.createObjectURL(blob)
    let image = document.createElement('image')
    image.src = objectURL
    document.body.appendChild(image)
  })
  .catch(e => console.log(e))
``` 

### Как это работает?

![how it works](https://media.giphy.com/media/OTnDHCCFNZHwc/giphy.gif)

Мы обернули код📟 внутри функции⚙️ и добавили ключевое🗝️ слово `async` перед ключевым🗝️ словом `function`. Вам нужно создать🏗️ асинхронную функцию⚙️, чтобы определить блок кода📟 , в котором будет запускаться асинхронный код📟 ; `await` работает только внутри асинхронных функций⚙️.

`Await` работает только в асинхронных функциях⚙️.

Внутри функции⚙️ `myFetch()` код📟 очень сильно напоминает версию на обещаниях, но с некоторыми отличиями. Вместо использования блока `.then()` после каждого метода, основанного на обещаниях, достаточно добавить ключевое🗝️ слово `await` перед вызовом метода и присвоить значение переменной. Ключевое🗝️ слово `await` заставляет движок JS приостановить выполнение кода📟 на данной строке, позволяя выполняться другому коду📟 , пока асинхронная функция⚙️ не вернет результат. Как только она выполнится, код📟 продолжит выполнение со следующей строки.

Например:

```javascript
let response = await fetch('coffee.jpg')
```

Значение, возвращаемое🔄 обещанием `fetch()`, присваивается переменной response, когда данное значение становится доступным, и «парсер» останавливается на этой линии до завершения обещания. Как только значение становится доступным, парсер переходит к следующей строчке кода📟 , которая создает🏗️ `Blob`. Эта строчка также вызывает основанный на обещаниях асинхронный метод, поэтому здесь мы также используем `await`. Когда результат операции возвращается🔄, мы возвращаем🔄 его из функции⚙️ `myFetch()`.

Это означает, что когда мы вызываем функцию⚙️ `myFetch()`, она возвращает🔄 обещание, поэтому мы можем добавить к ней `.then()`, внутри которого мы обрабатываем отображение изображения на экране.

Когда меньше блоков `.then()` для оборачивания кода📟 , все это выглядит как синхронный код📟 , поэтому он интуитивно понятен. -->

## Обработка ошибок с `try...catch`

![code rewriting](https://media.giphy.com/media/ZVik7pBtu9dNS/giphy.gif)

Если вы хотите добавить обработку ошибок, у вас есть несколько вариантов.

Вы можете использовать синхронную структуру `try...catch` вместе с `async/await`:

```javascript
async function myFetch() {
  try {
    let response = await fetch('https://jsonplaceholder.typicode.com/users')
    let data = await response.json()
    console.log(data[0].name + ' and ' + data[2].name)
  } catch (e) {
    console.log(e)
  }
}

myFetch()
```

Блок `catch(){}` принимает объект ошибки🙅‍♂️, который мы назвали `e`. Теперь мы можем вывести его в консоль, это позволит нам получить сообщение💬 о том, в каком месте кода📟 произошла ошибка🙅‍♂️.

Целенаправленно создадим ошибку в `url` и посмотрим на вывод ошибки.

```javascript
async function myFetch() {
  try {
    let response = await fetch('https://jsonplaceholder.typicode.com/sers')
    let data = await response.json()
    console.log(data[0].name + ' and ' + data[2].name)
  } catch (e) {
    console.log(e)
  }
}

myFetch()
```



## Итого

![Conclusion](https://media.giphy.com/media/3o6ZsVl2hv8ZnhSXug/giphy.gif)

`Async/await` позволяет писать 🖊️ асинхронный код, который легко читать и поддерживать. Шесть причин почему его лучше использовать вместо промисов читайте [здесь](https://habr.com/ru/company/ruvds/blog/326074/).