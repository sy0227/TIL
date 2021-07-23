# Windows에 WSL2 설치

### WSL2이란?
Windows Subsystem for Linux 2의 준말이다. WSL은 윈도우에서 경량 가상화 기술을 사용해 리눅스를 구동할 수 있도록 도와주는 기능이다. WSL2는 WSL을 대폭 개선해 훨씬 더 뛰어난 성능과 통합된 환경을 이용할 수 있다. 또한 윈도우 10 홈에서도 사용할 수 있어서 홈 에디션에서도 도커Docker를 사용할 수 있다.

### 설치하기

#### 1. 윈도우 터미널(Windows Terminal) 설치하기
Microsoft Store 앱에서 **Terminal**을 검색하고 검색 결과에서 **Windows Terminal**을 선택한다.
![windows terminal image](https://user-images.githubusercontent.com/31719817/126410881-351aa3c9-3f0f-4275-bafd-ee54ad1ba4a9.png)

#### 2. WSL2 활성화를 위한 DISM 명령어 실행
windows terminal을 **관리자 권한**으로 실행하고 다음 두 명령어를 차례로 실행한다.
```
> dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
> dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```
작업이 완료되면 재부팅한다.

#### 3. WSL용 리눅스 배포판 설치
[링크](https://aka.ms/wslstore)로 이동하여 WSL에서 사용할 수 있는 리눅스 배포판을 다운받는다. 나는 Ubuntu를 설치했다.
![image](https://user-images.githubusercontent.com/31719817/126411702-66f5d42b-d76e-4f67-9375-481bd8f5e695.png)

설치가 완료되고 Ubuntu를 실행하면 우분투 터미널이 실행되는데, 여기서 사용자 이름과 패스워드를 지정해준다.
이후에 windows terminal에서 `wsl -l` 명령어를 입력하여 설치된 것을 확인할 수 있다.

#### 4. WSL2 리눅스 커널 업데이트 및 배포판에서 2 버전 활성화하기
[링크](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi)를 클릭하여 리눅스 커널 업데이트를 진행한다.
`wsl -l -v`명령어를 통해 현재 적용된 WSL 버전을 확인할 수 있다. 버전이 1이라고 나오면 `wsl --set-version Ubuntu 2`명령어로 버전을 2로 변경할 수 있다. 그리고 `wsl --set-default-version 2`명령어를 통해 새로 설치하는 모든 배포판에 WSL2가 적용되도록 기본값을 변경해준다.
그리고 `wsl -l -v`명령어를 통해 WSL2가 잘 적용되었는지 확인해본다.

#### 5. WSL2에서 우분투 시작하기
Windows Terminal에서 새 탭(`+`) 우측 버튼을 클릭하여 Ubuntu를 선택하면 WSL 우분투 배포판 셀이 실행된다.

### TroubleShooting
3번 과정에서 우분투를 설치할 때, 처음에는 20.04버전을 설치했다. 그런데 우분투를 실행했을 때 자꾸 `The Windows Subsystem for Linux optional component is not enabled. Please enable it and try again.` 에러가 발생해서 사용할 수 없었다. 검색을 해보니 `제어판-프로그램 및 기능-Windows 기능 켜기/끄기-Linux용 Windows 하위 시스템`을 켜주면 해결된다고 했다. 그런데 난 이미 활성화된 상태여서 난감했다.. 그래서 20.04버전을 삭제하고 3번에 첨부한 이미지의 우분투를 설치해봤는데도 동일한 에러가 발생했다. 그래서 `Linux용 Windows 하위 시스템`을 끄고 재부팅하고 다시 켜고 재부팅해보니까 에러가 사라졌다!

##### 출처
[WSL2 설치 및 사용 방법](https://www.44bits.io/ko/post/wsl2-install-and-basic-usage)
