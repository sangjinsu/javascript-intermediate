# Function Object

- Function.prototype.call()

## Function Object 생성

- `function` 키워드 사용
- Function Object 의 prototype에 연결된 메서드로 function object 생성

## Function Object 저장

- {name: value} 형태로 저장
- **{[함수 이름] : [생성된 function object]} 형태**
- 함수 호출시 저장된 object를 함수 이름으로 검색하여 value값을 구하고 value 가 function object이면 호출한다 
- 함수 호출시 엔진은 {name: value} 형태로 실행 환경 설정하여 함수 코드 실행

## Function Object 생성 과정

1. `function square() { ... }` 형태에서 function 키워드를 만나면 object를 생성하고 `{square: { ... }}` 형태로 저장한다. 현재 `{ ... }` object는 프로퍼티가 빈 상태이다

2. square object에 prototype 오브젝트를 더한다

   ```js
   square = {
       prototype : {
           constructor: square
           __proto__: {}
       }
   }
   ```

3. prototype에 constructor 프로퍼티를 더한다

4. prototype에 `__proto__` object 를 더한다

5. Object.prototype 메소드로 Object 인스턴스를 생성하여 `prototype.__proto__` 에 더한다

6. square object 에 `__proto__` object를 더한다

7. Function.prototype 메서드로 function 인스턴스를 생성하여 `square.__proto__` 에 더한다

8. square object property 초기값을 설정한다 => arguments, caller, length, name

   ```js
   square = {
       arguments: {},
       caller: {},
       length: 1,
       name: "square",
       prototype : {
           constructor: square
           __proto__: Object.prototype
       }
       __proto__: Function.prototype
   }
   ```

## 함수 실행 환경 인식

- 실행 환경 설정 시점
  - function 키워드로 function object 생성할 때

- 설정 요소
  - 실행 영역, 스코프  lexical scope
  - 파라미터, 코드 등 함수 요소

- 함수 실행 환경 저장
  - 바로 실행하지 않고 함수 호출시 사용할 환경을 생성한 function object 에 저장한다
  - function object 내부 프로퍼티에 인식한 환경을 설정한다

- 내부 프로퍼티
  - 엔진이 내부 처리에 사용하는 프로퍼티
  - 스펙 표기로 외부에서 사용을 할 수 없다
  - [[]] => example [[Prototype]]

 ## 내부 프로퍼티

- 공통 내부 프로퍼티
  - 모든 object 에 공통으로 설정되는 프로퍼티

- 선택적 내부 프로퍼티

  - object 에 따라 선택적으로 설정되는 프로퍼티

  - 해당되는 object에만 설정

## 함수 정의 형태 

- 함수 선언문

  ```js
  function add(a, b){
      return a + b
  }
  ```

- 함수 표현식

  ```js
  const add = function(a, b) {
      return a + b
  }
  ```

- Function 키워드

  ```js
  const add = new Function('a', 'b', 'return a+b')
  ```

## 엔진 해석 방법

	### 엔진 해석 순서

1. 함수 선언문을 순서대로 해석한다
2. 표현식을 순서대로 해석한다 (함수 표현식 포함),  **값을 우선적으로 undefined로 설정하고 후에 값을 할당한다**

## 함수 코드 해석 순서

``` js
function study(){
    debugger
    const title = 'javascript'
    function goStudy(){
        return title
    }
    const studyHard = function(){}
    goStudy()
}
study()
```

1. 함수 선언문 해석
   - `goStudy(){}`

2. 변수 초기화
   - title = undefined,  studyHard = undefined
3. 코드 실행 
   - title = 'javascript', studyHard = function(){}
   - goStudy()

## Hoisting

- 함수 선언문은 초기화 단계에서 function object를 생성하므로 어디서든지 함수를 호출할 수 있다

## Overloading

- 함수 이름이 같으나 파라미터 타입이나 수가 다르다
- **자바스크립트는 오버로딩을 지원하지 않는다** => 자바스크립트는 파라미터 수와 값 타입을 구분하지 않고 {name: value} 형태로 저장하기 때문이다

