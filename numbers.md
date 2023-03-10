
## Числа


В современном JavaScript существует два 2️⃣ типа чисел:

### `number`

Обычные числа в JavaScript хранятся в 64-битном формате IEEE-754, который также называют «числа с плавающей точкой двойной точности» (double precision floating point numbers). Это числа, которые мы будем использовать чаще всего. Целые числа не рассматриваются как отдельный тип чисел. В дополнение к числам с плавающей запятой, к числовому типу данных относятся также три символьные величины: `Infinity`, `-Infinity`, и `NaN` (не-число).

![Numbers](https://media.giphy.com/media/JtBZm3Getg3dqxK0zP/giphy.gif)

## Видео

<YouTube videoId="wltQLqPeOyc" /> 

### `bigInt`

Числа дают возможность работать с целыми числами произвольной длины. Они нужны достаточно редко и используются в случаях, когда необходимо работать со значениями за пределами максимального безопасного целочисленного значения `Number`.

Любое число, пусть даже десятичная дробь с уймой знаков после запятой, никогда не берётся в кавычки.

Вы можете использовать четыре типа числовых литералов: десятичный, двоичный, восьмеричный и шестнадцатеричный. Так как три последних используются довольно редко, то мы опустим их детальное описание 🖊️ , ну а любопытные могут познакомиться с ними [здесь](https://developer.mozilla.org/ru/docs/Web/JavaScript/Guide/Numbers_and_dates).

:::caution
Будьте внимательны при использование нулей в начале чисел! Значит не надо ставить ноль перед десятичным числом.
:::

```jsx
1234567890
42

0888 // 888 обрабатывается как десятичное
0777 // обрабатывается как восьмеричное в нестрогой форме (511 в десятичной)
```

## Арифметические действия

![Arithmetic operation](https://media.giphy.com/media/gEvab1ilmJjA82FaSV/giphy.gif)

По двум или нескольким целым числам можно составить новое целое число. Способов составлять новое целое число очень много. Способ составлять новое число по двум или нескольким числам называется арифметическим действием.
Вообще арифметических действий много, но основных только четыре: сложение, вычитание, умножение и деление. Они названы основными, ибо все остальные действия приводятся к ним.

Знак плюс `+` используется для выражения сложения: `4 + 4` Ответ: `8`

Минус `–` для вычитания: `7 - 6` Ответ: `1`

Звёздочкой `*` изображается умножение: `3 * 4` Ответ: `12`

Прямым слэшем `/` деление: `15 / 5` Ответ: `3`

Если в строке совершается более одного действия, то, чтобы отделить их друг от друга, а также сделать код📟 более читабельным, мы пользуемся — (скобками). Давайте наберём следующие предложения в консоли. Ответ по каждому из них должен состоять только из одной цифры9️⃣:

```
 3 * (2 + 1)
(3 + 24) / (10 - 7)
(2 + 5 * 5) / (6 -  3)
 3 * (5 - 8 / 2) * (2 + 1)
```

Введите в `LIVE EDITOR` перечисленые значения 👇 :

```jsx {2} live
function learnJavaScript() {
  let result = 2 + 3 // здесь
  return result
}
```

## Комбинированное присваивание

![Conbination](https://media.giphy.com/media/l2Sq8jlaqqnqBoGhG/giphy.gif)

Оператор представляет собой символическое обозначение некоторого действия, выполняемого с операндами в выражении(Например: `+`, `-`, `*`, `/`).

Операнд представляет собой некоторую величину, обрабатываемую в программе. Операнды могут относиться к любому типу данных. Операнд слева от оператора - левый операнд, операнд справа от оператора - правый операнд.

Основной оператор комбинированного присваивания - это знак равно `=`, он и присваивает значение правого операнда, левому. То есть - `x = y` присваивает значение переменной 🔔 `y`, переменной 🔔 `x`.

Вы уже не раз видели, как при помощи математических операторов происходит присваивание значений переменным 🔔 . Например, так:

```javascript
let sum = 2 + 3 // значение суммы 7
```

А ещё вы, наверное, не успели позабыть, что в любой момент можно изменить значение уже известной переменной 🔔 :

```jsx live
function learnJavaScript() {
  let sum = 2 + 3
  sum = sum + 3 // теперь значение суммы стало 8
  return sum
}
```

Присваивание со сложением `+=` для того, чтобы быстро увеличить значение переменной! Вот вам несколько примеров:

```javascript
let значение = 5
значение += 2 // значение теперь 7 (то же самое, что значение = // значение + 2)
значение += 3 // значение теперь 10 (то же самое, что значение = // значение + 3)
значение = значение + значение // 20 (а можно просто значение += // значение)
значение += значение // 40 (то же самое, что значение = значение + // значение)
```

Вы ведь уже догадались, что подобные штуки работают и с прочими математическими действиями, да?!

```javascript
значение –= 25 // значение теперь 15 (то же, что и значение = значение − // 25)
значение -= 2 // значение теперь 30 (то же самое, что значение = // значение - 2)
значение /= 3 // значение теперь 10 (то же самое, что значение = // value / 3)
значение // Ответ: 10
```

Далее проверьте все перечисленые примеры в `LIVE EDITOR`:

```jsx live
function learnJavaScript() {
  let значение = 0 + 0
  return значение
}
```

Подробней о комбинированном присваивании можно почитать [здесь](https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/Operators/Assignment_Operators)

## Инкремент и декремент

![increment](https://media.giphy.com/media/ZZaCZyXh5yR4bkJmlR/giphy.gif)

Оператор `++` (инкремент) увеличивает значение своего операнда на единицу. Если значение операнда не является числом, оператор автоматически преобразует его в число, увеличивает на единицу и возвращает результат, который присваивается обратно операнду:

```jsx live
function learnJavaScript() {
  let increment = 0
  increment++
  return increment
}
```

Оператор `--` (декремент) работает аналогично оператору инкремент, но не увеличивает значение своего операнда, а наоборот, уменьшает его на единицу:

```jsx live
function learnJavaScript() {
  let decrement = 6
  decrement--
  return decrement
}
```

## Оператор modulo

![function](https://media.giphy.com/media/seVVu09CPz2upPeU1s/giphy.gif)

Знаком `%` (процентов) мы обозначаем остаток от деления. Оператор возвращает🔄 целый остаток от деления левого операнда на правый. Возвращаемое🔄 значение всегда получает знак делимого, а не делителя. Он использует встроенную функцию⚙️ modulo, для получения результата, которая является целочисленным остатком деления `let1` на `let2`.

`12 % 5` результат `2`

`NaN % 2` результат `NaN`

`1 % 2` результат `1`

`2 % 3` результат `2`

`4 % 2` результат `0`

`5.5 % 2` результат `1.5`

Проверьте все перечисленые примеры в `LIVE EDITOR` и сразу все поймете:

```jsx live
function learnJavaScript() {
  let modulo = 12 % 5
  return modulo
}
```

## Округление

![Balls](https://media.giphy.com/media/6glYLqOQ3dlok/giphy.gif)

Метод `Math.round()` возвращает🔄 число, округлённое к ближайшему целому. Если дробная часть числа больше, либо равна `0,5`, аргумент будет округлён до ближайшего большего целого. Если дробная часть числа меньше `0,5`, аргумент будет округлён до ближайшего меньшего целого.

`result = Math.round(20.49)` Вернёт значение 20

`result = Math.round(20.5)` Вернёт значение 21

проверьте сами:

```jsx live
function learnJavaScript() {
  let result = Math.round(20.49)
  return result
}
```

## React Native
Числа вставляются в `React Native` приложения также просто как и строки.

```SnackPlayer name=index.js
import * as React from 'react'
import { Text } from 'react-native'

const App = () => {
  const str = 999 
  return (
    <Text>{str}</Text>
)}


export default App
```
