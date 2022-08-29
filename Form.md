# Form

```react
import { useRef } from 'react'
function NewForm() {
    const titleInputRef = useRef();
    
    function submitHandler(event){
        event.preventDefault();
        
        const enteredTitle = titleInputRef.current.value;
        const credential = {title:enteredTitle}
    }
    
    return <Card>
        <form onSubmit={submitHandler}>
        	<div>
            	<label htmlFor="title">Title</label>
                <input type="text" required id='title' ref={titleInputRef} />
            </div>
        </form>
        <button>생성</button>
        <Card />
}
```

- `for` 가 javascript에 있기에 htmlFor 사용
- `onSubmit` 를 통해 {}안의 함수가 실행
  - 자동으로 해당 함수에 html기본 event가 인자로 들어가게 됨
  - 이벤트를 막기 위해 `event.preventDefault();`사용(Javascript 기본 문법)

- `useRef`

  - `.current` 프로퍼티로 전달된 인자로 초기화된 변경 가능한 ref 객체 반환 

  - 내용이 변경될 때 알려주지는 않음(리 랜더링 발생x)
  
  - input에 `ref`값을 binding
  - 현재 값을 가져오려면 `.current.value`
  - 필요한 데이터 수 만큼 `const titleInputRef = useRef();`와 같이 정의하여 사용