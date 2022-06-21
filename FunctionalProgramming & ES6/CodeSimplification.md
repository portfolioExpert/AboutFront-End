## 코드를 값으로 다루어 표현력 높히기

### 1. go

- 인자와 함수를 전달해 값을 평가하는 것

~~~javascript
const products =[
  {name: '반팔티', price: 15000},
  {name: '긴팔티', price: 20000},
  {name: '핸드폰케이스', price: 15000},
  {name: '후드티', price: 30000},
  {name: '바지', price: 25000},
]



const go = (...args) => reduce((a, f) => f(a), args) // 111이 되는데
//a에는 0이 들어가고 f에는 함수가 들어가 끝날 때 까지 수행 해준다.
go(
  0,
  a => a + 1,
  a => a + 10,
  a => a + 100,
  log)

~~~



### 2. pipe

- 함수가 나열된 합성된 함수를 만드는 것

~~~javascript
//위에 go함수를 이용한다.
const pipe = (...fs) => (a) => go(a, ...fs)

const f = pipe(
  a => a + 1,
  a => a + 10,
  a => a + 100)

//인자가 여러개 일 때
//f로 첫 번째 함수만 꺼내서 나머지 인자를 f(...as)로 넣어준다.
const pipe = (f, ...fs) => (...as) => go(f(...as), ...fs)

//이코드와 동일 한 기능
const f = pipe(
  add(0, 1),
  a => a + 10,
  a => a + 100,
	log)
~~~



### 3. go를 사용하여 읽기 좋은 코드로 만들기

~~~javascript
log(
  reduce(
  add,
  map(p=>p.price, 
      filter(p => p.price < 20000, products))))

//go함수로 표현 하기
go(products,
   products => filter(p => p.price < 20000, products),
   products => map(p => p.price, products),
   prices => reduce(add, prices),
   log)
~~~



### 4. go+curry를 사용하여 더 읽기 좋은 코드로 만들기

- curry: 함수를 받아서 함수를 리턴하고 인자를 받아서 인자가 원하는 개수만큼 인자가 들어왔을 때 나중에 평가 시키는 함수

~~~javascript
//함수를 받아서 리턴하고 인자가 2개이상일 경우 받아둔 함수를 즉시 실행하고 작다면 함수를 다시 리턴하고 이후에 받은 인자를 합쳐서 실행하는 것
const curry = f = (a, ..._) => length ? (a, ..._) : (..._) => f(a, ..._)

const mult = (a, b)

//go함수로 표현된 것을 간략화 하기
//products로 받은 것을 다시 인자로 넣어주는 것은 그대로 함수만 넣어주면 같은 코드라는 말
go(products,
   filter(p => p.price < 20000),
   map(p => p.price),
   reduce(add),
   log)
~~~



### 5. 함수 조합으로 함수 만들기

- 함수를 함수로 묶어서 코드 간략화

~~~javascript
//before
go(products,
   filter(p => p.price < 20000),
   map(p => p.price),
   reduce(add),
   log)

const total_price = pipe(
  map(p => p.price), 
  reduce(add))

//after
go(products,
   filter(p => p.price < 20000),
   total_price,
   log)

//after after
const base_total_price = predi => pipe(
filter(predi),
total_price)

go(products,
   base_total_price(p => p.price < 20000),
   log)
~~~



