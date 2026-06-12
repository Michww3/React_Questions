## Webpack

Webpack — это модульный сборщик (module bundler) для JavaScript-приложений. Он анализирует зависимости проекта, объединяет различные файлы в оптимизированные бандлы и подготавливает приложение для запуска в браузере.

Webpack позволяет работать не только с JavaScript, но и с другими ресурсами:

* CSS / SCSS.
* Изображения.
* Шрифты.
* TypeScript.
* JSX.

---

### Как работает Webpack?

Webpack строит граф зависимостей (Dependency Graph).

Например:

```
index.js
   |
   ├── App.jsx
   |      |
   |      └── Button.jsx
   |
   └── styles.css
```

Webpack анализирует все импорты:

```javascript
import App from "./App";
import "./styles.css";
```

После анализа он создает итоговые файлы:

```
dist/
 ├── main.js
 ├── styles.css
 └── assets/
```

---

### Основные понятия Webpack

### Entry (точка входа)

Файл, с которого начинается сборка.

Пример:

```javascript
module.exports = {
  entry: "./src/index.js"
};
```

---

### Output (результат сборки)

Определяет, куда будут помещены готовые файлы.

```javascript
module.exports = {
  output: {
    filename: "bundle.js",
    path: "./dist"
  }
};
```

---

### Loaders

Webpack сам понимает только JavaScript и JSON.

Loaders позволяют обрабатывать другие типы файлов.

Пример обработки JSX:

```javascript
module.exports = {
  module: {
    rules: [
      {
        test: /\.jsx$/,
        use: "babel-loader"
      }
    ]
  }
};
```

---

Популярные loaders:

| Loader       | Назначение           |
| ------------ | -------------------- |
| babel-loader | JSX, современный JS  |
| ts-loader    | TypeScript           |
| css-loader   | CSS                  |
| style-loader | Добавление CSS в DOM |
| file-loader  | Файлы                |

---

### Plugins

Plugins расширяют возможности Webpack.

Примеры:

* Генерация HTML.
* Минификация.
* Очистка папки сборки.
* Анализ размера бандла.

Популярные:

* `HtmlWebpackPlugin`
* `MiniCssExtractPlugin`
* `CleanWebpackPlugin`

---

### Mode

Webpack имеет три режима:

```javascript
mode: "development"
```

Разработка.

```javascript
mode: "production"
```

Продакшен.

```javascript
mode: "none"
```

Без оптимизаций.

---

### Dev Server

Webpack Dev Server запускает локальный сервер разработки:

```bash
webpack serve
```

Возможности:

* Hot Module Replacement (HMR).
* Автоматическая пересборка.
* Быстрая разработка.

---

### Code Splitting

Разделение большого бандла на несколько частей.

Например:

```javascript
import("./AdminPage");
```

Код страницы загрузится только при необходимости.

---

### Зачем нужен Webpack в React?

Webpack используется для:

* Трансформации JSX в JavaScript.
* Обработки CSS и изображений.
* Оптимизации production-сборки.
* Минификации кода.
* Разделения кода.
* Запуска dev-сервера.

---

# Что такое Virtual DOM и как он работает?

Virtual DOM (виртуальный DOM) — это легковесная JavaScript-копия настоящего DOM, которую React использует для эффективного обновления интерфейса.

---

## Проблема обычного DOM

Изменение настоящего DOM является относительно дорогой операцией.

Например:

```javascript
document.getElementById("title").innerHTML = "Hello";
```

Браузеру необходимо:

1. Изменить DOM.
2. Пересчитать стили.
3. Выполнить layout.
4. Перерисовать страницу.

---

## Как работает Virtual DOM?

Процесс состоит из нескольких этапов:

### 1. Создание Virtual DOM

React создает дерево объектов JavaScript:

```javascript
{
  type: "div",
  props: {
    children: "Hello"
  }
}
```

---

### 2. Изменение состояния

Например:

```javascript
setCount(count + 1);
```

React создает новое виртуальное дерево.

---

### 3. Diffing

React сравнивает старый Virtual DOM с новым.

Этот процесс называется:

**Reconciliation (согласование)**.

React ищет:

* Добавленные элементы.
* Удаленные элементы.
* Измененные свойства.

---

### 4. Reconciliation и обновление DOM

React применяет только необходимые изменения к реальному DOM.

---

Пример:

Было:

```jsx
<h1>Hello</h1>
```

Стало:

```jsx
<h1>Hello World</h1>
```

React изменит только текст внутри элемента.

---

## Преимущества Virtual DOM

1. Производительность.

Минимизация операций с настоящим DOM.

2. Декларативность.

Разработчик описывает состояние:

```jsx
return <h1>{name}</h1>;
```

React сам решает, что обновить.

3. Удобная модель разработки.

Нет необходимости вручную управлять DOM.

---

# React

React — это JavaScript-библиотека для создания пользовательских интерфейсов, разработанная компанией Meta Platforms.

Основная идея React — построение интерфейса из независимых компонентов.

