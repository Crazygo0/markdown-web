# React Router DOM

## Примеры

### Основная маршрутизация

В приведенном ниже примере у нас имеется 3 страницы, обрабатываемые роутером: главная (home), контакты (about) и страница с пользователями (users). При клике по `<Link>` (ссылке) роутер рендерит соответствующий `<Route>` (маршрут, путь).

_Обратите внимание_: за сценой `<Link>` рендерит `<a>` с настоящим `href`, так что люди, использующие клавиатуру для навигации или экранные считываюющие устройства (screen readers), смогут без проблем пользоваться приложением.

```js
import React from 'react';
import {
  BrowserRouter as Router,
  Switch,
  Route,
  Link,
} from 'react-router-dom';

export const App = () => (
  <Router>
    <header>
      <nav>
        <ul>
          <li>
            <Link to="/">Главная</Link>
          </li>
          <li>
            <Link to="/about">Контакты</Link>
          </li>
          <li>
            <Link to="/users">Пользователи</Link>
          </li>
        </ul>
      </nav>
    </header>

    <main>
      {/* <Switch> рендерит первый <Route>, совпавший с URL */}
      <Switch>
        <Route path="/about">
          <About />
        </Route>
        <Route path="/users">
          <Users />
        </Route>
        <Route path="/">
          <Home />
        </Route>
      </Switch>
    </main>
  </Router>
);

const Home = () => <h2>Главная</h2>;

const About = () => <h2>Контакты</h2>;

const Users = () => <h2>Пользователи</h2>;
```

### Вложенный роутинг

Ниже приводится пример вложенного роутинга. Маршрут `/topics` загружает компонент `Topics`, который, в свою очередь, рендерит дальнейшие `<Route>` на основе значения `:id`.

```js
import React from 'react';
import {
  BrowserRouter as Router,
  Switch,
  Route,
  Link,
  useRouteMatch,
  useParams,
} from 'react-router-dom';

export const App = () => (
  <Router>
    <header>
      <nav>
        <ul>
          <li>
            <Link to="/">Главная</Link>
          </li>
          <li>
            <Link to="/about">Контакты</Link>
          </li>
          <li>
            <Link to="/topics">Темы</Link>
          </li>
        </ul>
      </nav>
    </header>

    <main>
      <Switch>
        <Route path="/about">
          <About />
        </Route>
        <Route path="/topics">
          <Topics />
        </Route>
        <Route path="/">
          <Home />
        </Route>
      </Switch>
    </main>
  </Router>
);

const Home = () => <h2>Главная</h2>;

const About = () => <h2>Контакты</h2>;

function Topics() {
  const match = useRouteMatch();

  return (
    <>
      <h2>Темы</h2>

      <nav>
        <ul>
          <li>
            <Link to={`${match.url}/components`}>
              Компоненты
            </Link>
          </li>
          <li>
            <Link to={`${match.url}/props-vs-state`}>
              Пропы против состояния
            </Link>
          </li>
        </ul>
      </nav>

      {/* Страница Topics имеет собственный <Switch> с маршрутами,
          основанными на URL /topics. Вы можете думать о втором
          <Route> как о странице для остальных тем
          или как о странице, отображаемой,
          когда ни одна из тем не выбрана */}
      <div>
        <Switch>
          <Route path={`${match.path}/:topicId`}>
            <Topic />
          </Route>
          <Route path={match.path}>
            <h3>Пожалуйста, выберите тему.</h3>
          </Route>
        </Switch>
      </div>
    </>
  );
}

function Topic() {
  const { topicId } = useParams();
  return <h3>Идентификатор выбранной темы: {topicId}</h3>;
}
```

## Основные компоненты

В `React Router` существует 3 категории компонентов:

- роутеры (routers), например, `<BrowserRouter>` или `<HashRouter>`
- маршруты (route matchers), например, `<Route>` или `<Switch>`
- и навигация (navigation), например, `<Link>`, `<NavLink>` или `<Redirect>`

Все компоненты, используемые в веб-приложении, должны быть импортированы из `react-router-dom`.

### Роутеры

Любая маршрутизация начинается с роутера. Для веб-проектов `react-router-dom` предоставляет `<BrowserRouter>` и `<HashRouter>`. Основное отличие между ними состоит в способе хранения URL и взаимодействия с сервером.

- `<BrowserRouter>` использует обычные URL. В этом случае URL выглядят как обычно, но требуется определенная настройка сервера. В частности, сервер должен обслуживать все страницы, используемые на клиенте. `Create React App` поддерживает это из коробки в режиме разработки и содержит инструкции для правильной настройки сервера.
- `<HashRouter>` хранить текущую локацию в хэш-части URL (после символа "#"), поэтому URL выглядит примерно так: `http://example.com/#/your/page`. Поскольку хэш не отправляется серверу, его специальная настройка не требуется.

Для использования роутера необходимо обернуть в него компонент верхнего уровня:

```js
import React from 'react';
import ReactDOM from 'react-dom';
import { BrowserRouter } from 'react-router-dom';

const App = () => <h1>Привет, React Router</h1>;

ReactDOM.render(
  <BrowserRouter>
    <App />
  </BrowserRouter>,
  document.getElementById('root')
);
```

### Маршруты

Существует 2 вида компонентов для поиска совпадений с URL: `Switch` и `Route`. При рендеринге `<Switch>` определяет `<Route>`, соответствующий текущему URL. При обнаружении такого маршрута, он рендерится, остальные маршруты игнорируются. Это означает, что вы должны помещать более специфические маршруты перед менее специфическими.

Если совпадения не найдено, `<Switch>` ничего не рендерит (точнее, рендерит `null`).

