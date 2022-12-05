# 이벤트 핸들링

이벤트란 사용자가 웹 브라우저에서 DOM 요소들과 상호 작용하는 것을 말한다.

<br/>
<h2>👉🏻 리액트의 이벤트 시스템</h2>

- 이벤트 이름은 카멜 표기법으로 작성합니다.
    - ex) onclick > onClick
- 이벤트에 실행할 자바스크립트 코드를 전달하는 것이 아니라, 함수 형태의 값을 전달합니다.
    - html에서 이벤트를 설정할 때는 큰따옴표 안에 실행할 코드를 넣었지만, 리액트에서는 함수 형태의 객체를 전달한다.
- dom 요소에만 이벤트를 설정할 수 있습니다.
    - 돔요소인 태그에는 이벤트를 설정할 수 있지만 **내가 직접만든 컴포넌트에는** 이벤트를 자체적으로 설정할 수 **없다.**
    - ex) `<MyComponet onClick={dosothing}/>` 이 있을 때 이는 그냥 이름이 onClick인 props를 MyComponet에 전달할 뿐이다.<br/>
    하지만 전달받은 props를 컴포넌트 내부의 dom 이벤트로 설정할 수 있다.
    <br/> 
    `<div onClick={this.props.onClick}/>`

<br/>
<h2>👉🏻 예제로 핸들링 익히기</h2>
<br/> 
<h3>📍 이벤트 알아보기</h3>

``` javascript 
import { Component } from "react";

class EventPractice extends Component {
    render() {
        return (
            <div>
                <h1>리액트 연습</h1>
                <input type="text" name="message" placeholder="입력해보세요" onChange={(e) => {console.log(e)}}/>
            </div>
        )
    }
}

export default EventPractice
```

위 코드를 실행했을 때 **이벤트 객체가** 콘솔에 나타나는데 객체는 syntheticeEvent로 웹 브라우저의 네이티브 이벤트를 감싸는 객체이다.
<image src="../images/syntheticeEvent.png">

syntheticeEvent는 네이티브 이벤트와 달리 이벤트가 끝나고 나면 초기화되어 0.5초뒤에 e객체를 참조하면 e객체 내부의 모든 값이 비워지게 된다. <br/>

이 경우 비동기적 이벤트가 일어났을 때 참조하기 위해서는 e.persist() 함수를 호출하여 **앞으로 변할 인풋 값인** e.target.value를 콘솔에 기록할 수 있다.

<br/>
<h3>📍 여러개의 input 상태 관리</h3>

``` javascript 
import { Component } from "react";

class EventPractice extends Component {

    state = {
        username: "",
        message: ""
    }

    hendleChange = (e) => {
        this.setState({
            [e.target.name] : e.target.value
        })
    }

    hendleClick = (e) => {
        this.setState({
            username:'',
            message:''
        })
    }

    render() {
        return (
            <div>
                <h1>리액트 연습</h1>
                <input type="text" name="username" placeholder="사용자명" value= {this.state.username} onChange={this.hendleChange}/>
                <input type="text" name="message" placeholder="내용" value= {this.state.message} onChange={this.hendleChange}/>

                <button onClick={this.hendleClick}>확인</button>
            </div>
        )
    }
}

export default EventPractice
```

<br/>

위 코드의 핵심은 객체 안에서 key를 []로 감싸면 그 안에 넣은 **레퍼런스가 가리키는 실제 값이 key값으로 사용된다.**

```javascript
    handleChange = e => {
        this.setState({
            [e.target.name] : e.target.value
        })
    }
```