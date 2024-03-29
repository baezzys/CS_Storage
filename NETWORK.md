# NETWORK

### 브라우저에 naver.com 를 입력하면 일어나는 일
<details>
   <summary> 자세히 보기 </summary>
 
 <br>

PC쪽에서 브라우저에 naver.com 를 입력하면

운영체제 수준에 따라 다른데 윈도우 기준으로는 도메인 이름을 기준으로 통신을 하려면 IP주소를 알아야한다.

그래서 1차적으로 DNS에 질의를 해야한다.

DNS를 hirachy한 구조를 가지고 있다. 분산형 DB구조이다.

하지만 DNS에 먼저 물어보기전에 컴퓨터마다 호스트파일이라는걸 가지고 있다.

그다음은 DNS Cache에 질의를 해서 캐시에 있을 경우 DNS에 질의하지 않는다.

DNS cache에도 없다면 DNS질의를 시작한다.

네트워크 설정에 따라서 DNS에 질의한다.

공유기가 DNS 포워딩 기능이 있어서 공유기가 DNS에 물어봐서 답을 컴퓨터에 전달해주는 구조도 있다.

또는 DNS에 직접 질의를 할 수도 있다.

그럼 IP주소를 획득하게 된다.

그다음 TCP연결을 한다. http 통신을 위해서

TCP연결이 성공한다면 이제 그다음 http request가 나간다.

하지만 조금 규모가 있는 회사는 무조건 GSLB를 타게 돼있다.

GSLB를 구현하는 방법이 여러가지가 있는데 그중에서 CDN서비스가 있다.

CDN은 PC에서 접속할떄 접속자의 IP를 판단하여 접속자의 위치를 판단한다.

그리고 사용자의 위치를 기반으로 어떤 서버로 접근할떄 가장 빠른지 판단한다. 이때 health check도 진행한다. 그리고 살아 있는 서버이면서 사용자에게 가장 가까운 서버에게 연결시켜주는 것이다.

그렇기 때문에 IP는 달라질 수 있다 왜냐? 내가 접속을 시도할때 가장 원활한 서버쪽으로 접근하기 때문이다.

    
</details>


### TCP통신에서 일어나는 일
<details>
   <summary> 자세히 보기 </summary>
 
 <br>

TCP통신에서는 먼저 3 - way handshake가 일어난다.

그다음 서버 입장에서 살펴보면 서버가 소켓이라는 파일을 열어서 Write또는 Receive를 하게된다.

소켓은 서버와 클라이언트가 양방향 통신을 하기 위해서 사용되는 파일이다.

socket은 TCP/IP 를 추상화 한 것이다.

socket과 TCP/IP 사이에서는 분해라는 것이 일어난다.

TCP에는 버퍼가 존재하는데 서버가 가지고 있는 메모리에 (버퍼) 담겨 있기 떄문에 버퍼에서 버퍼로 데이터를 보내는 과정을 Buffered I/O라고 한다.

TCP에서 IP쪽으로 데이터가 내려갈때 버퍼 데이터를 잘개 쪼갠다. 그것을 우리는 세그먼트라고 부른다. (이것이 분해)

분해가 일어날때 우리는 각각의 세그먼트에게 번호를 붙인다.

그래서 누군가 패킷이란 무엇이냐라고 물어본다면 이를 택배박스와 굉장히 유사하다고 말할 수 있다.

패킷에는 세그먼트가 담겨있고 이는 NIC로 내려가면서 L2레이어에서 프레임 형태에 담기게 된다.

