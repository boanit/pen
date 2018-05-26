### Postman

Postman은 HTTP Request, Response 패킷을 통하여 개발한 API서버를 용이하게 테스트 할 수 있는 툴입니다.
Fiddler나 Burpsuit에서도 패킷을 보내거나 받을 수 있지만 Postman은 프록시 설정을 하지 않아도 된다는 장점을 가지고 있으며,
API서버 테스트에 용이하도록 GUI 환경이 구성되어있습니다.

### 설치하기

Postman은 크롬 브라우저의 확장 프로그램으로 구글에서 설치할 수 있습니다.

초기화면

![설치](./installation2.png)

### 사용하기

먼저 요청하고자하는 URL 및 요청 메소드를 선택합니다.

선택 후 헤더 영역을 요청하고자 하는 API 양식에 맞추어 작성합니다.
(OAuth, AWS Signature 등 API 서버의 인증이 필요할 경우 Authorization 메뉴를 통해 인증 키 혹은 ID/PWD를 설정할 수 있습니다.)

<div>
<img src="./test01.png" width="90%"></img>
</div>


헤더 영역을 모두 작성한 후 바디 영역을 작성합니다.

<div>
<img src="./test02.png" width="90%"></img>
</div>

바디영역 작성 시 form-data, x-www-form-urlencoded, raw, binary(파일 업로드) 형식으로 선택하여 작성이 가능하며,
raw로 작성할 경우 Text,Text(test/plain), JSON, Javascript, xml(application/xml), xml(test/xml), HTML(text,html) 으로 형식에 맞게 작성이 가능합니다.

<div>
<img src="./json.png" width="90%"></img>
</div>

Send 메뉴를 클릭하며 해당 Request 값에 대한 Response가 아래와 같이 출력됩니다.

<div>
<img src="./response.png" width="90%"></img>
</div>

### Postman Interceptor

Postman Interceptor를 활성화 경우 좌측 History에 로컬 브라우저에서 요청한 패킷에 대한 Histroy가 쌓이므로 유용하게 사용할 수 있습니다.

postman과 같이 크록 확장프로그램으로 구글 검색 후 설치할 수 있으며 상단의 Postman Interceptor메뉴를 통해 활성화 할 수 있습니다.

<div>
<img src="./postmaninterceptor.png" width="90%"></img>
</div>

### 활용하기 

postman은 Save메뉴를 통하여 자신의 요청 패킷을 계정에 저장할 수 있으며 Import를 통해 저장한 패킷을 불러 올 수 있습니다.

또한 Team Libary 메뉴를 통해 자신의 패킷을 다른 사용자들과 공유할 수 있습니다.

<div>
<img src="./teamlibrary.png" width="90%"></img>
</div>


