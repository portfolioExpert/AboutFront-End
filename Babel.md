## 바벨

- ECMAScript2015+로 작성한 코드를 모든 브라우져에서 동작하도록 호환성을 지켜준다. 타입스크립트, JSX처럼 다른 언어로 분류되는 것도 포함.
- ES6 -> ES5로 변환



### 바벨 빌드 순서

파싱 -> 변환 (플러그인)-> 출력

- ECMAScript2015+를 ECMAScript5 버전으로 변환할 수 있는 것만 빌드한다. 그렇지 못한 것들은 풀리필 이라고 부르는 코드 조작을 추가해서 해결.
