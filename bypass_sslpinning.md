### SSL PINNING 
최근 대부분의 앱에서 프록시 툴(burp, fiddler)을 이용하여 동적진단이 어려워졌습니다..

이유는 SSL PINNING에 있습니다. 최근 구글, 트위터, 금융앱 등에서 SSL PINNING은 이용하고 있는데,

앱은 디바이스의 신뢰할 수 있는 저장소를 무시하고 자체적으로 앱 내부에 저장된 인증서로 서명된 호스트에 SSL 연결을 맺고있습니다. 따라서 우리는 디바이스에 버프인증서와 같은 프록시 툴 인증서로 SSL 연결을 맺기 어려워졌습니다.

하지만 위의 과정은 클라이언트 측 (앱)에서 이루어지는 것이기 때문에 frida 혹은 별도 툴로 우회할 수 있는데, 이번엔 루팅되지 않는 안드로이드 환경에서 SSL PINNING 우회할 수 있는 두 가지 기술에 대해 알아보겠습니다.

### Xposed Framework
Xposed Framework는 프레임워크로 해당 프레임워크를 설치한 후 여러가지 모듈들을 작동시킬 수 있습니다.

사실 Xposed Frimework를 설치하기 위해선 Xposed Installer에서 리커버리 모드에 진입하여 friamework를 설치해야하기 때문에 루팅이 된 단말에서 설치하려 동작시킬 수 있지만, 녹스에뮬레이터 환경에선 루팅을 활성/비활성 할 수 있는 기능이 있기 때문에 루팅을 활성화 한 후 프레임워크 및 이용하고자 하는 모듈을 설치하고 루팅을 비활성화 한 후 우회 기능을 동작시킬 수 있습니다. 

## 1. Xposed Installer apk 설치 

먼저 Xposed Framework를 설치하기위해 우리는 아래 2 가지 항목을 다운로드받아야합니다.

1. Xposed Installer apk (https://forum.xda-developers.com/showthread.php?t=3034811)
3. JustTrustMe apk (실제 pinning우회 기능을 하는 모듈) https://github.com/Fuzion24/JustTrustMe/releases/tag/v.2
(참고로 롤리팝(5.X)버전으로 테스트를 진행했으며, 최근엔 누가(7.X)버전에서도 안정화 되었다고 하니 각 환경에 맞게 진행하면 될 것 같습니다.)


그리고 adb install XposedInstaller_3.1.5.apk 명령어 혹은 에뮬레이터에 apk를 마우스로 끌어다 놓으면 xposed installer가 설치됩니다.

## 2. Xposed Framework


