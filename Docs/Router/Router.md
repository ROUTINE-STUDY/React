## Router란?

React는 SPA(Single Page Application)입니다. SPA이기 때문에 페이지 이동이 불가능하므로 이것을 해결해 주기 위한 기능이 React Router입니다.

- 라우팅: 주소에 따라 알맞는 뷰를 보여주는 것
- SPA(Single Page Application): 페이지가 1개인 어플리케이션

## 프로젝트 준비

- react 프로젝트를 설치합니다. (npx create-react-app 프로젝트명)  
![image](https://user-images.githubusercontent.com/74242937/125160599-d1802380-e1b8-11eb-8cfc-81fbeb6b130c.png)
- 프로젝트 폴더안에서 터미널을 사용하여 react-router-dom을 설치합니다. (npm i(install) react-router-dom)  
![image](https://user-images.githubusercontent.com/74242937/125160754-99c5ab80-e1b9-11eb-86c0-392f3ca9c948.png)
- src폴더 안에 page폴더와 Home.jsx, Info.jsx, About.jsx 파일을 만듭니다.  
![image](https://user-images.githubusercontent.com/74242937/125160815-faed7f00-e1b9-11eb-8653-458601fa005a.png)
- Home.jsx, Info.jsx, About.jsx 파일에 간단한 Component를 작성합니다.  
```js
// Home.jsx
export default Home() {
  return <div>Home 페이지입니다.</div>;
}

// Info.jsx
export default Info() {
  return <div>Info 페이지입니다.</div>;
}

// About.jsx
export default About() {
  return <div>About 페이지입니다.</div>;
}
```
- App.js 파일에 다음과 같이 작성합니다.
```js
import { BrowserRouter, Route } from 'react-router-dom';
import About from './page/About';
import Home from './page/Home';
import Info from './page/Info';

function App() {
  return (
    <BrowserRouter>
      <Route path='/' component={Home} />
      <Route path='/info' component={Info} />
      <Route path='/about' component={About} />
    </BrowserRouter>
  );
}

export default App;
```

### 결과 확인

1. 터미널에 npm start로 실행합니다.  
![image](https://user-images.githubusercontent.com/74242937/125161722-d9db5d00-e1be-11eb-9796-463c13a21ca9.png)
![image](https://user-images.githubusercontent.com/74242937/125161732-e52e8880-e1be-11eb-9d9e-3f7a63189aaa.png)
![image](https://user-images.githubusercontent.com/74242937/125161727-e1026b00-e1be-11eb-9dc3-3fd7560d9256.png)

- 주소에 localhost:3000/은 제대로 나오지만 --/info와 --/about은 Home과 겹쳐서 나오게 됩니다. 그 이유는 Home의 path='/'가 info와 about에도 겹치기 때문에 Home은 혼자서 표시하지만 나머지 Component들은 같이 표시하게 됩니다.

<hr>

2. 해결 방안
- <Route /> 컴포넌트 안에 exact를 작성합니다.
- exact: 주어진 경로와 똑같이 맞아 떨어져야만 화면에 컴포넌트를 보여줍니다.
```js
<Route path='/' exact component={Home} />
```
or
```js
<Route path='/' exact={true} component={Home} />
```
![image](https://user-images.githubusercontent.com/74242937/125161709-cdef9b00-e1be-11eb-9f39-c2d9bb449ecc.png)
![image](https://user-images.githubusercontent.com/74242937/125161707-c9c37d80-e1be-11eb-9498-a0b0a40f62d2.png)

<hr>

지금까지 간단한 Router 사용법을 알아보았습니다. 틀린내용이 있다면 PR보내주시면 감사하겠습니다.

<hr>

### 사용버전

![image](https://user-images.githubusercontent.com/74242937/125161619-53268000-e1be-11eb-824e-e5de4aaf06e5.png)
