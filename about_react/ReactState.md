# React State란?
### 리액트에서 데이터가 변할 때 화면을 다시 렌더링 해주기 위해서는 React State를 사용해야 한다.

### React State란 무엇인가
컴포넌트의 렌더링 결과물에 영향을 주는 데이터를 갖고 있는 객체 <br>
(State가 변경되면 컴포넌트는 리랜더링(Re-rendering)된다.<br>
또한 State는 컴포넌트 안에서 관리된다.<br>

## 리액트 State 생성하기

```javascript
let todoData = [
    {
        id: "1",
        title: "공부하기",
        completed: true,
    }
]
```
🔽🔽🔽
filter메소드를 사용해서 데이터를 지웠음에도 화면상에선 그 결과가 나타나지 않았었음<br>
화면상에서 렌더링이 안되었기 때문임<br>
React State를 사용해 화면상에서도 그 결과물이 나타날 수 있게 한다<br>
🔽🔽🔽
```javascript
state = {
    todoData: [
        {
        id: "1",
        title: "공부하기",
        completed: true,
        }
    ],
    value: "", //할 일을 입력했을 때 그 값을 보관해두는 값이 들어감
}
```