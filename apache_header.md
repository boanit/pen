### 아파치 헤더 보안 설정
아파치 서버의 경우 Default로 Respons 헤더에 서버 정보가 노출되는 것을 확인할 수 있습니다.
![header_exposure](./header_exposure.png)

### 조치 방법

/etc/httpd/conf/httpd.conf 경로에서 설정 파일을 수정합니다.

![header_modify](./header_modify.png)

(수정 후 아파치서버를 restart해야 설정이 적용되니 참고하시기 바랍니다.)

### 옵션
ServerTokens Prod : Apache
ServerTokens Min : Apache 버전
ServerTokens OS : Apache 버전 및 운영체제(설치 시 Default)
ServerTokens Full : 모든 정보

### 조치 결과

아래와 같이 Prod로 설정시 Apache만 확인할 수 있습니다.
![header_result](./header_result.png)