```js
import React from 'react';
import ReactDOM from 'react-dom';
import {
  BrowserRouter as Router,
  Switch,
  Route,
} from 'react-router-dom';

const App = () => (
  <main>
    <Switch>
      {/* Если текущим URL является /about, рандерится данный маршрут,
          остальные игнорируются */}
      <Route path="/about">
        <About />
      </Route>

      {/* Обратите внимание на порядок расположения этих двух маршрутов.
          Более специфический path="/contact/:id" находится перед path="/contact" */}
      <Route path="/contact/:id">
        <Contact />
      </Route>
      <Route path="/contact">
        <AllContacts />
      </Route>

      {/* Если ни один из предыдущих роутеров не совпал,
          рендерится данный маршрут (он является резервным).

          Важно: маршрут с path="/" всегда будет совпадать с
          URL, поскольку все URL начинаются с /. Поэтому
          мы поместили его последним */}
      <Route path="/">
        <Home />
      </Route>
    </Switch>
  </main>
);

ReactDOM.render(
  <Router>
    <App />
  </Router>,
  document.getElementById('root')
);
```

_Обратите внимание_, что `<Route path>` ищет совпадение с началом, а не со всем URL. Поэтому `<Route path="/">` всегда будет совпадать с URL. Поэтому в `<Switch>` мы, обычно, помещаем его последним. Другим возможным решением является использование атрибута `exact`: `<Route exact path="/">`, который заставляет роутер искать полное совпадение.

### Навигация

`React Router` предоставляет компонент `<Link>` для создания ссылок в приложении. При использовании `<Link>` в HTML рендерится `<a>`.

```js
<Link to="/">Главная</Link>
// <a href="/">Главная</a>
```

`<NavLink>` - это специальный тип `<Link>`, позволяющий определять стили для активного состояния ссылки.

```js
<NavLink to="/react" activeClassName="hurray">
  React
</NavLink>

// Когда URL является /react, рендерится это:
// <a href="/react" className="hurray">React</a>

// Когда URL является другим:
// <a href="/react">React</a>
```

Для принудительной навигации используется `<Redirect>`. При рендеринге `<Redirect>` выполняется перенаправление.

```js
<Redirect to="/login">
```

## API

### Хуки

`React Router` предоставляет несколько хуков для доступа к состоянию роутера и навигации внутри компонентов.

- useHistory
- useLocation
- useParams
- useRouteMatch

Указанные хуки предоставляют доступ к следующим объектам:

- history
- location
- match
- matchPath

#### useHistory

Данный хук предоставляет доступ к экземпляру истории (history instance), который может использоваться для навигации:

```js
import { useHistory } from 'react-router-dom';

function HomeButton() {
  const history = useHistory();

  function handleClick() {
    history.push('/home');
  }

  return (
    <button type="button" onClick={handleClick}>
      Вернуться на главную
    </button>
  );
}
```

#### history

Термины "история" (history) и "объект истории" (history object) являются ссылками на пакет <a href="https://github.com/ReactTraining/history">history</a>, одну из двух зависимостей `React Router` (вторая - сам `React`), представляющий собой несколько реализаций, позволяющих управлять историей сессии с помощью `JavaScript` в разных окружениях.

Объекты истории, как правило, имеют следующие свойства и методы:

- `length`: number - количество вхождений в стеке истории (history stack)
- `action`: string - текущая операция (`PUSH`, `REPLACE` или `POP`)
- `location`: object - текущая локация. Может иметь следующие свойства:
  - `pathname`: string - адрес URL
  - `search`: string - строка запроса URL
  - `hash`: string - хэш-фрагмент URL
  - `state`: object - специфичное для локации состояние, переданное, например, с помощью `push(path, state)` при помещении локации в стек. Доступно только в браузере и истории, хранящейся в памяти
- `push(path, [state])`: func - помещает новое вхождение в стек истории
- `replace(path, [state])`: func - заменяет текущее вхождение в стеке истории
- `go(n)`: func - перемещает указатель в стеке истории на n вхождений
- `goBack()`: func - эквивалент go(-1)
- `goForward()`: func - эквивалент go(1)
- `block(prompt)`: func - запрещает переход на другую страницу

#### useLocation

Данный хук возвращает объект локации (location object), содержащий информацию о текущем URL. Вы можете думать о нем как о `useState`, возвращающем новую локацию при изменении URL.

Это может быть полезным в ситуации, когда необходимо получить новое представление страницы с помощью инструмента веб-аналитики при загрузке новой страницы, как в следующем примере:

```js
import React from 'react';
import ReactDOM from 'react-dom';
import {
  BrowserRouter as Router,
  Switch,
  useLocation,
} from 'react-router-dom';

function usePageViews() {
  let location = useLocation();
  React.useEffect(() => {
    ga.send(['pageview', location.pathname]);
  }, [location]);
}

function App() {
  usePageViews();
  return <Switch>...</Switch>;
}

ReactDOM.render(
  <Router>
    <App />
  </Router>,
  node
);
```

#### location

Объект локации выглядит следующим образом:

```js
{
  key: 'ac3df4', // отсутствует в HashHistory
  pathname: '/somewhere',
  search: '?some=search-string',
  hash: '#howdy',
  state: {
    [userDefined]: true
  }
}
```

Объект локации доступен в:

- Компоненте `Route` как `this.props.location` (`props.location`)
- Пропе `render` компонента `Route` как `({ location }) => ()`
- Потомках (`children`) компонента `Route` как `({ location }) => ()`
- `withRouter` как `this.props.location`

Он также доступен в `history.location`.

Объект локации, в отличие от объекта истории, никогда не мутирует, поэтому его можно использовать для определения того, выполнялась ли навигация, например, для получения данных и запуска анимации.

Вы можете использовать `location` для навигации вместо строк в:

- `Link to` для веба
- `Link to` для React Native
- `Redirect to`
- `history.push`
- `history.replace`

Обычно, во всех перечисленных случаях мы используем строку, однако, когда необходимо добавить некоторое "состояние локации", которое будет доступным при возвращении приложения в данную локацию, можно использовать объект локации. Это может пригодиться в случае, когда определенные части интерфейса зависят от истории навигации, а не от путей (например, модульные окна).

```js
// обычно, это все, что нам нужно
<Link to="/somewhere"/>

// однако, вместо этого можно использовать location
const location = {
  pathname: '/somewhere',
  state: { fromDashboard: true }
}

<Link to={location}/>
<Redirect to={location}/>
history.push(location)
history.replace(location)
```

Наконец, `location` можно передавать в следующие компоненты:

- `Route`
- `Switch`

