프로젝트는 [Router.md](./Router.md)에 이어서 합니다.

## 동적 라우팅이란?

Route 경로에 특정 값을 넣어 해당 페이지로 이동할 수 있게 하는 것을 말합니다.

### 특정 값 동적라우팅 사용해보기

1. App.js 파일에 동적라우트를 작성합니다.
```js
import { BrowserRouter, Route } from 'react-router-dom';
import About from './page/About';
import Home from './page/Home';
import Info from './page/Info';

function App() {
  return (
    <BrowserRouter>
      <Route path='/' exact component={Home} />
      <Route path='/info' exact component={Info} />
      <Route path='/info/:name' component={Info} />
      <Route path='/about' component={About} />
    </BrowserRouter>
  );
}

export default App;
```

2. info.jsx 파일에 props를 console에 찍어서 확인해봅니다.
```js
export default function Info(props) {
  console.log(props);
  return (
    <>
      <h2>Info 페이지입니다.</h2>
    </>
  );
}
```
![image](https://user-images.githubusercontent.com/74242937/125190717-78c48f80-e279-11eb-9a2e-6be0e56201a5.png)

- console에 나온 것을 확인해보면 객체가 생성이 되고 넣어준 특정 값은 match -> params -> name으로 값이 들어있는 것을 확인할 수 있습니다.

3. 주소로 넘겨 준 특정 값을 변수에 담아 화면에 출력해봅니다.
```js
export default function Info(props) {
  const name = props.match.params.name;
  return (
    <>
      <h2>Info 페이지입니다.</h2>
      {name && <p>name은 {name}입니다.</p>}
    </>
  );
}
```
![image](https://user-images.githubusercontent.com/74242937/125191325-c1ca1300-e27c-11eb-8f0b-58a695cb1b4f.png)

- 주소에 특정 값을 넘겨준다면 위와 같이 화면이 출력되고 넘겨주지 않는다면 h2 태그의 내용만 출력하게 됩니다.

### URLSearchParams을 사용한 동적라우팅 사용해보기

1. 주소로 쿼리 스트링을 넘겨서 about.jsx 파일에 props를 console에 찍어 확인해 봅니다.
```js
export default function About(props) {
  console.log(props);
  return <h2>About 페이지입니다.</h2>;
}
```
![image](https://user-images.githubusercontent.com/74242937/125192049-aa8d2480-e280-11eb-8d15-6d5c2e63a678.png)

- 주소로 넘긴 title=react는 location -> search 안에 있는 것을 확인할 수 있습니다.

2. 쿼리 스트링 값을 변수에 담아 출력합니다.
```js
export default function About(props) {
  const searchParmas = props.location.search;
  console.log(searchParmas);
  return <h2>About 페이지입니다.</h2>;
}
```
![image](https://user-images.githubusercontent.com/74242937/125192176-6f3f2580-e281-11eb-98ca-11764e554131.png)

- 문제는 ?와 파라미터 값까지 뽑아오기 때문에 value 값만 뽑아올 작업을 해야 합니다.

3. URLSearchParams 인터페이스를 사용합니다.
- URLSearchParams: URL의 쿼리 문자열에 대해 작업할 수 있는 유틸리티 메서드를 정의합니다.
```js
export default function About(props) {
  const searchParmas = props.location.search;
  console.log(searchParmas);
  const obj = new URLSearchParams(searchParmas);
  console.log(obj.get('title'));
  return <h2>About 페이지입니다.</h2>;
}
```
![image](https://user-images.githubusercontent.com/74242937/125192332-40757f00-e282-11eb-9646-adf4d61c7c90.png)

- URLSearchParams의 get메서드를 활용해서 title의 value값을 꺼내옵니다.

![image](https://user-images.githubusercontent.com/74242937/125192492-238d7b80-e283-11eb-92bc-0075eb165b40.png)

- 단점은 Explorer를 지원하지 않습니다.

### query-string 패키지를 사용한 동적라우팅

1. 터미널에서 query-string 패키지를 설치합니다.(npm i query-string)  
![image](https://user-images.githubusercontent.com/74242937/125193225-4cfbd680-e286-11eb-8570-7898333e642b.png)

2. query-string을 import합니다. queryString의 parse메서드를 활용하여 값을 추출합니다.
```js
import queryString from 'query-string';

export default function About(props) {
  const searchParmas = props.location.search;
  console.log(searchParmas);
  const query = queryString.parse(searchParmas);
  console.log(query);
  return (
    <>
      <h2>About 페이지입니다.</h2>
    </>
  );
}
```
![image](https://user-images.githubusercontent.com/74242937/125193298-b4b22180-e286-11eb-9655-166eec7d6759.png)

- 값을 확인하면 객체 타입으로 추출하는 것을 알 수 있습니다.

3. 추출한 값을 이용하여 화면에 출력해 봅니다.
```js
import queryString from 'query-string';

export default function About(props) {
  ---
  return (
    <>
      <h2>About 페이지입니다.</h2>
      {query.title && <p>title은 {query.title}입니다.</p>}
    </>
  );
}
```
- ---는 같은 코드이므로 생략합니다.

![image](https://user-images.githubusercontent.com/74242937/125193377-11154100-e287-11eb-9f84-ff4985404ded.png)

<hr>

p.s 추후에 Hooks를 이용한 Dynamic Router를 작성하면 링크를 달도록 하겠습니다!!
지금까지 간단한 Dynamic Router 사용법을 알아보았습니다. 틀린내용이 있다면 PR보내주시면 감사하겠습니다.

<hr>

### 사용버전

- "query-string": "^7.0.1"
