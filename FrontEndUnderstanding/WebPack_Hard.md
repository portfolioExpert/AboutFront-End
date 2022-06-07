## WebPack(Hard)

- Webpack-dev-server: 개발용 서버(우리가 흔히 쓰는 localhost 같은 것)
- 설치: npm i webpack-dev-server
- contentBase: 정적 파일을 제공할 경로. 기본값은 웹팩 아웃풋이다.
- publicPath: 브라우져를 통해 접근하는 경로. 기본값은 '/' 이다.
- Host: 개발환경에서 도메인을 맞추어야 하는 상황에서 사용한다. 예를들어 쿠키 기반의 인증은 인증 서버와 동일한 도메인으로 개발환경을 맞추어야 한다. 운영체제의 호스트 파일에 해당 도메인과 127.0.0.1 연결한 추가한 뒤 host 속성에 도메인을 설정해서 사용한다.

- overlay: 빌드시 에러나 경고를 브라우져 화면에 표시
- Port: 개발 서버 포트 번호를 설정한다. 기본값은 8080
- stats: 메시지 수준을 정할 수 있다. 'none', 'errors-only', 'minimal', 'normal', 'verbose'로 메시지 수준을 조절
- historyApiFallBack: 히스토리 api를 사용하는 SPA 개발시 설정한다. 404가 발생하면 index.html로 리 다이렉트



### API 연동

- 웹팩에서 목업 API를 제공 -> Json으로 더미 데이터를 두고 실행해볼 수 있다.

  Ex)

  webpack.confing.js 파일에 devServer에서 함수로 선언

  ~~~javascript
  before: app => {
    app.get("/api/users", (req,res) =>{
  		res.json([
        {
        id:1,
        name:"Alice"
      	}
      ]);
  	});
  }
  ~~~



- connect-api-mocker 

  - 실제 api가 나오기 전에 테스트를 할 수 있는 것
    - 설치: npm i -D connect-api-mocker
    - 루트에 mock/api/users를 만들고 메소드 이름으로 json 파일(GET.json)을 만든다.
    - 다음 데이터를 넣어둔다.
    - webpack.config.js에 app.use(apiMocker('/api', 'mocks/api')) 추가

  

  ex)

  ~~~json
  [
    {
    "id": 1,
    "name": "Alice"
  	},
   {
     "id": 2,
     "name": "Bek"
   },
   {
     "id": 3,
     "name": "Chris"
   }
  ]
  ~~~



- CORS 정책은 같은 도메인에서 api 요청을 할 수 있는데 이것은 front에서 apiURL을 proxy로 잡아주거나 서버에서 애스터리스크를 추가해 준다.