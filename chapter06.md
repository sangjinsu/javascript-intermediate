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

2. 빈 Object 를 생성한다
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
  - [[Construct]] 가 실행될 때 생성한 오브젝트의 [[Class]] 에 'Object' 를 설정하기 때문이다
  - <u>**object 타입으로 변경된다는 점은 인스턴스의 성격과 목적이 달라졌다는 것이다**</u>

## prototype, 상속

#### Prototype 오브젝트 목적

- prototype 확장
  - prototype 에 프로퍼티를 연결하여 prototype 확장
  - Book.prototype.getName = function(){}

- 프로퍼티 공유

  - **<u>생성한 인스턴스에서 원본 prototype 프로퍼티 공유</u>**

  - 인스턴스는 클래스의 함수를 참조하여 사용할 뿐이다
  - obj.getName()

- 인스턴스 상속
  - function 인스턴스를 연결하여 상속
  - Point.prototye = new Book()
  - 프로토타입의 상속이라고도 볼 수 있다

#### 인스턴스 상속

- 인스턴스 상속 방법
  - **<u>prototype 에 연결된 프로퍼티로 인스턴스로 생성하여 상속 받을 prototype 에 연결한다</u>**
  - <u>**prototype-based 상속이라고 한다**</u>

```js
// ES5
function Book(title){
    this.name = name
}
Book.prototype.getTitle = function(){
    return this.title
}
function Point(title){
    Book.call(this, title)
}
Point.prototype = Object.create(Book.prototype. {})

const boj = new Point('한국사')
console.log(boj.getTitle()) // '한국사'
```

- 자바스크립트에서 prototype 은 상속보다 프로퍼티 연결이 의미가 더 크고 인스턴스 연결도 프로퍼티 연결의 하나이다
- ES5 상속은 OOP 상속 기능이 부족하지만 ES6의 Class로 상속을 사용한다 

```js
// ES6
class Book{
    constructor(title){
        this.title = title
    }
    getName(){
        return this.name
    }
}

class Point extends Book{
    constructor(title){
        super(title)
    }
}

const boj = new Point('한국사')
console.log(boj.getTitle()) // '한국사'
```

## 프로토타입 확장 방법

- prototype 에 프로퍼티를 연결하여 작성한다

- name 에 프로퍼티 이름을 작성한다

- prototype 에 null 을 설정하면 확장할 수 없다 

- prototype 에 연결할 프로퍼티가 많을 경우

  `Book.prototype = {name: value  ....}`

- 하지만 프로퍼티를 많이 연결한 경우 constructor가 사라진다. 그래서 다시 constructor를 연결한다

```js
function Book(){}
Book.prototype = {
    constructor: Book,
    setPoint: function(){}
}
```

#### prototype 확장과 인스턴스 형태

```js
function Book(title){
    this.title = title
}
Book.prototype.getTitle = function(){
    return this.title
}
const obj = new Book('자바스크립트')
obj.getTitle()
```

```
obj : {
	title: '자바스크립트'
	__proto__ = {
		constructor: Book,
		getPoint: function(){},
		__proto__: Object
	}
}
```

1. `function Book(title){}`

   Book 오브젝트 생성

2. Book.prototype에 getTitle 메소드 연결
3. Book 인스턴스를 생성하여 obj 에 할당
4. obj.getTitle() 호출
5. 인스턴스를 생성하면 prototype 에 연결된 메소드를 인스턴스.메소드이름() 형태로 호출한다

## this와 프로토타입

### this로 인스턴스 참조

- this 로 메소드를 호출한 인스턴스 참조
- 인스턴스에서 메소드 호출 방법
  - prototype 에 연결된 프로퍼티가 `__proto__` 에 설정되며 인스턴스 프로퍼티가 된다
  - this.prototype.setPoint() 형식이 아닌 this.setPoint() 형태로 출력된다

```js
function Book(){
    console.log(this.point)
}
Book.prototype.getPoint = function(){
    this.setBook()
    console.log(this.point)
}
Book.prototype.setPoint = function(){
    this.point = 100
}

const obj = Book() // undefined
obj.getPoint() // 100
```

## prototype 프로퍼티 공유 시점

- 사용 시점에 prototype 프로퍼티 공유
- prototype 프로퍼티로 인스턴스 생성하지만 인스턴스 프로퍼티는 원본 prototype의 프로퍼티 참조를 한다
- 인스턴스 메소드 호출시 원본 prototype 메소드를 호출한다
- ***<u>원본 prototype 에 메소드를 추가하면 생성된 모든 인스턴스에서 추가한 메소드를 사용할 수 있다!</u>***

```js
function Book(){
    this.point = 100
}
const obj = new Book()
obj.getPoint() // undefined

Book.prototype.getPoint = function(){
    return this.point
}
obj.getPoint() // 100
```

## 인스턴스 프로퍼티

- prototype 에 연결된 프로퍼티도 인스턴스 프로퍼티가 된다 
- 직접 인스턴스에 연결된 프로퍼티와 차이가 있다
- ***<u>인스턴스 프로퍼티를 prototype 으로 만든 인스턴스 프로퍼티 보다 먼저 사용하게 된다</u>***
- 인스턴스 마다 값을 다르게 가질 수 있다 

 