---

## Основные концепции React

### Компоненты

Компонент — независимая часть UI.

Пример:

```jsx
function Button() {
  return (
    <button>
      Click
    </button>
  );
}
```

---

React поддерживает два типа компонентов:

* Function Components.
* Class Components.

---

# Function Components

Современный подход.

Это обычные JavaScript-функции, которые возвращают JSX.

Пример:

```jsx
function User({name}) {
  return (
    <h1>
      {name}
    </h1>
  );
}
```

---

Преимущества:

* Меньше кода.
* Используют Hooks.
* Проще тестировать.
* Основной подход в современных проектах.

---

# Class Components

Старый подход до появления Hooks.

Компоненты создаются через классы ES6.

Пример:

```jsx
class User extends React.Component {

  render() {
    return (
      <h1>
        {this.props.name}
      </h1>
    );
  }

}
```

---

## State в Class Components

```jsx
class Counter extends React.Component {

  constructor(props) {
    super(props);

    this.state = {
      count: 0
    };
  }


  render() {
    return (
      <button>
        {this.state.count}
      </button>
    );
  }

}
```

---

## Lifecycle методы Class Components

Жизненный цикл:

### componentDidMount()

Вызывается после первого рендера.

```javascript
componentDidMount() {
  console.log("Mounted");
}
```

Используется для:

* API запросов.
* Подписок.
* Инициализации.

---

### componentDidUpdate()

Вызывается после обновления.

```javascript
componentDidUpdate(prevProps) {
}
```

---

### componentWillUnmount()

Вызывается перед удалением компонента.

```javascript
componentWillUnmount() {
}
```

Используется для:

* Очистки таймеров.
* Отписки от событий.

---

# Props

Props (properties) — это данные, которые передаются от родительского компонента дочернему.

Props являются:

* Только для чтения.
* Неизменяемыми внутри компонента.

---

Пример:

Родитель:

```jsx
<User name="John" />
```

Дочерний компонент:

```jsx
function User(props) {
  return (
    <h1>
      {props.name}
    </h1>
  );
}
```

---

## Деструктуризация props

Вместо:

```jsx
function User(props) {
  return <h1>{props.name}</h1>;
}
```

Можно:

```jsx
function User({name}) {
  return <h1>{name}</h1>;
}
```

---

## Props в Class Components

```jsx
class User extends React.Component {

render() {
  return (
      <h1>
        {this.props.name}
      </h1>
    );
  }
}
```

---

## Передача функций через props

Родитель:

```jsx
<Button onClick={handleClick}/>
```

Дочерний:

```jsx
<button onClick={props.onClick}>
Click
</button>
```

---

# Какие хуки вы знаете?

Hooks — это функции React, которые позволяют использовать состояние и другие возможности React внутри функциональных компонентов.

Hooks появились в React 16.8.

---

# useState

Используется для хранения состояния.

Пример:

```jsx
const [count, setCount] = useState(0);
```

Изменение:

```javascript
setCount(count + 1);
```

---

# useEffect

Используется для выполнения побочных эффектов.

Например:

* API запросы.
* Таймеры.
* Подписки.

Пример:

```jsx
useEffect(() => {

 console.log("Mounted");

}, []);
```

---

# useContext

Используется для доступа к Context без передачи props.

```jsx
const value = useContext(UserContext);
```

---

# useReducer

Альтернатива `useState` для сложной логики состояния.

```jsx
const [state, dispatch] = useReducer(
 reducer,
 initialState
);
```

---

# useRef

Хранит значение между рендерами и позволяет получить ссылку на DOM.

Пример:

```jsx
const inputRef = useRef();

inputRef.current.focus();
```

---

# useMemo

Мемоизация вычислений.

Используется для оптимизации:

```jsx
const result = useMemo(
 () => calculate(value),
 [value]
);
```

---

# useCallback

Мемоизация функций.

```jsx
const handleClick = useCallback(() => {

}, []);
```

---

# useLayoutEffect

Похож на `useEffect`, но выполняется синхронно после изменения DOM до отрисовки браузером.

Используется для:

* Измерения размеров элементов.
* Синхронных DOM-изменений.

---

# useImperativeHandle

Настраивает значение, которое доступно через `ref`.

Используется вместе с:

```javascript
forwardRef()
```

---

# useId

Создает уникальные идентификаторы.

Пример:

```jsx
const id = useId();
```

Используется для:

* Accessibility.
* Связки label/input.

---

# Пользовательские хуки (Custom Hooks)

Можно создавать собственные хуки.

Пример:

```javascript
function useFetch(url) {

 const [data, setData] = useState(null);

 useEffect(() => {

   fetch(url)
     .then(res => res.json())
     .then(setData);

 }, [url]);

 return data;
}
```

---

# Правила использования Hooks

Hooks можно вызывать только:

1. На верхнем уровне компонента.

Нельзя:

```javascript
if(condition){
 useState();
}
```

---

2. Только внутри React-компонентов или Custom Hooks.

---

