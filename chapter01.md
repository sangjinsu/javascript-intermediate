# Lexical environment 정적 환경
- 선언 시점에서 스코프 결정

- function 키워드를 만나면 function object 생성

- 함수 호출시 FO 의 [[Scope]] 를 실행 콘텍스트의 lexical 환경 컴포넌트의

- 외부 lexical 환경 참조에 설정한다

  ```js
  var point = 123
  function book() {
    function getPoint() {
      console.log(point)
    }
  }
  book()
  ```

- var 변수 선언은  global 오브젝트에 설정된다
- lexical 환경 구조에 맞지 않다
  - ES5 => 'use strict'
  - ES6 => let, const 사용으로 스코프를 제약한다

## 동적 환경

- 실행 시점에서 스코프 결정
  - with, eval()
  - with 문은 strict 모드에서 에러 발생한다
  - eval() 함수는 보안에 문제가 있다

## node.js 코드 형태

- 서버 프로그램 고려 사항 => 10000 명이 동시 접속하는가?
- javascript는 싱글 스레드, 동기 처리
- nodejs는 비동기 처리, C++ 의 semapore, mutex 사용
- context 형태가 효율적이다
- 실행 context에 최적화된 형태로 코드를 작성해야함으로 엔진 처리를 이해해야 한다