Это предотвратит использование ими актуальной локации из состоянии роутера. Это может быть полезным для анимации и отложенной навигации, а также для замены локации, в которой рендерится компонент.

#### useParams

Данный хук возвращает объект с параметрами URL в формате `ключ: значение`. Используется для доступа к `match.params` текущего `<Route>`:

```js
import React from 'react';
import ReactDOM from 'react-dom';
import {
  BrowserRouter as Router,
  Switch,
  Route,
  useParams,
} from 'react-router-dom';

function BlogPost() {
  const { slug } = useParams();
  return <div>Отображается пост {slug}</div>;
}

ReactDOM.render(
  <Router>
    <Switch>
      <Route exact path="/">
        <HomePage />
      </Route>
      <Route path="/blog/:slug">
        <BlogPost />
      </Route>
    </Switch>
  </Router>,
  node
);
```

#### useRouteMatch

Данный хук пытается найти совпадение для текущего URL подобно `<Route>`. Он может быть полезен для доступа к совпадающим данным без рендеринга `<Route>`.

Это позволяет вместо

```js
import { Route } from 'react-router-dom';

function BlogPost() {
  return (
    <Route
      path="/blog/:slug"
      render={({ match }) => {
        // работаем с match...
        return <div />;
      }}
    />
  );
}
```

делать так

```js
import { useRouteMatch } from 'react-router-dom';

function BlogPost() {
  const match = useRouteMatch('/blog/:slug');

  // работаем с match...
  return <div />;
}
```

`useRouteMatch`:

- без аргументов: возвращает объект совпадения текущего `<Route>`
- принимает один аргумент, эквивалентный пропу `matchPath.argument`. Это может быть `pathname` в виде строки, как в приведенном выше примере, или объект с пропами, принимаемыми `<Route>`, как в следующем примере:

```js
const match = useRouteMatch({
  path: '/BLOG/:slug/',
  strict: true,
  sensitive: true,
});
```

#### match

Объект совпадения (match object) содержит информацию о том, насколько `<Route path>` совпадает с URL. Он имеет следующие свойства:

- `params`: object - пары ключ/значение, соответствующие динамической части URL
- `isExact`: bool - `true`, если имеет место совпадение
- `path`: string - паттерн пути, используемый для поиска совпадения. Используется для построения вложенных `<Route>`
- `url`: string - совпавшая часть URL. Используется для создания вложенных `<Link>`

Доступ к объекту совпадения можно получить в:

- `Route` как `this.props.match` (`props.match`)
- Пропе `render` компонента `Route` как `({ match }) => ()`
- Потомках `Route` как `({ match }) => ()`
  `withRouter` как `this.props.match`
  `matchPath` в виде возвращаемого значения
  `useRouteMatch` в виде возвращаемого значения

Если `Route` не имеет пропа `path` и поэтому всегда совпадает, мы получаем его ближайшего предка. Тоже самое справделиво для `withRouter`.

##### Совпадение с null

`<Route>`, имеющий проп `children`, вызывает функцию данного пропа даже при отсутствии совпадения с текущей локацией. В этой ситуации `match` будет иметь значение `null`. Может быть полезным иметь возможность рендерить контент `<Route>` при совпадении, но на этом пути существует несколько препятствий.

Обычный способ "разрешения" URL заключается в объединении строки `match.url` и "относительного" пути.

```js
const path = `${match.url}/relative-path`;
```

Если вы попытаетесь это сделать при нулевом совпадении, будет выброшено исключение `TypeError`. Это означает, что объединение "относительных" путей внутри `<Route>`, использующего для этого проп `children`, является небезопасным.

Похожая ситуация возникает при использовании `<Route>` без `path` внутри `<Route>`, генерирующего нулевой объект совпадения.

```js
// location.pathname = '/matches'
<Route path="/does-not-match"
  children={({ match }) => (
    // match === null
    <Route
      render={({ match: pathlessMatch }) => (
        // pathlessMatch === ???
      )}
    />
  )}
/>
```

`<Route>` без `path` наследует объект совпадения от предка. Если `match` предка равняется `null`, то его `match` также будет иметь значение `null`. Это означает, что, во-первых, любой дочерний маршрут/ссылка будут абсолютными (отсутствует предок для разрешения пути), во-вторых, маршрут без пути, родительский `match` которого может иметь значение `null`, должен будет использовать проп `children` для рендеринга.

#### matchPath

Позволяет использовать такой же код, что и `<Route>`, но за пределами нормального цикла рендеринга, например, на сервере для сбора информации об используемых данных перед рендерингом.

```js
import { matchPath } from 'react-router';

const match = matchPath('/users/123', {
  path: '/users/:id',
  exact: true,
  strict: false,
});
```

Принимает следующие аргументы:

- `pathname`: string - название пути для поиска совпадения. `req.path` на сервере
- `props` - пропы для поиска совпадения; соответствуют пропам, принимаемым `<Route>`

```js
{
  path, // например, /users/:id, строка или массив строк
  strict, // опционально, по умолчанию false
  exact, // опционально, по умолчанию false
}
```

При совпадении возвращается такой объект:

```js
matchPath('/users/2', {
  path: '/users/:id',
  exact: true,
  strict: true,
});

//  {
//    isExact: true
//    params: {
//        id: "2"
//    }
//    path: "/users/:id"
//    url: "/users/2"
//  }
```

В противном случае, возвращается `null`.

### `<Router>`

Общий низкоуровневый интерфейс для компонентов роутера. Обычно, используется один из следующих роутеров:

- `<BrowserRouter>`
- `<HashRouter>`
- `<MemoryRouter>`
- `<StaticRouter>`
- `<NativeRouter>`

Одним из случаев использования низкоуровневого `<Router>` является синхронизация пользовательской истории с такими библиотеками для управления состоянием приложения, как `Redux` или `MobX`. _Обратите внимание_, что делать этого не рекомендуется.

#### Пропы

- `history`: object - атрибут, используемый для навигации
- `children`: node - дочерний элемент

### `<BrowserRouter>`

`<Router>`, использующий `HTML5 history API` (события "pushState", "replaceState" и "popState") для синхронизации UI с URL.

