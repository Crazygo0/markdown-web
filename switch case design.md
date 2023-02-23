## Конструция switch case

Конструкция `switch` служит для сравнения значения на равенство с различными вариантами.

При этом равенство подразумевается в смысле оператора строгое равенство `===`, сравнивать с регулярным выражением или как-то еще `switch` не умеет. То есть значения должны быть одного типа, чтобы выполнялось равенство.

![comparison](https://media.giphy.com/media/icJA0VF7ntoEL18Jez/giphy.gif)

Если условие совпадает, то выполняется блок кода📟 , связанный с соответствующим `case`. Если ни одно условие не подошло, то выполняется код📟 , указанный в блоке `default`, если он есть. Для выхода из конструкции используется команда `break`. Если ее не указывать, автоматически выполнится блок кода📟 в следующем `case` и т.д. Поэтому `break` используем в наших скриптах обязательно, чтобы не гонять интерпретатор по всем `case` тем самым снижая производительность скрипта.

## Видео

<YouTube videoId="s2fLXDgA1wQ" />

## Синтаксис

![Syntax](https://media.giphy.com/media/yR4xZagT71AAM/giphy.gif)

Конструкция `switch` имеет один или более блоков `case` и необязательный блок `default`.

Выглядит она так:

```jsx
switch (n) {
  case 1:
    // блок кода 1;
    break
  case 2:
    // блок кода 2;
    break
  // .......
  // другие варианты  case
  // .......
  default:
  // блок кода если не подошло ни одно условие;
}
```

`n` - это булеан [boolean](https://jscamp.app/docs/javascript08) условие.

## Примеры

![Math](https://media.giphy.com/media/xT1Ra5h24Eliux3UVq/giphy.gif)

Рассмотрим простейший пример 👇 :

```jsx live
function learnJavaScript() {
  let a = 4
  let str
  switch (a) {
    case 3:
      str = 'Маловато'
      break
    case 4:
      str = 'В точку!'
      break
    case 5:
      str = 'Перебор'
      break
    default:
      str = 'Я таких значений не знаю'
  }
  return str
}
```

Здесь оператор `switch` последовательно сравнит `a` со всеми вариантами из `case`.
Сначала `3`, затем – так как нет совпадения – `4`. Совпадение найдено, будет выполнен этот вариант, со строки `str = 'В точку!'` и далее, до ближайшего `break`, который прервёт выполнение.

![Wow](https://media.giphy.com/media/3oriO13KTkzPwTykp2/giphy.gif)

Рассмотрим такой пример 👇 :

```jsx live
function learnJavaScript() {
  let a = 'Apples'
  let str
  switch (a) {
    case 'Apples':
      str = 'I love ' + a
      break
    case 'Oranges':
      str = 'I love ' + a
      break
    case 'Bananas':
      str = 'I love ' + a
      break
    default:
      str = 'I like other fruits'
  }
  return str
}
```

Здесь оператор `switch` последовательно сравнит `a` со всеми вариантами из `case`. Но здесь идет сравнение не чисел, а строк. Так можно сделать с любыми типами данных, главное чтобы сравнивались одинаковые типы данных.

## Замена `if`

Также `Switch` используется чтобы заменить множественные `if`.

Например, можно заменить данный код 👇 :

```jsx live
function learnJavaScript() {
  let number = 2
  let str
  if (number === 0) {
    str = 'Вы ввели число 0'
  }

  if (number === 1) {
    str = 'Вы ввели число 1'
  }

  if (number === 2 || number === 3) {
    str = 'Вы ввели число 2, а может и 3'
  }
  return str
}
```

На этот 👇 :

```jsx live
function learnJavaScript() {
  let number = 2
  let str
  switch (number) {
    case 0:
      str = 'Вы ввели число 0'
      break

    case 1:
      str = 'Вы ввели число 1'
      break

    case 2:
    case 3:
      str = 'Вы ввели число 2, а может и 3'
      break
  }
  return str
}
```

Результат будет тот же, но код📟 станет более читабельным и удобным для работы.

## React Native
Пример использования в `React Native` приложениях.

```SnackPlayer name=index.js
import * as React from 'react'
import { Text } from 'react-native'

const App = () => {
  const userType = 'Admin'
  
  return (
    <>
      {(() => {
           switch (userType) {
              case 'Admin':
                  return (
                    <Text>You are a Admin.</Text>
                  )
              case 'Manager':
                  return (
                    <Text>You are a Manager.</Text>
                  )
              default:
                  return (
                    <Text>You are a User.</Text>
                  )
           }
        })()}
    </>
  )
}

export default App
```
