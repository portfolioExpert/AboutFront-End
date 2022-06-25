## 고차함수 코드 간략화 예시

### 1. 총 수량, 총 가격

~~~javascript
const products =[
  {name: '반팔티', price: 15000, quantity: 1},
  {name: '긴팔티', price: 20000, quantity: 2},
  {name: '핸드폰케이스', price: 15000, quantity: 3},
  {name: '후드티', price: 30000, quantity: 4},
  {name: '바지', price: 25000, quantity: 5},
]

const add = (a, b) => a + b

//총 수량
const total_quantity = pipe(
  map(p => p.quantity),
  reduce(add))

//총 가격
const total_price = pipe(
  map(p => p.price * p.quantity),
  reduce(add))

//더 높은 추상화
const sum = (f, iter) => go(
	iter,
  map(f),
  reduce(add))

//총 수량
const total_quantity = products =>
	sum(p => p.quantity, products)

//총 가격
const total_price = products =>
	sum(p => p.price * p.quantity, products)

//curry 이용
const sum = curry((f, iter) => go(
	iter,
  map(f),
  reduce(add)))

//총 수량
const total_quantity = sum(p => p.quantity)

//총 가격
const total_price = sum(p => p.price * p.quantity)
~~~