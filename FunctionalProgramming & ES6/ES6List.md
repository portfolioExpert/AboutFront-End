## ES6에서의 순회와 이터러블: 이터레이터 프로토콜

### 1. ES6 리스트 순회

~~~javascript
const list = [1,2,3]
for(const a of list){
	log(a)
}
~~~

- 이터러블: 이터레이터를 리턴하는 \[Symbol.iterator\]()를 가진 값
- 이터레이터: {value, done} 객체를 리턴하는 next() 를 가진 값으로 done이 true가 되면 for문을 빠져나온다.
- 이터러블/이터레이터 프로토콜: 이터러블을 for...of로 , 전개 연산자 등과 함께 동작하도록한 규약



### 2. Array, Set, Map 이터러블, 이터레이터 프로토콜

- Array: \[Symbol.iterator\]()를 계속 순회하면서 value라는 값을 변수에 넣어서 순회하는 것 -> 이터러블/이터레이터 프로토콜

ex)

~~~javascript
const arr = [1,2,3]
let iter1 = arr[Symbol.iterator]()
for(const a of iter1)log(a)
~~~

- Set: 이터러블/이터레이터 프로토콜로 \[Symbol.iterator\]()를 계속 순회하는 것

ex)

~~~javascript
const set = new Set([1,2,3])
for(const a of set)log(a)
~~~

- Map: Map또한 이터러블/이터레이터 프로토콜로 \[Symbol.iterator]()를 계속 순회한다.

~~~javascript
const map = new Map([['a',1], ['b', 2], ['c', 3]])
for(const a of map.keys()) log(a)//key만 뽑고
for(const a of map.values()) log(a)//value만 뽑고
for(const a of map.entries()) log(a)//key, value 모두 뽑는다
~~~



### 3. 사용자 정의 이터러블, 이터러블/이터레이터 프로토콜

- \[Symbol.iterator\]()를 정의해 값을 조율해 줄 수 있다.

~~~javascript
const iterable ={
  [Symbol.iterator]() {
    let i = 3;
    return {
      next() {
        return i == 0 ? {done: true}: {value: i--, done: false}
      }
    }
  }
}
~~~



### 4. 전개연산자

- 이터러블, 이터레이터 프로토콜

~~~javascript
const a = [1,2]
log([...a, ...[3,4]]) //[1,2,3,4]
~~~