```js
<BrowserRouter
  basename={optionalString}
  forceRefresh={optionalBool}
  getUserConfirmation={optionalFunc}
  keyLength={optionalNumber}
>
  <App />
</BrowserRouter>
```

#### Пропы

- `basename`: string - базовый URL для всех локаций. Если приложение обслуживается из поддиректории на сервере, базовый URL должен иметь значение данной поддиректории

```js
<BrowserRouter basename="/calendar">
    <Link to="/today"/> // рендерится как <a href="/calendar/today">
    <Link to="/tomorrow"/> // рендерится как <a href="/calendar/tomorrow">
    ...
</BrowserRouter>
```

- `getUserConfirmation`: func - функция для подтверждения перехода на другую страницу (по умолчанию используется `window.confirm`)

```js
<BrowserRouter
  getUserConfirmation={(message, callback) => {
    // поведение по умолчанию
    const allowTransition = window.confirm(message);
    callback(allowTransition);
  }}
/>
```

- `forceRefresh`: bool - если `true`, выполняется полное обновление страницы. Используется для имитации поведения сервера при переключении страниц
- `keyLength`: number - длина `location.key` (по умолчанию равняется 6)
- `children`: node - дочерние элементы

### `<HashRouter>`

`<Router>`, использующий хэш-часть URL (т.е. `window.location.hash`) для синхронизации UI с URL.

_Обратите внимание_, что хэш-история не поддерживает `location.key` или `location.state`.

```js
<HashRouter
  basename={optionalString}
  getUserConfirmation={optionalFunc}
  hashType={optionalString}
>
  <App />
</HashRouter>
```

#### Пропы

- `basename`: string - базовый URL для всех локаций

```js
<HashRouter basename="/calendar"/>
<Link to="/today"/> // рендерится как <a href="#/calendar/today">
```

- `getUserConfirmation`: func - функция для подтверждения перехода на другую страницу (по умолчанию используется `window.confirm`)
- `hashType`: string - тип кодировки для `window.location.hash`. Доступные значения:
  - `slash` - `#/` и `#/sunshine/lollipops` (значение по умолчанию)
  - `noslash` - `#` и `#sunshine/lollipops`
  - `hashbang` - `#!/` и `#!/sunshine/lollipops` (признан устаревшим в Chrome)
- `children`: node - дочерний элемент

### `<MemoryRouter>`

`<Router>`, хранящий историю URL в памяти (не читает и не пишет в адресную строку). Используется для тестирования и вне браузера (например, в `React Native`).

```js
<MemoryRouter
  initialEntries={optionalArray}
  initialIndex={optionalNumber}
  getUserConfirmation={optionalFunc}
  keyLength={optionalNumber}
>
  <App />
</MemoryRouter>
```

#### Пропы

- `initialEntries`: array - массив локаций в стеке истории. Локации могут быть полноценными объектами с `{ pathname, search, hash, state }` или строками

```js
<MemoryRouter
  initialEntries={['/one', '/two', { pathname: '/three' }]}
  initialIndex={1}
>
  <App />
</MemoryRouter>
```

- `initialIndex`: number - индекс начальной локации в массиве `initialEntries`
- `getUserConfirmation`: func - функция для подтверждения перехода на другую страницу (по умолчанию используется `window.confirm`)
- `keyLength`: number - длина `location.key` (по умолчанию - 6)
- `children`: node - дочерние элементы

### `<StaticRouter>`

`<Router>`, не изменяющий локацию. Используется в сценариях рендеринга на стороне сервера и для тестирования результатов рендеринга при подключении определенной локации.

Пример node-сервера, отправляющего статус-код 302 для `<Redirect>` и обычный HTML в ответ на другие запросы:

```js
import http from 'http';
import React from 'react';
import ReactDOMServer from 'react-dom/server';
import { StaticRouter } from 'react-router';

http
  .createServer((req, res) => {
    // Данный объект контекста содержит результаты рендеринга
    const context = {};

    const html = ReactDOMServer.renderToString(
      <StaticRouter location={req.url} context={context}>
        <App />
      </StaticRouter>
    );

    // context.url будет содержать URL для перенаправления при использовании <Redirect>
    if (context.url) {
      res.writeHead(302, {
        Location: context.url,
      });
      res.end();
    } else {
      res.write(html);
      res.end();
    }
  })
  .listen(3000);
```

#### Пропы

- `basename`: string - базовый URL для всех локаций
- `location`: string - URL, принимаемый сервером (`req.url`)
- `location`: object - объект локации вида `{ pathname, search, hash, state }`
- `context`: object - обычный JS-объект. В процессе рендеринга компоненты могут добавлять свойства к этому объекту для хранения информации о рендеринге

```js
const context = {}
<StaticRouter context={context}>
  <App />
</StaticRouter>
```

При совпадении, `<Route>` передает компоненту, подлежащему рендерингу, объект контекста как проп `staticContext`. После рендеринга, эти свойства могут использоваться для настройки ответа сервера:

```js
if (context.status === '404') {
  // ...
}
```

- `children`: node - дочерние элементы

### `<Link>`

- `<NavLink>`

Обеспечивает декларативный и доступный способ навигации в приложении.

```js
<Link to="/about">Контакты</Link>
```

#### Пропы

- `to`: string - строковое представление локации, создаваемое посредством объединения свойств "pathname", "search" и "hash"

```js
<Link to="/courses?sort=name" />
```

- `to`: object - объект, который может иметь следующие свойства:
  - `pathname`: string - название пути
  - `search`: string - параметры строки запроса
  - `hash`: string - хэш-часть URL
  - `state`: object - состояние локации

```js
<Link
  to={{
    pathname: '/courses',
    search: '?sort=name',
    hash: '#the-hash',
    state: { fromDashboard: true },
  }}
/>
```

- `to`: func - функция, которой в качестве аргумента передается текущая локация и которая должна вернуть представление локации в виде строки или объекта

```js
<Link to={location => ({ ...location, pathname: "/courses" })} />
<Link to={location => `${location.pathname}?sort=name`} />
```