# В чем разница между состоянием и пропсами в React?

В React данные внутри компонентов могут храниться двумя основными способами:

* **Props (properties)** — данные, передаваемые компоненту извне.
* **State (состояние)** — внутренние данные компонента, которые могут изменяться во время работы приложения.

---

## Props

Props — это параметры компонента, которые передаются от родительского компонента к дочернему.

Пример:

```jsx
function User(props) {
  return (
    <h1>
      Hello, {props.name}
    </h1>
  );
}


function App() {
  return (
    <User name="John" />
  );
}
```

Компонент `User` получает значение `name` через props.

---

### Особенности Props

* Передаются только сверху вниз (от родителя к ребенку).
* Доступны только для чтения.
* Компонент не должен изменять свои props.
* Используются для передачи данных и функций.

---

Пример передачи функции:

```jsx
function Button({ onClick }) {
  return (
    <button onClick={onClick}>
      Click
    </button>
  );
}
```

---

# State

State — это внутреннее состояние компонента.

Используется, когда данные могут изменяться во время работы приложения.

Пример:

```jsx
function Counter() {

  const [count, setCount] = useState(0);

  return (
    <button onClick={() => setCount(count + 1)}>
      {count}
    </button>
  );

}
```

При изменении состояния React выполняет повторный рендер компонента.

---

## Особенности State

* Хранится внутри компонента.
* Может изменяться.
* Изменение вызывает повторный рендер.
* Управляется через `useState`, `useReducer` или `setState`.

---

## State в Class Components

```jsx
class Counter extends React.Component {

  constructor(props) {
    super(props);

    this.state = {
      count: 0
    };
  }


  render() {
    return (
      <button>
        {this.state.count}
      </button>
    );
  }

}
```

Изменение:

```javascript
this.setState({
  count: this.state.count + 1
});
```

---

## Сравнение Props и State

|                   | Props                  | State               |
| ----------------- | ---------------------- | ------------------- |
| Кто управляет     | Родительский компонент | Сам компонент       |
| Можно изменять    | Нет                    | Да                  |
| Назначение        | Передача данных        | Хранение состояния  |
| Вызывает ререндер | При изменении props    | При изменении state |
| Где хранится      | В родителе             | В компоненте        |

---

### Простое правило:

> Props используются для передачи данных в компонент, а State используется для хранения данных, которые принадлежат самому компоненту и могут изменяться.

---

# Что такое условный рендеринг в React?

Условный рендеринг (Conditional Rendering) — это отображение разных элементов интерфейса в зависимости от определенного условия.

В React условный рендеринг реализуется обычными JavaScript-условиями.

---

## Использование if

```jsx
function User({isLoggedIn}) {

  if (isLoggedIn) {
    return <h1>Welcome</h1>;
  }

  return <h1>Please login</h1>;
}
```

---

## Тернарный оператор

Часто используется внутри JSX.

```jsx
function App({isAdmin}) {

  return (
    <div>
      {
        isAdmin
          ? <AdminPanel />
          : <UserPanel />
      }
    </div>
  );

}
```

---

## Логический оператор `&&`

Используется для отображения элемента только при выполнении условия.

```jsx
function Notification({count}) {

  return (
    <div>
      {count > 0 && (
        <span>
          New messages: {count}
        </span>
      )}
    </div>
  );

}
```

Если `count` равен `0`, элемент не будет отображен.

---

## Оператор `||`

Используется для значения по умолчанию:

```jsx
function User({name}) {

  return (
    <h1>
      {name || "Guest"}
    </h1>
  );

}
```

---

## Условный рендеринг компонентов

```jsx
function App({role}) {

  return (
    <>
      {
        role === "admin"
          ? <Admin />
          : <User />
      }
    </>
  );

}
```

---

## Зачем используется?

* Отображение авторизации.
* Loading-состояния.
* Ошибки.
* Разные интерфейсы для разных ролей.
* Показ/скрытие элементов.

---

# Что такое контекст (Context) в React и для чего он используется?

Context API — это механизм React для передачи данных между компонентами без необходимости передавать props через каждый уровень дерева компонентов.

Проблема, которую решает Context, называется **Prop Drilling**.

---

## Проблема Prop Drilling

Например:

```
App
 |
User
 |
Profile
 |
Avatar
```

Если `Avatar` нужен пользователь:

```jsx
<App user={user}/>
```

↓

```jsx
<User user={user}/>
```

↓

```jsx
<Profile user={user}/>
```

↓

```jsx
<Avatar user={user}/>
```

Приходится передавать props через промежуточные компоненты.

---

## Создание Context

```jsx
const UserContext = React.createContext();
```

---

## Provider

Компонент, который предоставляет значение.

```jsx
function App() {

  const user = {
    name: "John"
  };

  return (
    <UserContext.Provider value={user}>
      <Profile />
    </UserContext.Provider>
  );

}
```

---

## Получение значения

Через `useContext`:

```jsx
function Profile() {

  const user = useContext(UserContext);

  return (
    <h1>
      {user.name}
    </h1>
  );

}
```

