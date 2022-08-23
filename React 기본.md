# React 기본

## 설치 및 시작

1. Nodejs 설치
2. CRA (Create React App)

```
npx create-react-app my-app
cd my-app
npm start
```

# 구조

- index.js에서 index.html을 핸들링
  - root.render에서 App.js를 injection

- App.js
  - 실제 코드 작성 부분



# 코드

### class 추가

- return()안의 값은 html처럼 보이지만 html -> javascript로 변환하는 과정이 존재
- 따라서 div 태그 안에 class='class_name' 형태로 하면 javascript class 로 인식
- `<div className = 'class_name'></div>`형태로 해야함



### Component

- (src)폴더에 `componentName.js`파일 생성 

- 함수의 이름은 항상 대문자로 시작
  - react가 html tag (p,h1,...)와 component를 대소문자로 구별

```react
// app.js
import Todo from './components/Todo';

function App() {
  return (
    <div>
      <h1>My Todos</h1>
      <Todo />
    </div>
  );
}

export default App;
```

```react
// Todo.js
function Todo(params) {
  return(
    <div className="card">
        <h2>Title</h2>
        <div className="actions">
          <button className="btn">Delete</button>
        </div>
      </div>
  )
}
export default Todo;
```



### props

- 부모 컴포넌트의 값(변수)를 자식 컴포넌트에 전달 하는 것 

```react
// 부모 컴포넌트
import Todo from './components/Todo';
function App() {
  return (
    <div>
      <h1>My Todos</h1>
      <Todo text='React props test' />
    </div>
  );
}
export default App;
```

```react
// 자식 컴포넌트
function Todo(props) {
  return(
    <div className="card">
        <h2>Title</h2>
        <p>{props.text}</p>
        {/* {}안의 결과를 javascript로 계산하는데, if(){}불가 */}
        <div className="actions">
          <button className="btn">Delete</button>
        </div>
      </div>
  )
}
export default Todo;
```

- `{javascript code}`형태로 javascript 변수 등을 사용 가능



### event

```react
function Todo(props) {
  function deleteHandler(){
    alert(props.text)
  }
  return(
    <div className="card">
        <h2>Title</h2>
        <p>{props.text}</p>
        {/* {}안의 결과를 javascript로 계산하는데, if(){}불가 */}
        <div className="actions">
          <button className="btn" onClick={deleteHandler}>Delete</button>
        </div>
      </div>
  )
}
export default Todo;
```

- tag에 `onClick={}` 형식으로 처리
  - {}안에 `()=>{즉석 함수}`로 처리해도 되고 함수를 정의해서 가져와도 가능
  - 함수를 가졍로 경우 ()를 붙이면 react가 해당 return을 검증 하는 순간 함수가 작동이 되버림



### State

- 값이 변경됨에 따라 동적으로 html을 구성하기 위해 사용

```react
import { useState } from 'react';
import Modal from './Modal';
import Backdrop from './Backdrop';
function Todo(props) {
  // useState는 두가지 인자를 가지는 배열을 반환, 첫번째는 useState의 인자(false), 두번째는 인자를 변경하는 함수
  const [ modalIsOpen, setModalIsOpen ] = useState(false);

  function closeModalHandler(){
    setModalIsOpen(false)
  }

  return(
    <div className="card">
        {/* { modalIsOpen ? <Modal/> : null}  */}
        { modalIsOpen && <Modal onCancel={closeModalHandler} onConfirm={closeModalHandler}/>} 
        { modalIsOpen && <Backdrop onClick={closeModalHandler} />} 
      </div>
  )
}
export default Todo;
```

```react
// 자식 컴포넌트
function Modal(props) {
  function cancelHandler(){
    props.onCancel();
  }
  //...
  return (
  <div className="modal">
    <p>Are you sure?</p>
    <button className="btn btn--alt" onClick={cancelHandler}>Cancel</button>
    <button className="btn" onClick={confirmHandler}>Confirm</button>
  </div>
  )
}
export default Modal;
```

- `import { useState } from 'react';` 
  - react에서 useState를 가져옴
- `const [ modalIsOpen, setModalIsOpen ] = useState(false);`
  - `useState(value)`는 array 형태로 두가지 변수를 return
  - 첫번째 인자는 value에 해당하는 값(위 예시엔 modalIsOpen에 false가 할당)
  - 두번째 인자는 value값을 바꾸는 함수
- html tag on/off
  - Vue에선 `v-if`를 이용 
  - React에선 javascript code`{ modalIsOpen && <Backdrop onClick={closeModalHandler} />}`

- **custom component**의 경우 `onClick`를 인식 불가 => props를 이용하여 해결