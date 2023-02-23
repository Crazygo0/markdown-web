## Деструктуризация массивов и объектов

Деструктуризация в JavaScript это синтаксис присваивания, который позволяет удобно, в одну строку, извлечь данные из массивов и объектов.

## Деструктуризация объектов

![object](https://media.giphy.com/media/3o85xx7Yll3UyNVQf6/giphy.gif)

```jsx live
function learnJavaScript() {
  // Создаём объект `fruit`
  let fruit = {
    title: 'banana',
    group: 'tropical',
    quantity: 5
  }

  // Деструктуризация объекта `fruit`
  let { title, group, quantity } = fruit

  // Выводим на экран `title`
  return title
}
```

Свойства `title`, `group` и `quantity`, повторяют структуру объекта `fruit` и копируют свои значения в идентичные переменные 🔔 находящиеся в `{...}`. Поэтому, если вы поменяете переменные 🔔 в `{...}` местами, то код будет так же прекрасно работать, попробуйте в примере выше поменять переменные 🔔 местами.

## Видео

<YouTube videoId="AGB030qG0zA" />

### Вложенный объект

![bookmark](https://media.giphy.com/media/3og0IDyqVFNH7qFpAI/giphy.gif)

Мы также можем деструктурировать вложенный объект.

```jsx live
function learnJavaScript() {
  let fruit = {
    title: 'banana',
    group: 'tropical',
    quantity: {
      store: 5,
      storeHaus: 99
    }
  }

  let {
    title,
    quantity: { store: s1, storeHaus: s2 }
  } = fruit

  return title + ', ' + parseFloat(s1 + s2)
}
```

### Другие названия

Если вам нужно использовать названия переменных 🔔 отличные от названия свойств, то будет работать такой синтаксис:

```jsx live
function learnJavaScript() {
  let fruit = {
    title: 'banana',
    group: 'tropical',
    quantity: 5
  }
  // title -> a; group -> b; quantity -> c
  let { title: a, group: b, quantity: c } = fruit

  return a
}
```

### Дефолтные значения

Если в `{...}` вы напишете переменную 🔔 свойства, которой не будут найдены, то ей присвоится значение `undefined`. Для назначения переменной 🔔 дефолтного значение, это значение ей можно присвоить. Если вы попытаетесь присвоить значение переменной 🔔 свойства которой будут найдены, то ей присвоится значение свойства. Рассмотрим на примере.

![Dafault](https://media.giphy.com/media/3oEduLzte7jSNmq4z6/giphy.gif)

```jsx live
function learnJavaScript() {
  let fruit = {
    title: 'banana'
  }
  let { title = 'lime', group, quantity = 5 } = fruit

  return title + ', ' + group + ', ' + quantity
}
```

В `title` выводится значение свойства, а не то, что мы ей присваиваем. Свойства `group` в объекте `fruit` не существует, а переменной 🔔 никаких значений мы не присваивали. Свойства `quantity` также не существует, но переменной 🔔 мы присвоили значение `5`.

### Остаток

![octatok](https://media.giphy.com/media/hvddF1vHatFIgQspUB/giphy.gif)

Если вам нужно получить из объекта одну переменную 🔔 , а оставшиеся сгруппировать в другой объект, то используйте `...` перед переменной 🔔 из которой будет создан объект с оставшимися свойствами.

```jsx live
function learnJavaScript() {
  let fruit = {
    title: 'banana ',
    group: 'tropical ',
    quantity: 5
  }
  let { group, ...prop } = fruit

  return prop.title + group
}
```

## Деструктуризация массивов

Деструктуризация массива происходит так же, как и у объекта. Единственная разница в том, что значения элементов массива будут присваиваться переменным 🔔 в порядке определения элементов.

![Take](https://media.giphy.com/media/IuBlckSD7dQv6/giphy.gif)

```jsx live
function learnJavaScript() {
  // Создаем массив `fruit`
  let fruit = ['banana', 'tropical', 5]

  // Деструктурируем массив `fruit`
  let [title, group, quantity] = fruit

  // Выводим на экран
  return `${title}, ${group}, ${quantity}`
}
```

### Остаток

По аналогии с объектами работает остаток.

```jsx live
function learnJavaScript() {
  let fruit = ['banana ', 'tropical ', 5]

  let [name, ...prop] = fruit

  return `${name}, ${prop}`
}
```
### Копия массива

Пример создания🏗️ копии массива.

![Copia](https://media.giphy.com/media/GI1KnTxySlrCE/giphy.gif)

```jsx live
function learnJavaScript() {
  let fruit = ['banana ', 'tropical ', 5]

  let _fruit = [...fruit]

  return _fruit
}
```

### Объединение массивов

![add](https://media.giphy.com/media/3gMrhfFtWHq9XxtqPy/giphy.gif)

Пример объединения массивов в один.

```jsx live
function learnJavaScript() {
  let name = ['banana '],
    prop = ['tropical ', 5],
    fruit = [...name, ...prop]

  return fruit
}
```