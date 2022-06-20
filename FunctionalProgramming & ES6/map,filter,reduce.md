## map, filter, reduce

### 1. map

~~~javascript
const products =[
  {name: '반팔티', price: 15000},
  {name: '긴팔티', price: 20000},
  {name: '핸드폰케이스', price: 15000},
  {name: '후드티', price: 30000},
  {name: '바지', price: 25000},
]

//키(이름)만 넣어주는 f함수와 map을 받아서 value를 출력하는 것
const map = (f, iter) => {
  let res = []
  for(const a of iter){
    res.push(f(a))
  }
  return res
}
log(map(p => p.name, products)) //[15000, 20000, 15000, 30000, 25000]
~~~



### 2. 이터러블 프로토콜을 따른 map의 다형성

~~~javascript
log([1,2,3].map(a=>a + 1))//[2,3,4]
function *gen(){
  yield 2
  if(false)yield 3
  yield 4
}
log(map(a => a * a, get())) //[4, 16]
~~~

- 이터러블 프로토콜을 따르는 함수를 사용하는 것은 많은 다른 헬퍼 함수들과 조합성이 좋아진다는 것

~~~javascript
let m = new Map()
m.set('a', 10)
m.set('b', 20)
log(new Map(map(([k, a]) => [k, a * 2], m)))
//map안에 map함수를 사용해 안쪽 값이 바뀐 객체를 만드는데 사용
~~~



### 3.filter

- 값을 어떠한 기준으로 골라내주는 함수

~~~javascript
const products =[
  {name: '반팔티', price: 15000},
  {name: '긴팔티', price: 20000},
  {name: '핸드폰케이스', price: 15000},
  {name: '후드티', price: 30000},
  {name: '바지', price: 25000},
]

//기존 값이 20000원 미만
let under20000 = []
for(const p of products){
  if(p.price < 20000) under20000.push(p)
}
log(...under20000)
//{name: 반팔티 price: 15000}, {name: 핸드폰케이스, price: 15000}

//바뀐 코드
const filter = (f, iter) =>{
  let res = []
  for(const a of iter){
    if(f(a)) res.push(a)
  }
  return res
}
log(...filter(p => p.price < 20000, products))
~~~



### 4. reduce

- 값을 축약하는  -> 이터러블값을 하나의 값으로 축약해 나가는 것

~~~javascript
const nums = [1,2,3,4,5]
let total = 0
for(const n of nums){
  total = total + n
}
log(total)

//합을 구하는 것을
//함수를 받고 누적값과 남은 배열을 이용해서 합을 구해준다.
//보조함수에 축약하는 방법을 위임하는 것
const reduce = (f, acc, iter) =>{
  if(!iter){
    iter = acc[Symbol.iterator]()
    acc = iter.next().value
  }
  for(const a of iter){
    acc = f(acc , a)
  }
  return acc
}

~~~



### 5. Map, filter, reduce 응용

~~~javascript
const products =[
  {name: '반팔티', price: 15000},
  {name: '긴팔티', price: 20000},
  {name: '핸드폰케이스', price: 15000},
  {name: '후드티', price: 30000},
  {name: '바지', price: 25000},
]

const add = (a, b) => a + b

//오른쪽 부터 읽어 나가면 된다.
//20000원 미만의 가격을 뽑고 add를 통해 더해준다
log(reduce(
  add,
  map(p=>p.price, filter(p => p.price < 20000, products))))

//같은 코드의 순서 변경
log(reduce(
  add, 
  filter(n => n >= 20000, map(p => p.price, products))))
~~~

