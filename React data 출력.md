# React data 출력

### 기본

```react
function DataTest(){
    return (
   		{[<li>Item1<li/>, <li>Item2<li/>]}
    )}
             
export default DataTest;
```



### Array 활용

```react
import NameItem from './NameItem'

const nameArray = ['ljm','jsw','phm','rss']

function AllMeetupsPage(props){
  return (
    <section>
      <div>All Meetups Page</div>
      <ul>
        {nameArray.map((name)=>{return <li key={name}>{name}</li>})}
      </ul>
      <ul>
      	{props.names.map(name => <NameItem key={name.id} name={name} />)}    
      </ul>
    </section>
  )
}

export default AllMeetupsPage
```



### component wrapper

 ```react
 // Card.js
 import classes from './Card.module.css';
 
 function Card(props){
     return <div className={classes.card}>{props.children}</div>
 }
 ```

```react
import classes from './nameItem.module.css'
import Card from './Card'
function NameItem(props){
    return (
    <li ClassName={classes.item}>
    	<Card>
        	<div>{ props.name }</div>    
        </Card>    
    </li>
        
    )
}
```

- `<Card><card />`사이에 표현하고자 하는 내용을 나열
- Card.js의 `{ props.children } `에 해당 내용이 표현 됨