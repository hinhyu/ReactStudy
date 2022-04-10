# React Hooks란
React Hooks는 ReactConf 2018에서 발표된, class없이 state를 사용할 수 있는 새로운 기능

## React Hooks이 필요한 이유
항상 기술은 그 전에 것의 불편함이나 문제점을 해결하기 위해서 더욱 발전한다. <br>
그와 같이 React Hooks도 주로 CLass Component로 사용되어온 React에서 느껴왔던 불편함이나 문제점을 해결하기 위해서 개발되었다. <br>
원래 React는 주로 Class Component를 사용하고 React Hooks는 Functional Component를 사용하기 때문에 먼저 그 부분을 비교해보자.<br><br>
#### Class Component
더 많은 기능 제공, 더 긴 코드 양, 더 복잡한 코드, 더딘 성능
#### Functional Component
더 적은 기능 제공, 짧은 코드 양, 더 심플한 코드, 더 빠른 성능

## React 16.8 Hooks UPDATE!
리액트의 생명주기를 함수형 컴포넌트에서는 사용을 못했기 때문에 함수형 컴포넌트가 더 간결하게 빠르더라도 클래스형 컴포넌트를 써왔음<br>
✨React 16.8 Hooks 업데이트로 변경됨✨<br>
이로 인해서 함수형 컴포넌트에서도 생명주기를 사용할 수 있기에 데이터를 가져오고 컴포넌트 시작하자마자 API도 호출하고 많은 부분을 할 수 있게 됨.<br>

```javascript
import React, { Component } from 'react'
import Axios from 'axios'

export default class Hello extends Component {
    constructor(props){
        super(props);
        this.state = { name:"" };
    }

    componentDidMount() {
        Axios.get('/api/user/name')
        .then(response => {
            this.setState({ name: response.data.name })
        })
    }

    render() {
        return{
            <div>
            My name is {this.state.name}
            </div>
        }
    }
}
```
```javascript
import React, { useEffect, useState } from 'react'
import Axios from 'axios'

export default function Hello(){
    const [Name, setName] = useState("")

    useEffect(()=>{
        Axios.get('/api/user/name')
        .then(response => {
            setName(response.data.name)
        })
    }, [])
    return (
        <div>
        My name is {Name}
        </div>
    )
}
```

## Hooks의 또 다른 이점
```javascript
//일반 클래스 컴포넌트에서 생명주기 사용하는 부분
componentDidMount(){
    //컴포넌트가 마운트 되면 updateLists함수를 호출
    this.updateLists(this.props.id)
}
componentDidUpdate(prevProps){
    if(preProps.id !== this.props.id){
        //updateLists함수를 호출할 때
        //사용되는 id가 달라지면 다시 호출
        this.updateLists(this.props.id)
    }
}
//updateLists 함수 정의
updateLists = (id) => {
    fetchLists(id)
    .then((lists) => this.setState({
        lists
    }))
}
```
```javascript
//React Hooks를 이용한 생명주기 이용
useEffect(() => {
    fetchLists(id)
    .then((repos) => {
        setRepos(repos)
    })
}, [id])
```
위쪽 코드와 아래 쪽 코드를 보면 선명하게 코드가 간결해진걸 볼 수 있음 <br>
그 이유는 Class Component 에서는 생명주기를 이용할 때 componentDidMount와 ComponentDidUpdate 그리고 componentWillUnmount이렇게 다르게 처리를 해주지만 리액트 훅을 사용할 때는 useEffect안에서 다 처리 해줄 수 있기 때문<br>

### 마지막으로 Hooks로 인한 장점 하나 더

HOC컴포넌트를 Custom React Hooks로 대체해서 너무나 많은 Wrapper컴포넌트를 줄이게 되는 것<br>

## HOC(Higher Order Component)란?
component를 인자로 받아서 새로운 React Component를 리턴하는 함수<br>
화면에서 재사용 가능한 로직만을 분리해서 component로 만들고, 재사용 불가능한 UI와 같은 다른 부분들은 parameter로 받아서 처리하는 방법<br>

```javascript
export default class Apage extends Component {
    state = {
        user: []
    }
    componentDidMount(){
        fetchUsers()
        .then(users => {
            this.setState({ users })
        })
    }
    render() {
        const { users } = this.state;
        return (
            <div>
                A페이지
                {users.map(({ name, url }) => (
                    <div key={name}>
                        <p>{name}, {url}</p>
                    </div>
                ))}
            </div>
        )
    }
}
```
```javascript
export default class Bpage extends Component {
    state = {
        user: []
    }
    componentDidMount(){
        fetchUsers()
        .then(users => {
            this.setState({ users })
        })
    }
    render() {
        const { users } = this.state;
        return (
            <div>
                B페이지
                {users.map(({ name, url }) => (
                    <div key={name}>
                        <p>{name}, {url}</p>
                    </div>
                ))}
            </div>
        )
    }
}
```
위에 보면 A페이지와 B페이지가 있는데 두 페이지에서 같은 소스를 사용하고 있는 부분이 있다 <br>
그 부분은 유저 리스트를 가져오는 부분이다. <br>
어떠한 페이지에서든 유저 리스트를 가져와야 하는 애플리케이션을 만드려고 한다. <br>
하지만 모든 페이지에서 유저 리스트를 가져오기 위해서 똑같은 소스를 넣어준다면 너무 많은 중복이 되기 때문에 중복이 되는 부분은 따로 HOC 컴포넌트에 넣어주고 그 HOC 컴포넌트로 각각의 컴포넌트를 감싸주면 모든 컴포넌트에 따로 인증을 위한 부분을 넣어주지 않아도 된다. <br>

```javascript
function usersHOC(Component) {
    return class userHOC extends React.Component {
        state = {
            users: []
        }

        componentDidMount() {
            fetfchUsers()
            .then(users => {
                this.setState({ users })
            })
        }

        render() {
            return (
                <Component
                    {...this.props}
                    {...this.state}
                />
            )
        }
    }
}
```
```javascript
funtion Apage ({ users }){
    //...
}
export default usersHOC(Apage)

funtion Bpage ({ users }){
    //...
}
export default usersHOC(Bpage)
```
하지만 이 방법에도 문제가 있다. <br>
바로 너무나 많은 Wrapper컴포넌트가 생길 수 있다는 것이다. <br>
```javascript
//EXAMPLE
<LanguageHOC>
    <ThemeHOC>
        <AuthHOC>
            <Apage/>
        </AuthHOC>
    </ThemeHOC>
</LanguageHOC>
```
이러한 문제는 Custom React Hooks를 이용해서 해결할 수 있다.<br>

```javascript
function useAuth(){
    const [users, set Users] = useState([]):

    useEffect(() => {
        fetchUsers().then(users => {
            setUsers(users);
        });
    }), []);
    return [users];
}

function Apage() {
    const [users] = useAuth();

    return (
        <div>
            A페이지
            {users.map(({ name, url }) => (
                <div key={name}>
                    <p>{name},{url}</p>
                </div>
            ))}
        </div>
    );
}
```

useAuth라는 CustomHooks를 만든다 <br>

#### Hooks에서 state을 업데이트 해주려면 어떻게 해야 하나요?
state을 정의해줄 때   const [ name, setName ] = useState(""); 이런식으로 해줌. <br>
여기서 setName을 이용해서 state을 업데이트 시켜 줄 수 있다.
