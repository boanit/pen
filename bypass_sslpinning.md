### SSL PINNING 
최근 대부분의 앱에서 프록시 툴(burp, fiddler)을 이용하여 동적진단이 어려워 졌다.

이유는 SSL PINNING에 있다. 최근 구글, 트위터, 금융앱 등에서 SSL PINNING를 이용하고 있는데,

앱은 디바이스의 신뢰할 수 있는 저장소를 무시하고 자체적으로 앱 내부에 저장된 인증서로 서명된 호스트에 SSL 연결을 맺는다. 따라서 우리는 디바이스에 버프인증서와 같은 프록시 툴 인증서로 SSL 연결을 맺기 어려워졌다.

하지만 위의 과정은 클라이언트 측 (앱)에서 이루어지는 것이기 때문에 frida 혹은 별도 툴로 우회할 수 있는데, 이번엔 루팅되지 않는 안드로이드 환경에서 SSL PINNING 우회할 수 있는 두 가지 기술에 대해 알아보겠다.

### Xposed Framework


### 옵션
ServerTokens Prod : Apache
ServerTokens Min : Apache 버전
ServerTokens OS : Apache 버전 및 운영체제(설치 시 Default)
ServerTokens Full : 모든 정보

### 조치 결과

아래와 같이 Prod로 설정시 Apache만 확인할 수 있습니다.
![header_result](./header_result.png)
