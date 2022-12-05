# ref:DOM에 이름달기

일반 html에서 DOM 요소에 이름을 달 때는 id를 사용한다.

리액트 예시

public > `index.html`
``` javascript
    <body>
        <noscript>You need to enable JavaScript to run this app.
        </noscript>
        <div id="root"></div>
    </body>
```

src > `ìndex.js`
```javascript
const root = ReactDOM.createRoot(document.getElementById('root'));
```
> id = root 인 요소에 리액트 컴포넌트를 렌더링해라

하지만 리액트 컴포넌트 안에서는 id 사용을 권장하지 않는다.
왜나하면 dom의 id는 **유일해야하는데** 컴포넌트를 여러번 사용하는 상황이 발생하면 중복을 일어나기 때문이다.

이 때, 리액트에서는 ref(=reference)를 사용한다.

<br/>

## ref의 사용예시
순수 자바스크리브 및 jQuery로 만든 웹 사이트에서 input을 검증할 때는 id를 가진 input에 클래스를 설정해 준다. 하지만 리액트에서는 dom에 직접 접근하지 않아도 **state로** 구현이 가능하다.

``` javascript
class ValidationSample extends Component {
    state = {
        password : "",
        clicked : false,
        validated : false
    }

    handleChange = (e) => {
        this.setState({
            password: e.target.value
        });
    }

    handelButtonClick = () => {
        this.setState({
            clicked : true,
            validated: this.state.password === '0000'
        })
    }

    render() {
        return (
            <div>
                <input type="password"
                value = {this.state.password}
                onChange={this.handleChange}
                className={this.state.clicked ? (this.state.validated ? 'success' : 'failure') : ''}/>
                <button onClick={this.handelButtonClick}>검증하기</button>
            </div>
        )
    }
}

export default ValidationSample
```

DOM을 꼭 사용해야 하는 상황 -> dom에 직접적으로 접근해야하는 상황
- 특정 input에 포커스 주기
- 스크롤 박스 조작하기
- canvas 요소에 그림 그리기 등


<br/>

### 📍 ref 사용 방법
- **콜백 함수를** 통한 ref 설정 
    - ref를 달고자 하는 요소에 **ref라는 콜백 함수를 props로 전달해 주면 된다.**
    - **함수형 컴포넌트에서는 사용할 수 없다**
        - ```Uncaught TypeError: Cannot set properties of undefined (setting 'scrollBox')```
    - ```<input ref = {(ref) => {this.input = ref}}/>```
- createRef를 통한 ref 설정
    ``` 
    input = React.CreatRef();
    handleFocus = () => {
        this.input.current.focus();
        }

    <input ref = {this.input}/>    
    ```
> 콜백함수와 차이점은 dom에 접근하기 위해 .current를 넣어주어야 한다.

<br/>

### 📍 컴포넌트에 ref 달기
컴포넌트에 ref를 사용하면 해당 컴포넌트의 내부 메서드 및 멤머 변수에도 접근 가능하다.

아래 코드는 부모 컴포넌트에서 자식 컴포넌트의 메서드를 불러오는 예제이다.

`app.js`
``` javascript
class App extends Component {
  render(){
    return (
    <div>
      <ScrollBox ref = {(ref) => this.hi = ref}/>
      <button onClick={()=> this.hi.scrollToBottom()}>
        맨 밑으로
      </button>
    </div>
  );
}
}

export default App;
```
`ScrollBox.js`
``` javascript
import { Component } from "react";

class ScrollBox extends Component {
    scrollToBottom = () => {
        const {scrollHeight, clientHeight} = this.box
        this.box.scrollTop = scrollHeight - clientHeight
    }
    render() {
        const style = {
            border : '1px solid black',
            height : '300px',
            width : '300px',
            overflow :'auto',
            position : 'relative'
        };

        const innerStyle = {
            width :'100%',
            height: '650px',
            background : 'linear-gradient(white, black)'
        }
        return(
            <div
                style={style}
                ref = {(ref) => {this.box = ref}}>
                <div style={innerStyle}/>
            </div>
        )
    }
}

export default ScrollBox
```

### ✋🏻 참고하기
위 코드에서 **문법상으로** onClick = {this.scrollBox.scrollToBottom} 의 형식이 틀린것은 아니지만 처음 렌더링 될 때 this.scrollBox 값이 **undefined으로** 값을 불러오는와 오류가 발생한다. <br/>
하지만 화살표 함수 문법으르 사용하여 아예 새로운 함수를 만들고 그 내부에서 실행하게 되면 버튼을 누를 때 이미 this.scorollBox를 설정한 시점이기 때문에 오류가 발생하지 않는다.