- `replace`: bool - если `true`, тогда новая локация заменяет текущую в стеке истории, а не добавляется к ней

```js
<Link to="/courses" replace />
```

- `component`: React.Component - для реализации собственного компонента навигации достаточно передать данный проп

```js
const FancyLink = React.forwardRef((props, ref) => (
  <a ref={ref} {...props}>💅 {props.children}</a>
))

<Link to="/" component={FancyLink} />
```

- другие - `title`, `id`, `className` и т.д.

### `<NavLink>`

Специальная версия `<Link>`, предназначенная для добавления стилей к элементу, совпадающему с текущим URL (активному элементу).

```js
<NavLink to="/about">About</NavLink>
```

#### Пропы

- `activeClassName`: string - класс активного элемента. Значением по умолчанию является `active`. Объединяется с пропом `className`

```js
<NavLink to="/faq" activeClassName="selected">
  Часто задаваемые вопросы
</NavLink>
```

- `activeStyle`: object - стили, применяемые к активному элементу

```js
<NavLink
  to="/faq"
  activeStyle={{
    fontWeight: 'bold',
    color: 'red',
  }}
>
  Часто задаваемые вопросы
</NavLink>
```

- `exact`: bool - если `true`, тогда активный класс/стили применяются только при точном совпадении
- `strict`: bool - если `true`, тогда при определении совпадения учитывается замыкающий (последний) слэш
- `isActive`: func - дополнительная логика для определения активности ссылки

```js
<NavLink
  to="/events/123"
  isActive={(match, location) => {
    if (!match) {
      return false;
    }

    // событие считается активным только при условии, что его идентификатор является нечетным числом
    const eventID = parseInt(match.params.eventID);
    return !isNaN(eventID) && eventID % 2 === 1;
  }}
>
  Событие 123
</NavLink>
```

- `location`: object - используется для сравнения с другой локацией
- `aria-current`: string - значение атрибута `aria-current` активной ссылки. Возможные значения: `page` (значение по умолчанию), `step`, `location`, `date`, `time`, `true`, `false`.

### `<Switch>`

Рендерит первый дочерний `<Route>` или `<Redirect>` при совпадении с текущей локацией (URL).

**В чем состоит особенность `<Switch>`?**

Особенность `<Switch>` состоит в том, что он рендерит только один маршрут из набора. Без `<Switch>` рендерится каждый маршрут, совпавший с локацией.

```js
import { Route } from 'react-router';

const routes = (
  <div>
    <Route path="/about">
      <About />
    </Route>
    <Route path="/:user">
      <User />
    </Route>
    <Route>
      <NoMatch />
    </Route>
  </div>
);
```

В приведенном примере при значении URL, равном `/about`, все 3 компонента будут совпадать с локацией и отрендерятся. Это позволяет выстраивать композицию компонентов ("сайдбары" - sidebars, "хлебные крошки" - breadcrumbs, "табы" - tabs и т.д.).

Тем не менее, обычно, мы хотим рендерить только один `<Route>`. Если мы находимся в `/about`, то едва ли мы хотим рендерить компонент `<User />` или страницу ошибки 404. Вот как добиться этого с помощью `<Switch>`:

```js
import { Route, Switch } from 'react-router';

const routes = (
  <Switch>
    <Route exact path="/">
      <Home />
    </Route>
    <Route path="/about">
      <About />
    </Route>
    <Route path="/:user">
      <User />
    </Route>
    <Route>
      <NoMatch />
    </Route>
  </Switch>
);
```

Это также может быть полезным для выполнения анимированных переходов, поскольку новый маршрут рендерится на той же позиции, что и предыдущий.

#### Пропы

- `location`: object - используется для поиска совпадения вместо текущего объекта локации (текущего браузерного URL)
- `children`: node - потомки `<Switch>` должны быть элементами `<Route>` или `<Redirect>`. `<Route>` совпадает по пропу `path`, `<Redirect>` - по пропу `from`. Указанные элементы без соответствующих пропов всегда совпадают. При включении `<Redirect>` в `<Switch>`, в последнем могут использоваться все пропы `<Route>` (`path`, `exact` и `strict`). Проп `from` - это синоним пропа `path`. Если в `<Switch>` передан проп `location`, значение `location` совпавшего потомка будет перезаписано.

```js
import { Redirect, Route, Switch } from 'react-router';

let routes = (
  <Switch>
    <Route exact path="/">
      <Home />
    </Route>

    <Route path="/users">
      <Users />
    </Route>
    <Redirect from="/accounts" to="/users" />

    <Route>
      <NoMatch />
    </Route>
  </Switch>
);
```

### `<Route>`

Данный компонент является ключевым в `React Router`. Поэтому важно хорошо знать, как он работает. В основном, он отвечает за рендеринг определенного UI при совпадении значения его пропа `path` с текущим URL.

Рассмотрим следующий код:

```js
import React from 'react';
import ReactDOM from 'react-dom';
import {
  BrowserRouter as Router,
  Route,
} from 'react-router-dom';

ReactDOM.render(
  <Router>
    <div>
      <Route exact path="/">
        <Home />
      </Route>
      <Route path="/news">
        <NewsFeed />
      </Route>
    </div>
  </Router>,
  node
);
```

Если локацией приложения будет `/`, то иерархия UI будет выглядеть так:

```js
<div>
  <Home />
  <!-- react-empty: 2 -->
</div>
```

А для локации `/news` так:

```js
<div>
  <!-- react-empty: 1 -->
  <NewsFeed />
</div>
```

Комментарии "react-empty" - это детали реализации нулевого рендеринга. Технически, маршрут рендерится всегда: при совпадении с текущей локацией рендерится компонент, при несовпадении - `null`. Если один и тот же компонент является потомком нескольких `<Route>`, `React` будет рассматривать его как один и тот же экземпляр и состояние компонента будет автономным, т.е. компонент не будет перерисовываться при изменении локации. Во избежание этого к каждому `<Route>` добавляется проп `key` с уникальным значением.

#### Методы рендеринга маршрута

Рекомендуемым способом рендеринга является использование дочерних элементов как в приведенном выше примере. Тем не менее, существует и другие способы:

