# function instance

- function 구분
  - 빌트인 Function 오브젝트
  - function 오브젝트: function 키워드로 생성
  - function instance: new 연산자로 생성

- function 오브젝트도 인스턴스
  - 빌트인 Function 오브젝트로 생성하기 때문에 인스턴스이다

- new 연산자로 생성한 인스턴스는 일반적으로 prototype에 프로퍼티를 작성한다 

  ```js
  function Book(name){
      this.name = name
  }
  Book.prototype.getName = function(){
      return this.name
  }
  const boj = new Book('한국사')
  boj.getName()
  ```

  ### 인스턴스 생성 순서

  1. `function Book(){}` Book 오브젝트를 생성하면서 Book.prototype도 생성된다
  2. `Book.prototype.getName = function(){ }` 
     - `Book.prototype`에 getName을 연결하고 function(){ }을 할당한다
     - Book.prototype이 오브젝트이므로 프로퍼티를 연결할 수 있다

  3. `const boj = new Book('한국사')` 
     - Book() 을 실행하여 인스턴스를 생성하고 생성할 인스턴스에 name 값을 설정한다 
     - Book.prototype 에 연결된 프로퍼티를 생성한 인스턴스를 할당한다 

## 생성자 함수, 인스턴스 생성 과정

### 생성자 함수

- `new` 연산자와 함께 인스턴스를 생성하는 함수
- `new` 연산자
  - 인스턴스 생성 제어 및 생성자 함수 호출

- 생성자 함수
  - 인스턴스 생성 및 반환
  - 인스턴스에 초깃값 설정

- 생성자 함수의 첫 문자는 대문자이다

### 생성자 함수 실행 과정

```js
function Book(name){
    this.name = name
}
Book.prototype.getName = function(){
    return this.name
}
const boj = new Book('한국사')
boj.getName()
```

1. 자바스크립트 엔진이 new 연산자를 만나면 function [[Construct]] 를 호출하면서 파라미터 값으로 10을 넘겨 줍니다 

2. function object를 생성할 때 Book 함수 전체를 참조하도록 [[Construct]] 에 설정하였다
3. [[Construct]]에서 인스턴스를 생성하여 반환한다 
4. 반환된 인스턴스를 new 연산자가 받아 new 연산자를 호출한 곳으로 반환한다
5. new 연산자는 function 오브젝트의 [[Construct]]가 인스턴스를 생성한다  