---

## Где используется Context?

Частые случаи:

* Тема приложения (Dark/Light mode).
* Авторизация.
* Локализация.
* Настройки приложения.
* Глобальные конфигурации.

---

## Context vs Redux

| Context                          | Redux                         |
| -------------------------------- | ----------------------------- |
| Встроен в React                  | Отдельная библиотека          |
| Простые глобальные данные        | Сложное управление состоянием |
| Меньше настроек                  | Больше возможностей           |
| Подходит для небольших состояний | Для больших приложений        |

---

# Что такое ключи (keys) в списках React-элементов и зачем они нужны?

`key` — это специальный атрибут React, который помогает определить, какие элементы списка были изменены, добавлены или удалены.

Keys используются при рендеринге коллекций.

---

Пример:

```jsx
const users = [
  {
    id: 1,
    name: "John"
  },
  {
    id: 2,
    name: "Mike"
  }
];


function Users() {

  return (
    <ul>
      {
        users.map(user => (
          <li key={user.id}>
            {user.name}
          </li>
        ))
      }
    </ul>
  );

}
```

---

## Зачем нужны keys?

React использует keys при процессе **Reconciliation**.

Они помогают понять:

* Какой элемент остался прежним.
* Какой был удален.
* Какой добавился.
* Какой нужно обновить.

---

## Плохой пример

Использование индекса массива:

```jsx
users.map((user, index) => (
  <User key={index} />
))
```

Это может привести к ошибкам.

Например:

Было:

```
[
 A,
 B,
 C
]
```

Добавили элемент:

```
[
 X,
 A,
 B,
 C
]
```

Индексы изменились, React может неправильно сопоставить элементы.

---

## Правила использования key

Хороший key:

```jsx
key={user.id}
```

Плохой:

```jsx
key={Math.random()}
```

Плохой:

```jsx
key={index}
```

если список может изменяться.

---

## Требования к key

Key должен быть:

* Уникальным среди соседних элементов.
* Стабильным.
* Предсказуемым.

---

# Что такое фрагменты (Fragments) в React?

Fragment — это специальный компонент React, который позволяет группировать несколько элементов без создания дополнительного DOM-элемента.

---

## Проблема без Fragment

React-компонент должен возвращать один корневой элемент.

Нельзя:

```jsx
function App() {

  return (
    <h1>Hello</h1>
    <p>World</p>
  );

}
```

Ошибка.

---

## Решение через div

```jsx
function App() {

  return (
    <div>
      <h1>Hello</h1>
      <p>World</p>
    </div>
  );

}
```

Но появляется лишний элемент в DOM:

```html
<div>
  <h1>Hello</h1>
  <p>World</p>
</div>
```

---

## Fragment

```jsx
function App() {

  return (
    <React.Fragment>
      <h1>Hello</h1>
      <p>World</p>
    </React.Fragment>
  );

}
```

В DOM:

```html
<h1>Hello</h1>
<p>World</p>
```

Дополнительного элемента нет.

---

## Короткая запись Fragment

```jsx
function App() {

  return (
    <>
      <h1>Hello</h1>
      <p>World</p>
    </>
  );

}
```

---

## Fragment с key

Если Fragment используется внутри списка, необходимо использовать полный синтаксис:

```jsx
items.map(item => (
  <React.Fragment key={item.id}>
    <h1>{item.name}</h1>
    <p>{item.description}</p>
  </React.Fragment>
))
```

Сокращенный вариант:

```jsx
<>
</>
```

не поддерживает `key`.

---

## Преимущества Fragment

* Не создает лишних DOM-узлов.
* Уменьшает количество элементов в DOM.
* Позволяет возвращать несколько элементов из компонента.
* Упрощает структуру HTML.

---

# Как использовать React DevTools для отладки приложения?

React DevTools — это расширение для браузера, которое позволяет анализировать и отлаживать React-приложения.

Оно доступно для:

* Google Chrome.
* Mozilla Firefox.
* Microsoft Edge.

Устанавливается как браузерное расширение **React Developer Tools**.

---

## Основные возможности React DevTools

### 1. Просмотр дерева компонентов

Вкладка **Components** показывает структуру React-компонентов.

Например:

```
App
 ├── Header
 ├── UserList
 │     └── UserItem
 └── Footer
```

Можно:

* Просматривать вложенность компонентов.
* Выбирать конкретный компонент.
* Смотреть его состояние и props.

---

## 2. Просмотр Props

Выбрав компонент:

```jsx
<User name="John" age={25}/>
```

React DevTools покажет:

```
Props

name: "John"
age: 25
```

Это позволяет быстро найти ошибки передачи данных.

---

## 3. Просмотр State

Для функционального компонента:

```jsx
function Counter() {

 const [count, setCount] = useState(0);

}
```

DevTools покажет:

```
Hooks

State: 0
```

После изменения:

```
State: 1
```

---

Для Class Component:

