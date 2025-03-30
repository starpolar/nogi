<details><summary>Protocol Specification to Insite</summary>  
  
  * Broadcast address 란? 네트워크에 연결된 모든 노드에게 전송하는 주소. 예로 특정 ID를 필터링 하지않고 모든 노드가 수신하게 설계한다면 이 ID는 브로드캐스트 주소다.(물리적인 브로드캐스트는 없다.)  
  
  
</details>  
  
* 개요  
  
* ECU(Eloctronic Control Unit)는? MCU를 포함하고 여러 제어 장치, 통신 등등을 추가해 포함한것.  
* CCU(Central Communication Unit)는? 여러 ECU간의 통신을 제어하는 중앙 장치.  
  
![IMAGE](https://raw.githubusercontent.com/nogi-bot/resources/main/starpolar/images/1359195f-5a60-4530-99cf-ffd58d836180-image.png)  
* CPU, CAN 컨트롤러, 트랜시버로 구성돼있고, 트위스트 페어로 시리얼 통신을 하되, 멀티 마스터로 버스에 물려있는 형태로 구성.  
* 자동차 산업에서는 안전, 편리, 공해, 운용의 경제성.  
  
![IMAGE](https://raw.githubusercontent.com/nogi-bot/resources/main/starpolar/images/b468b657-cc92-422b-9875-26294e07eb62-image.png)  
* 초기 차량의 네트워크망은 UART구조 였다. 사용자의 서비스 요구사항이 많아지면서 ECU가 많아지고 케이블이 늘어나며 공간이 좁아져 편리함 감소하고, 무게가 늘어 연비가 감소해 경제성이 낮아졌다. 그래서 그 당시에 통신은 RS485였고 하지만 안정성이 안좋아 직접 만들자고 한게 CAN 통신이였다.  
  
* CAN의 특징 및 장점  
  
* 차량엔 크게 3가지 네트워크로 나눠져 있고 파워트레인(엔진 부분), 차체 제어, 멀티미디어다. 각각은 게이트웨이로 이어져있고, 나뉜 이유는 효율성을 위해서다.  
  
![IMAGE](https://raw.githubusercontent.com/nogi-bot/resources/main/starpolar/images/350a43ab-f489-47ae-be19-c51131031a1e-image.png)  
* osi 레퍼런스 모델 7계층중에서 아래 1계층부터 비트를 데이터로 바꾸며 계층을 올라가면 헤더를 빼고, 내려가면 헤더를 더하며 데이터가 올라가고 내려간다. 이것을 캡슐레이션이라고 부름.  
* CAN의 계층 모델과 구현 모델  
  
* 표준 사양의 따른 컨트롤러와 트랜시버 연결.  
  
* 고속 CAN과 저속 CAN의 특징  
  
* 고속 CAN의 통신 방법  
  
  
* 저속 CAN의 통신 방법  
  
* CAN의 속도와 거리 관계  
---  
* CAN Frame의 확장형  
* Frame의 종류  
  
* Frame의 구조  
  
---  
* 동기화  
---  
**CAN의 에러처리**  
  
![IMAGE](https://raw.githubusercontent.com/nogi-bot/resources/main/starpolar/images/a394fe89-d07b-49ab-a569-7c55c040182b-image.png)  
* 비트 에러 감지  
* 스터핑 비트 검사  
* 메세지 형식 검사  
* CRC  
* ACK 검사  
  
**에러 검사 범위**  
![IMAGE](https://raw.githubusercontent.com/nogi-bot/resources/main/starpolar/images/28f485d3-6db4-4163-b058-13d879080b6c-image.png)  
* 각 에러 종류들의 검사 범위들.  
  
![IMAGE](https://raw.githubusercontent.com/nogi-bot/resources/main/starpolar/images/6381bc01-16ce-4f8f-9a67-7c30952f2c51-image.png)  
* 문제가 생겼을때 Error Counter을 1개씩 올리고, 심각한 문제가 생겼을때는 한 8개씩 많이 올린다. 그리고 정상적인 메세지 송수신이 완료되면 에러 카운터를 1개씩 줄여 나간다. 그래서  즉, 정상적인 상태의 기기는 적당한 선에서 에러카운터가 유지가 되고 있다.  
* Error Active: 이상하지 않는 일반적인 상태. Error Passive: TEC, REC가 >127 인 상태로 문제가 있는 상태. Bus OFF: 버스 정지. 다시 Active 상태로 동작하려면? 소프트웨어 리셋 or  11개의 연속적인 열성(1)비트열 128번 발생.(열성의 긴 비트를 송신할 때 중간에 아무도 통신을 사용하지 않아야만 이 상태를 유지할 수 있다.)= IDLE 상태. 하지만 이런 상태가 되지도 않을 뿐더러 그전에 교체를 해야된다함.  
  
![IMAGE](https://raw.githubusercontent.com/nogi-bot/resources/main/starpolar/images/02aaf3e3-8d66-4982-aa0d-f9405d4c94d4-image.png)  
* 능동 에러 프레임은 우성(0)으로 6비트가 이어지고, 수동 에러 프레임은 열성(1)으로 6비트가 이어진다. 즉, 에러 프레임만 봐도 장비의 상태를 알 수 있다.  
* 에러프레임은 데이터 프레임 도중에 발생해서 그 후로 쭉 에러프레임을 날린다.  
  
![IMAGE](https://raw.githubusercontent.com/nogi-bot/resources/main/starpolar/images/d0d71cae-6d1b-4174-ab17-3f64c3b7fd20-image.png)  
* 에러프레임 이후 IFS(inter frame space)라고 3비트를 날린 후 다시 데이터프레임 전송 재시도를 한다.  
* Bus Off는 아예 못쓰는 상태이기 때문에 제외하고 나머지 active, passive 두개만 다룬다.  
* Passive 에서는 Active와 다르게 IFS 후 재전송 시 8비트의 텀이 있다. 이는 오류가 많이나는 노드이니 패널티 식으로 더 쉬는것이고, 이 때문에 우선순위에 밀리며, 다른 정상적 노드들을 방해하지 마라라는 뜻의 기능이다. (suspend: 일시중단, transmission: 전송)  
  
* 이 에러 핸들링들은 즉, 정상적인 노드들이 통신하는데 방해가 되지 않도록 하는 전략임.  
  
---  
**CAN 통신의 미래**  
  
![IMAGE](https://raw.githubusercontent.com/nogi-bot/resources/main/starpolar/images/1eb6f09d-8806-4544-bf85-0151dc354512-image.png)  
* CAN FD의 차이점은? 기존의 데이터 프레임은 중재구간과 데이터 구간으로 나눴다. 그리고 데이터 구간을 8배 빠르게 전송 하면서 데이터량이 기존 8 Byte에서 64 Byte로 증가했다. 그래서 기존에는 클럭의 주기가 모두 같았지만, FD는 나뉜다.  
  
![IMAGE](https://raw.githubusercontent.com/nogi-bot/resources/main/starpolar/images/ad2c9a1d-a88b-4cfc-b476-ac3592b21275-image.png)  
* 기존 CAN과의 호환성. 어떻게? 데이터 필드만 빼고 나머지는 같게 할 수 있는듯.  
* FlexRay보다 더 대두되고 있는 FD.  
  
![IMAGE](https://raw.githubusercontent.com/nogi-bot/resources/main/starpolar/images/c5292ee1-29bd-43e0-9f27-8bf2aefb5aa3-image.png)  
* 각 상태를 표시해주는 비트들을 추가.  
  
![IMAGE](https://raw.githubusercontent.com/nogi-bot/resources/main/starpolar/images/1d6b96fb-f0f3-4971-aa88-86d553bd71cc-image.png)  
* 일반 CAN에서는 특허가 만료가 되서 특별한건 많이 없어졌고, XL같이 다른건 특허가 보쉬사에 유효하기에, 사용하려면 로얄티를 지불해야 할 것임.  
  
![IMAGE](https://raw.githubusercontent.com/nogi-bot/resources/main/starpolar/images/e9368ef0-3625-48df-96ff-e45487fe771d-image.png)  
* XL에는 Acceptance Field가 추가.(Acceptance: 수락)  
* FD에 CRC가 두가지 유형인데, 데이터 필드의 바이트 수의 따라서 어느정도 기준하에 작을때는 17, 클땐 21비트로 나뉨.  
  
![IMAGE](https://raw.githubusercontent.com/nogi-bot/resources/main/starpolar/images/4c21cff1-04b2-4e4f-93f0-503129a2147d-image.png)  
* 차량의 네트워크들  
* FlexRay는 큰 장점이 없었는지 컨소시엄도 없어져서 잘 사용안함.  
* MOST는 정보 오락용.  
  
![IMAGE](https://raw.githubusercontent.com/nogi-bot/resources/main/starpolar/images/524a484c-531b-4c99-9789-642864652448-image.png)  
* V2X의 X 뜻은: 모든것. Everything  
* V2V: 무인 자동차 같이 차량과 차량의 통신.  
* V2I: 교통 상황과의 통신.  
  
---  
**Insite 요약**  
  
CPU, 컨트롤러, 트랜시버로 구성.  
차동신호 방식.  
고속, 저속 CAN은 종단 저항 유무와 장애 대응 방식으로 분별.  
고속은 끝단 종단저항 있어야하며, 저속은 노드의 저항으로 충분.  
2.0A는 ID 11bit, 2.0B는 29bit로 프로토콜 프레임 형식이라 고속, 저속 두개의 모두 해당 가능함.  
원격 프레임으로 통신하면 응답 프레임은 ID가 같다.  
매 엣지마다 계속 동기화를 맞춤.  
에러카운터로 장비의 동작 여부가 결정됨.(때에 따라 올라갔다 내려감)  
다른 신세대 CAN이 있지만, 라이센스가 있다. 2.0B는 오래돼 특허권이 만료가 많이 됐다.  
  
기간도 길었고 시간도 꽤 많이썼다. 그런데  
요약은 적다. 그래도 실무에서 떠오르는 지식이 될 것임.  
이 다음에는 기간을 많이 줄이자. 부지런히 이해하고 마지막에 총 요약으로 소화하자.  