패킷은 기본적으로 end to end로 가게되는 반면 프레임 형태 네트워크를 거치면서 자주 교체되게 된다.

  
   ![image](https://user-images.githubusercontent.com/55564829/192148300-bbe203ab-9f69-4af9-ba32-1563c8970591.png)
  
서버에서 처음 프레임을 받는 네트워크 장치에서는 프레임을 제거하고 상위 레이어로 올린다.

그다음 IP 계층에서 패킷을 제거하고 세그먼트 형태로 TCP에 올리고 TCP 버퍼에 해당 세그먼트 데이터가 적재된다.

이때 세그먼트를 잘 받았다는 걸 서버에게 알려주는 것이 ACK이다.


</details>


### Subnetting
<details>
   <summary> 자세히 보기 </summary>
 
 <br>
   서브넷팅은 하나의 물리적 네트워크를 더 작은 논리적인 그룹 여러개로 쪼개는 행위이다. IP주소는 네트워크 세그먼트와 호스트 세그먼트를 포함하고 있다. 서브넷은 호스트 부분의 아이피 어드레스 비트들을 활용하여 더 작은 서브 네트워크를 형성한다.
   
   네트워크 IP 내에서는 서로 다른 호스트 IP들은 라우터와 같은 통신 장비 없이 통신할 수 있다. 다만 서브넷 네트워크는 서로 다른 서브넷 네트워크랑 통신하기 위해 라우터와 같은 통신 장비가 필요하다.
   
   서브넷팅은 네트워크 트래픽을 줄이는 도움을 줄 수 있고 네트워크 복잡성을 줄이는데 도움을 준다. 서브넷팅은 여러개의 LAN 세그먼트들에게 IP를 할당하는데 필수적이다.
   
   서브넷은 서브넷마스크라는 비트를 사용해서 구분할 수 있습니다. 서브넷 마스크는 IP 대역중 어떤 비트까지 서브넷팅을 할지 결정해줍니다.
   
   IP주소와 서브넷 마스크를 AND연산 했을때의 결과를 사용해서 서브넷 네트워크를 구할 수 있습니다. 

</details>

### Cookie 와 Session의 차이
<details>
   <summary> 자세히 보기 </summary>
 
 <br>

   
   ##### cookie

쿠키는 유저 컴퓨터에 저장되는 작은 텍스트 파일이다. 쿠키의 맥시멈 사이즈는 4KB이다. 유저가 웹사이트를 방문했을때 웹사이트측에서 유저에게 보내는 데이터이다. 쿠키는 오직 발행된 도메인에서만 읽을 수 있다. 보통 광고 업계에서는 유저를 타겟팅하기 위해서 쿠키싱크를 통해서 타 도메인에서 발행된 도메인을 읽을 수 있게 하는 기술이 존재한다. 쿠키의 지속시간은 서버에서 정할 수 있으며 쿠키의 성격에 따라서 sesison이 만료됨에 따라서 (브라우저 종료) 사라지는 쿠키와 일정 기간동안 계속 저장돼있는 쿠키가 있다. 

##### session

세션은 서버에 저장된다. 저장되는 위치는 크게 네가지로 나눌 수 있다. in-memory방식 (브라우저 종료시 삭제, 대신 빠름), file-based (영구적이지만 느림), databased-based(조금 느리지만 scalable하다.), distributed-cache(redis나 memcache -> 빠르게 접근 가능하며 scalable하다.) 세션은 유니크 id를 할당받고 저장된 값을 읽어오는데 사용된다. 세션이 생성될때 세션의 유니크 아이디는 쿠키에 저장되어 모든 서버 요청에 세션의 유니크 id를 가지고 가게 된다. 만약 클라이언트의 브라우저가 쿠키를 지원하지 않는다면 유니크 세션 id는 URL에 나타나게 된다. 세션은 쿠키에 비해서 더 많은 양의 데이터를 저장할 수 있다.

##### session의 활용

세션 로그인 방식은 다음과 같다. 우리가 로그인을 하면 서버는 세션을 생성하고 쿠키에 세션ID를 태워서 보내준다. 그래야 클라이언트에서 어떠한 action이 발생했을때 서버는 그 액션이 누구의 것인지 확인할 수 있다. 이렇게 해야 하는 이유는 http가 stateless이기 떄문에 모든 요청에 내가 누구임을 확인시켜줄 요소가 필요한 것이다. 세션은 보통 타임 리밋이 있다. 그리고 세션은 보통 서버의 메모리나 파일시스템에 저장된다. 

##### session의 한계

요즘은 서버들이 보통 여러대가 존재하고 로드벨런서가 앞단에 존재한다. 그러면 이런 경우 세션은 어떻게 관리되어야 하는가? 이럴 경우 세션은 서버에 종속되어 있으므로 로드벨런서는 요청이 처음 갔던 서버에게 계속 보내줘야하는 부담이 생긴다. 이는 로드밸런서에 부하를 주게 된다. 또 다른 방법으로는 central한 디비를 하나 생성하여 세션 정보를 해당 디비에서 관리하는 것이다. 이런 경우에는 로드밸런서는 요청을 아무 서버에나 보내도 되기 때문에 로드밸런서에서 받는 부하를 줄일 수 있다. 대신 매 요청마다 DB I/O가 생길 수 있다는 단점이 있다. 또 다른 방법으로는 클러스터링된 서버들이 모두 같은 세션을 공유하게 하는 것이다. NFS와 같은 공용스토리지를 사용한다면 해당방법을 실현할 수 있다. 사실 세션의 한계는 분명히 존재하는 것처럼 보인다. session id 와 매칭되는 정보를 서버에서 저장해야된다라는 session과 서버의 종속성이 생기기 때문이다. 이를 해결하기 위해선 그냥 클라이언트에서 인증 관련 데이터를 같이 보내오면 될 것이다.


</details>

### Socket이란?
<details>
   <summary> 자세히 보기 </summary>
 
 <br>
우리가 개발하는 네트워크 애플리케이션은 end point에서 실행되는 프로세스이다. 종단간 통신방법은 각각의 client와 server가 소켓을 통해 메시지를 주고 받는다.

소켓은 어떠한 하드웨어 디바이스가 아니다 소켓은 OS단에서 제공 되는 추상화된 인터페이스이다. 소켓 자체가 커널의 일부분이라고 얘기할 수는 없다. 다만 커널이 제공하는 추상화이다. 소켓이 생성되면 그것은 특정한 포트와 ip어드레스에 bound 된다. 이것은 해당 ip어드레스와 포트로부터 오는 데이터를 받아들일 수 있다는 의미이다. 소켓은 TCP또는 UDP를 사용할지 결정될 수 있다. 보통 소켓이 생성된다는 의미는 소켓에 필요한 리소스를 할당받고 OS가 소켓 오브젝트는 초기화되어 kernel memory안에 저장되는 것을 의미한다.

우리가 애플리케이션에서 커널의 기능을 사용하려면 시스템 콜을 사용해서 커널에서 실행되는 함수로 변화시키듯이 소켓 I/O도 마찬가지이다. 소켓 I/O를 통해 시스템 콜을 생성해 내면 커널은 네트워크 디바이스와 커뮤니케이션을 통해 이를 처리하고 데이터를 전달한다. 


   

</details>