```jsx
class Counter extends React.Component {

 state = {
   count: 0
 }

}
```

будет отображаться:

```
State

count: 0
```

---

## 4. Проверка Hooks

React DevTools показывает используемые хуки:

```jsx
useState
useEffect
useMemo
useContext
```

Например:

```
Hooks

State
Effect
Context
```

---

## 5. Изменение Props и State

В режиме разработки можно изменять значения прямо через DevTools.

Например:

Было:

```javascript
count: 0
```

Можно изменить:

```javascript
count: 10
```

и увидеть результат в интерфейсе.

---

## 6. Проверка производительности

Вкладка **Profiler** позволяет анализировать:

* Время рендера компонентов.
* Причины повторного рендера.
* Медленные компоненты.

---

Пример:

```
App
 ├── UserList   120ms
 ├── Button      5ms
 └── Header     10ms
```

Можно определить, какой компонент снижает производительность.

---

## 7. Highlight Updates

Опция:

```
Highlight updates when components render
```

подсвечивает компоненты, которые повторно отрисовываются.

Используется для поиска лишних ререндеров.

---

# Как создать собственный хук в React?

Custom Hook (пользовательский хук) — это функция, которая позволяет вынести повторяющуюся логику React-компонентов в отдельный переиспользуемый модуль.

Главное правило:

> Имя пользовательского хука должно начинаться с `use`.

---

## Пример простого хука

Допустим, нужно управлять счетчиком.

Создаем:

```javascript
function useCounter(initialValue = 0) {

  const [count, setCount] = useState(initialValue);


  const increment = () => {
    setCount(count + 1);
  };


  const decrement = () => {
    setCount(count - 1);
  };


  return {
    count,
    increment,
    decrement
  };

}
```

---

Использование:

```jsx
function Counter() {

 const {
   count,
   increment,
   decrement
 } = useCounter(0);


 return (
   <>
     <h1>{count}</h1>

     <button onClick={increment}>
       +
     </button>

     <button onClick={decrement}>
       -
     </button>
   </>
 );

}
```

---

## Хук для работы с API

Пример:

```javascript
function useFetch(url) {

 const [data, setData] = useState(null);
 const [loading, setLoading] = useState(true);
 const [error, setError] = useState(null);


 useEffect(() => {

   fetch(url)
     .then(response => response.json())
     .then(data => {
       setData(data);
       setLoading(false);
     })
     .catch(error => {
       setError(error);
       setLoading(false);
     });

 }, [url]);


 return {
   data,
   loading,
   error
 };

}
```

---

Использование:

```jsx
function Users() {

 const {
   data,
   loading
 } = useFetch("/api/users");


 if (loading) {
   return <p>Loading...</p>;
 }


 return (
   <UserList users={data}/>
 );

}
```

---

## Правила Custom Hooks

Custom Hook:

* Может использовать другие хуки.
* Не должен вызываться внутри условий.
* Не должен вызываться внутри циклов.
* Должен начинаться с `use`.

---

## Преимущества Custom Hooks

* Повторное использование логики.
* Разделение ответственности.
* Уменьшение размера компонентов.
* Более удобное тестирование.

---

# Middleware (Thunk, Saga)

Middleware — это промежуточный слой между отправкой action и изменением состояния в Redux.

Схема работы:

```
Component
    |
 dispatch(action)
    |
 Middleware
    |
 Reducer
    |
 Store
    |
 UI
```

---

## Зачем нужны Middleware?

Redux по умолчанию работает только с синхронными объектами:

```javascript
{
 type: "ADD_USER",
 payload: user
}
```

Но реальные приложения требуют:

* API запросы.
* Таймеры.
* Логирование.
* Обработку ошибок.
* Асинхронные операции.

Для этого используются middleware.

---

# Redux Thunk

Redux Thunk — middleware, позволяющий отправлять функции вместо обычных объектов action.

---

Обычный action:

```javascript
{
 type: "GET_USERS"
}
```

Thunk:

```javascript
dispatch(function(dispatch){

});
```

---

Пример:

```javascript
const fetchUsers = () => {

 return async function(dispatch) {

   dispatch({
     type: "USERS_LOADING"
   });


   const response = await fetch("/users");

   const users = await response.json();


   dispatch({
     type: "USERS_SUCCESS",
     payload: users
   });

 };

};
```

---

Использование:

```javascript
dispatch(fetchUsers());
```

---

## Плюсы Redux Thunk

* Простая реализация.
* Подходит для большинства приложений.
* Минимум дополнительного кода.

---

## Минусы

* Логика может смешиваться с action creators.
* Сложно управлять сложными потоками.

---

# Redux Saga

Redux Saga — middleware для управления сложными асинхронными процессами.

Использует генераторы JavaScript.

---

Пример:

```javascript
function* fetchUsersSaga() {

 try {

   const users = yield call(api.getUsers);


   yield put({
     type: "USERS_SUCCESS",
     payload: users
   });


 }
 catch(error) {

   yield put({
     type: "USERS_ERROR",
     error
   });

 }

}
```

