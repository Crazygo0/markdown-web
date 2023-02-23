## Замыкание

Замыкание - это функция⚙️, у которой имеется доступ к внешней функции⚙️, даже после того, как работа внешней функции️ прекратилась. Замыкание нужно, чтобы обеспечить доступ внутренней функции к области видимости внешней функции️, но при этом закрыть доступ из внешнего окружения к переменным внутренней функции⚙️.

![Snake](https://media.giphy.com/media/3oFzmdjqH15YebLQ52/giphy.gif)

Требования для создания🏗️ замыкания:

1. Внешняя функция, которая вызывается в коде.
2. Во внешней функции находится внутренняя функция.
3. В качестве результата внешняя функция возвращает внутреннюю.

Рассмотрим создание🏗️ замыкания на примере:

```jsx live
function learnJavaScript() {
  const getFruit = () => {
    let fruit = 'Banana',
      show = () => {
        return fruit
      }
    return show
  }
  let showFruit = getFruit()
  return showFruit()
}
```

1. В примере мы создали внешнюю функцию `getFruit`;
2. Внутри `getFruit` создали внутреннюю функцию `show`.
3. В качестве результата функция `getFruit` выдаёт функцию `show`.
4. Далее в коде мы присвоили результат функции `getFruit` переменной `showFruit`.
5. Т.к. результат работы `getFruit` является функцией, то `showFruit` становится не переменной🔔 , а функцией.
6. Результатом всей конструкции стала переменная🔔 `fruit` находящаяся внутри функции `getFruit`, она стала замкнутой. Теперь мы можем только узнать значение этой переменной🔔 , изменить её нельзя.

## Видео

<YouTube videoId="bsWqPzc4g-8" />

## Примеры

![Math](https://media.giphy.com/media/xT1Ra5h24Eliux3UVq/giphy.gif)

Рассмотрим больше примеров для понимания.

### Счётчик

Счётчик, самый простой пример, на котором можно рассмотреть работу замыкания.

<!-- ![Counter](https://media.giphy.com/media/QSNvClMu5zWJW/giphy.gif) -->

```jsx live
function learnJavaScript() {
  const makeCounter = () => {
    let x = 0
    return () => {
      return ++x
    }
  }
  const counter = makeCounter()
  return counter()
}
```

### Улучшенный счётчик

![Counter](https://media.giphy.com/media/3o6Zt6fzS6qEbLhKWQ/giphy.gif)

В качестве результата у нас будет не одна функция⚙️, а сразу несколько.

```jsx live
function learnJavaScipt() {
  let makeCounter = () => {
    let x = 0
    return {
      inc: () => {
        return ++x
      },
      dec: () => {
        return --x
      },
      val: () => {
        return x
      }
    }
  }

  let counter = makeCounter()
  counter.inc() // 1
  counter.inc() // 2
  counter.inc() // 3
  counter.inc() // 4
  counter.dec() // 3
  return counter.val()
}
```

### Замыкание в цикле

![circle](https://media.giphy.com/media/u5s2ezDicmyuA/giphy.gif)

```jsx live
function learnJavaScript() {
  let res = []
  for (let i = 0; i < 5; i++) {
    res[i] = () => {
      return i
    }
  }
  return res[2]()
}
```

### Запоминаем фразу

![l](https://media.giphy.com/media/l4pTfqyI6TCjUW4Yo/giphy.gif)

```jsx live
function learnJavaScript() {
  let phrase = x => {
    return y => {
      return x + ' ' + y
    }
  }

  hello = phrase('Hello')
  return hello('World')
}
```

## Итого

Замыкания — одна из важнейших фундаментальных концепций JavaScript, её должен понимать каждый JS-разработчик. Понимание 💡 замыканий — это одна из ступеней пути к написанию 🖊️ эффективных и качественных приложений.