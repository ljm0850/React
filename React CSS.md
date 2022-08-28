# React CSS

## module

- `cssname.module.css` 파일 생성

```css
.header{
    color: red;
}
```

- 해당 css를 사용하고 싶은 component에서 import
  - `import cuscss from './cssname.css';`
- css 적용할 곳에 prop 추가

```react
import cuscss from './cssname.css';

function CssTest(){
    return (
    	<header className={cuscss.header}></header>
    )
}
```

