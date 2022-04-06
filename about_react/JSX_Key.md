# JSX Key 속성 이해하기

### map 메소드 사용해서 데이터 나열하기
```javascript
{this.todoData.map((data) => (
    <div style={this.getStyle()} key={data.id}>
    <input type="checkbox" defaultChecked={false}/>
    {data.title}
    <button style={this.btnStyle}> X </button>
    </div>
))}
```

### 만약 key속성을 넣지 않는다면?
```
Warning: Each child in on array or iterator should have a unique "key" prop ...
```
라는 에러가 발생한다.

### JSX Key 속성은 무엇인가?
리액트에서 요소의 리스트를 나열할 때는 Key를 넣어줘야 한다.<br>
키는 React가 변경, 추가 또는 제거된 항목을 식별하는 데 도움이 된다.<br>
요소에 안정적인 ID를 부여하려면 배열 내부의 요소에 키를 제공해야 한다. <br>

### 리액트는 가상 돔을 이용해서 바뀐 부분문 실제 돔에 적용!
가상 돔을 이용해서 <b>바뀐 부분만</b> 실제 돔에 적용해준다고 했다.<br>
리액트에서는 리스트를 나열할 때 바뀐 부분만 찾을 때 어떻게 해야 할까?<br>

### key를 이용해서 어떠한 부분이 바뀌었는지 인식할 수 있다.
### key에는 유니크한 값을 넣어준다.(index는 비추천)
