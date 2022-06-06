## 핫 로딩

- 간단하게 사용: webpack.config.js에서 hot: true



### 핫 모듈 리플레이스먼트

- 결과가 바뀐 부분만 핫 모듈을 이용해 전체 렌더링을 하는 것이 아닌 부분 렌더링을 가능하도록 한다.

Ex)

~~~javascript
module.hot.accept('./result', async () ={
  console.log("result 모듈 변경됨");
	resultEl.innerHTML = await result.render();
});
~~~

-> 변화가 필요한 부분만 accept에 넣어준다.