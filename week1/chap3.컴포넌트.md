# 컴포넌트

<h2>✅ 컴포넌트 선언 방식</h2>

- 함수 컴포넌트
- 클래스형 컴포넌트

```javascript
import { Component } from "react";

class Counter extends Component {
  render() {
    const name = "리액트";
    return <div>{name}</div>;
  }
}

export default Counter;
```

차이점으로는 함수 컴포넌트는 선언이 편린하며 클래스형보다 메모리자원, 배포 후 결과물의 파일크기가 작다. (하지만 파일크기와 성능에서 큰 차이점이 있지는 않다.)

또한 큰 차이점으로 클래스 컴포넌트에는 state와 라이프사이클 API의 사용 불가능하다는 점인데 Hooks 기능이 도입되며 함수형에서도 사용이 가능하다.

<h2>✅ props</h2>
<br/>

```javascript
import React from "react";
import PropTypes from "prop-types";
import { Component } from "react";

class MyComponent extends Component {
  static defaultProps = {
    // props값이 없을 경우 기본값 설정
    name: "기본 이름",
  };

  static propTypes = {
    //propTypes를 통한 props 검증
    name: PropTypes.string,
    favoritNumber: PropTypes.number.isRequired,
  };
  render() {
    const { name, favoritNumber, children } = this.props; //비구조화 할당
    return (
      <div>
        안녕하세요, 제 이름은 {name}입니다. <br />
        children 값은 {children}입니다.
        <br />
        제가 좋아하는 숫자는 {favoritNumber}입니다.
      </div>
    );
  }
}

export default MyComponent;
```

<h2>✅ state</h2>
<br/>

```javascript
import React, { Component } from "react";

class Counter extends Component {
  constructor(props) {
    super(props);
    this.state = {
      number: 0,
    };
  }

  render() {
    const { number } = this.state;

    return (
      <div>
        <h1>{number}</h1>
        <button
          onClick={() => {
            this.setState(
              {
                number: number + 1,
              },
              () => {
                console.log("방금 호출됨");
                console.log(this.state);
              }
            );
          }}
        >
          +1
        </button>
      </div>
    );
  }
}

export default Counter;
```

- 클래스형 컴포넌트에서 state를 설정할 때는 constructor 메서드를 작성하고 반드시 super(props)를 호출해 주어야 한다.
- 이벤트로 설정할 함수를 넣어줄 대는 화살표 함수 문법을 사용하여 넣어준다.
- state 객체 안에는 여러 값이 있을 수 있다.

**useState**

- 객체가 아닌 자유로운 형태의 값 사용 가능
- state를 바꿀때는 setState 혹은 useState를 통해 전달받은 세터 함수를 사용해야한다.
- 한 컴포넌트 안에서 여러 번 사용 가능
