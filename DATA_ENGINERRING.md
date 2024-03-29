# 데이터 엔지니어링



</details>

### Hadoop의 동작
<details>
   <summary> 자세히 보기 </summary>
 
 <br>


![lRpoU](https://user-images.githubusercontent.com/55564829/191906711-ac0f4302-f58a-484f-948d-59619453e691.jpeg)


사용자는 본인의 비즈니스 로직은 Mapper, Reducer클래스에 맞춰서 작성한다.
  
사용자의 코드는 분산환경의 slave node에서 실행된다.
  
InputFormat은 inputSplit() 함수를 통해서 input file을 small piece들로 쪼갠다.
  
그다음 RecordReader가 raw data를 key-value 형태의 데이터로 변환시킨다.
  
Mapper가 이 key-value형태의 데이터를 가공한 뒤에 OutputCollector에게 보낸다.
  
Reporter() 함수가 유저에게 mapping task가 끝났음을 알린다.
  
Reduce() 함수는 매퍼로 부터 온 key-value데이터를 최종 데이터 형태로 만든다.
  
OutputFormat은 최종 데이터를 HDFS에 기록한다.


### Shuffling은 왜 필요한 것인가? 

→ 매퍼로 부터 나온 데이터를 같은 키 별로 묶어서 리듀서에게 전달해주기 위해 필요한 과정이다.

  ### sort는 왜 필요한 것인가?

→ 키를 기준으로 정렬하여 리듀서에게 이전의 키들과 구분이 가능하게 하여 새로운 리듀서의 생성을 용이하게 해준다. 

우리는 Mapper에서만 실행되는 (Reducer 없이) Job을 생성할 수 있다. 
job.setNumreduceTasks(0) 이 설정을 넣어준다면 Reducer가 없이 Mapper에서 나온 output이 최종 output이 되는 job을 생성할 수 있다.

이 것의 장점은 shuffle과 sorting이 자원을 많이 잡아먹는 Task이기 떄문에 reducer가 꼭 필요한 상황이 아니라면 해당 설정을 사용할 수 있다.



### Data locality
큰 볼륨의 데이터로 인해 발생하는 cross-swtich network traffic을 해결하기 위해 나온 것이다.

큰 볼륨의 데이터를 계산하는 곳으로 옮기는 것이 아닌 계산을 데이터 근처에서 하는 것을 의미한다.

하둡에서 dataset은 datanode에 저장되어 있다. 유저가 MapReduce job을 실행시키면 이 job은 관련 있는 데이터 노드로 가서 실행된다.


</details>


</details>

### KAFKA
<details>
   <summary> 자세히 보기 </summary>
 
 <br>
   
![kafka](https://user-images.githubusercontent.com/55564829/191907333-ec19d61c-5611-4e70-ad33-58b1a58bbfeb.png)

Publish-Subscribe구조의 message system이다.

Message broker Opensource이다.





## Message broker란?
서로 다른 이기종 시스템간에 메시지를 주고받을 수 있게 해주는 소프트웨어입니다.



## Message broker의 작동 방식
Producer: Message Broker에서 메시지 Sender에 해당하는 시스템입니다. Publish/Subscribe 구조에서는 Publisher로 불립니다.
Consumer: Message Broker에서 메시지 Receiver에 해당하는 시스템입니다. Publish/Subscribe 구조에서는 Subscriber로 불립니다.
Queue/topic: 파일시스템 안에 있는 폴더입니다. 메시지 브로커가 메시지들을 저장하는 데에 사용됩니다.


## Message broker는 왜 쓰는가?
기본적으로 이기종간 시스템이 통신하기 위해서는 가운데 인터페이스가 필요합니다. 서로 어떤 데이터 형태로 데이터를 주고 받을지 정의내려야 하며 그 것을 토대로 통신해야만 합니다.

이러한 작업에는 오버헤드가 발생하며 메시지 브로커는 이러한 인터페이스를 따로 정의할 필요 없이 메시지 브로커가 정의한대로 메시지를 주고 받으면 되기 때문에 편리하다는 이점을 제공합니다.

또한 Provider와 Consumer가 동시에 실행되고 있을 필요가 없습니다. 이는 굳이 컨슈머와 연결을 안해도 되며 컨슈머의 state를 체크하지 않아도 되는 이점이 있습니다.

마지막으로 메시지 브로커가 중간에 누락된 메시지는 재 전송하는 프로토콜을 가지고 있기 때문에 신뢰성이 높습니다.



## Message broker의 단점
새로운 element가 추가되야 하므로 기존 아키텍쳐 구성에서 변경되어야할 부분이 많이 있을 수 있습니다. 

또한 메시지가 제대로 전송되지 않았을때 해당 메시지가 어떤 부분에서 잘못됐는지 파악하기 위해서 반드시 모니터링이 필요합니다.



## Stream processing이란?
연속적인 데이터의 흐름 (배치의 반대 개념)



## kafka 장점
backward compatibility가 우수하고 많은 프로그래밍 언어를 지원함으로써 integration이 우수하다.

Stream processsing과 daya analytics에 유리하다.



## Topic
kafka에서 사용되는 개념으로 일종의 카테고리이다. 데이터를 categorizing하기 위해 사용된다.



## 카프카의 구성요소는 다음과 같다.

Broker: 클라이언트로 부터 들어온 모든 요청을 핸들링한다. 데이터를 복제하여 클러스터에 저장한다.
Zookeeper: 클러스터의 상태를 계속 추적한다.
Producer: records를 브로커에게 보낸다.
Consumer: 브로커로 부터 데이터 batch를 받아서 사용한다.

![kafka-broker-beginner](https://user-images.githubusercontent.com/55564829/191907391-94cd8bcf-408b-45f1-9a77-259534b08e99.png)



카프카는 한개 또는 여러개의 서버(브로커)로 구성되어있다. producers는 records를 브로커 안에 토픽에 보낸다. 그리고 컨슈머는 카프카 토픽으로 부터 records를 꺼내어 사용한다.

분산 처리 환경에서는 여러개의 분산 서버를 관리하는 하나의 master 노드가 필요하기 마련인데 이 역할을 하는 것이 Zookeeper이다. 이러한 주키퍼는 클러스터 안에 존재하며 한개 또는 여러개가 있을 수 있습니다.



토픽은 여러개의 파티션으로 분리됩니다. 파티션안에 있는 record는 유니크한 offset을 할당받습니다.

파티션은 토픽을 여러개의 데이터로 쪼개서 관리할 수 있게해줌으로써 병렬처리를 용이하게 합니다. 카프카는 replication을 파티션 레벨에서 진행합니다.

파티션은 여러개로 복제가 되어 있고 그중 한개가 리더 역할을 담담합니다. 만약 리더가 죽을시 나머지 팔로우 파티션들중 하나가 리더 파티션이됩니다.



컨슈머는 특정 오프셋으로부터 메시지를 읽을 수 있습니다.


</details>



### Hadoop block size
<details>
   <summary> 자세히 보기 </summary>
 
 <br>
  HDFS의 블록은 디스크 블록에 비해 상당히 크다. 그 이유는 탐색 비용을 최소화 하기 위함인데 블록이 매우 크면 블록의 시작점을 탐색하는데 걸리는 시간을 줄일 수 있기 때문이다. 탐색 시간을 줄이면 데이터를 전송하는데 더 많은 시간을 할애할 수 있다. 여러개의 블록으로 구성된 대용량 파일을 전송하는데에는 디스크 전송속도에 크게 영향을 받는다. HDFS에서 블록의 크기는 default가 128MB이나 대부분 이보다 큰 블록 사이즈를 사용한다.

</details>


### 네임노드와 데이터노드
<details>
   <summary> 자세히 보기 </summary>
 
 <br>
  HDFS 클러스터는 마스터 - 워커 패턴으로 동작하는 네임노드와 데이터노드로 이루어져있다. 네임노드는 파일시스템의 네임스페이스를 관리한다.
   
   네임노드는 파일시스템 트리와 그 트리에 포함된 모든 파일과 디렉터리에 대한 메타데이터를 유지한다. 이 정보는 네임스페이스 이미지와 에디트 로그라는 두 종류의 파일로 로컬 디스크에 영속적으로 저장된다.
   
   네임노드는 또한 파일에 속한 블록이 어떤 데이터노드에 있는지 다 파악하고 있다. 블록의 위치정보는 시스템 시작시에 데이터노드로 부터 받아서 구성한다.
   
   HDFS클라이언트는 사용자를 대신해서 네임노드와 데이터 노드 사이에서 통신하고 파일시스템에 접근한다.
   
   데이터노드는 블록을 저장하고 탐색하며 저장하고있는 블록의 목록을 네임노드에 주기적으로 보고한다.
   
   네임노드의 정보가 없으면 파일을 찾을 수 없기 때문에 하둡은 두가지 백업 메커니즘을 제공한다.
   
   첫째는 파일형태로 메타데이터를 백업해두는 것이고 두번째는 보조 네임노드를 운영하는 것이다.
   
   보조 네임노드는 에디트 로그의 사이즈가 너무 커지는 것을 방지하기 위해 네임스페이스와 에디트로그를 합친 새로운 네임스페이스 이미지를 만든다.
   
   네임스페이스는 파일 시스템과 비슷하다. 트리형태로 계층구조로 나타나는 파일시스템에 대한 메타데이터이며 모든 파일과 디렉토리에 대한 메타데이터를 트리구조로 가지고 있다.
   
   보조 네임노드는 주 네임노드의 네임스페이스 이미지도 가지고 있다. 만약 주 네임노드에 장애가 발생하면 NFS에 저장돼있는 네임스페이스 이미지를 부 네임노드로 옮겨서 새로 병합된 네임스페이스 이미지를 만들고 그것을 주 네임노드에 복사한 다음 실행시킨다.
   
  
</details>


### HDFS 페더레이션
<details>
   <summary> 자세히 보기 </summary>
 
 <br>
   네임노드는 모든 파일과 블록에 대한 참조정보를 메모리에서 관리한다. 메모리는 비싸고 용량이 작기 때문에 대형 클러스터에서 확장성에 제약이 생기게 된다.
   
   이를 해결하기 위해 나온 것이 HDFS 페더레이션이다. 쉽게 말해 네임노드 여러개를 두어 네임노드들이 네임스페이스의 일부분씩 나눠서 관리하는 것을 의미한다.
   
   예를 들면 어떤 네임노드는 /tmp 어떤 네임노드는 /var을 관리하는 것이다.
   
   네임노드들은 네임스페이스 볼륨은 나눠서 관리하지만 블록풀은 나눠져 있지 않다. 한마디로 모든 데이터 노드는 네임노드별로 전부 저장하고 있는 것이다.
  
</details>


### Hadoop Job Tracker
<details>
   <summary> 자세히 보기 </summary>
 
 <br>
    JobTracker는 하둡안에 있는 데몬 서비스이며 MR task를 특정한 노드로 뿌리는 역할을 한다.

이상적으로 해당 노드는 데이터를 가지고 있거나 최소한 같은 랙이여야 한다.

JobTracker는 다음과 같은 순서로 작동한다.

1. Client application은 잡을 Job Tracker에게 넘긴다.
2. Job Tracker는 네임노드에게 데이터의 위치를 결정하라고 한다.
3. Job Tracker는 선택된 Task Tracker node에게 일을 전달한다.
4. Trask Tracker는 모니터링되며 만약 hearbeat를 원활하게 보내지 않을 경우 해당 일은 다른 Trask Tracker에게 스케쥴된다.
5. TaskTracker는 task가 실패했을때 잡트래커에게 노티를 보내야 한다. 
6. 일이 끝나면 JobTracker는 상태를 업데이트 한다.
7. 클라이언트는 JobTracker로부터 정보를 가져올 수 있다.

JobTracker는 실패지점이 될 수 있다. 만약 JobTracker가 죽는다면 돌고 있는 잡들도 모두 중단된다.

   
  
</details>

### Hadoop Client란?
<details>
   <summary> 자세히 보기 </summary>
 
 <br>
   
   하둡 클라이언트는 하둡파일시스템과 통신할 수 있는 인터페이스를 나타낸다.
   
   하둡 클라이언트에는 다양한 종류가 있는데 hdfs dfs가 가장 기본적이다.
   hdfs dfs는 파일과 관련된 다양한 task를 실행할 수 있다.
   
   그것은 클라이언트 프로토콜을 사용하여 네임노드 데몬과 통신하여 datanode에 다이렉트로 연결되어서 파일을 읽고 쓸 수 있다. 
   
   하둡 클라이언트는 하둡이 설치돼있는 노드에서 관련된 CLI command를 통해서 호출될 수 있다. 단 해당 노드는 하둡 파일시스템에 연결되기 위한 라이브러리나 환경설정 파일들이 필요하다. 그러한 노드를 우리는 보통 하둡 클라이언트라고 부른다.
   
</details>
