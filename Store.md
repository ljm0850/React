# Store

- Vue의 Vuex 역할(store)

- **Redux**

- **Context**
  - React 내장

## Context

#### store

```react
// store
import { createContext,useState } from 'react'

const TestContext = createContext({
    testArray : [],
    cntArray : 0,
    // itemIsTestValue: (item)=>{} 추후 다른곳에서 ide 자동완성 편하게 하려면 추가
});

// 값 업데이트 용
export function TestContextProvider(props){
    const [testValue,setTestValue] = useState([])
    
    function addTestArray(testItem){
        //setTestValue(testValue.concat(testItem))
        setTestValue((prevTestValue)=>{
            return prevTestValue.concat(testItem)
        })
    }
    function removeTestArray(testId){
        setTestValue((prevTestValue)=>{
            return prevTestValue.filter(item => item.id !== testId)//false값이 나오면 삭제
        })
    }
    function itemIsTestValue(itemId){
        return testValue.some(item => item.id === itemId)
    }
    
    const context = {
        testArray: testValue,
        cntArray: testValue.length,
        addTestArray: addTestArray,
        removeTestArray: removeTestArray,
        itemIsTestValue: itemIsTestValue
        
    };
    
    return <TestContext value={context}>
        {props.children}
    </TestContext>
}
export default TestContext
```

- `createContext()`가 Component를 반환
  - 그래서 TestContext를 대문자로 시작(컴포넌트 시작은 대문자로 하는게 암묵적 합의)

- `function addTestArray(testItem)`
  - `export` : 다른 객체에서 사용하기 위해
  - `setTestValue(testValue.concat(testItem)`
    - `concat`은 push와 비슷하지만, 새로운 array를 반환하는 차이가 있음
    - 위와 같은 식으로 코드를 짜면 testValue 값이 즉각 업데이트가 안됨



#### component에서 사용

```react
// index.js
import React from 'react';
import ReactDOM from 'react-dom';
import { BrowserRouter } from 'react-router-dom'

import './index.css';
import App from './App';
import { TestContextProvider } from './해당 위치'

ReactDOM.render(
    <TestContextProvider>
    	<BrowserRouter>
        	<App />
    	</BrowserRouter>
    </TestContextProvider>
    document.getElementById('root'));
```

```react
// 컴포넌트
import { useContext } from 'react'
import TestContext from 'store 주소'
function Item(props) {
    const testStore = useContext(TestContext);
    const itemIsTestValue = testStore.itemIsTestValue(props.id);
    
    function toggleTestItem(){
        if (itemIsTestValue){
            testStore.removeTestArray(props.id)
        } else {
            testStore.addTestArray({
                id: props.id,
                title: props.title,
                ...:
            })
        }
    }
    return (
    	<div>
        <button onClick={toggleTestItem}>{itemIsTestValue ? 'Remove' : 'add'}</button>
        </div>
    )
}
```

- `useContext` : 컴포넌트와 context를 연결하는 역할