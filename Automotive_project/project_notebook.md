# 2021/03/05
### .dbc 파일 -> .csv 파일로 변환하기
- 차량 CAN 데이터의 딕셔너리 역할을 하는 CAN 데이터베이스 파일을 dbc 파일이라고 한다.
- OEM이나 차량 관련 기업에서는 고가의 프로그램이 있기 때문에 dbc 파일을 입력해주기만 하면 차량에 떠다니는 CAN 데이터를 파싱할 수 있지만, 대학원에서는 이러한 장비가 없기 때문에 CAN 데이터를 파싱할 수 있는 환경을 직접 구축해주어야 한다.
- 그러기 위해서는 우선 dbc 파일을 csv 파일과 같이 우리가 읽을 수 있는 파일로 변환해주어야 한다.
- 다행히도 우리와 같은 사람이 워낙 많기 때문에 파일을 변환해주는 프로그램이 깃허브에 이미 존재한다.
- 이 중에서 내가 사용할 것은 파이썬 패키지로, 사용할 아래의 레포지토리에서 다운로드할 수 있다.  
    > [Canmatrix](https://github.com/ebroecker/canmatrix.git)  
- 레포지토리의 `README.md`에 설치에 대한 링크도 있으므로 참고하면 된다.
- 패키지 설치를 완료하면 아래의 명령어를 통해 매우 간단하게 dbc 파일을 csv 파일로 변환할 수 있다.  
    >`canconvert [candatabase.dbc] [candatabase.csv]`  

# 2021/03/24
### 차량용 PC 이더넷 다중 연결
- 차량용 PC에는 카메라 및 LIDAR도 이더넷을 통해 연결하기 때문에 인터넷을 연결하는 이더넷을 포함해서 두 개의 이더넷을 커넥트해야 한다.
- 카메라 및 라이다를 인식하는 이더넷은 업체에서 제공하는 SDK(Software Development Kit)을 통해 연결이 이미 되어 있기 때문에 문제가 없다.
- 그러나 카메라 및 라이다용 이더넷을 연결해 놓으면 PC에서 와이파이 연결이 안되는 문제가 있었다.
- 몇시간 동안 마구잡이식으로 이것저것 해보다가 해결한 방법이라 정확하게 적지는 못하지만, 그래도 일단 추후에 이런 상황이 또 발생할 수 있기 때문에 기억나는대로 기록해두려고 한다.
- 그래서 해결책으로 주로 무선 공유기로 사용하는 `iptime`을 공유기가 아닌 라우터(router)로 사용하여 핫스팟이나 포켓와이파이 같이 무선 네트워크를 받아와 PC로 연결하여 인터넷이 접속하는 방식을 시도해보기로 했다.
- 일단 이러한 연결 방식을 무선 WAN이라고 하고, 무선공유기의 신호를 받아 유선으로 연결하는 방식이다.
- 가장 먼저 PC에 공유기를 연결하고서 `iptime`의 관리자 ip 주소인 `192.168.0.1`로 접속한다.
- 설정을 들어갔을 때 비밀번호를 입력해야 하면, 비밀번호는 `admin`(ID와 동일)이다.
- 여기서 `고급설정 -> 무선랜 관리 -> 무선 확장설정`으로 들어가서 무선확장 방식을 `무선 WAN`으로 설정하고 `AP 검색`을 눌러서 무선 네트워크를 검색한다.
- 연결할 무선 네트워크를 클릭하고 암호를 입력한 후 적용을 누르면 설정이 완료된다.
- 여기까지는 사실 일반 데스크탑으로도 쉽게 설정할 수 있는 것이기 때문에 어렵지 않다.
- 그러나 기기를 차량용 PC에 이더넷으로 연결하고서 위의 과정을 진행했는데도 인터넷이 접속되지 않았다.
- 몇시간 동안 고생 끝에 찾은 결과는 인터넷을 연결하는 포트의 IP 주소를 잡을 때 네트워크 설정에서 `Manual`이 아닌 `Automatic`으로 설정해주어야 한다는 것이다.
- 차량용 PC를 처음 설정할 때 아마 고정 IP를 사용하기 위해 `Manual`로 설정되어 있었던 것 같은데, 이렇게 하니까 필요한 정보를 다 입력되지 않았는지 인터넷 연결이 안되서 이걸 `Automatic`으로 연결하니까 인터넷이 접속되었다.
- 인터넷 연결이 되었으니, 다음 작업은 ROS를 사용해서 차량의 CAN 데이터를 불러오는 것이다.
- 아래의 명령어들은 네트워크 연결 작업을 하면서 알게된 명령어들이다.

`ifconfig`
  - "interface configuration"의 약자로 리눅스 네트워크 관리를 위한 인터페이스 구성 유틸리티이다.
  - 현재 네트워크 구성 정보를 표시해준다.
  - 네트워크 인터페이스에 IP 주소, 넷 마스크 또는 broadcast 주소를 설정하고, 인터페이스의 별칭을 만들거나 하드웨어 주소 설정, 인터페이스 활성화 및 비활성화 등을 할 수 있다고 한다.  
  
`ifconfig -a`  
  - `-a` 옵션을 주면 비활성화된 네트워크 인터페이스도 모두 볼 수 있다.  

`ifconfig [interface name] down`  
  - [interface name]에 해당하는 인터페이스를 비활성화한다.
  - 연결을 해제하는 것으로 생각하면 될 것 같다.

`ifconfig [interface name] up`  
  - [interface name]에 해당하는 인터페이스를 활성화한다.

`sudo ethtool -p [interface(port) name]`  
  - PC에 이더넷 포트가 여러 개 있을 때 어느 것이 어느 이름을 가지고 있는지 알 수 없을 때 사용하면 좋은 방법이다.
  - 인터페이스 이름을 입력하여 명령어를 실행하면 해당 이너넷 포트의 LED가 깜빡깜빡 거린다.

# 2021/04/05
### cantools를 사용한 CAN 디코딩
- `cantools`는 파이썬에서 CAN 데이터 인코딩 및 디코딩을 할 수 있는 패키지이다.
- 차량용 컴퓨터에 kvaser CANusb 드라이버를 설치한 후, cantools 패키지를 사용하여 차량의 CAN 데이터를 분석보려고 한다.
- cantools 패키지 설치
  ```
  $ python3 -m pip install cantools
  ```
- 현재(2021.04.05일자) 아래의 명령어를 통해 CAN raw data가 출력되는 것을 확인하였다.
  ```
  $ sudo modprobe can
  $ sudo modprobe kvaser_usb
  $ sudo ip link set can0 type can bitrate 500000
  $ sudo ifconfig can0 up
  $ candump can0
  ```
- 추후 작업:
  - 현재 차량용 컴퓨터에 우분투를 포맷 후 재설치하여 matplotlib 등과 같은 아주 기본적인 파이썬 패키지도 설치가 되어있지 않아 CAN 메세지를 디코딩해보지 못하였다.
  - 기본적인 환경 구축이 되면 아래의 명령어를 통해 CAN 메세지를 디코딩해볼 예정이다.
  ```
  $ candump can0 | cantools decode [CAN.dbc directory]
  ```
  [cantools github repository](https://github.com/eerimoq/cantools)  
  [reference(dgist-artiv)](https://dgist-artiv.github.io/hwcomms/2020/08/31/socketcan-connect.html)

# 2021/04/06
### cantools로 CAN 디코딩 확인
- 차량용 컴퓨터의 기본적인 환경 구성을 완료한 후, 터미널 상에서 cantools를 사용하여 .dbc 파일을 입력하였더니 CAN raw data로부터 디코딩을 하여 우리가 확인할 수 있는 값들을 출력해주었다.
- 아래의 명령어는 오늘 테스트를 하면서 사용하였던 명령어이다.
  ```
  $ candump can0 | cantools decode [CAN.dbc directory] ## 디코딩된 CAN 데이터가 출력된다.
  $ cantools dump [CAN.dbc directory] ## .dbc 파일을 알아보기 쉽게 요약해준다.
  $ candump can0 | cantools decode [CAN.dbc directory] | grep -P '...CAN signal names' > result.txt ## grep 명령어로 필요한 값만 가져와 텍스트 파일로 입력하였다.
  ```
- 추후 작업:
  - 파이썬에서 cantools 패키지를 사용하여 CAN 데이터를 디코딩해보려 했는데, 여전히 파이썬에서는 에러가 발생한다.
  - 파이썬 패키지가 어떻게 구성되어 있는지 살펴보고 에러를 해결해서 파이썬 상에서 CAN 데이터를 파싱할 수 있도록 코드를 작성해보려 한다.