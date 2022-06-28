# Spring

### Spring AOP란 무엇인가?
<details>
   <summary> 자세히 보기 </summary>
 
 <br>
   
![spring-aop-diagram](https://user-images.githubusercontent.com/55564829/176193666-7dfdc8ea-a3a0-41d3-9827-f62a762ca763.jpg)

Spring에서 Aspect Oriented Programming을 가능케 해주는 기능이다. 
Spring AOP를 위해서는 필수적으로 알아야할 개념이 3가지 정도가 존재한다.

Joint point: 에러 핸들링 또는 함수의 실행을 시작할 포인트를 얘기한다. Spring AOP에서는 언제나 함수의 실행이 joint point가 된다. 

Pointcut: 조인포인트와 매칭되는 표현식을 얘기한다. pointcut은 한개 이상의 jointpoint를 담고 있을 수 있다. 
한마디로 어떤 조인포인트에서 함수를 실행시킬지 범위를 뜻한다.

Advice: 포인트 컷에 매칭되는 조인포인트에서 실행되는 것을 얘기한다.

이러한 AOP는 트랜잭션과 같이 자주 중복되는 관심사를 모듈로 빼내어 효과적으로 관리할 수 있을 뿐만 아니라 보일러 플레이트 코드를 줄일 수 있다는 장점이 있다. 

또한 기존의 코드 로직은 변경시키지 않은채 새로운 작업을 추가시킬 수 있어서 기능 확장에 유리하다.

</details>


### filter VS Handler interceptor?
<details>
   <summary> 자세히 보기 </summary>
 
 <br>

두 가지 모두 요청이 Controller로 오기전에 요청으로 가로채서 특정한 작업을 수행한다는 점에서 동일하다. 하지만 두개는 요청을 가로채는 시점이 다르다. filter는 spring mvc와 무관하게 적용될 수 잇다.
   
   ![filters_vs_interceptors-768x287](https://user-images.githubusercontent.com/55564829/176193620-e32cf887-f398-4183-b989-dbaf4927ea95.jpg)

filter는 제일 앞단에서 들어오는 요청과 나가는 응답에 대해서 제어를 하며 handler interceptor는 Dispatcher servlet과 Controller사이에 위치하여 그 사이의 요청들을 제어한다.
   
filter는 모든 요청에 대해서 제일 앞단에서 요청을 관리한다는 점에서 조금 더 범용적인 용도로 사용될 수 있다.  
   
   * 인증
   * 로깅
   * 데이터 압축
에 주로 사용된다.

   반면 Handler interceptor는 spring mvc 안에서 동작하므로 조금 더 application specific한 동작들을 처리하는데 특화되어 있다.
   
   * 애플리케이션 로그
   * 디테일한 유저 권한 체크
   
Filter역시 Spring boot내에서는 bean으로 등록되어 있기 때문에 커스텀이 가능하다.

   Spring security역시 Filter가 추가되어서 앞단에서 유저에 대한 인증을 진행하고 있다.
   
   Spring security는 DelegatingFilterProxy라는 것에 많이 의존하고 있는데 이것은 spring framework에서 제공하는 웹 모듈로  javax.Servlet.Filter interface를 구현한 모든 클래스를 filter chain에 등록하여 스프링이 관리할 수 있는 filter로 바꿔주는 역할을 한다.

</details>