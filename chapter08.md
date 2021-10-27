# 논리적 정리

## 재귀 함수, 프로퍼티 연동 방지, 재귀 함수 형태

### 프로퍼티 연동 방지

```js
var origin = {
    member: 100
}
var dup = origin 
dup.member = 200
console.log(origin.member) // 200

var origin = [1, 2, 3]
var dup = origin 
dup[1] = 200
// [1, 200, 3]
```

```js
var origin = {
    member: 100
}
var dup = {}
for (var name in origin){
    dup[name] = origin[name]
}
dup.member = 200
console.log(origin.member) // 100
```

#### 재귀 함수

- 함수 안에서  자기 자신을 다시 호출하는 형태 

```js
var book = {
    member : {name:100},
    point : {value:200}
}
function show(param){
    for (var type in param){
        typeof param[type] === "object" ?
            show(param[type]):
        	console.log(type + ":", param[type])
    }
}
show(book)
```



## 즉시 실행 함수

- 함수 즉시 실행

  - 엔진이 함수를 만난 경우

  - 자동으로 함수를 실행한다

    ```js
    (function(){
        console.log("direct")
    }());
    ```

- 함수 표현식이 아니고 익명 함수라고도 불린다 

```js
var value = (function(){
  return 100;  
}());
console.log(value)
```

## 클로저

- Closure
  - function 오브젝트 생성시 함수가 속한 스코프를 [[Scope]] 에 설정하고 
  - 함수 호출시 [[Scope]] 의 프로퍼티를 사용하는 메커니즘이다 

- [[Scope]] 의 설정과 사용 방법을 이해하면 클로저는 단지 논리적인 설명이다 

  

### 논리

- 실행 중인 function 오브젝트에 작성한 변수, 함수를 선언적 환경 레코드에 설정한다
- [[Scope]] 의 변수, 함수를 외부 렉시컬 환경 참조에 바인딩
- 변수 이름으로 접근하여 값을 사용하거나 변경할 수 있다
- 함수를 호출할 수 있다 

외부 렉시컬 환경 참조를 선언적 환경 레코드에서 사용하는 논리이다

```
실행 컨텍스트 : {
	렉시컬 환경 컴포넌트 : {
		환경 레코드: {
			선언적 환경 레코드: {},
			오브젝트 환경 레코드: {}
		},
		외부 렉시컬 환경 참조: {}
	}
}
```

```js
function book(){
    var point = 100
    var getPoint = function(param) {
        point  = point + param
        return point
    }
    return getPoint
}
var obj = book()
console.log(obj(200)) // 300
```