- `<Route component>`
- `<Route render>`
- `<Route children>`

Следует придерживаться одного стиля.

#### Пропы маршрута

Все 3 метода рендеринга принимают следующие пропы:

- `match`
- `location`
- `history`

#### component

Компонент, подлежащий рендерингу при совпадении с локацией. Данному компоненту доступны все пропы маршрута:

```js
import React from 'react';
import ReactDOM from 'react-dom';
import {
  BrowserRouter as Router,
  Route,
} from 'react-router-dom';

// Все пропы маршрута (match, location и history) доступны для User
const User = (props) => (
  <h1>Привет, {props.match.params.username}!</h1>
);

ReactDOM.render(
  <Router>
    <Route path="/user/:username" component={User} />
  </Router>,
  node
);
```

При использовании `component` (вместо `render` или `children`), маршрут использует `React.createElement` для создания нового React-элемента. Это означает, что при передаче встроенной функции в качестве пропа компонента, при каждом рендеринге будет создаваться новый компонент. Это приводит к размонтированию/монтированию нового компонента вместо обновления существующего. Поэтому при необходимости передачи встроенной функции следует использовать `render` или `children`.

#### render: func

Это позволяет реализовать встроенный рендеринг без нежелательного перемонтирования.

Вместо создания нового элемента с помощью пропа `component`, можно передать функцию, вызываемую при совпадении с локацией. Данная функция имеет доступ ко всем пропам маршрута:

```js
import React from 'react';
import ReactDOM from 'react-dom';
import {
  BrowserRouter as Router,
  Route,
} from 'react-router-dom';

// встроенный рендеринг
ReactDOM.render(
  <Router>
    <Route path="/home" render={() => <div>Главная</div>} />
  </Router>,
  node
);

// композиция
// Вы можете распаковать routeProps, чтобы сделать их доступными для Component
const FadingRoute = ({ component: Component, ...rest }) => (
  <Route
    {...rest}
    render={(routeProps) => (
      <FadeIn>
        <Component {...routeProps} />
      </FadeIn>
    )}
  />
);

ReactDOM.render(
  <Router>
    <FadingRoute path="/cool" component={Something} />
  </Router>,
  node
);
```

#### children: func

Порой нам требуется условный рендеринг. В этом случае можно использовать функцию в качестве значения пропа `children`. Она работает как `render`, за исключением того, что вызывается в зависимости от совпадения с локацией.

Данный проп принимает те же пропы маршрута. При несовпадении маршрута, проп `match` будет иметь значение `null`. Это позволяет динамически обновлять UI. В приведенном ниже примере мы динамически добавляем класс `active`:

```js
import React from 'react';
import ReactDOM from 'react-dom';
import {
  BrowserRouter as Router,
  Link,
  Route,
} from 'react-router-dom';

const ListItemLink = ({ to, ...rest }) => (
  <Route
    path={to}
    children={({ match }) => (
      <li className={match ? 'active' : ''}>
        <Link to={to} {...rest} />
      </li>
    )}
  />
);

ReactDOM.render(
  <Router>
    <ul>
      <ListItemLink to="/somewhere" />
      <ListItemLink to="/somewhere-else" />
    </ul>
  </Router>,
  node
);
```

Это также может использоваться для анимации:

```js
<Route
  children={({ match, ...rest }) => (
    {/* Animate будет рендерится всегда, поэтому можно использовать жизненный цикл
        для анимации монтирования/размонтирования его потомков */}
    <Animate>
      {match && <Something {...rest}/>}
    </Animate>
  )}
/>
```

#### Пропы

- `path`: string, string[] - любой валидный URL или массив таких URL (маршрут без `path` совпадает с любой локацией)

```js
<Route path="/users/:id">
  <User />
</Route>
<Route path={["/users/:id", "/profile/:id"]}>
  <User />
</Route>
```

- `exact`: bool - если `true`, осуществляется поиск точного совпадения с `location.pathname`

```js
<Route exact path="/one">
  <About />
</Route>
```

- `strict`: bool - если `true`, при поиске совпадения учитывается замыкающий слэш
- `location`: object - используется для поиска совпадения с указанной локацией вместо текущей
- `sensitive`: bool - если `true`, при поиске совпадения учитывается регистр

### `<Redirect>`

Рендеринг `<Redirect>` приводит к перемещению в новую локацию. Новая локация перезаписывает текущую в стеке истории, как при серверном перенаправлении (HTTP 3xx).

```js
<Route exact path="/">
  {loggedIn ? (
    <Redirect to="/dashboard" />
  ) : (
    <PublicHomePage />
  )}
</Route>
```

#### Пропы

- `to`: string - любой валидный URL
- `to`: object - объект локации для перенаправления

```js
<Redirect
  to={{
    pathname: '/login',
    search: '?utm=your+face',
    state: { referrer: currentLocation },
  }}
/>
```

В компоненте `Login` объект `state` доступен через `props.location.state`, а ключ `referrer` - через `props.state.referrer`.

- `push`: bool - если `true`, новая локация добавляется в стек истории, а не заменяет текущую
- `from`: string - любой валидный URL. Может использоваться только при включении в `<Switch>`

```js
<Switch>
  <Redirect from="/old-path" to="/new-path" />
  <Route path="/new-path">
    <Place />
  </Route>
</Switch>

// Перенаправление с совпавшими параметрами
<Switch>
  <Redirect from="/users/:id" to="/users/profile/:id" />
  <Route path="/users/profile/:id">
    <Profile />
  </Route>
</Switch>
```

- `exact`: bool - точное совпадение, аналог `Route.exact`. Может использоваться только совместно с `from`
- `strict`: bool - учет замыкающего слэша, аналог `Route.strict`. Может использоваться только совместно с `from`
- `sensitive`: bool - учет регистра, аналог `Route.sensitive`

### `<Prompt>`

Используется для обращения к пользователю перед переключением страницы. Это может быть полезным для предотвращения преждевременного или случайного переключения страницы пользователем (например, при наполовину заполненной форме).

```js
<Prompt
  when={formIsHalfFilledOut}
  message="Вы уверены, что хотите покинуть страницу?"
/>
```

