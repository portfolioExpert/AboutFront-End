## Javascript Basic

- 평가: 코드가 계산되어 값을 만드는 것
- 일급
  - 값으로 다룰 수 있다.
  - 변수에 담을 수 있다.
  - 함수의 인자로 사용될 수 있다.
  - 함수의 결과로 사용될 수 있다.
- 일급 함수 -> 함수는 일급
  - 함수를 값으로 다룰 수 있다.
  - 조합성과 추상화의 도구
- 고차 함수: 함수를 값으로 다루는 함수
  - 함수를 인자 값으로 다루는 것
  - 함수를 리턴할 수 있는 것

~~~javascript
const addMaker = a => b => a + b; //클로저를 리턴하는 함수
const add10 = addMaker(10);
log(add10(5)); //=> 15
log(add10(10)); //=> 20
~~~

- 클로저: 안에있는 함수가 a를 계속 기억하는 것