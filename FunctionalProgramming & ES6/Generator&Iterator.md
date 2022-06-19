## 제너레이터와 이터레이터

### 1. 제너레이터와 이터레이터

- 제너레이터: 이터레이터이자 이터러블을 생성하는 함수
- 제너레이터는 마지막 done이 true가 되면서 return값을 만들 수 있다.
- 제너레이터는 문장을 값으로 만들 수 있고, 문장을 통해 어떠한 값이나 상태든 순회할 수 있도록 만들 수 있다.

Ex)

~~~javascript
function *gen(){
	yield 1;
  yield 2;
  yield 3;
  return 100
}
let iter = gen()
log(iter.next())// value: 1, done: false
log(iter.next())// value: 2, done: false
log(iter.next())// value: 3, done: false


~~~



### 2. 홀수 출력하는 예제

~~~javascript
function *infinity(i = 0){ //끝없이 증가하는 제너레이터
	while(true)yield i++
}
function *limit(l, iter){ //제한 값과 이터레이터를 받아 정지시키는 제너레이터
  for(const a of iter){
    yield a;
    if(a == l)return
  }
}
function *odds(l){ //정해진 범위에서 홀수만 출력하는 제너레이터
  for(const a of limit(l, infinity(1))){
    if(a % 2)yield a
  }
}
//1부터 40까지 홀수만 출력
for(const a of odds(40)) log(a)
~~~



### 3. 제너레이터의 전개 연산자, 구조 분해, 나머지 연산자

Ex)

~~~javascript
log(...odds(10))// 1 3 5 7 9
log([...odds(10), ...ods(20)]) // 1,3,5 ... 17, 19
const [head, ...tail] = odds(5)
log(head) // 1
log(tail) // [3,5]
~~~

