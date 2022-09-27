## 모던 자바스크립트 Deep Dive



### Chapter 13. 스코프



##### 스코프

- 모든 식별자는 자신이 선언된 위치에 의해 다른 코드가 식별자 자신을 참조할 수 있는 유효 범위가 결정되는 것

~~~javascript
var x = 'global';
function foo() {
    var x = 'local';
    console.log(x); // local
}

foo();
console.log(x);//global
~~~

- var 키워드로 선언한 변수는 중복선언이 되므로 되도록 let을 쓰자



##### 스코프 종류

- 전역 스코프: 전역변수로 코드의 가장 바깥 영역
- 지역 스코프: 지역변수로 함수 몸체 내부 영역



##### 스코프 체인

- 스코프가 계층적으로 연결된 것
- 변수를 참조할 때 자바스크립트 엔진은 스코프 체인을 통해 변수를 참조하는 코드의 스코프에서 시작하여 상위 스코프 방향으로 이동하며 선언된 변수를 검색

~~~javascript
var x = "global x";
var y = "global y";

function outer(){
  var z = "outer's local z";
  
  console.log(x); //global x
  console.log(y); //global y
  console.log(z); //outer's local z
  
  function inner(){
    var x = "inner's local x";
    
    console.log(x); //inner's local x
    console.log(y); //global y
    console.log(z); //outer's local z
  }
  
  inner();
}

outer();

console.log(x);//global x
console.log(z); //ReferenceError: z is not defined
~~~



> 렉시컬 환경
>
> 스코프 체인은 실행 컨텍스트의 렉시컬 환경을 단방향으로 연결한 것이다. 전역 렉시컬 환경은 코드가 로드되면 곧바로 생성되고 함수의 렉시컬 환경은 함수가 호출되면 곧바로 생성된다.



##### 함수 레벨 스코프

- 코드 블록이 아닌 함수에 의해서만 지역 스코프가 생성된다.

- 블록 레벨 스코프: if, for, while, try/catch 등으로 생성된 지역 스코프

- var 키워드로 선언된 변수는 오로지 함수의 코드 블록(함수 몸체)만을 지역 스코프로 인정한다. 

  -> if, for, while, try안에서는 변수를 중복 선언해도 전역변수 처리

~~~javascript
var x = 1;

if(true){
	var x = 10;
}

console.log(x); //10이 출력
~~~



##### 렉시컬 스코프

~~~javascript
var x = 1;
function foo(){
  var x = 10;
  bar();//전역스코프를 기억한다.
}

function bar(){
  console.log(x);//1을 기억하고있다.
}

foo();//1
bar();//1
~~~

- 동적 스코프: 함수를 어디서 호출했는지에 따라 함수의 상위 스코프를 결정한다.
- 렉시컬 스코프: 함수를 어디서 정의했는지에 따라 함수의 상위 스코프를 결정한다.

자바스크립트는 렉시컬 스코프를 따른다.



---

### Chapter 14. 전역 변수의 문제점



##### 변수의 생명주기

- 지역변수의 생명주기는 함수의 생명주기와 일치한다.
- var 키워드로 선언한 전역 변수는 전역 객체의 프로퍼티가 된다. 따라서, 전역변수의 생명주기는 전역객체의 생명주기와 일치한다.

~~~javascript
var x = 'global';

function foo(){
  console.log(x); //지역변수 local을 참조해 출력
  var x = 'local';
}

foo();
console.log(x); //global
~~~

>전역 객체
>
>코드가 실행되기 이전 단계에 자바스크립트 엔진에 의해 어떤 객체보다도 먼저 생성되는 특수한 객체.
>
>전역 객체는 클라이언트 사이드에서는 window, 서버 사이드 환경은 global 객체를 의미하며 식별자로 window, self, this, frames, global이 존재했으나 ES11에서 globalThis로 통일



##### 전역 변수의 문제점

- 암묵적 결합: 모든 코드가 전역 변수를 참조하고 변경할 수 있다.
- 긴 생명주기: 전역 변수는 생명주기가 길다.
- 스코프 체인 상에서 종점에 존재: 전역 변수의 검색 속도가 가장 느리다.
- 네임스페이스 오염: 자바스크립트는 파일이 분리되어 있다 해도 하나의 전역 스코프를 공유한다는 것



##### 전역 변수의 사용을 억제하는 방법

- 즉시 실행 함수: 함수의 정의와 동시에 즉시 실행 함수는 단 한 번만 호출. 모든 코드를 즉시 실행 함수로 감싸면 모든 변수는 즉시 실행 함수의 지역 변수가 된다.

~~~javascript
(function (){
  var foo = 10;
}());

console.log(foo);//ReferenceError foo is not defined
~~~



- 네임스페이스 객체: 전역 변수처럼 사용하고 싶은 변수를 프로퍼티로 추가하는 방법

~~~javascript
var MYAPP = {};
MYAPP.name = 'Lee';

console.log(MYAPP.name); //Lee
~~~

-> 네임스페이스 객체 자체가 전역 변수에 할당되므로 그닥 유용하진 않다.



- 모듈 패턴: 클래스를 모방해서 관련이 있는 변수와 함수를 모아 즉시 실행 함수로 감싸 하나의 모듈을 만든다. 또한, 클로저 기반으로 동작한다.

~~~javascript
var Counter = (function (){
  var num = 0;
  
  //외부로 공개할 데이터나 메서드를 프로퍼티로 추가한 객체를 반환
  return {
    increase(){
      return ++num;
    },
    decrease(){
      return --num;
    }
  };
}());

// private으로 노출 되지 않는다. 
console.log(Counter.num);//undefined

console.log(Counter.increase()); //1
console.log(Counter.increase()); //2
console.log(Counter.decrease()); //1
console.log(Counter.decrease()); //0
~~~





##### ES6 모듈

- 파일 자체의 독자적인 모듈 스코프를 제공한다.
- var 키워드로 선언한 변수는 더는 전역 변수가 아니며 window 객체의 프로퍼티도 아니다.
