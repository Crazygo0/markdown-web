## Параметры по умолчанию

Параметры по умолчанию позволяют задавать параметрам функции⚙️ значения по умолчанию в случае, если функция⚙️ вызвана без аргументов, или если параметру явным образом передано значение `undefined`.

![Teacher](https://media.giphy.com/media/3ohc10nduj1irsuzgA/giphy.gif)

В JavaScript параметры функции⚙️, которым при ее вызове не передаются значения, принимают по умолчанию значение `undefined`. Однако в некоторых случаях может быть полезно задать иное значение по умолчанию. Именно для таких случаев предназначены параметры по умолчанию.

## Синтаксис

![book](https://media.giphy.com/media/l0HlOBZcl7sbV6LnO/giphy.gif)

```jsx live
function learnJavaScript() {
  const multiply = (a, b = 1) => {
    //Значение по умолчанию у b равно 1
    return a * b
  }
  //Если b будет undefined, то ему присвоится значение по умолчанию
  return multiply(5, 2) // удалите запятую, второй аргумент и получите 5 * 1
}
```

## Видео

<YouTube videoId="J89Qcz0cunw" />

### Передача других "ложных" значений

![basketball](https://media.giphy.com/media/3oEdv5e5Zd2gsczAhG/giphy.gif)

Если формальному параметру при вызове передано любое значение, отличное от `undefined`, в том числе одно из "ложных" значений, таких как false ❎ , `0`, `""`, `''`,`null`, `NaN`, то в этом случае значение по умолчанию присвоено параметру не будет. В этом случае нужно самому прописывать 🖊️ код который будет отлавливать эти "ложные значения".

## Примеры

![Math](https://media.giphy.com/media/xT1Ra5h24Eliux3UVq/giphy.gif)

В параметрах по умолчанию можно использовать значения предыдущих (расположеннных левее в списке) параметров:

```jsx live
function learnJavaScript() {
  const greet = (name, greeting, message = greeting + ' ' + name) => {
    return [name, greeting, message]
  }

  return greet('David ', 'Hi ')
}
```

Пример функции с параметрами по умолчанию и без них 👇 :

```jsx live
function learnJavaScript() {
  const withDefaults = (a = 1, b = 3, c = 2) => {
    //Функия с параметрами по умолчанию
    return [a, b, c]
  }
  const withoutDefaults = (a, b, c) => {
    //Функция без параметров по умолчанию
    if (a == undefined) {
      a = 1
    }
    if (b == undefined) {
      b = 3
    }
    if (c == undefined) {
      c = 2
    }
    return [a, b, c]
  }

  return withDefaults()
}
```

Результат будет тот же, но без параметров по умолчанию код📟 может стать заметно больше.

## React Native

Большинство компонентов можно настроить при их создании с различными параметрами. Эти параметры создания называются - `props`. Обратите внимание на то, что в третий компонент `HelloWorld` мы не передаем `name` поэтому рапечатывается имя `Вася`


```SnackPlayer name=index.js
import * as React from 'react'
import { Text } from 'react-native'

const HelloWorld = ({ name = 'Вася' }) => (
  <Text>Hello {name}!</Text>
)

const App = () => (
  <>
    <HelloWorld name='Luk' />
    <HelloWorld name='John' />
    <HelloWorld /> 
  </>
)

export default App
```

Использование `name` в качестве `props` позволяет нам настроить компонент приветствия, чтобы мы могли повторно использовать этот компонент для каждого из наших приветствий. В этом примере также используется компонент `HelloWorld` в JSX. Способность делать это - вот что делает React таким крутым.
