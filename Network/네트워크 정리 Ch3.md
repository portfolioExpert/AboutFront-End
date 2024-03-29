# 네트워크 정리 Ch3



###### 들어가기 전

- 교환: 전달 경로가 둘 이상일 때 라우터에서 데이터를 어느 방향으로 전달할지를 선택하는 기능으로 다양한 기준에 따라 데이터를 올바른 경로로 전달할 수 있도록 해준다.
- 전송: 특정한 물리 매체에 의하여 일대일로 직접 연결된 두 시스템 간의 신뢰성 있는 데이터 전송을 보장하기 위한 것이다.(라우팅 기능은 포함 안된다.)



---



## 1. 교환 시스템

###### 참고

https://ddingz.tistory.com/146?category=964460


<img width="516" alt="스크린샷 2022-10-23 오후 5 39 39" src="https://user-images.githubusercontent.com/52316270/200431958-8331824b-cb1a-4295-b91e-d0bf2632fb25.png">


#### 1.1 회선 교환

- 통신하고자 하는 호스트가 데이터를 전송하기 전에 연결 경로를 미리 설정하는 방식.
- 연결 설정 과정에서 송수신 호스트 간의 경로가 결정되기 때문에 모든 데이터가 같은 경로로 전달된다.
- 고정 대역의 논리적인 전송 선로를 전용으로 할당받으므로, 안정적인 데이터 전송률을 지원한다.



#### 1.2 메시지 교환

- 데이터를 전송하기 전에 경로를 미리 설정하지 않고, 대신 전송하는 메시지의 헤더마다 목적지를 표시하는 방식.
- 중간의 교환 시스템은 이전 교환 시스템에서 보낸 전체 메시지가 도착할 때까지 받은 메시지를 일시적으로 버퍼에 저장한다.
- 이후 모든 메시지가 도착하면 다음 교환 시스템으로 전달하는 방식을 사용하므로 데이터 전송이 교환기 단위로 이어진다.
- 따라서 메시지 교환 방식은 송신 호스트가 전송하는 전체 데이터가 하나의 단위로 교환 처리된다고 볼 수 있다.
- 메시지 교환의 장점은 교환 시스템에서 전송 데이터를 저장하는 기능을 제공하기 때문에 송신 호스트가 보낸 시점과 수신 호스트가 받은 시점이 반드시 일치할 필요가 없다는 것



#### 1.3 패킷 교환

- 회선 교환과 메시지 교환의 장점을 모두 이용한다.
- 송신 호스트는 전송할 데이터 패킷이라는 일정 크기로 나누어 전송하며, 각 패킷은 독립적으로 라우팅 과정을 거쳐 목적지에 도착한다.
- 패킷 교환 시스템의 장점은 전송 대역의 효율적 이용, 호스트의 무제한 수용, 패킷에 우선순위 부여 라는 장점이 있다.

> 장점
>
> 전송 대역의 효율적 이용: 여러 호스트에서 전송한 패킷들이 동적인 방식으로 전송 대역을 공유하기 때문에 전송 선로의 이용 효율을 극대화할 수 있다.
>
> 호스트의 무제한 수용: 임의의 연결 요청에 고정 대역을 할당하지 않으므로 이론상 호스트를 무한히 수용할 수 있다. 전송 대역을 사용하는 호스트의 수가 늘면 네트워크 혼잡도가 높아져 패킷의 전송 지연이 심화될 뿐이다.
>
> 패킷에 우선순위 부여: 특정 호스트가 전송하는 패킷들을 먼저 전송할 패킷과 나중에 전송해도 되는 패킷으로 구분하여 선택적으로 우선순위를 부여할 수 있다.

###### 가상회선 방식

<img width="522" alt="스크린샷 2022-10-23 오후 6 00 57" src="https://user-images.githubusercontent.com/52316270/200432003-71776529-a0b4-4273-97ca-b32d68ad6e78.png">

- 연결형 서비스를 지원하기 위한 기능으로 연결을 통해 전송되는 모든 패킷의 경로가 동일하다.
- 송수신 호스트 사이트에 설정된 가상의 단일  파이프를 통해 송신 호스트가 입력단으로 패킷을 송신하고, 수신 호스트가 출력단에서 패킷을 수신
- 모든 패킷이 하나의 파이프로 표현되는 동일 경로로 전송되므로 패킷이 도착하는 순서가 보낸순서가 같다.(순서 보장)
- 여기서 파이프는 한 프로세스의 출력을 다른 프로세스의 입력으로 사용할 수 있도록 프로세스를 연결하는 논리적 통신 매체.
- 회선 교환 방식과 비슷하나 가상 회선 방식은 패킷 교환 방식을 기반으로 한다.



###### 데이터그램

<img width="547" alt="스크린샷 2022-10-23 오후 6 01 19" src="https://user-images.githubusercontent.com/52316270/200432028-7c09884f-860e-43bf-b2ff-f25e9d91c8d5.png">

