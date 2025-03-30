* 개요  
  
* ECU(Eloctronic Control Unit)는? MCU를 포함하고 여러 제어 장치, 통신 등등을 추가해 포함한것.  
* CCU(Central Communication Unit)는? 여러 ECU간의 통신을 제어하는 중앙 장치.  
  
![IMAGE](https://raw.githubusercontent.com/nogi-bot/resources/main/starpolar/images/4993a7c8-9589-410d-906b-4a83ac548306-image.png)  
* CPU, CAN 컨트롤러, 트랜시버로 구성돼있고, 트위스트 페어로 시리얼 통신을 하되, 멀티 마스터로 버스에 물려있는 형태로 구성.  
* 자동차 산업에서는 안전, 편리, 공해, 운용의 경제성.  
  
![IMAGE](https://raw.githubusercontent.com/nogi-bot/resources/main/starpolar/images/68185842-3586-44e5-9c87-c0155cc7c6b2-image.png)  
* 초기 차량의 네트워크망은 UART구조 였다. 사용자의 서비스 요구사항이 많아지면서 ECU가 많아지고 케이블이 늘어나며 공간이 좁아져 편리함 감소하고, 무게가 늘어 연비가 감소해 경제성이 낮아졌다. 그래서 그 당시에 통신은 RS485였고 하지만 안정성이 안좋아 직접 만들자고 한게 CAN 통신이였다.  
  
* CAN의 특징 및 장점  
  
* 차량엔 크게 3가지 네트워크로 나눠져 있고 파워트레인(엔진 부분), 차체 제어, 멀티미디어다. 각각은 게이트웨이로 이어져있고, 나뉜 이유는 효율성을 위해서다.  
  
![IMAGE](https://raw.githubusercontent.com/nogi-bot/resources/main/starpolar/images/baac588b-61a9-47f1-abc7-f16b1d893a8e-image.png)  
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
  