#### Пропы

- `message`: string - сообщение, выводимое при попытке пользователя перейти на другую страницу
- `message`: func - вызывается со следующей локацией и операцией при попытке пользователя перейти на другую страницу. Возвращает строку - сообщение для пользователя или `true` для выполнения перехода

```js
<Prompt
  message={(location, action) => {
    if (action === 'POP') {
      console.log('Возвращаемся назад...');
    }

    return location.pathname.startsWith('/app')
      ? true
      : `Вы уверены, что хотите перейти к ${location.pathname}?`;
  }}
/>
```

- `when`: bool - вместо условного рендеринга `<Prompt>`, можно рендерить его всегда, передавая `when={true}` или `when={false}` для контроля навигации

### generatePath

Функция `generatePath` может вызываться для генерации URL для маршрутов. В ней используется библиотека `path-to-regexp`.

```js
import { generatePath } from 'react-router';

generatePath('/user/:id/:entity(posts|comments)', {
  id: 1,
  entity: 'posts',
});
// Возвращается /user/1/posts
```

Результаты компиляции путей кэшируются, так что генерация множества путей на основе одного шаблона не приводит к лишнему расходу памяти.

#### Аргументы

- `pattern`: string - шаблон, передаваемый как атрибут `path` в `<Route>`
- `params`: object - объект с параметрами для шаблона. При несовпадении параметров и пути, выбрасывается исключение

```js
generatePath('/user/:id/:entity(posts|comments)', {
  id: 1,
});
// TypeError: Expected "entity" to be defined (Ожидалось, что "entity" будет определено)
```

### withRouter

С помощью компонента высшего порядка `withRouter` можно получить доступ к свойствам объекта `history` и `match` ближайшего маршрута. `withRouter` передает дочернему компоненту обновленные пропы `match`, `location` и `history` при его рендеринге:

```js
import React from 'react';
import PropTypes from 'prop-types';
import { withRouter } from 'react-router';

// Простой компонент, отображающий название пути текущей локации
class ShowTheLocation extends React.Component {
  static propTypes = {
    match: PropTypes.object.isRequired,
    location: PropTypes.object.isRequired,
    history: PropTypes.object.isRequired,
  };

  render() {
    const { match, location, history } = this.props;

    return (
      <div>Вы находитесь здесь: {location.pathname}</div>
    );
  }
}

// Создаем новый компонент, который "подключен" к роутеру
const ShowTheLocationWithRouter = withRouter(
  ShowTheLocation
);
```

_Обратите внимание_, `withRouter` не подписывается на изменение локации подобно подключению `React Redux` к изменению состояния. Повторный рендеринг после изменения локации "распространяется" от `<Router>`. Это означает, что `withRouter` перерисовывается только вслед за родительским компонентом.

_Статические методы и свойства_ (не принадлежащие React) оборачиваемого компонента автоматически копируются в "подключенный" компонент.

- `Component.WrappedComponent` - оборачиваемый компонент преобразуется в статическое свойство `WrappedComponent` возвращаемого компонента, что, помимо прочего, может использоваться для тестирования компонента в изоляции.

```js
// MyComponent.js
export default withRouter(MyComponent)

// MyComponent.test.js
import MyComponent from './MyComponent'
render(<MyComponent.WrappedComponent location={{...}} ... />)
```

- `wrappedComponentRef`: func - функция, передаваемая оборачиваемому компоненту в качестве пропа `ref`

```js
class Container extends React.Component {
  componentDidMount() {
    this.component.doSomething();
  }

  render() {
    return (
      <MyComponent
        wrappedComponentRef={(c) => (this.component = c)}
      />
    );
  }
}
```

## Рендеринг на стороне сервера

Маршрутизация на стороне сервера немного отличается ввиду отсутствия состояния. Основная идея состоит в том, что компонент верхнего уровня оборачивается в `<StaticRoute>` вместо `<BrowserRoute>`. Затем мы передаем роутеру запрашиваемый URL и контекст.

```js
// клиент
<BrowserRouter>
  <App/>
</BrowserRouter>

// сервер (это еще не все)
<StaticRouter
  location={req.url}
  context={context}
>
  <App/>
</StaticRouter>
```

При рендеринге `<Redirect>` на клиенте, история браузера изменяется, и мы получаем новое представление (видим новый экран). В статическом серверном окружении мы не может менять состояние приложения. Вместо этого, мы используем проп `context` для определения результата рендеринга. Если мы обнаруживаем `context.url`, значит, имело место перенаправление. Это позволяет выполнять перенаправление на сервере.

```js
const context = {};
const markup = ReactDOMServer.renderToString(
  <StaticRouter location={req.url} context={context}>
    <App />
  </StaticRouter>
);

if (context.url) {
  // где-то был отрендерен <Redirect>
  redirect(301, context.url);
} else {
  // все в порядке, отправляем ответ
}
```

### Добавление информации о контексте

Роутер просто добавляет `context.url`. Однако, вам может потребоваться указать код 301 или 302. Или вы хотите отправлять ответ 404 для некоторых частей UI, или 401 при отсутствии авторизации. Проп `context` находится в вашем распоряжении, так что вы можете его изменять. Ниже приводится способ указания кодов 301 и 302:

```js
const RedirectWithStatus = ({ from, to, status }) => (
  <Route
    render={({ staticContext }) => {
      // на клиенте отсутствует `staticContext`
      // так что следует выполнить проверку
      if (staticContext) staticContext.status = status;

      return <Redirect from={from} to={to} />;
    }}
  />
);

// где-то в приложении
const App = () => (
  <Switch>
    {/* другие маршруты */}
    <RedirectWithStatus
      status={301}
      from="/users"
      to="/profiles"
    />
    <RedirectWithStatus
      status={302}
      from="/courses"
      to="/dashboard"
    />
  </Switch>
);

// на сервере
const context = {};

const markup = ReactDOMServer.renderToString(
  <StaticRouter context={context}>
    <App />
  </StaticRouter>
);

if (context.url) {
  // мы можем использовать `context.status`,
  // который мы добавили в RedirectWithStatus
  redirect(context.status, context.url);
}
```