- 패킷 교환 방식에서 비연결형 서비스를 이용해 패킷을 독립적으로 전송하는 것
- 패킷을 송신하기 전에 연결을 설정하는 과정이 없으므로, 미리 경로를 할당하지 않는다.
- 패킷들이 독립적인 경로로 전달된다.
- 데이터그램 방식은 전송할 정보의 양이 적거나 상대적으로 신뢰성이 중요하지 않은 환경에서 사용된다.



---



## 2. 데이터 전송 방식

참고

https://ddingz.tistory.com/150?category=964460

#### 2.1 점대점 방식

- 네트워크에서는 교환 호스트가 송수신 호스트의 중간에 위치한다.
- 종류로는 스타형, 링형, 완전형, 불규칙형이 있다.



###### 스타형

<img width="139" alt="스크린샷 2022-10-26 오전 10 22 45" src="https://user-images.githubusercontent.com/52316270/200432061-caf7986a-cb93-483a-9892-0764548d4cf2.png">

- 중앙에 있는 하나의 중개 호스트 주위로 여러 호스트를 일대일로 연결하는 형태
- 주변 호스트가 데이터를 송수신하려면 반드시 중앙의 중개 호스트를 거쳐야 한다.
- 중앙 호스트의 신뢰성과 성능이 전체 네트워크의 성능과 신뢰성에 영향을 많이 준다.
- 데이터를 적절한 목적지로 전송하는 중개 기능도 중앙 호스트가 독점적으로 담당한다.
- 단점으로 중앙 호스트에 문제가 발생하면 전체 네트워크의 동작에 영향을 많이 준다는 단점이 있다.



###### 링형

<img width="153" alt="스크린샷 2022-10-26 오전 10 22 58" src="https://user-images.githubusercontent.com/52316270/200432095-721c993c-6dd6-464a-b1b4-ce9fca4fcfe6.png">

- 호스트의 연결이 순환 고리 구조이며, 전송 데이터가 브로드캐스팅되는 특징이 있다.
- 호스트가 일대일로 직접 연결되기 때문에 점대점 방식에도 포함된다.
- 링형의 단점은 한 호스트가 고장나면 전체 네트워크가 동작하지 않을 수 있다는 것
- 따라서 정전이나 다른 원인에 의해 오동작하는 호스트는 네트워크에서 논리적으로 분리하여 고립시킬 수 있어야 한다.



###### 완전형

<img width="149" alt="스크린샷 2022-10-26 오후 2 19 46" src="https://user-images.githubusercontent.com/52316270/200432141-1d0aaa78-bcad-461e-8ac0-db3896c30fc8.png">

- 네트워크에 존재하는 모든 호스트가 다른 모든 호스트와 일대일로 직접 연결하는 방식
- 호스트끼리 서로 공유하지 않는 전용 전송 매체로 직접 연결하기 때문에 교환기능이 필요없다.
- 단점은 사용하는 전송 매체의 개수가 증가하면 비용 측면에서 극단적으로 비효율적이다.



#### 2.2 브로드 캐스팅 방식

- 특정 호스트가 전송한 데이터가 네트워크에 연결된 모든 호스트에 전달된다는 특징
- 네트워크의 모든 호스트가 하나의 전송 매체를 공유하므로 임의의 송신 호스트에서 보낸 데이터가 네트워크의 모든 호스트에 전달된다.



###### 버스형

<img width="235" alt="스크린샷 2022-10-26 오후 4 12 26" src="https://user-images.githubusercontent.com/52316270/200432170-01d91eef-c226-4b01-ac0e-749475bbf2e4.png">

- 다수의 호스트가 하나의 전송 매체를 공유하므로 전송 데이터를 모든 호스트에서 수신할 수 있다.
- 그러나 둘 이상의 호스트에서 데이터를 동시에 전송하면 데이터 충돌이 발생할 수 있으므로 충돌에 따른 오류 문제를 해결해야 한다.

> 충돌 문제 해결
>
> - 호스트의 전송 권한을 제한함으로써 사전에 충돌을 예방할 수 있다. 이 방식에서 호스트가 데이터를 전송하려면 사전에 전송 권한을 확보 해야 한다. 전송 권한을 확보하기 위해서는 전송 시간대를 분할하여 각 호스트별로 데이터를 전송할 수 있는 시간대를 다르게 지정하는 방법과 토큰으로 전송 권한을 순환적으로 이용하는 방법이 있다.



###### 링 형

<img width="153" alt="스크린샷 2022-10-26 오전 10 22 58" src="https://user-images.githubusercontent.com/52316270/200432207-fb425ec7-2ce8-472f-812e-589fd66c0c55.png">

- 전송 데이터가 링 주위를 특정 방향으로 순환하면서 전달된다.

---



## 3. 오류 제어

참고

https://ddingz.tistory.com/151?category=964460

