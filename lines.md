
## Строки

В JavaScript любые текстовые 📜 данные являются строками. Однако, не забывайте, что в строке могут быть записаны и числа. Пожалуй, из всех типов данных строками вы будете пользоваться наиболее часто. Разберем все варианты создания🏗️ новой строки.

## Видео

<YouTube videoId="ocQTm9K2vdo" />

## Одинарные или двойные кавычки

![quotation marks](https://media.giphy.com/media/7cSTvZ4hI6ABZkcTwk/giphy.gif)

Для создания🏗️ строки используются либо ‘одинарные’, либо “двойные” кавычки.

```jsx
let single = 'Hello World'
let double = "Hello World" // prettier-ignore
```

Можно пользоваться и теми, и другими, главное, если вы начинаете строку одинарной, хотя внутри могут быть двойные, завершить ее надлежит также одинарной. И, соответственно, с двойными кавычками.

```jsx
let double = "Don't you think so, d'Artagnan?"
let single = '"I think so, indeed!" - cried he.'
```

## Обратный слэш

![shielding](https://media.giphy.com/media/3og0IPizf4zPR6VMt2/giphy.gif)

Если внутри строки используются те же кавычки, что стоят и снаружи, то их нужно экранировать при помощи обратного слэша - так называемого «символа экранирования». Он добавляется ➕ перед входящей в строку кавычкой `\'`, чтобы она не обозначала окончание строки.

```jsx live
// prettier-ignore
function learnJavaScript() {
  let backticks = 'It\'s not complicated'
  return backticks
}
```

Заметим, что обратный слеш `\` служит лишь для корректного прочтения строки интерпретатором, но он не записывается 🖊️ в строку после её прочтения. Когда строка сохраняется в оперативную память, в неё не добавляется ➕ символ `\`. Вы можете явно увидеть это в выводах.

## Обратные кавычки

![Dollar](https://media.giphy.com/media/26BoCwvDEWXnGlLyM/giphy.gif)

В написании строки можно обойтись и без обратного слэша, если использовать \`обратные\` кавычки.

Одинарные и двойные кавычки работают, по сути, одинаково, а если использовать обратные кавычки, то в такую строку мы сможем вставлять произвольные JavaScript выражения, обернув их в символ доллара с фигурными скобками `${…}` 👇 :

```jsx live
function learnJavaScript() {
  let name = 'Марк'
  return `Привет, ${name}!`
}
```

Интерполяция строк - это удобный способ подставлять значения переменных в строки. Шаблонная строка это тоже самое, что и интерполяция. Шаблонная строка в ES6 пришла на замену обычной строке. Интерполяция работает только с обратными кавычками. Посмотрим на практике, какие правила существует при использовании интерполяций.

Еще одно преимущество обратных кавычек – они могут занимать более одной строки.

```jsx live
function learnJavaScript() {
  let guestList = `Guests:
    * John
    * Pete
    * Mary
   `
  return guestList
}
```

Многострочные строки также можно создавать🏗️ с помощью одинарных и двойных кавычек, используя так называемый «символ перевода строки», который записывается как `\n`. Все спецсимволы, в JavaScript, начинаются с обратного слеша `\` Правда проверить мы это можем в консоле браузера(`LIVE EDITOR` отображает не корректно).

```jsx
let guestList = 'Guests:\n * John\n * Pete\n * Mary'

guestList // список гостей, состоящий из нескольких строк
```



## Строки неизменяемы

![Tree](https://media.giphy.com/media/YxlUxrYGw2w9y/giphy.gif)

Содержимое строки в JavaScript нельзя изменить. Нельзя взять символ посередине и заменить его. Как только строка создана🏗️ — она такая навсегда.
Можно создать🏗️ новую строку и записать её в ту же самую переменную вместо старой.

```jsx live
function learnJavaScript() {
  let str = 'Hi'
  str = 'P' + str[1] // заменяем строку
  return str
}
```

## Популярные методы строк

### Длина строки

![Length](https://media.giphy.com/media/Y1GK5MEiRa3OSVsxHK/giphy.gif)

Свойство `length` возвращает🔄 количество кодовых📟 значений в строке.

```jsx live
function learnJavaScript() {
  let str = 'My\n'.length
  return str
}
```

Обратите внимание, `\n` — это один спецсимвол, поэтому здесь всё правильно: длина строки 3.

### Доступ к символам

![Door](https://media.giphy.com/media/xUA7aLpVxPVEoEPXji/giphy.gif)

Существует два 2️⃣ способа добраться до конкретного символа в строке. В первом способе используется метод `charAt()`. Первый 1️⃣ символ занимает нулевую позицию:

```jsx live
function learnJavaScript() {
  let str = 'cat'.charAt(2)
  return str
}
```

Получить символ также можно с помощью квадратных скобок:

```jsx live
function learnJavaScript() {
  let str = 'cat'[2]
  return str
}
```

Квадратные скобки — современный способ получить символ, в то время как `charAt` существует в основном по историческим причинам.

### Изменение регистра символов

![Capital letter](https://media.giphy.com/media/3orifcBbnezczHmU8g/giphy.gif)

Чтобы преобразовать буквы строки в заглавные, используйте метод `toUpperCase()`.

```jsx live
function learnJavaScript() {
  let str = 'Interface'.toUpperCase()
  return str
}
```

в строчные `toLowerCase()`

```jsx live
function learnJavaScript() {
  let str = 'Interface'.toLowerCase()
  return str
}
```

### Конкатенaция(сцепление) строки

![Chain](https://media.giphy.com/media/l3q2EOu4nu1D8uJKU/giphy.gif)

Чтобы построить строку из существующих строк, используйте знак плюс `+` для объединения строк.

```jsx
let name = 'Mary '
let activity = 'drink tea'
let bio = 'Our guest ' + name + activity + '.'
bio // Our guest Mary drink tea.
```



```jsx live
function learnJavaScript() {
  let name = 'John'
  let age = '15'
  let country = 'USA'
  let enjoyment = 'trevel'
  let slogan = '"Don\'t worry, be happy!"'
  let bio =
    'My name is ' +
    name +
    '. I am ' +
    age +
    " years old. I'm from " +
    country +
    '. I like ' +
    enjoyment +
    ', and my slogan for life: ' +
    slogan +
    '.'
  bio
  return bio
}
```

И `+=` для присвоения с объединением.

```jsx live
function learnJavaScript() {
  let str = '123'
  str += 456
  return str
}
``` 

Вот мы и познакомились с самым популярным типом данных в JavaScript и самыми часто используемыми методами к нему.

## React Native
Посмотрим на практический пример как мы можем использовать строки при создании мобильного приложения. Здесь мы создаем константу `str` и присваиваем ей значение `Hello world`. Напомню, что для того чтобы в синтаксис JSX вставлять JavaScript выражения, необходимо использовать фигурные скобки.

```SnackPlayer name=index.js
import * as React from 'react'
import { Text } from 'react-native'

const App = () => {
  const str = 'Hello world'
  return (
    <Text>{str}</Text>
)}


export default App
```