### 404, 401 или любой другой статус

Делаем тоже самое. Создаем компонент, добавляющий контекст, и рендерим его в приложении для получения разных статус-кодов.

```js
const Status = ({ code, children }) => (
  <Route
    render={({ staticContext }) => {
      if (staticContext) staticContext.status = status;
      return children;
    }}
  />
);
```

После этого вы можете рендерить `Status` где угодно для получения кода для `staticContext`:

```js
const NotFound = () => (
  <Status code={404}>
    <div>
      <h1>Запрашиваемая страница отсутствует.</h1>
    </div>
  </Status>
);

const App = () => (
  <Switch>
    <Route path="/about" component={About} />
    <Route path="/dashboard" component={Dashboard} />
    <Route component={NotFound} />
  </Switch>
);
```

### Все вместе

_Сервер_:

```js
import http from 'http';
import React from 'react';
import ReactDOMServer from 'react-dom/server';
import { StaticRouter } from 'react-router-dom';

import App from './App.js';

http
  .createServer((req, res) => {
    const context = {};

    const html = ReactDOMServer.renderToString(
      <StaticRouter location={req.url} context={context}>
        <App />
      </StaticRouter>
    );

    if (context.url) {
      res.writeHead(301, {
        Location: context.url,
      });
      res.end();
    } else {
      res.write(`
      <!doctype html>
      <div id="root">${html}</div>
    `);
      res.end();
    }
  })
  .listen(3000);
```

_Клиент_:

```js
import ReactDOM from 'react-dom';
import { BrowserRouter } from 'react-router-dom';

import App from './App';

ReactDOM.render(
  <BrowserRouter>
    <App />
  </BrowserRouter>,
  document.getElementById('root')
);
```

### Загрузка данных

Данные должны загружаться перед рендерингом. `React Router` предоставляет статическую функцию `matchPath`, которая используется для определения маршрута. Вы можете использовать эту функцию на сервере для определения данных, которые потребуются приложению, перед рендерингом.

Суть данного подхода заключается в использовании статических настроек для определения данных по маршруту:

```js
const routes = [
  {
    path: '/',
    component: Root,
    loadData: () => getSomeData(),
  },
];
```

Затем этот конфиг используется для рендеринга маршрутов:

```js
import { routes } from './routes.js';

const App = () => (
  <Switch>
    {routes.map((route) => (
      <Route {...route} />
    ))}
  </Switch>
);
```

_Сервер_:

```js
import { matchPath } from 'react-router-dom';

// внутри запроса
const promises = [];
// используем `some` для имитации поведения `<Switch>` при выборе
// первого совпадения
routes.some((route) => {
  // используем `matchPath`
  const match = matchPath(req.path, route);
  if (match) promises.push(route.loadData(match));
  return match;
});

Promise.all(promises).then((data) => {
  // обрабатываем данные, чтобы клиент
  // имел к ним доступ при рендеринге приложения
});
```

Наконец, клиент должен каким-либо способом получить данные.

## Разделение кода (code splitting)

Одной из замечательных возможностей веба является то, что нам не нужно заставлять пользователей загружать все приложение целиком. Вы можете думать о разделении кода как о постепенной загрузке приложения. Для реализации этого мы будем использовать <a href="https://webpack.js.org/">`webpack`</a>, <a href="https://babeljs.io/docs/en/babel-plugin-syntax-dynamic-import/">`@babel-plugin-syntax-dynamic-import`</a> и <a href="https://github.com/gregberge/loadable-components">`loadable-components`</a>.

`Webpack` имеет встроенную поддержку динамического импорта, однако, при использовании <a href="https://babeljs.io/">`Babel`</a> для компиляции JSX в JavaScript требуется `@babel-plugin-syntax-dynamic-import`. Данный плагин позволяет Babel разбирать (парсить) динамический импорт, чтобы вебпак мог осуществить разделение кода. Ваш файл `.babelrc` должен выглядеть примерно так:

```js
{
  "presets": ["@babel/preset-react"],
  "plugins": ["@babel/plugin-syntax-dynamic-import"]
}
```

`loadable-components` - это библиотека для загрузки компонентов с помощью динамического импорта. Она значительно облегчает разделения кода за счет автоматической обработки всех крайних случаев.

```js
import loadable from '@loadable/component';
import Loading from './Loading.js';

export const LoadableComponent = loadable(
  () => import('./Dashboard.js'),
  {
    fallback: <Loading />,
  }
);
```

Это все, что нужно сделать. Просто используйте данный компонент в своем приложении. `fallback` - это компонент-заместитель на время загрузки настоящего компонента. `loadable-components` также может использоваться при рендеринге на стороне сервера.

## Восстановление прокрутки

### Прокрутка на верх страницы

В большинстве случаев нам требуется выполнить прокрутку на верх страницы из-за длинного контента, который при навигации, остается "прокрученным". Этого можно добиться с помощью компонента `<ScrollToTop>`, который будет выполнять прокрутку при каждой навигации:

```js
import { useEffect } from 'react';
import { useLocation } from 'react-router-dom';

export default function ScrollToTop() {
  const { pathname } = useLocation();

  useEffect(() => {
    window.scrollTo(0, 0);
  }, [pathname]);

  return null;
}
```

Помещаем этот компонент на верхнем уровне приложения, но внутри роутера:

```js
const App = () => (
  <Router>
    <ScrollToTop />
    <App />
  </Router>
);
```

Если в вашем приложении имеются вкладки, подключенные к роутеру, тогда, возможно, прокрутка на верх страницы при каждом переключении вкладки - это не то, что вам нужно. Как насчет компонента `<ScrollToTopInMount>`, выполняющего прокрутку к месту его расположения:

```js
import { useEffect } from 'react';

function ScrollToTopOnMount() {
  useEffect(() => {
    window.scrollTo(0, 0);
  }, []);
}

// рендерим данный компонент где-либо в приложении с помощью:
// <Route path="..." children={<LongContent />} />
const LongContent = () => (
  <div>
    <ScrollToTopOnMount />

    <h1>Страница с длинным контентом</h1>
    <p>...</p>
  </div>
);
```