---

## Основные эффекты Saga

### call

Вызов функции:

```javascript
yield call(api.getUsers);
```

---

### put

Отправка action:

```javascript
yield put({
 type:"SUCCESS"
});
```

---

### takeEvery

Запуск при каждом action:

```javascript
yield takeEvery(
 "GET_USERS",
 fetchUsersSaga
);
```

---

### takeLatest

Отменяет предыдущий запрос:

```javascript
yield takeLatest(
 "SEARCH",
 searchSaga
);
```

Используется для поиска.

---

## Thunk vs Saga

|                 | Thunk   | Saga       |
| --------------- | ------- | ---------- |
| Подход          | Функции | Генераторы |
| Сложность       | Низкая  | Высокая    |
| Асинхронность   | Простая | Сложная    |
| Отмена запросов | Нет     | Да         |
| Тестирование    | Среднее | Хорошее    |
| Большие проекты | Реже    | Часто      |

---

# Redux

Redux — это библиотека управления состоянием приложения.

Основная идея:

> Все состояние приложения хранится в одном месте (Store), а изменения происходят через отправку действий (Actions), которые обрабатываются Reducers.

---

## Архитектура Redux

```
        Action
          |
          v
       Reducer
          |
          v
        Store
          |
          v
     Components
```

---

# Store

Store хранит состояние приложения.

Пример:

```javascript
const store = {
 users: [],
 isLoading: false
}
```

---

# Action

Action — это объект, описывающий событие.

Пример:

```javascript
{
 type: "ADD_USER",
 payload: {
   id:1,
   name:"John"
 }
}
```

---

Требование:

Action обязательно должен иметь поле:

```javascript
type
```

---

# Reducer

Reducer — чистая функция, которая принимает:

* Текущее состояние.
* Action.

И возвращает новое состояние.

---

Пример:

```javascript
function usersReducer(
 state = [],
 action
) {

 switch(action.type) {

  case "ADD_USER":

    return [
      ...state,
      action.payload
    ];


  default:
    return state;

 }

}
```

---

# Dispatch

Dispatch отправляет action:

```javascript
dispatch({
 type:"ADD_USER",
 payload:user
});
```

---

# Selector

Получение данных из Redux Store:

```javascript
const users = useSelector(
 state => state.users
);
```

---

# Provider

Подключение Redux к React:

```jsx
<Provider store={store}>
  <App/>
</Provider>
```

---

# Saga + Actions + Reducer

Типичный поток Redux Saga:

```
Component
    |
dispatch(GET_USERS)
    |
Action
    |
Saga Middleware
    |
API Request
    |
dispatch(GET_USERS_SUCCESS)
    |
Reducer
    |
Store Update
    |
Component Rerender
```

---

## Actions

Создание action:

```javascript
export const getUsers = () => ({
 type: "GET_USERS"
});


export const getUsersSuccess = users => ({
 type: "GET_USERS_SUCCESS",
 payload: users
});
```

---

## Saga

```javascript
function* getUsersSaga() {

 const response =
   yield call(api.getUsers);


 yield put(
   getUsersSuccess(response)
 );

}


export function* rootSaga(){

 yield takeEvery(
   "GET_USERS",
   getUsersSaga
 );

}
```

---

## Reducer

```javascript
const initialState = {
 users: [],
 loading: false
};


function usersReducer(
 state = initialState,
 action
){

 switch(action.type){

 case "GET_USERS":

   return {
    ...state,
    loading:true
   };


 case "GET_USERS_SUCCESS":

   return {
    ...state,
    loading:false,
    users: action.payload
   };


 default:
   return state;

 }

}
```

---

# MobX

MobX — это библиотека управления состоянием приложения в JavaScript/TypeScript, которая использует реактивный подход.

Основная идея MobX:

> Состояние хранится в обычных JavaScript-объектах, а библиотека автоматически отслеживает зависимости и обновляет только те компоненты, которые используют изменившиеся данные.

В отличие от Redux, где изменения проходят через **Actions → Reducers → Store**, в MobX состояние изменяется напрямую через методы или действия.

---

# Основные концепции MobX

MobX строится вокруг четырех основных понятий:

1. **Observable**
2. **Actions**
3. **Computed values**
4. **Reactions**

---

# Observable (наблюдаемое состояние)

`Observable` — это данные, за которыми MobX следит.

Когда Observable изменяется, MobX автоматически обновляет связанные компоненты.

Пример:

```typescript
import { makeAutoObservable } from "mobx";


class UserStore {

    users = [];

    constructor() {
        makeAutoObservable(this);
    }

}
```

Теперь поле `users` является отслеживаемым.

---

# Actions (действия)

Action — это функция, которая изменяет состояние.

Пример:

```typescript
class UserStore {

    users = [];

    constructor() {
        makeAutoObservable(this);
    }


    addUser(user) {
        this.users.push(user);
    }

}
```

Метод `addUser()` изменяет Observable состояние.

---

# Computed Values

