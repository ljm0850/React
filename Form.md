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

  - input된 값을 읽어오는데 주로 사용

  - input에 `ref`로 binding
  - 현재 값을 가져오려면 `.current.value`
  - 필요한 데이터 수 만큼 `const titleInputRef = useRef();`와 같이 정의하여 사용