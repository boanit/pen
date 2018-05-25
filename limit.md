### 불필요한 메소드란
웹 서비스 제공 시 불필요한 Method(PUT, DELETE, OPTIONS 등) 허용으로 공격자에 의해 악성파일을 업로드 하거나 중요파일 삭제가 가능해지는 취약점입니다.

### 점검 방법
점검 방법은 프록시 툴을 이용하여 점검할 수 있습니다.
OPTIONS 메소드를 사용하여 Request 패킷을 전송해 응답 값 헤더영역에 Allow필드에 허용된 메소드를 확인할 수 있습니다.
아래와 같이 apache 설치 시 디폴트로 GET, HEAD, POST, OPTIONS, TRACE 메소드가 허용되어있음을 확인할 수 있습니다.

<div>
<img src="https://github.com/boanit/pen/blob/master/options.png" width="90%"></img>
</div>

### 조치 방법

/etc/httpd/conf/httpd.conf 경로에서 설정 파일을 수정합니다.
<div>
<img src="https://github.com/boanit/pen/blob/master/httpdconf.png" width="90%"></img>
</div>
(수정 후 아파치서버를 restart해야 설정이 적용되니 참고하시기 바랍니다.)

### 조치 결과

아래와 같이 OPTIONS메소드를 사용한 경우 사용자 정의 에러페이지가 출력되며 허용된 메소드가 출력되지 않는 것을 확인할 수 있습니다.

<div>
<img src="https://github.com/boanit/pen/blob/master/result.png" width="90%"></img>
</div>