Computed — это вычисляемые значения, которые зависят от Observable данных.

MobX автоматически пересчитывает их только при изменении зависимостей.

Пример:

```typescript
class CartStore {

    items = [];

    constructor() {
        makeAutoObservable(this);
    }


    get totalPrice() {

        return this.items.reduce(
            (sum, item) => sum + item.price,
            0
        );

    }

}
```

`totalPrice` автоматически обновится при изменении `items`.

---

# Reactions

Reaction — это автоматическое выполнение кода при изменении состояния.

Основные виды:

* `autorun`
* `reaction`
* `when`

---

Пример:

```typescript
autorun(() => {
    console.log(store.users);
});
```

Каждый раз при изменении `users` функция будет выполняться.

---

# Использование MobX с React

Для React используется:

MobX React Lite

Основной компонент:

```javascript
observer()
```

Он подписывает компонент на изменения Observable данных.

---

Пример Store:

```typescript
class CounterStore {

    count = 0;


    constructor() {
        makeAutoObservable(this);
    }


    increment() {
        this.count++;
    }

}


export const counterStore =
    new CounterStore();
```

---

Компонент:

```jsx
import { observer } from "mobx-react-lite";


const Counter = observer(() => {

    return (
        <>
            <h1>
                {counterStore.count}
            </h1>

            <button
                onClick={() =>
                    counterStore.increment()
                }
            >
                +
            </button>
        </>
    );

});
```

---

# MobX vs Redux

|                    | MobX                      | Redux                |
| ------------------ | ------------------------- | -------------------- |
| Подход             | Реактивный                | Flux-подобный        |
| Изменение данных   | Напрямую через actions    | Только через reducer |
| Boilerplate        | Меньше                    | Больше               |
| Состояние          | Несколько store           | Обычно один store    |
| Контроль изменений | Автоматический            | Явный                |
| Асинхронность      | Через обычный async/await | Middleware           |
| Обучение           | Проще                     | Сложнее              |

---

# Преимущества MobX

### 1. Меньше шаблонного кода

Redux:

```javascript
dispatch({
 type: "ADD_USER",
 payload:user
});
```

MobX:

```javascript
store.addUser(user);
```

---

### 2. Автоматическая оптимизация

MobX сам определяет:

* какие компоненты используют данные;
* какие компоненты нужно обновить.

---

### 3. Простая работа с состоянием

Нет необходимости создавать:

* Action creators.
* Reducers.
* Switch-case.

---

# Недостатки MobX

* Магия реактивности может усложнить отладку.
* Меньше строгих правил архитектуры.
* Большая свобода может привести к разным стилям кода.

---

# MobX-State-Tree (MST)

MobX-State-Tree — это надстройка над MobX, которая добавляет строгую структуру управления состоянием.

Основная идея:

> MobX дает реактивность, а MST добавляет архитектуру, типизацию и контроль изменений.

---

Основные элементы MST:

* Models.
* Types.
* Actions.
* Views.
* Snapshots.

---

Пример модели:

```typescript
import { types } from "mobx-state-tree";


const User = types.model({

    id: types.number,

    name: types.string

})
.actions(self => ({

    changeName(name) {
        self.name = name;
    }

}));
```

---

# TypeScript (TS)

TypeScript — это строго типизированный язык программирования, являющийся надстройкой над JavaScript.

TypeScript компилируется в обычный JavaScript.

Схема работы:

```
TypeScript
     |
     v
 TypeScript Compiler (tsc)
     |
     v
 JavaScript
     |
     v
 Browser / Node.js
```

---

# Зачем нужен TypeScript?

JavaScript является динамически типизированным:

```javascript
let age = 25;

age = "hello";
```

Ошибка обнаружится только во время выполнения.

---

TypeScript:

```typescript
let age: number = 25;

age = "hello";
```

Ошибка появляется сразу при компиляции:

```
Type 'string' is not assignable to type 'number'
```

---

# Основные возможности TypeScript

## Типы данных

Примитивы:

```typescript
let name: string;

let age: number;

let active: boolean;
```

---

Массивы:

```typescript
let numbers: number[] = [
    1,
    2,
    3
];
```

или:

```typescript
let numbers: Array<number>;
```

---

Tuple:

```typescript
let user: [string, number];

user = [
    "John",
    25
];
```

---

Enum:

```typescript
enum Role {

    Admin,

    User

}
```

---

# Interfaces

Interface описывает структуру объекта.

```typescript
interface User {

    id: number;

    name: string;

    email: string;

}
```

Использование:

```typescript
const user: User = {

    id: 1,

    name: "John",

    email: "test@test.com"

};
```

---

# Type

`type` также используется для создания типов.

```typescript
type User = {

    id:number;

    name:string;

};
```

---

## Interface vs Type

| Interface                | Type                           |
| ------------------------ | ------------------------------ |
| Для объектов             | Любые типы                     |
| Можно расширять          | Более гибкий                   |
| Часто используется в OOP | Используется для сложных типов |

---

