# React Route

## route

- `npm install react-router-dom`



### intro

1. index.js 설정

```react
import React from 'react';
import ReactDOM from 'react-dom';
import {BrowserRouter} from 'react-router-dom'

import './index.css';
import App from './App';

ReactDOM.render(
  <BrowserRouter>
    <App />
  </BrowserRouter>,
 document.getElementById('root'));
```



2.  page 작성

```react
// AllMeetups.js
function AllMeetupsPage(){
  return <div>All Meetups Page</div>
}
export default AllMeetupsPage
```



3. url 설정

```react
// App.js
import { Route, Routes } from 'react-router-dom'
import AllMeetupsPage from './pages/AllMeetups';
import NewMeetupPage from './pages/NewMeetup';
import FavoritesPage from './pages/Favorites';
import Nav from './pages/Nav'

function App() {
  return (
    <div>
      <Nav />
      <Routes>
        <Route path='/' element={<AllMeetupsPage />}/>
        <Route path='/new-meetup' element={<NewMeetupPage />}/>
        <Route path='/favorites' element={<FavoritesPage />}/>
      </Routes>
    </div>
  )
}
export default App;
```



### Link

```react
import { Link,NavLink } from 'react-router-dom'
import classes from './MainHeader.module.css';
const Nav = ()=>{
  return (
    <section>
      <ul>
        <li>
          <Link to='/'>Home</Link>
        </li>
        <li>
          <NavLink to='/new-meetup' className={(navData) => navData.isActive ? classes.active : ''}>new meetup</NavLink>
        </li>
        <li>
          <Link to='/favorites'>favorites</Link>
        </li>
      </ul>
    </section>
  )
}
export default Nav;
```

- NavLink
  - 현재 경로와 Link에서 사용하는 경로가 같을 경우 CSS 클래스(특정 스타일)를 적용할 수 있는 컴포넌트



### router params

- 주소에 `:pageid` 형식으로 params가 있어 사용 할 때

```react
import { useParams } from 'react-router-dom'

const ArticleDetail = ()=>{
    const params = useParams();
    return (
    	<section>
        	<p>{params.pageid}</p>
        </section>
    )
}
```



### Navigate

- redirect 개념

```react
import { Route,Routes,Navigate } from 'react-router-dom';

function App() {
    return (
    <div>
    	<Routes>
            <Route path = '/' element={<Navigate to="/new-meetup" />} />
        <Routes/>
    </div>
    )
}
```

- useNavigate

```react
import { useNavigate } from 'react-router-dom';

export default function Test() {
  const navigate = useNavigate();
	
  const back = () => navigate(-1); // 뒤로가기, -1,-2 1 등 입력 가능
  const move = () => {
    navigate('/test', {
      state: {name:ljm},
      replace:true // 뒤로가기 하여도 직전의 페이지로 못오게 막음
    });
  };
  return (
    <div>
      <button onClick={move}>이동</button>
    </div>
  );
}
```





 ### 중첩 Route

### Type 1 

1. App.js에서 NewMeetupPage를 Route

```react
// App.js
import { Route, Routes } from 'react-router-dom'
import NewMeetupPage from './pages/NewMeetup';

function App() {
  return (
    <div>
        <Route path='/new-meetup/*' element={<NewMeetupPage />}/>
      </Routes>
    </div>
  )
}
export default App;
```

2. NewMeetupPage에서 Route

```react
// NewMeetup.js
import { Link,Route, Routes } from 'react-router-dom'
function NewMeetupPage ()=>{
    return(
        <div>New Meetup Page</div>
        <Link to="check">체크 확인하기</Link>
        <Routes>
            <Route path="check" element={<p>check route</p>}
        </Routes>
    )
}
```

- 경로가 `/new-meetup` 에선 check route가 안보임
- 경로가 `/new-meetup/check`에선 check route가 보임

- 중첩 route 구조에서는 Link도 to 주소에 앞부분이 자동으로 채워져 있음



#### Type 2

```react
// App.js
import { Route, Routes } from 'react-router-dom'
import NewMeetupPage from './pages/NewMeetup';

function App() {
  return (
    <div>
        <Route path='/new-meetup/*' element={<NewMeetupPage />}>
       		<Route path="check" element={<p>check route</p>}
        </Route>
      </Routes>
    </div>
  )
}
export default App;
```

- App.js에서 중첩된 Route를 정의 하는 형태

- NewMeetup.js 와 같은곳에 분산형태로 Route를 할 필요 없이 모아서 할 수 있는 장점

```react
// NewMeetup.js
import { Link,Outlet } from 'react-router-dom'
function NewMeetupPage ()=>{
    return(
        <div>New Meetup Page</div>
        <Link to="check">체크 확인하기</Link>
        <Outlet />
    )
}
```

- `Outlet` 위치에 중첩 라우팅이 표현됨