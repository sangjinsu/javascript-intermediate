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

1. 자바스크립트 엔진이 new 연산자를 만나면 function [[Construct]] 를 호출하면서 파라미터 값으로 '한국사' 를 넘겨준다

2. function object를 생성할 때 Book 함수 전체를 참조하도록 [[Construct]] 에 설정한다
3. [[Construct]]에서 인스턴스를 생성하여 반환한다 
4. 반환된 인스턴스를 new 연산자가 받아 new 연산자를 호출한 곳으로 반환한다
5. new 연산자는 function 오브젝트의 [[Construct]]가 인스턴스를 생성한다  

### 인스턴스 생성 과정

```
Book 인스턴스: {
	name = '한국사'
	__proto__ = {
		constructor : Book
		getName: function(){},
		__proto__: Object
	}
}
// [[Construct]] 는 내부 프로퍼티
// constructor 는 외부 프로퍼티이다 
```

1. new Book('한국사') 실행
   - Book 오브젝트의 [[Consturct]] 호출한다
   - 파라미터 값을 [[Construct]]로 넘겨준다

2. 빈 Object 를 상성한다
3. 오브젝트에  공통 프로퍼티와 선택적 프로퍼티를 설정한다
4. 오브젝트의 [[Class]] 에 "Object" 설정에 따라서 생성한 인스턴스 타입은 Object 이다
5. Book.prototype 에 연결된 프로퍼티(메소드)를 생성한 인스턴스의 [[Prototype]]에 설정한다. 그리고 contructor 도 같이 설정한다

### constructor 프로퍼티, constructor 비교

- 생성하는 function 오브젝트를 참조한다

- function 오브젝스 생성시 설정되며 prototype에 연결되어 있다 

  ```js
  const Book = function(){}
  const result = Book === Book.prototype.constructor
  console.log(result) // true
  
  const obj = new Book()
  console.log(Book === obj.constructor) // true
  
  console.log(typeof Book) // function
  console.log(typeof obj)  // object
  ```

  - function 오브젝트를 인스턴스로 생성한 경우 object로 인스턴스의 타입이 변경된다
  - <u>[[Construct]] 가 실행될 때 생성한 오브젝트의 [[Class]] 에 'Object' 를 설정하기 때문이다</u>
  - <u>**object 타입으로 변경된다는 점은 인스턴스의 성격과 목적이 달라졌다는 것이다**</u>

## prototype, 상속

