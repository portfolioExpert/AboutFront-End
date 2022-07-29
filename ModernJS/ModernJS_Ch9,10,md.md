## 모던 자바스크립트 Depp Dive



### Chapter 9 타입 변환과 단축 평가

###### 암묵적 타입 변환

- 자바스크립트 엔진은 표현식을 평가할 때 개발자의 의도와는 상관없이 코드의 문맥을 고려해 암묵적으로 데이터 타입을 강제 변환



###### 명시적 타입 변환

- 타입을 개발자에 의해 명시적으로 변화시켜주는 것



###### 단축평가

- 표현식을 평가하는 도중에 평가결과가 확정된 경우 나머지 평가 과정을 생략하는 것
- 논리 연산의 결과를 결정하는 피연산자를 타입 변환하지 않고 그대로 반환

Ex)

~~~javascript
'Cat' && 'Dog' //Dog 반환, 이유는 Dog에 의해 true로 평가되기 때문
'Cat' || 'Dog' //Cat 반환, 이유는 Cat에 의해 true로 평가되기 때문
~~~



###### 옵셔널 체이닝

?. 연산자: null또는 undefined인 경우 undefined를 반환하고, 그렇지 않으면 우항의 프로퍼티 참조를 이어간다.

-> 일반적으로 null이나 undefined일 경우 TypeError를 발생시킨다.

ex)

~~~javascript
var value = elem?.value;//elem이 null또는 undefinded면 undefined를 반환하고 그렇지 않으면 우항 프로퍼티 참조를 이어간다.
~~~



###### null 병합 연산자

?? 연산자: 피연산자가 null이가 undefined일 경우 우항의 피연산자를 반환하고 그렇지 않으면 좌항을 반환

ex)

~~~javascript
var foo = null ?? 'default string';
//foo는 default string
~~~



### Chapter 10 객체 리터럴

###### 객체

- 프로퍼티와 메서드로 구성된 집합
  - 프로퍼티: 객체의 상태를 나타내는 값
  - 메서드: 프로퍼티를 참조하고 조작할 수 있는 동작

> 인스턴스
>
> 클래스에 의해 생성되어 메모리에 저장된 실체로 객체는 클래스와 인스턴스를 포함한 개념이다. 클래스는 인스턴스를 생성하기 위한 템플릿 역할을 한다.



###### 프로퍼티 축약 표현

~~~javascript
let x = 1, y = 2;
const obj = {x, y};
console.log(obj); // {x: 1, y: 2}
~~~