# Union Types

Позволяют указать несколько возможных типов.

```typescript
let id: number | string;

id = 10;

id = "abc";
```

---

# Intersection Types

Объединение типов.

```typescript
type User = {
    name:string;
};


type Admin = {
    permissions:string[];
};


type AdminUser =
    User & Admin;
```

---

# Generics

Позволяют создавать переиспользуемый типизированный код.

Пример:

```typescript
function identity<T>(
    value:T
):T {

    return value;

}


identity<number>(10);

identity<string>("hello");
```

---

# Classes в TypeScript

Поддерживаются модификаторы доступа:

* public
* private
* protected
* readonly

Пример:

```typescript
class User {

    private id:number;


    constructor(id:number){

        this.id = id;

    }

}
```

---

# Utility Types

TypeScript имеет встроенные инструменты изменения типов.

---

## Partial

Все свойства становятся необязательными:

```typescript
Partial<User>
```

---

## Required

Все свойства обязательные:

```typescript
Required<User>
```

---

## Pick

Выбор отдельных свойств:

```typescript
Pick<User, "name">
```

---

## Omit

Удаление свойств:

```typescript
Omit<User, "id">
```

---

## Record

Создание объекта с ключами определенного типа:

```typescript
Record<string, User>
```

---

# TypeScript в React

Использование типов для Props:

```typescript
interface Props {

    name:string;

}


function User(
    {name}:Props
){

    return (
        <h1>
            {name}
        </h1>
    );

}
```

---

Типизация State:

```typescript
const [count,setCount] =
    useState<number>(0);
```

---

Типизация событий:

```typescript
const handleClick =
(
 event: React.MouseEvent<HTMLButtonElement>
) => {

};
```

---

# TypeScript в Redux

Типизация State:

```typescript
interface RootState {

    users: User[];

}
```

Типизация Action:

```typescript
interface AddUserAction {

    type:"ADD_USER";

    payload:User;

}
```

---

# Преимущества TypeScript

1. Ошибки обнаруживаются до запуска приложения.
2. Улучшенный автокомплит.
3. Безопасный рефакторинг.
4. Документирование кода через типы.
5. Удобная разработка больших проектов.

---

# Краткие ответы для собеседования

**MobX:**

> MobX — библиотека управления состоянием, использующая реактивный подход. Данные помечаются как observable, изменения выполняются через actions, вычисляемые данные создаются через computed, а компоненты React обновляются автоматически через observer.

**Redux vs MobX:**

> Redux использует строгий однонаправленный поток данных через Action и Reducer, а MobX использует реактивную модель с автоматическим отслеживанием зависимостей.

**TypeScript:**

> TypeScript — это надстройка над JavaScript с системой статической типизации. Он позволяет находить ошибки на этапе компиляции, улучшает автодополнение и делает код более надежным и поддерживаемым.

**State и Props:**

> Props — это данные, передаваемые компоненту извне и доступные только для чтения. State — это внутреннее состояние компонента, которое может изменяться и вызывает повторный рендер.

**Conditional Rendering:**

> Это способ отображения разных элементов интерфейса в зависимости от условий через JavaScript-операторы `if`, `&&`, `?:`.

**Context:**

> Context позволяет передавать глобальные данные через дерево компонентов без Prop Drilling. Используется для тем, авторизации, локализации и настроек.

**Keys:**

> Keys помогают React идентифицировать элементы списка при обновлении Virtual DOM и эффективно выполнять reconciliation.

**Fragments:**

> Fragment позволяет группировать несколько React-элементов без создания дополнительного DOM-узла. Используется через `<React.Fragment>` или сокращенный синтаксис `<>...</>`.

**React DevTools:**

> Инструмент для анализа React-приложений. Позволяет смотреть дерево компонентов, props, state, hooks, отслеживать ререндеры и анализировать производительность через Profiler.

**Custom Hook:**

> Это функция, начинающаяся с `use`, которая позволяет вынести и переиспользовать логику React-компонентов.

**Middleware:**

> Middleware в Redux используется для обработки промежуточной логики, например асинхронных запросов. Redux Thunk использует функции, а Redux Saga — генераторы и эффекты.

**Redux:**

> Redux — это библиотека управления состоянием с единственным Store, где изменения происходят через Action и Reducer.

**Saga + Actions + Reducer:**

> Component отправляет Action через dispatch, Saga перехватывает его и выполняет асинхронную операцию, после чего отправляет новый Action, который Reducer использует для обновления Store.

## Основные хуки

| Hook            | Назначение                   |
| --------------- | ---------------------------- |
| useState        | Управление состоянием        |
| useEffect       | Побочные эффекты             |
| useContext      | Глобальные данные            |
| useReducer      | Сложное состояние            |
| useRef          | Ссылки и сохранение значений |
| useMemo         | Оптимизация вычислений       |
| useCallback     | Оптимизация функций          |
| useLayoutEffect | Синхронные DOM-эффекты       |
| Custom Hooks    | Переиспользование логики     |

