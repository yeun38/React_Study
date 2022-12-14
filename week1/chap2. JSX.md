# 리액트 코드

<h2>✅ 파일을 불러올 때 import 사용</h2>

- node.js 에서 지원하는 기능으로 모듈을 불러와 사용한다.
- 브라우저에서도 사용하기 위해 번들러를 사용한다.
- 번들러의 예시로 웹팩, Parcel, browserify라는 도구들이 존재한다.
- 리액트에서는 주로 확장성과 편의성이 뛰어난 웹팩을 사용한다.
- 번들러는 불러온 모듈을 모두 합쳐서 하나의 파일을 생성해 주며 최적화 과정에서는 여러개의 파일로 분리될 수도 있다.
- 파일들을 불러올 때는 웹팩의 로더라는 기능이 담당
  - 그 중 babel-loader는 자바스크립트 파일들을 불러오면서 최신 자바스크립트 문법을 바벨이라는 도구를 통해 ES5문법으로 변환해준다.
    <br/>
    **✋ 최신 자바스크립트의 코드를 변환하는 이유는??**
    <br/>
  - 구 웹버전과 호환하기 위해서
  - JSX는 정식 자바스크립트 문법이 아니기때문에 변환해주기 위해서

<h2>✅ JSX </h2>
<h3>Javascript에 XML을 추가한 확장한 문법이다.</h3>

<h3>특징</h3>

- 보기 쉽고 익숙하다.
- 더욱 높은 활용도
- 컴포넌트 내부는 하나의 DOM 트리 구조로 이루어져야한다는 규칙 존재

  ```
  import {Fragment} from 'react'
      function App(){
          return (
              <Fragment>
              <h1>리액트 안녕</h1>
              <h2>주니어 안녕</h2>
              </Fragment>
          )
      }
  export default App
  ```

- 자바스크립트 표현이 가능 > {코드}
- 조건부 연산자 (삼항 연산자) 사용
- AND 연산자를 사용한 조건부 렌더링
- OR 연산자를 사용한 undefined 렌더링 하지 않기
  - 논리곱(&&) 연산은 두 개 항이 참이어야 참이다. 왼쪽과 오른쪽 항을 평가해야 참인지 거짓인지 알 수 있다. 참일 경우 진행 방향에 따라 오른쪽 항의 값을 반환한다.
  - 논리곱(||) 연산은 두 개 항 중에서 하나만 참이어도 참이다. 진행 방향에 따라 첫번째 항이 참이라면 첫번째 항을 반환하며 두번째 항만이 참이라면 두번째 항을 반환한다. 첫 번째 항을 거짓으로 두고 반환값을 두번째 항에 두면 거짓 조건을 평가할 수 있다.
- class 대신 className 사용

<br/>

<h3> ➕ ESLint 와 Prettier</h3>

- ESLint는 문법 검사 도구로 코드에러 및 경고 메세지를 VS Code에서 바로 확인할 수 있다.
- Prettier는 코드 스타일 자동 정리 도구로, 해당 프로젝트에 맞게 설정하여 사용할 수 있다.
