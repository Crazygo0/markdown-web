## Import Export

Чтобы сделать объекты, функции, классы или переменные 🔔 доступными для внешнего мира, достаточно просто экспортировать их, а затем импортировать, где это необходимо, в другие файлы проекта.

## Видео

<YouTube videoId="eObrJvg0Y5s" />

## «Hello, World!» на Node.js

`Node.js®` — это JavaScript окружение построенное на движке [Chrome V8](https://v8.dev).

Начнем работу с `Node.js` просто набрав node в консоли:

```javascript
$ node
>
```

Если он у вас не стоит, то [скачайте](https://nodejs.org) его и установите на свой компьютер.

![Node](https://media.giphy.com/media/kdFc8fubgS31b8DsVu/giphy.gif)

А теперь давайте попробуем что-то напечатать:

```javascript
$ node
> console.log('hello from Node.js')
// После нажатия Enter вы получите следующее:
hello from Node.js
undefined
```

![Export](https://media.giphy.com/media/3ohzAiaRIBBrge2jQc/giphy.gif)

Не стесняйтесь эспериментировать с `Node.js` с помощью этого интерфейса: обычно тестируют небольшие фрагменты кода здесь, если не целесообразно помещать их сразу в файл.

Пришло время создать наше приложение Hello Node.js!

Начнем с создания файла `index.js`. Следующей командой мы создаем папку `myProject` и входим в нее.

```bash
mkdir myProject && cd myProject
```

Теперь создаем сам файл `index.js`

```bash
touch index.js
```

Откройте свой редактор кода или скачайте и установите его. Мы рекомендуем [VS Code](https://code.visualstudio.com).

Откройте редактор кода и добавьте в него папку созданого нами проекта.



Теперь откройте боковое меню нажав этот значок.



Cкопируйте в него следующий фрагмент кода:

```javascript
// index.js
console.log('hello from Node.js')
```

Чтобы запустить этот файл, вы должны снова открыть свой терминал и перейти в каталог, в котором размещён `index.js`.

В `VS Code` это можно сделать нажав на эти значки.



И выбрать таб `TERMINAL`



Как только вы успешно переместитесь в нужное место, запустите файл, используя команду

```javascript
node index.js
```

Вы увидите, что эта команда будет выдавать тот же результат, что и раньше, выводя строку непосредственно в терминале.



## Модульность приложения

![Export](https://media.giphy.com/media/3o7btSt2Et1GgIaDAY/source.gif)

Пришло время перейти на следующий уровень! Давайте создадим что-то более сложное, разделив наш исходный код на несколько JavaScript-файлов с целью удобочитаемости и поддерживаемости.

### Структура проекта

Создайте следующую структуру каталогов (с пустыми файлами), но пока не создавайте `package.json,` мы сгенерируем его автоматически на следующем шаге:

```javascript
├── app
|   ├── calc.js
|   └── index.js
├── index.js
└── package.json
```

Чтобы создать новый файл или папку в `VS Code` нажмите соответствующую иконку как показано на картинке.



### package.json

Каждый проект `Node.js` начинается с создания файла `package.json`. Вы можете думать о нем как о JSON-представлении приложения и его зависимостей. Он содержит имя вашего приложения, автора (вас) и все зависимости, необходимые для запуска приложения. Это карта вашего проекта.

Вы можете интерактивно генерировать файл `package.json` с помощью команды

![npm](https://media.giphy.com/media/gHnBLyeYE6hboT3t3o/giphy.gif)

```bash
npm init
```

в терминале. После запуска команды вас попросят ввести некоторые данные, например имя вашего приложения, версию, описание и так далее. Не нужно беспокоиться, просто нажимайте `Enter`, пока не получите сформированный JSON и вопрос `is it ok`?. Нажмите `Enter` в последний раз и вуаля: ваш `package.json` был автоматически сгенерирован и помещен в папку вашего приложения. Если вы откроете этот файл в своей IDE, он будет очень похож на фрагмент кода ниже.

```json
// package.json
{
  "name": "myproject",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC"
}
```

Хорошей практикой является добавление стартового скрипта в ваш пакет `package.json`. Поэтому добавьте в объект `scripts` строчку:

```json
"scripts": {
  "start": "node index.js", // эту строчку
  "test": "echo \"Error: no test specified\" && exit 1"
}
```

Как только вы это сделаете, вы можете запустить приложение с помощью команды `npm start`.

## Импорт

Теперь давайте вернемся к первому созданному вами файлу под названием `index.js`. Рекомендуется оставить этот файл очень компактным: только подключение самого приложения (файл `index.js` из подкаталога `/app`, созданного ранее). Скопируйте следующий код в свой файл `index.js` и сохраните:

```javascript
// index.js
require('./app/index')
```

или сокращеная запись для всех файлов `index.js`

```javascript
// index.js
require('./app')
```

Если не указан конкретный файл, то интерпретатор кода ищет файл `index.js` и заходит в него. Вот так просто мы подключили свой первый файл в проект.

![Export](https://media.giphy.com/media/W6Lidy1RgOl3kYdARr/giphy.gif)

## Экспорт

Теперь пришло время приступить к созданию реального приложения. Откройте файл `index.js` из папки `/app`, чтобы создать очень простой пример: добавление массива чисел. В этом случае файл `index.js` будет содержать только числа, которые мы хотим добавить, а логика, требующая вычислений, должна быть помещена в отдельный модуль в файле `calc.js`.
Вставьте этот код в файл `index.js` в каталоге `/app`.

```javascript
// app/index.js
const calc = require('./calc')
const numbersToAdd = [3, 4, 10, 2]
const result = calc.sum(numbersToAdd)

console.log(`The result is: ${result}`)
```

Теперь вставьте фактическую бизнес-логику в файл `calc.js,` который можно найти в той же папке.

```javascript
// app/calc.js
const sum = arr => {
  return arr.reduce((a, b) => a + b, 0)
}

module.exports.sum = sum // export
```

В этом файле мы создали функцию `sum` и экспортировали ее, сделали доступными в других файлах проекта.

Чтобы проверить, всё ли вы сделали правильно, сохраните эти файлы, откройте терминал и введите `npm start` или `node index.js`. Если все сделали правильно, то получите ответ: `19.` Если что-то пошло не так, внимательно просмотрите лог в консоли и найдите проблему на его основе.



## Итого

Вот мы и завершили с вами подготовительный, перед курсом по [мобильной разработке](https://jscamp.app/docs/start000), курс по JavaScript.