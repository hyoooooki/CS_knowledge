OS(운영체제) -operating system


##### [1.System Architecture(시스템 구조)](#System-Architecture)

##### [2.Process and Thread(프로세스와 쓰레드)](#Process-and-Thread)

##### [3.Scheduling(스케줄링)](#Scheduling)

##### [4. Synchronization(프로세스 동기화)](#Synchronization)

##### [5. Deadlocks(교착상태)](#Deadlocks)
##### [6. Memory management(메모리 관리)](#Memory-Management)


##### [7. File System(파일시스템)](#File-System)

##### [8. MassStorage Management(대용량저장소 관리)](#MassStorage-Management)
---



## System Architecture

### 1. Operating-System Services

*운영체제가 사용자를 위해 제공하는 기능들은 다음과 같다.*


- **사용자 인터페이스(User Interface)** :


  UI는 크게  CLI(Command-Line Interface), GUI(Graphical User Interface)로 나뉜다.

  CLI는 과거 MS-DOS, 리눅스 터미널처럼 직접 명령어를 입력해 실행하는 방식이고,

  GUI는 윈도우나 Mac OS X 처럼 마우스를 통해 화면을 클릭하여 실행하는 방식이다.


- **프로그램 실행(Program execution)**

  시스템은 프로그램을 메모리에 올려 실행시킬 수 있어야 한다. 이때 프로그램이 정상이던 비정상이던 실행을 끝낼 수 있어야 한다.

- **입출력 연산(I/O operation)**

  프로세스는 입/출력을 요구할 수 있다. 일반적인 사용자는 입/출력 장치를 제어할 수 없으므로 운영체제가 수행 수단을 제공해야 한다.

- **파일 시스템 조작(File system manipulation)**

  파일을 읽고, 쓸 수 있으며, 이름으로 생성, 검색, 삭제가 가능해야 한다.  또한 접근 권한도 조정이 가능하다.

- **통신(Communication)**

  여러 개의 프로세스가 메모리의 한 부분을 공유하도록 하는 <u>공유 메모리(Shared memory)</u>,

  패킷(packet)을 사용해 시스템 간 프로세스 사이를 이동하는 <u>메세지 전달(Message passing)</u>

  두 가지 방법을 사용한다.

- **오류 탐지(Error detection)**

  운영체제는 가능한 모든 오류를 항상 의식하고 있어야 하고, 그에 따른 적당한 조치를 취할 준비가 되어 있어야 한다.

- **자원할당(Resource allocation)**

  운영체제는 다수의 사용자, 작업들이 동시에 실행될 때 각각에 대해 효율적으로 자원을 할당 할 수 있어야 한다.

- **회계Accounting)**

  운영체제는 특정 사용자, 작업이 어떤 시스템의 자원을 얼마나 사용하는지 확인할 수 있어야 한다.

- **보호(Protection)와 보안(Security)**

  보호는 기본적으로 시스템 자원에 대한 모든 접근이 통제되도록 보장하는 것을 말한다.  

  운영체제는 다양한 위협요소에 대한 보안정책을 수립할 필요가 있다.



### 2. System Calls (시스템 콜)

*운영체제는 커널 모드(Kernel Mode) 와 사용자 모드(User Mode)로 나뉘어 구동되는데, 이때 커널 영역의 기능을 사용자가 사용 가능하게 해주는 역할을 한다.*

시스템 콜은 아래와 같이 6가지로 분류할 수 있다.

- **프로세스 제어 :** end, abort, load, execute
- **파일 관리 :** create, delete, open, close, read, write
- **장치 관리 :** read, write, request, release
- **정보 유지 :** time, date
- **통신 :** send/receive messages, transfer status
- **보호**



### 3. Operating System Structure

1.  ####  Simple Structure

   - MS-DOS 에서는 사실상 계층이 구분되어 있지 않아 Kernel에 직접 접근할 수 있었다. 즉, 사용자 프로그램에 문제가 생기면 전체 시스템에 문제가 생겼다.

     ex)

   - UNIX 에서는  MS-DOS와 비교하면 기능이 많이 분리 되었지만, 운영체제의 일반적인 기능을 커널과 동일한 메모리 공간에 적재, 실행하는 Monolithic kernel을 사용하여 유지보수가 쉽지 않았다.

     ex)


2.  #### Layered Approach (계층적 접근)

    운영체제의 복잡도를 낮추기 위한 방안이다. 이 방식은 유지보수가 편리한 장점이 있다.

    ex)



3. #### Microkernels (마이크로 커널)

   커널에서 핵심적인 요소만 남긴 가벼운 커널이고, 서버들 간 통신/에플리케이션의 서비스 콜 전달과 같은 기능을 한다.

4.  #### Modular kernel (모듈화 커널)

    커널을 확장하기 위한 기술로, 객체지향 프로그래밍 기법을 사용한다. 이 커널은 부팅 중 혹은 실행 중에 부가적인 서비스들을 링크한다.



5. #### Hybrid Systems(혼성 구조)

   커널의 핵심만 남기고 나머지는 따로 구현한 시스템이다. Mac OS X, 안드로이드가 혼성 구조를 사용한다.
___







## Process and Thread

#### 프로세스(Process)

​	연속적으로 실행중인 프로그램을 의미한다. 각 프로세스는 메모리에 적재 가능하며 CPU의 	할당을 받을 수 있다.



​	**프로세스가 포함하는 것**

  1. Code 영역 : 프로그램 코드 등
  2. Stack 영역 : 지역변수, 매개변수, 리턴 값 등 임시 데이터로 사용.
  3. data 영역 : 전역변수, 정적변수, 배열, 구조체 등
  4. heap 영역 : 동적변수 등
  5. PC(program counter) , register

<img src="/assets/memory.png">



​	**프로세스가 가지는 상태**

1. new : 프로세스 생성
2. running : 명령 실행
3. waiting : 특정 이벤트 발생했을 때 대기 상태에 들어감
4. ready : CPU를 할당 받기 위해 대기
5. terminate : 실행 종료

<img src="/assets/process state.png">



**PCB(Process Control Block)**

=> 특정한 프로세스를 관리할 필요가 있는 정보를 포함하는, 운영체제 커널의 자료구조

프로세스마다 하나씩 가지고 있음.

1. Process state : ready, running 등등
2. Process number : 프로세스 id
3. Program counter : 다음 실행할 명령어 주소
4. CPU registers
5. CPU scheduling information :  우선 순위, 최종 실행시각, CPU 점유시간 등
6. Memory-management information  : 해당 프로세스의 주소 공간 등
7. Accounting information  : 페이지 테이블, 스케줄링 큐 포인터, 소유자, 부모 등
8. I/O status information   : 프로세스에 할당된 입출력장치 목록, 열린 파일 목록 등



​	context switch가 발생할 때에 PCB를 저장하고 다른 프로세스의 PCB를 load하여 실행.



**프로세스 스케줄러**

1. job queue : 시스템의 모든 프로세스의 집합, secondary storage에 위치

2. ready queue : 실행 대기 상태에 있는 프로세스의 집합, 메모리에 위치

3. device queue : I/O device를 위한 프로세스 집합, 디바이스 컨트롤러에 위치


**장기스케줄러(Long-term scheduler or job scheduler)**

​	메모리는 한정되어 있는데 많은 프로세스들이 한꺼번에 메모리에 올라올 경우, 대용량 메모	리(일반적으로 디스크)에 임시로 저장된다. 이 pool 에 저장되어 있는 프로세스 중 어떤 프로	세스에 메모리를 할당하여 ready queue 로 보낼지 결정하는 역할을 한다.

* 메모리와 디스크 사이의 스케줄링을 담당.

* 프로세스에 memory(및 각종 리소스)를 할당(admit)

* degree of Multiprogramming 제어  
  메모리에 여러 프로그램이 올라가는 것) 몇 개의 프로그램이 올라갈 것인지를 제어

* 프로세스의 상태  
  new -> ready(in memory)


_cf) 메모리에 프로그램이 너무 많이 올라가도, 너무 적게 올라가도 성능이 좋지 않은 것이다. 참고로 time sharing system 에서는 장기 스케줄러가 없다. 그냥 곧바로 메모리에 올라가 ready 상태가 된다._



**단기스케줄러(Short-term scheduler or CPU scheduler)**

* CPU 와 메모리 사이의 스케줄링을 담당.
* Ready Queue 에 존재하는 프로세스 중 어떤 프로세스를 running 시킬지 결정.
* 프로세스에 CPU 를 할당(scheduler dispatch)
* 프로세스의 상태  
  ready -> running -> waiting -> ready



 **중기스케줄러(Medium-term scheduler or Swapper)**

- 여유 공간 마련을 위해 프로세스를 통째로 메모리에서 디스크로 쫓아냄 (swapping)
- 프로세스에게서 memory 를 deallocate
- degree of Multiprogramming 제어
- 현 시스템에서 메모리에 너무 많은 프로그램이 동시에 올라가는 것을 조절하는 스케줄러.
- 프로세스의 상태
  ready -> suspended



**Context Switch(문맥 교환)**

​	CPU를 사용하고 있는 프로세스를 교환하기 위한 작업

​	바뀌기 전에 PCB에 저장을 한 후 바뀌게 된다. 이 작업은 overhead가 큰 작업이다.



**Parent - child process**

=> 기본적으로 pid에 의해서 관리가 되며 부모자식간의 형태는 트리형태이다.



​	자원공유

* Parent and children **share all resources**

* Children **share subset of parent’s resources**
* Parent and child **share no resources**



​	실행

* 부모와 자식은 동시에 실행

* 부모는 자식이 종료될 때까지 대기



​	fork를 이용하여 자식을 생성하며 자식은 부모와 같은 context를 가진다.

​	(program counter, register, memory info 등등)



​	변수 pid 선언 fork();를 호출하면 커널모드가 된다. 프로세스는 fork가 리턴할 때 까지 기다린	다. 그리고 시스템콜은 커널에서 시행이 된다. 수행하고 나면 메모리에 새로운 PCB가 생기고 	부모의 PCB를 똑같이 복제하여 쓴다. 그리고 그 후에 둘 다 ready큐에 위치한다. 그리고 반환	이 된다. 이때 부모에게는 자식의 pid값을 자식에게는 0을 리턴 해준다. exec함수가 호출되는 	순간 이때 부모와 자식이 address space가 완전히 달라진다. Program count의 값이 초기화	된다. 자식이 새로운 address space를 가지게 된다. 부모는 자식이 돌아올 때까지 wait상태로 	대기한다.



​	**IPC(interprocess communication)**

​	=> 프로세스 사이에 communication을 하는 과정, 이를 통해서 프로세스간의 협업 가능



**message passing**

1.  Blocking(synchronous)
    - 발신 : 메세지를 보낸 후 응답이 올 때까지 대기
    - 수신 : available한 메세지를 받을 때까지 대기

2.  Non-Blocking(asynchronous)
    - 발신 : 메세지를 보내고 다른 작업 진행
    - 수신 : 정상적으로 수신하거나 안받음


​	**Buffering**

1. zero capacity : 발신자가 무조건 대기 (sync)
2. bounded capacity : n개의 메세지를 queue에 쌓아둠. 만약 queue가 꽉차면 발신자 대기
3. unbounded capacity : 무제한으로 메세지를 쌓아둠. 발신자는 대기 X



#### 쓰레드(Thread)

​	스레드(thread)란 프로세스(process) 내에서 실제로 작업을 수행하는 주체를 의미합니다. 모든 프로세스에는 한 개 이상의 스레드가 존재하여 작업을 수행합니다.



​	**쓰레드 구성요소**

1. program counter

  2. register set

  3. stack space


​	**스택을 스레드마다 독립적으로 할당하는 이유**

​	스택은 함수 호출 시 전달되는 인자, 되돌아갈 주소값 및 함수 내에서 선언하는 변수 등을 저	장하기 위해 사용되는 메모리 공간이므로 스택 메모리 공간이 독립적이라는 것은 독립적인 	함수 호출이 가능하다는 것이고 이는 독립적인 실행 흐름이 추가되는 것이다. 따라서 스레드	의 정의에 따라 독립적인 실행 흐름을 추가하기 위한 최소 조건으로 독립된 스택을 할당한다.

​	**PC Register 를 스레드마다 독립적으로 할당하는 이유**

​	PC 값은 스레드가 명령어의 어디까지 수행하였는지를 나타나게 된다. 스레드는 CPU 를 할당	받았다가 스케줄러에 의해 다시 선점당한다. 그렇기 때문에 명령어가 연속적으로 수행되지 	못하고 어느 부분까지 수행했는지 기억할 필요가 있다. 따라서 PC 레지스터를 독립적으로 할	당한다.



​	**공유요소**

 1. code

 2. data

 3. files

  <img src="/assets/thread struct.png">



​	장점

1. 사용자에 대한 응답성 증가
   - 응용 프로그램의 일부분이 봉쇄 또는 긴 작업 수행 시에도 프로그램 실행을 계속 허용하여 사용자에 대한 응답성이 증가

2. 프로세스의 자원과 메모리 공유 가능
   - 스레드는 그들이 속한 프로세스의 자원과 메모리를 공유하므로, 응용 프로그램 하나가 같은 주소 공간에서 여러 개의 스레드를 실행, 시스템 성능 향상과 편리함 제공

3. 경제성
   - 한 프로세스의 자원을 공유하므로 프로세스를 생성하는 것보다 오버헤드를 줄일 수 있음

4. 다중 프로세서 구조 활용 가능
   - 다중 프로세서 구조에서 각 스레드는 다른 프로세서에서 병렬로  실행될 수 있음



​	**User thread**

​	=> OS는 thread의 존재를 모른다. OS는 프로세스에 모든 걸 할당하고 프로세스에서 thread 	library를 이용하여 일을 한다.(user level에서 이루어진다.) => 빨라진다

​	문제점 : 만약에 하나의 쓰레드라도 I/O를 만들어 내면 CPU는 프로세스가 I/O하는 줄 알고 전	체를 wait로 넣어버린다



​	**Kernel thread**

​	=> OS가 쓰레드를 지원해준다.

​	장점 : 쓰레드 하나가 I/O를 발생시켜도 그 쓰레드에 대해서만 wait가 들어간다. 할당 문제도 	OS가 해준다.

​	단점 : 만들 때도 커널이 만들어주고 죽일 때도 커널이 죽이기 때문에 느리다.



#### **쓰레드 이슈**

​	**fork시에 어떻게 자식 생성**

  1. fork이후에 exec를 바로 호출하면 모든 쓰레드를 복제할 필요가 없음.
     - 어짜피 새로운 프로그램에 의해서 새로운 쓰레드를 결정함.
  2. fork이후에 exec를 호출 안하면 모든 쓰레드를 복제해야함.



​	**Thread cancellation**

1. Asynchronous
   - 그냥 바로 쓰레드를 종료시킨다.
   - 데이터 문제 등 많은 문제가 발생할 가능성이 있으므로 주의해서 사용
2. Deferred
   -  순서에 맞게 체크를 통해 깔끔하게 종료를 시키는 것



​	**Thread handling**

​	=> 시그널이 발생하면 프로세스에 전달 된다. Signal을 받는 놈(쓰레드)을 정할 필요가 있다. 	(os마다 정책적으로 결정한다)



​	**thread pool**

​	=> OS가 미리 쓰레드를 만들어두고 만들어 달라고 하면 바로 준다.

​	=> 필요시에 바로 줄 수 있지만 사용을 하지 않을 때는 불필요한 공간을 잡아먹는 것이다.



​	**Thread specific data(TSD)**

​	=> 전역변수라도 쓰레드들이 각각 다른 값은 assign하게 해준다.

​	=> 공유된 변수라 하더라도 쓰레드마다 처리하는 값은 다를 수 있다.


## Scheduling

*운영체제가 준비완료 큐(Ready queue)에 있는 프로세스들 중에서 어떤 프로세스를 디스패치(Dispatch)할 것인가 정하는 것을 스케줄링(Scheduling)이라고 한다.*  

*디스패치 : 프로세스를 CPU에 할당하는 것 ( 이때 프로세스 상태 ready -> running )*



### Preemptive vs Non-preemptive ( 선점 vs 비선점 )



- Preemptive(선점) :  선점 스케줄링은 운영체제가 강제로 프로세스의  사용권을 통제하는 방식.

  즉, CPU에 프로세스가 할당되어 있어도 운영체제가 개입해 강제로 다른 프로세스에게 CPU 할당이 가능하다.

- Non-preemptive(비선점) : 비선점 스케줄링은 프로세스가 스스로 다음 프로세스에게 자리를 넘겨주는 방식.

  즉, 프로세스가 종료되거나 IO request가 발생하여 자발적으로 대기 상태로 들어갈 때까지 계속 실행된다.


### Scheduling Criteria



- CPU utilization(CPU 사용률) : CPU가 작업을 처리하는 시간의 비율

- Throughput(처리율) : 단위 시간 당 끝마친 프로세스의 수

- Turnaround time(반환시간) : 하나의 프로세스가 레디 큐에서 대기한 시간부터 작업을 마칠 때까지 걸리는 시간

- Wating time(대기시간) : 프로세스가 레디 큐에서 대기한 시간

- Response time(응답시간) : 프로세스가 처음 CPU를 할당받기까지 걸린 시간



### Scheduling Algorithms



1. ####  FCFS(First-Come First-Served)

   - 먼저 CPU를 요청하는 프로세스를 먼저 할당하는 방식

   - Queue의 FIFO(First-In First-Out)와 동일하다.

   - 프로세스 처리 순서에 따라 성능이 크게 달라질 수 있다.

   - convoy effect(콘보이 효과)가 발생한다는 문제점이 있다.

     convoy effect : 소요시간이 긴 프로세스가 먼저 도달하여 효율성을 낮추는 현상

   - 비선점 스케줄링 방식

2.  ####  SJF (Shortest Job First)


    - 수행 시간이 짧은 프로세스를 우선 할당하는 방식
    
    - Waiting time(대기시간)을 줄이는 관점에선 SJF가 가장 좋다.
    
    - Starvation(기아)가 발생한다는 문제점이 있다. (Aging(에이징) 기법으로 해결 가능)
    
      Starvation : Burst time이 큰 프로세스는 계속 순서가 뒤로 밀려나 CPU를 할당받을 수 없는 현상
    
      Aging : 오래 있었던 프로세스일수록 우선순위를 높여주는 방식
    
    - 비선점 스케줄링 방식








3.  ####  SRTF (Shortest Remaining Time First)

    - 프로세스의 남은 수행 시간이 짧은 순서에 따라 할당하는 방식

    - SJF의 preemptive(선점) 버전

    - 각 프로세스의 burst time 추적, 선점을 위한 문맥 교환 등으로 인한 오버헤드가 크다는 문제점이 있다.  

    - 선점 스케줄링 방식



4.  ####  Priority Scheduling

    - 특정 기준으로 프로세스에게 우선순위를 부여해 그 순서에 따라 할당하는 방식

    - 프로세스를 Aging(에이징)해서 오래 대기한 프로세스의 우선순위를 높이는 방식으로 사용된다.

    - 다른 스케줄링 알고리즘과 결합해 사용할 수 있기 때문에 선점, 비선점 모두 가능하다.

      선점 스케줄링 방식 :  더 높은 우선순위의 프로세스가 도착하면 실행중인 프로세스를 멈추고 CPU 를 선점한다.

      비선점 스케줄링 방식 : 더 높은 우선순위의 프로세스가 도착하면 Ready Queue 의 Head 에 넣는다.



5.  ####  RR (Round Robin)

    - 프로세스들 사이에 우선순위를 두지 않고, Time Quantum(시간 단위)으로 여러 프로세스를 번갈아가며 할당하는 방식

    - Response time이 빨라진다.

    - 적당한 Time Quantum을 설정하는 것이 중요하다.

      Time Quantum -> ∞  : FCFS와 동일

      Time Quantum -> 0  : context switching overhead가 빈번하게 발생

    - 선점 스케줄링 방식



6.  ####  Multilevel Queue

    - 작업들을 여러 종류의 그룹으로 나누어 여러개의 Queue를 이용하는 방식

    - 각 Queue는 특성에 맞는 독립된 스케줄링 정책을 사용한다.

      ex)  foreground 작업은 RR 방식의 큐에, background 작업은 FCFS 방식의 큐에 둔다. 이렇게 하면 RR 방식의 큐에 많은 CPU 시간을 할당할 수 있다.

    - 각각의 Queue에 절대적 우선순위가 존재하며, Queue 간 이동이 불가능하다.



7.  ####  Multilevel Feedback Queue

    - Multilevel Queue에서 Queue 간 이동이 불가능한 점을 개선한 방식

    - 각 큐마다 다른 Time Quantum을 부여하며 시간안에 완료되지 못한 프로세스는 다음 단계 큐로 넘어간다.

    - 모든 프로세스는 가장 상위 큐로 들어오고, 다른 Queue로 점진적으로 이동한다.

    - 기아 상태 우려 시 Aging 기법을 사용해 우선순위 높은 Queue로 이동한다.







# Synchronization

- Concurrent(병행) 하게 동작 :

*A라는 프로세스가 동작할 때 인터럽트가 언제든지 발생 할 수 있고, 이로 인해 부분적으로만 수행을 하고 잠시 멈추게 되는 경우가 존재 할 수 있다. 이는, inconsistency하게 발생하므로 Consistency가 보장될 필요성이 있다.*

<br>

- Consumer-Producer problem

  - Producer는 버퍼를 계속 채우려하고, Consumer는 비우려고 할 때, 버퍼 카운터를 서로 늘리고 줄인다.

  - Producer 입장에서는 버퍼를 채웠을 때 카운터는 증가해야 하고, Consumer 입장에서는 버퍼를 비웠을 때 카운터는 감소해야 한다.

<br>

### Race Condition

​	동시에 여러 개의 프로세스가 동일한 자료(공유 자원)에 접근하여 경쟁하는 현상을 말한다.

​	공유 자원의 최종 값은 어떠한 프로세스가 마지막에 동작 하는지에 따라 의존성을 갖는다.

<br>

### Critical Section Problem(임계 구역 문제)

##### Critical Section(임계 구역)

- 공유 데이터에 접근하는 코드 블럭. 공유 데이터에 동시에 접근 하게 되면 데이터의 무결성이 손상 될 수 있다. 이러한 문제가 바로 __Critical Section Problem__ 이다. 둘 이상의 프로세스(혹은 스레드)가 공유하는 데이터에 동시에 접근 할 수 없고, 특정 시간에 오직 하나의 프로세스만 접근이 가능한 코드 영역이다. 따라서, 이러한 임계 구역으로 진입하려면 진입 허가를 요청해야 한다. 이러한 요청을 구현하는 코드 부분을 진입 구역(Entry section)이라고 부르며, 임계 구역 뒤에는 퇴출 구역(Exit section)이 따라올 수 있다. 코드의 나머지 부분들은 총칭하여 나머지 구역(Remainder section)이라고 부른다.

<br>

<img src="/assets/Critical section.PNG">

<br>

##### Critical Section Problem 해결 조건

1. Mutual Exclusion :

   프로세스 A가 임계 구역에서 돌고 있으면, 다른 프로세스들은 임계 구역에서 수행될 수 없다.

2. Progress:

   임계 구역에서 수행 되고 있는 프로세스가 존재하지 않고, 임계 구역에 진입하기 위해 대기 중인 프로세스가 존재하는 경우 대기 중인 프로세스 중 하나의 프로세스는 선택 되어 곧바로 임계 구역에 진입되어야 한다.

3. Bounded Waiting:

   임계 영역을 요청한 프로세스는 무제한 대기 되어서는 안되며, 제한된 대기 시간을 가져야 한다.(프로세스가 기아 상태에 빠지는 것을 방지 하여야 한다.)

<br>

### Critical Section Problem 해결 방법

#### Algorithm 1

<pre>
do {
	while (turn != 0);	/* My  turn? : P0's turn  */
	critical section
	turn = 1;		/* Now P1’s turn  */
	remainder section
} while (1);</pre>

프로세스 0가 Critical section에서 작업을 끝내고 난 후 연달아 프로세스0가 Critical section 진입을 요청할 경우 turn 값이 1이기 때문에 Critical section에 진입할 수 없게 된다.

즉, 프로세스 1이 Critical section에서 작업을 한 번 해줘야 프로세스 0가 번갈아 가면서 진입 할 수 있다.

=>  Mutual Exclusion은 충족 하지만, Progress는 충족 하지 못한다.

<br>

#### Algorithm 2

<pre>
do {
	flag[i] = true;		/* Pretend  I am in */
    while (flag[j]);	/* Is he also in? then wait*/
    critical section
	flag [i] = false;	/* I am out now*/
	remainder section
} while (1);
</pre>

프로세스 i가 Critical section에 진입하기 위해 flag값을 true로 변경한 후에 인터럽트가 발생하여 프로세스 j에게 CPU를 뺏겼다고 가정해보자. 프로세스 j 또한 Critical section에 진입 하기 위해 대기 중이였다면, flag값을 true로 변경할 것이고  프로세스 i의 flag값이 false로 변경 되기만을 기다릴 것이다.

문제는 프로세스 i가 다시 CPU를 차지하더라도, j의 flag값이 false로 변경 되기만을 기다릴 것이고, 두 프로세스 모두 끊임없이 대기하는 상황이 발생할 것이다.

=>  즉, 해당 알고리즘도 Mutual Exclusion은 충족하지만, Progress는 충족하지 못한다.

<br>

#### Peterson's solution (Algorithm 3)

<pre>
do {
	flag [i]= true;  	  /* My intention is to enter …. */
	turn = j;	     	  /* Set to his turn */
	while (flag [j] and turn == j) ;  /* wait only if …*/
	critical section
	flag [i] = false;
	remainder section
} while (1);
</pre>

Algorithm1과 Algorithm2를 결합한 Algorithm

2개의 프로세스에 대해 Critical-section Problem을 해결할 수 있다. 하지만, CPU Burst time이 다할 동안 while문을 계속 루프하며 대기하기 때문에(busy waiting or spin lock) 비효율적인 문제점을 가지고 있다. while조건을 충족하면 계속 루프를 돌기 보다는, 다른 프로세스에게 빨리 CPU를 넘기는 것이 효율적이다.

=> Mutual Exclusion, Progress 둘 다 충족

<br>

#### Synchronization Hardware

동기화 문제는 항상 어떠한 데이터를 변경하는 와중에 CPU를 뺏겨서 발생한다. __데이터를 읽어서 변경을 하고 저장하는 과정__ 을 CPU를 뺏기지 않고, 한번에(atomic) 수행할 수 있다면 동기화 문제는 발생하지 않는다. Atomic 구문으로 이루어진 구간은 처음부터 끝까지, preemption이 발생할 수 없다.

이 atomic한 과정을 __Hardware__ 를 통해 수행할 수 있다.

<br>

 Atomic hardware instruction을 구현하는 방법

1. Test_and_Set()

   <pre>
   boolean test_and_set(boolean *target) {
   	boolean rv = *target;
   	*target = true;
   	return rv;
     }
     // lock initialization: "false"
   do {
   	while(test_and_set(&lock));
   	// critical section
   	lock = false;
   	// remainder section
   } while(true);
   </pre>

   1. test_and_set(&lock)은 현재의 lock 값(false)를 리턴한다. (단, lock값은 true로 변경 되어 있음)
   2. 작업이 끝나면 lock을 false로 변경해주어, 다른 프로세스가 while문을 빠져나올 수 있도록 한다.

   =>  Mutual Exclusion, Progress 만족

<br>


2. Compare_and_Swap()

   <pre>
   void compare_and_swap(int *value, int expected, int new_value) {
   	int temp = *value;
   	if(*value == expected)
   		*value = new_value;
   	return temp
   }
   // lock initialization: "0"
   do {
   	while(compare_and_swap(&lock, 0, 1) != 0);
   	// critical section
   	lock = 0;
   	// remainder section
   } while(true);
   </pre>

   1. compare_and_swap(&lock, 0, 1)은 lock의 원래 값을 리턴한다. (단 lock은 0일 때만 1로 변경) 처음에 0인 lock의 값이 1로 바뀌어지고 임계 구역에 들어가면 이후 진입하려는 프로세스들은 1만 리턴하기 때문에 while문을 빠져나오지 못한다.
   2. 임계 구역에 진입한 프로세스가 작업을 수행하고 lock을 0으로 바꾸면서 대기중인 프로세스가 while문을 빠져나오며 임계구역에 진입이 가능해진다.

   =>  Mutual Exclusion, Progress 만족

<br>

__하지만  위의 두 방식 모두 Bounded Waiting을 만족하지 못함__

(한 프로세스가 Lock 값을 바꾸자마자 다시 진입이 가능 하기 때문)

<br>

3. Bounded_Waiting 보장

   <pre>
   // waiting[], lock initialization "false"
   do {
   	waiting[i] = true;
   	key = true;
   	while(waiting[i] && key) {
   		key = test_and_set(&lock);
   	}
   	waiting[i] = false;
   	// critical section
   	j = (i+1) % n;
   	while((j != i) && !waiting[j]) {
   		j = (j+1) % n;
   	}
   	if(j == i) lock = false;
   	else waiting[j] = false;
   	// remainder section
   } while(true);
   </pre>

   1. 처음 false 값을 가지고 있는 waiting[i]와 key는 true로 바뀌고 while문이 수행된다.
   2. test_and_set 명령어를 통해 초기값 false인 lock 값이 false를 반환하고 true로 lock 값을 바꾼다.
   3. 처음에 key는 false 값을 가지게 되고 임계구역에 진입한다. (임계구역에 들어간 프로세스만 waiting 값을 false로 바꾼다. 나머지는 while문에서 true 값이 반복된다.
      => **Mutual exclusion 만족**
   4. 작업이 끝나면 waiting 배열을 순회하면서 임계구역에 들어갈 프로세스를 찾는다. waiting 값이 true이면(임계구역을 기다리는 프로세스) while문을 빠져나온다.
      => **Bounded waiting 만족 (최대 n-1회만 양보하면 임계구역에 진입 가능)**
   5. 찾는다면, 그 프로세스의 waiting 값을 false로 바꾸어 임계구역에 들어갈 수 있도록 한다.
      => **Progress 만족**
   6. waiting 배열 값이 전부 false로  통과하게 되면 j==i 조건문이 수행되어 lock을 false로 변경하고(처음 lock의 초기값과 같아짐) 종료하게 된다.

<br>

#### Busy-wait VS Block-wakeup

**Busy waiting :** 프로세스가 임계구역에 있는 동안 기다리는 다른 프로세스들은 acquire( ) 함수의 반복문을 계속 실행해야 한다.

lock이 사용될 수 있기를 기다리면서 프로세스가 계속 회전을 하고 있어 **spinlock**이라고도 한다. 이러면 다른 프로세스가 실행되지 못하기에 CPU 사이클 낭비를 초래하며, **위의 명령어 모두 이런 단점을 지니고 있다.**

하지만 lock을 기다리는 동안은 **context switching을 필요로 하지 않기에**(프로세스가 상태가 변경되었다가 다시 돌아오는게 아닌 계속 실행 상태이기에) multiprocessing에서 spinlock이 사용된다.
→ 조금만 기다리면 바로 쓸 수 있다는 점을 이용해서 **lock-unlock의 타임이 짧을 때 유용**하다.

<br>

Busy waiting 해결 : 프로세스를 대기 큐(wait queue)에 넣고 대기 상태로(waiting) 전환하여 다른 프로세스가 실행되도록 한다. → wait( )

임계구역을 나온 프로세스의 signal( ) 함수 호출에 따라 대기 상태인 프로세스가 준비 큐(ready queue)로 들어가 프로세스를 재시작하여 임계구역에 진입하게 된다.

__block( )과 wakeup( )을 사용해 이를 해결한다.(링크드 리스트 사용)__

<pre>
typedef struct {
	int value;
	struct process *list;
}semaphore;

void wait(semaphore *S) {
​	S->value--;
​	if(S->value < 0) {
​		// insert process into S->list.
​		block();
​	}
}

void signal(semaphore *S) {
​	S->value++;
​	if(S->value <= 0) {
​		// delete process from S->list.
​		wakeup(P);
​	}
}
</pre>

+ block( ) 함수는 자기를 호출한 프로세스를 중지시킨다.
+ wakeup(P)은 봉쇄된 프로세스 P를 재시작한다.
+ pooling방식이 아닌 인터럽트 기반 방식으로 구현되며 빈번한 context switching이 발생한다.
+ queue를 만들기 위해 링크드 리스트를 사용

<br>

**→ 임계구역이 짧으면 busy waiting, 길면 block & wake-up 방식을 사용한다.**  

<br>

#### Mutex Locks

Mutual exclusion의 축약형태로 임계구역에 들어가기 전에 lock을 획득하고 빠져 나올 때 lock을 반환한다.

- Mutex_lock(): entry section
- Mutex_unlock(): exit section

boolean 변수 available을 통해 Lock의 가용 여부를 표시한다.

<pre>
Mutex_lock() {
	while(!available) wait(); //대기열(큐) 진입
	available = false;
}
Mutex_unlock() {
	available = true;
	signal(); //대기열(큐) 호출
}
</pre>

1. available의 초기값이 true로 처음 Mutex_lock( ) 함수를 호출하면 available을 false로 변경하고 함수를 빠져나온다.
2. 빠져나온 프로세스는 임계구역에 진입하고 나머지 프로세스들은 Mutex_lock( ) 함수에서 lock이 사용될 수 있기를 기다린다. (while문에서 빠져나오질 못한다.)
3. 작업을 모두 수행하였으면 Mutex_unlock( ) 함수를 호출하여 available을 true로 바꾸어 lock을 반환한다. 이제 다른 프로세스가 임계구역에 진입할 수 있게 된다.

- 두 opeartion은 atomic하게 일어난다.(OS에서 설계가 그렇게 됨)
- 프로세스 작업 순서를 정해줄 수 있게 된다.

<pre>
S1; // Process 1
signal(S);
wait(S);
S2; // Process 2
</pre>

S가 0으로 초기화 되어있다면 P1이 S1 작업 이후, S가 1로 증가될 때 비로소 P2가 S2 작업을 수행할 수 있게 된다.

<br>

#### Semaphore

- S라는 정수형 변수, wait( )와 signal( ) 함수로 접근
- S는 동시에 변경할 수 없다. (atomic)
- Mutex와 다른점은 counting이 가능하다는 것이다. 가용할 수 있는 프로세스들을 동시에 실행시키는게 가능하다.

<pre>
wait(S) {
    S--;
    if(S < 0) block();
}
signal(S) {
​	S++;
​	if(s <= 0) wakeup();
}
</pre>

- Counting semaphore: 몇 개가 접근하고 있는지 셀 수 있다.(0~N)
  - 자원을 사용하려는 프로세스는 wait( )를 호출하여 S를 감소시킨다.
  - 자원을 방출할 때는 signal( )를 호출하여 S를 증가시킨다.

<br>

### Mutex-lock VS Binary-semahpore

Mutex lock은 잠금 메커니즘으로서 하나의 작업에 대해서 접근을 획득한 프로세스만 해당 잠금을 해지 할 수 있으나, 세마포어는 신호 전달 메카니즘으로서 어떠한 프로세스라도 해당 value에 대한 접근이 가능하고 변경 할 수 있다.

<img src="/assets/mutexnsemaphore.png">

<br>

### Deadlock and Starvation

**Deadlock** 이란 프로세스가 서로의 Signal을 기다리게 되면서 모두 무한정 대기하게 되는 현상

<img src="/assets/deadlock.png">

<br>



**Starvation**은 앞에서 언급했던 Blocking & Wake-Up 방식에서 Ready Queue에 대기하고 있는 프로세스 중 하나를 선택하는 스케줄링 과정에서 여러 이유 중 하나로 선택되지 못하여 실행되지 못하는 프로세스가 생기는 현상

<br>

### Priority Inversion

우선순위 역전 현상이란 간단히 말하자면 우선순위가 낮은 프로세스 때문에 우선순위가 높은 프로세스가 실행되지 않는 현상을 말한다.

<img src="/assets/priorityinversion.jpg">

ProcessA가 ProcessC가 획득한 Sem-A를 요청한 상태에서 Context Switching이 일어나 Process C보다 우선순위가 높은 프로세스가 실행된다면 (여기선 Process B) Process C는 우선순위에 밀려 계속 실행되지 않고 이로 인해 자원 반납이 되지 않아 Process A가 실행되지 않게 된다. 이러한 현상을 Priority Inversion, 우선순위 역전 현상이라고 한다.

<br>

이러한 Priority Inversion의 해결 방안으로는,

특정 프로세스가 우선순위가 높은 프로세스에서 요구하는 자원을 가지고 있을 때 그 특정 프로세스의 우선순위를

자원을 요구하는 프로세스의 우선순위로 높여주는 방법이 있으며, 이러한 방법을 ***Priority Inheritance Protocol* (우선순위 계승)**이라고 한다.

<img src="/assets/PriorityInheritanceProtocol.jpg">

<br>

### 동기화 주요 이슈들

#### Bounded-Buffer Problem

상호작용하는 두 프로세스는 buffer를 통한 데이터 주고받는데, Producer 프로세스는 데이터를 하나 만들면

buffer에 추가하고 Consumer 프로세스는 buffer에 데이터가 있으면 하나씩 가져와 처리를 한다.

이때, buffer 안의 데이터 개수의 동기화 문제가 발생할 수 있는데 이때 Semaphore을 사용하여 해결할 수 있다.

<br>

1. Mutex : buffer의 접근을 관리하는 것으로 1로 초기화.

2. Full : buffer의 들어가 있는 데이터의 수를 관리하는 것으로 0으로 초기화.

3. Empty : buffer의 빈 공간의 개수를 의미하는 것으로 buffer 전체 크기인 N으로 초기화.

<img src="/assets/boundedbufferproblem.png">

Producer는 buffer에 빈 공간이 있는지 확인 후 buffer의 접근을 시도하고, Consumer는 buffer에 가져올 데이터가 있는지 확인 후 buffer의 접근을 시도

이때 wait(mutex)를 통해 하나의 프로세스만 buffer에 접근을 할 수 있게 되고 데이터를 집어넣거나 가져온 후에는 signal(mutex)를 통해 buffer 접근 권한을 내려놓는다.

<br>

#### Readers-Writers Problem

공유 데이터 공간에 대해 데이터를 입력하는 것은 하나의 Writer 프로세스만이 접근이 가능하고 데이터를 읽을 때는 여러 개의 Readers 프로세스가 접근이 가능할 때 데이터를 저장하고 읽어올 때 충돌로 인한 데이터의 불일치를 방지할 때 역시 Semaphore를 이용하여 문제를 해결할 수 있다.

<br>

1. readcount : 현재 몇 개의 Reader 프로세스가 데이터 읽기를 시도하는지를 관리.

2. mutex : readcount의 값을 변경할 때 값의 일치성을 관리.

3. wrt :  데이터 접근에 대해 Reader와 Writer를 동시에 접근할 수 없게 관리.

<img src="/assets/readerwriterproblem.jpg">

Writer는 wait(wrt)를 통해 데이터에 쓰기를 수행하기 위해서는 Reader가 현재 읽기를 수행하고 있는지 확인을 해야 하고 그렇지 않다면 데이터 쓰기를 수행

Reader가 데이터 읽기를 하기 위해서는 먼저 읽기를 하려는 Reader의 readcount를 증가시켜야 하는데 이때 readcount의 불일치를 방지하기 위해 wait(mutex)와 signal(mutex)를 위아래에 작성해준다.

그리고 하나의 Reader라도 읽기를 수행하고 있다면 wait(wrt)을 통해 Writer 프로세스의 접근을 막는다.

역시 읽기 수행이 끝나고 readcount를 감소시킬 때도 wait(mutex)와 signal(mute)를 통해 데이터의 일치성을 보장해주고 더 이상 데이터 읽기를 수행하는 Reader 프로세스가 존재하지 않는다면 signal(wrt)를 통해 Writer 프로세스의 데이터 접근을 허용한다.

<br>

#### Dining-Philosophers

5명의 철학자가 원형 테이블에 앉아 있고 테이블 중앙에는 밥이, 테이블에는 5개의 젓가락이 놓여 있다.(쌍이 아닌) 배고픈 철학자가 동시에 젓가락을 2개 집으면, 식사를 마칠 때까지 젓가락을 놓지 않고 식사를 한다.
→ deadlock과 starvation을 발생시키지 않고 여러 스레드에게 자원을 할당해야 할 필요를 표현한 것이다.

- 5명 모두가 동시에 배고파서 왼쪽 젓가락 잡고 각자 자신의 오른쪽 젓가락 잡게되면 없기에 deadlock & starvation
- 5개의 semaphore(젓가락)가 상호 의존성을 지니면 deadlock이 생길 수 있다.

Deadlock handling

 - 각각의 철학자를  P_{1},P_{2},P_{3},P_{4},P{5}라고 하고, 각 철학자의 왼쪽 포크를 f_{1},f_{2},f_{3},f_{4},f_{5}라고 하자. P_{5}를 제외한 네 명은 먼저  f_{n}를 집은 후 f{n+1}를 집는 방식을 취한다. 그리고 P_{5}는 이와 반대로, f_{1}를 먼저 집은 후 f_{5}를 집는다. 이것은 원래 방식의 대칭성을 제거하고, 따라서 교착 상태를 막을 수 있다.
 - 동시에 2개를 잡을 수 있는 경우에만 젓가락을 잡아라 → critical section

<br>

### Monitors

Semaphore는 충돌이나 동기화의 문제들을 해결해주지만

직접 프로그래머가 작성해주어야 하고 이로 인해 사소한 실수에도 심각한 문제를 일으킬 수 있게 된다. (Deadlock, Starvation, Priority Inversion 등등) 그래서 프로그래밍 언어의 설계 단계에서부터 이러한 것들을 언어 자체가 해결할 수 있게 해주는 기능이 Monitor이다.

Monitor는 동시 접근에 대한 문제는 해결해주지만 동기화에 대한 문제를 완전히 해결하지는 못하는데, 이를 해결하기 위해 도입한 것이 Condition 변수입니다. Condition 변수를 통해 프로세스들은 순서를 보장받게 됩니다.

<br>

Monitor와 Semaphore의 가장 뚜렷한 차이점은 직접 작성하냐 기능을 제공받느냐, 값에 따라 여러 프로세스가 접근할 수 있는지 아니면 오로지 하나의 프로세스만이 접근할 수 있는지 등이 존재한다.

<br>

# Deadlocks

+ ### Deaklock

  Deaklock 이란 프로세스 P1이 자원 A를 갖고 있으면서 B를 필요로 하고 프로세스 P2는 자원 B를 갖고 있으면서 자원 A를 필요로 하는 상황에서 두 프로세스 모두 더 이상 진행이 되지 않는 상황

  <br>

  ### Deadlock 발생조건

  + 다음 4가지가 동시에 만족되었을 때 일어날 수 있다.(항상 발생은 아님)

    1. **Mutual exclusion**: 오직 하나의 프로세스만 하나의 자원을 사용할 수 있다. 적어도 하나의 자원은 공유가 불가능한 자원이다.

    2. **no preemeption**: 중간에 끊을 수 없는 상황, 이미 할당된 자원이 갑자기 반납되어서는 안된다. 프로세스가 스스로 반납.
    3. **Hold and wait**: 적어도 하나의 자원을 보유한 프로세스가 다른 프로세스의 자원을 추가로 얻기를 기다릴 때
    4. **circular wait**: 프로세스들이 자원을 소유하고 요청하는 형태가 원형을 이룰 때를 말한다.
       각 프로세스에는 하나의 자원이 할당되어있고, P1은 P2자원을 기다림, P2는 P3자원을 기다림, P3는 P1자원을 기다릴 때 원형을 이룬다.

  <br>

  ### Deadlock과 Cycle

  Deadlock은 프로세스들 간의 자원 요구와 소유를 간단하게 표현한 **그래프를 통해 보다 쉽게 검사**할 수 있다.
  밑의 그림에서 P -> R 은 해당 자원을 필요로 하는 것을, R -> P는 프로세스가 해당 자원을 소유하고 있는 것을 의미

  <img src="/assets/deadlock2.png">

  <br>

  P1은 R2를 소유하면서 R1을 요청

  P2는 R1을 소유하면서 R3 를 요청

  P3라는 R3를 소유하면서 R2를 요청

  즉, P1은 R1을 할당받고 작업을 완료해야 R2와 R1을 반납

  P2는 R3를 할당받고 작업을 완료해야 R3와 R1을 반납

  P3는 R2를 할당받고 작업을 완료해야 R2와 R3를 반납

  => **Deadlock이 발생**

  여기서 **반드시 인지하셔야 할 조건은 No preemption 조건**

  현 상황에서는 어떠한 프로세스도 작업을 완료할 수 없고 어떠한 자원도 반납할 수 없기 때문에
  Deadlock이 발생하게 된다.

  <br>

  보다 빠르고 쉽게 판단하려면 자원 요청이 사이클이 존재하시는지 확인을 하면 된다.
  위의 그림은 자원 요청의 화살표가 사이클을 이루고 있는데요. 이러한 **사이클이 있다면 Deadlock을** 의심해봐야 한다.(무조건 사이클이 존재한다고 Deadlock 발생은 아님)

  <br>

  **Cycle이 존재하지만 Deadlock이 발생하지 않는 경우**

  <img src="/assets/Nodeadlock.png">

  <br>

  ### Method of handling Deadlock

  Deadlock을 다루는 방법에는 크게 세 가지가 있다.

  **첫째, Deadlock 현상 자체를 미연에 방지하는 방법**

     말 그대로 애초에 Deadlock이 발생하지 않도록 하는 방법이다.

     -Deadlock prevention, Deadlock Avoidance

  **둘째, Deadlock 상태를 허용하면서 그것을 복구하는 방법**

     현재 상태를 주기적으로 체크하면서 Deadlock 상태인지를 확인하며 Deadlock에 빠지면 복구를 하는 방법이다.

     -Deadlock Detection Algorithm

  **셋째, Deadlock 문제 자체를 무시해버리는 방법**

     사실상 대부분의 운영체제가 이 방법을 사용한다. 위의 두 가지 방법은 그에 따른 비용이 높기 때문에

     문제가 있는 프로세스를 Kill 하거나 시스템 자체를 리부팅하여 Deadlock 문제를 해결을 한다.

    -Kill Process, Rebooting

  <br>

  #### 1. Deadlock Prevention

  Deadlock Prevention은 이전 글에서 다루었던 Deadlock이 일어나기 위한 조건 4 가지 중 아무것이나 하나를 충족시키지 않게 함으로써 Deadlock을 방지하는 방법이다. 4 가지의 조건이 모두 만족해야 Deadlock이 발생하기 때문에 하나만 충족시키지 않아도 Deadlock은 발생하지 않게 된다.

  **(1) Mutual Exclusion 부정**

  ​     사실 이 조건을 충족시키지 않는 방법은 존재하지 않는다.

  ​     애초에 자원에 동시 접근이 불가능하기 때문에 동시에 접근을 하게 하는것은 불가능

  **(2) Hold and Wait 부정**

  ​     프로세스가 자원을 요청할 때는 항상 어느 자원도 소유하고 있지 않게 해야 한다.

  ​     프로세스가 실행되기 전에 필요한 자원들을 모두 요청하고 할당받아야 한다. 

  → 할당된 모든 자원이 바로 사용되지 않기에 자원의 이용도가 낮을 수 있다.

  →  우선순위가 낮은 프로세스들은 자원을 할당받지 못하는 시간이 길어지는 Starvation 문제가 생길 가능성도 생긴다.

  **(3) No Preemption 부정**

  ​	1번 resource를 잡고있는 process가 2번 resource를 요청했을 때 바로 받을 수 없다면 1번과 (다른 프로세스에	게 할당된) 2번 모두 release 하도록 한다. release함으로써 preemption이 되어버린다.

  ​	또한, 프로세스는 요청 중인 새로운 자원을(2번) 할당받고 또한 대기 중에 선점되었던(끊겼던) 모든 자원(1번)을 	회복할 때에만 다시 시작할 수 있다.

  **(4) Circular Wait 부정**

  ​	resource에 ordering(순서)을 부여하여 순서에 맞게 resource를 요청할 수 있고 할당받을 수 있게 한다. 동시에 	요청 불가능하기에 원형을 이룰 수 없다.

  #### 2.Deadlock Avoidance

  Deadlock Avoidance는 운영체제에게 자원 요청이 들어오면 자원을 할당해주었다고 가정한 상태에서 잠재적으로 Deadlock이 일어나는지 유무를 판단하여 Deadlock이 일어난다면 자원이 충분함에도 불구하고 할당해주지 않는 방법이다.

  판단을 했을 때 Deadlock이 일어나지 않는 상태를 Safe State라 하고 현재 이용 가능한 자원, 현재 각각의 프로세스에게 할당되어 있는 자원 그리고 각각의 프로세스들이 사용하고 반납할 자원들의 정보를 바탕으로 잠재적 Deadlock의 유무를 판단한다.

  프로세스 간 자원 할당 순서 중 Safe State Sequence가 하나라도 존재한다면 Safe State라고 판단을 한다.

  <br>

  Safe State Sequence란 일종의 자원을 필요로 하는 프로세스들에게 자원을 할당해주는 순서인데 바로 이전 프로세스가 수행을 마치고 반납한 자원과 현재 할당 가능한 자원을 이용해 현재 프로세스에게 할당이 가능한 프로세스의 자원 할당 순서를 Safe State Sequence라고 힌다.  당장 할당이 불가능해도 이전의 프로세스들이 반납을 함으로써 할당이 가능하다면 그 순서 또한 Safe State Sequence라고 한다. 

  <br>



  예를 들어, 두 개의 프로세스 P1, P2는 Printer라는 자원을 필요로 하고 있다. 그럼 운영체제는 Printer 자원을 *P1 - P2* 순서로 할당해 줄 수도 있고 *P2-P1* 순서로 할당해 줄 수 있다. 

  물론 Printer 자원이 충분히 많다면 동시에 할당해줌으로써 병렬적 처리를 하게 된다. 하지만 만일 Printer 자원이 부족하다면 하나의 프로세스가 작업을 끝내고 자원을 반납해야 다음 프로세스가 사용할 수 있다.

  현재 상태에서 Printer의 자원 인스턴스가 8개이고 P1은 Printer 자원을 5개 소유하고 있으며 작업을 끝내려면 Printer 자원 6개가 더 필요하며, P2는 2개를 소유하고 있으며 9개를 요청한 상태라고 가정해보자.

  만일 **P2-P1**의 순서대로 Printer 자원을 요청한다면 P2는 9개의 자원을 요청했지만 현재 지원 가능한 자원은 8개이므로 지속해서 대기해야 하고 다른 프로세스가 반납을 해야 자원을 할당받고 작업을 수행할 수 있기 때문에 Deadlock의 가능성이 있다.

  그럼 반대로 **P1-P2**의 순서대로 Printer 자원을 지원한다면 P1은 6개만을 요청하였기 때문에 현재 자원으로 할당이 가능하다.

  그리고 할당받은 자원으로 작업을 수행하고 끝낸다면 원래 소유하고 있던 Printer 자원 5개와 할당받은 자원 6개를 반납하여 Printer의 현재 할당 가능한 자원 인스턴스의 수는  2 + 5  + 6 = 13이 되게 된다.

  그러면 현재 할당 가능한 Printer의 자원은 13이므로 P2가 요청하는 9개를 할당해주고 P2까지 Printer 자원을 필요로 하는 모든 작업들을 Deadlock 없이 완료할 수 있게 된다.

  여기서 P1-P2, 이 순서를 Safe State Sequence라고 합니다. 자원을 주었다고 가정한 상태에서 계산을 했다는 것이 요점이다.

  > *Safe State Sequence가 1개라도 존재한다면 Safe State입니다.*
  >
  > *만일 Safe State라면 Deadlock은 반드시 일어나지 않고*
  >
  > *Safe State가 아니라 해도 Deadlock이 일어날 수도 있고 일어나지 않을 수도 있습니다.*

  <br>



  ### Deadlock Avoidance Alogrithm - Banker's Algorithm

  Banker's Algorithm는 Resource Request Algorithm의 큰 흐름

  Resource Request Algorithm 이란 어느 프로세스로부터 운영체제에게 자원 할당의 요청이 들어온다면 운영체제는 해당 프로세스가 요청한 자원에 대해 할당이 가능한지를 판단하고 할당이 가능하다면 할당을 해주었다 가정한 이후에 프로세스들 간의 Deadlock의 발생할지를 검사하여 만약 Deadlock이 발생한다고 판단되어지면 자원을 할당하지 않고, Deadlock이 발생하지 않는다면 자원을 할당해주는 알고리즘이다.

  <img src="/assets/resourcerequest.png">

  1. n : 프로세스의 개수, m : 자원 타입의  개수

  2. Available : m 길이의 Vector로 현재 자원들의 할당 가능한 인스턴스들을 나타낸다.

  3. Max : n X m 형태의 Matrix로 Max[i, j] = k라면 이는 P(i) 프로세스는 작업을 완료하기 위해 R(j) 자원을 최대 k 개 필요함을 의미.

  4. Allocation : n X m 형태의 Matrix로 Allocation[i, j] = k라면 현재 P(i) 프로세스는 R(j) 자원을 k 개 할당받았다는 것을 의미.

  5. Need : n X m 형태의 Matrix로 Need[i, j] = k라면 현재 P(i) 프로세스는 작업을 완료하기까지 R(j) 자원을 k 개 더 필요함을 의미.

  **즉 Max[i, j] - Allocation[i, j] = Need[i, j]**

  먼저 하나의 프로세스 P가 자원을 요청을 하면 요청한 자원의 양이 현재 P가 필요로 하는 자원의 양과 비교

  만약 필요한 양보다 많은 양을 요청을 하게 된다면 에러 처리를 하고, 요청한 자원의 양이 현재 할당 가능한 자원의 양보다 크다면, 즉 당장 요청한 자원에 대해 할당해줄 자원이 부족하다면 다른 프로세스들이 반납할 때까지 기다린다.

  두 조건을 모두 만족하면 할당해주었다 가정하고 다음과 같은 값의 상태(가정)로 Safe State를 검사한다.

  *Available = Available - Request*

  *Allocation = Allocation + Request*

  *Need = Need - Request*

  그리고 위의 상태에서 Safe State 인지를 판단하기 위해 Safe State Sequence를 찾는 Safety Algorithm을 사용

  그리하여 Safe State라 판단이 된다면 실제로 자원을 할당하고 위의 상태로 바꿔준다.

  <br>

  #### Safety Algorithm

  Safety Algorithm은 직접적으로 Safe State 인지를 검사하는 알고리즘으로 Safe State Sequence를 찾는 알고리즘

  <img src="/assets/safetyalgorithm.png">

  <img src="/assets/safetyalgorithmex.png">

  Safety Algorithm으로 위의 예시의 상황에서 Safe State Sequence 중 하나로 < P1, P3, P4, P0, P2 > 순서가 뽑힐 수 있다. 자원들의 시작 전 총 Available은 (10 , 5, 7)이나 현 상태에서는  (3, 3, 2)가 됩니다.

  그러므로 Work는 (3, 3, 2)가 되고 Finish들은 모두 false로 초기화됩니다. 결과론적인 방법이긴 하나 먼저 P1에게 자원들을 할당해주면 현재 Finish[1] 은 false이며 P1의 Allocation은 (2, 0, 0)이고 Max는 (3, 2, 2)이므로 Need는 (1, 2, 2)가 된다. 그러므로 Need <= Work이므로 3단계로 넘어가서 Work는 Work(3, 3, 2)에 현재 P1의 Allocation (2, 0, 0)을 더한 (5, 3, 2)가 된다.

  그리고 Finish[1]을 작업을 완료했다는 의미로 True로 바꿔주고 다시 2단계로 돌아가 자원을 할당해줄 프로세스를 선택하고 이 과정은 Finish의 모든 값이 True가 될 때까지 반복해준다.

  왜 이렇게 하는 것일까?

  P1이 현재 필요로 하는 자원의 양이 현재 할당 가능한 자원보다 작다는 것은 할당해줄 수 있다는 뜻이고 그것을 할당해주고 작업을 완료하면 현재 할당되어 있는 자원들까지 회수되기 때문에 작업이 완료되었다 가정하고 Available에 Allocation을 더해줌으로써 P1이 끝난 후에 Available 현황을 알 수 있게 된다. 그리고 Available의 현황을 이용하여 다음 프로세스를 고르는 작업을 반복하고 회수한 자원들로 증가된 Available로 자원을 할당하여 모든 프로세스의 작업을 끝내게 되면 Finish는 모두 True가 되고 그렇게 뽑힌 순서가 바로 Safe State Sequence가 된다.




# Memory-Management

<h2>가상 메모리부터 물리 메모리까지</h2>
프로세스 내에서 유저 메모리영역은 OS에서 각 프로세스 간 메모리 공간을 보호하기 위해 가상메모리 기법을 이용하여 각 프로세스마다 독립적으로 메모리 공간을 사용할 수 있도록 분리하고 있다.

32비트 환경에서 가상 메모리 주소가 물리 메모리주소로 어떠한 과정을 거쳐서 변환이 되는지 알아보자.

```c
#include <stdio.h>
#include <stdlib.h>

int data=100; //초기화한 전역 변수
int bss; //초기화하지 않은 전역 변수

int main () {
  int stack; //지역 변수
  int *heap = (int*)malloc(sizeof(int)); //동적할당 변수
  data = 1;
  bss = 2;
  stack = 3;
  *heap = 4;
  return 0;
}
```

위 코드를 컴파일한 후 디스어셈블리하면 아래의 코드가 나온다.
<image src="/assets/disassembled code.PNG" width="80%">

각 변수에 1, 2, 3, 4 넣는 어셈블리 코드를 확인하면
```nasm
mov dword ptr ds:[403010],1
```
1을 넣는 것은 data 변수(초기화된 전역변수, data 영역)
```nasm
lea rax,qword ptr ds:[407A20]
mov dword ptr ds:[rax],2
```
2를 넣는 것은 bss 변수 (초기화되지 않은 전역변수, bss 영역)

```nasm
mov dword ptr ss:[rbp-C],3
```
3을 넣는 것은 지역 변수 (stack 영역)
```nasm
call <JMP.&malloc>
mov qword ptr ss:[rbp-8],rax
… 생략…
mov rax,qword ptr ss:[rbp-8]
mov dword ptr ds:[rax],4
```
4를 넣는 것은 동적할당된 변수 (heap 영역)

잘 보면, 하드코딩된 상수 가상 메모리주소나, 레지스터에 저장된 가상메모리 주소값을 그대로 참조하는 것이 아닌
ds:[rax], ss:[rbp-8]처럼 세그먼트 레지스터 표기와 함께 있다.

이는 가상메모리 주소를 **세그멘테이션**(**segmentation**)을 거쳐 **선형 주소**(**linear address**)로 바꾸는 것을 나타낸다.

<br>
<h3>세그먼트 레지스터</h3>
아래는 64bit intel 환경에서 디버깅창에서 볼 수 있는 레지스터 화면이다.
<image src="/assets/x64 registers.PNG" width="70%">

사진에서 맨 아래에 있는 6개의 \*s로 끝나는 레지스터들이 세그먼트 레지스터다.

저 중 cs, ds, ss가 각각 code, data, stack 세그먼트에 대한 정보를 저장하고 있는 **세그먼트 레지스터**다.

<image src="/assets/segment register.png" width="50%">

세그먼트 레지스터는 위 사진처럼 x86기준 16bit 정보를 저장하고있다. 저장하고 있는 정보는 kernel 이 가지고 있는 **GDT**(**global descriptor table**)이나 LDT(local descriptor table)에 저장된 해당 세그먼트 descriptor가 저장된 index 번호와 RPL(request privilege level) 정보를 저장하고 있다.

세그먼트 레지스터는 세그먼트 디스크립터가 저장된 인덱스 번호를 저장하고 있어 **segment descriptor selector**라고도 불린다.

RPL은 현재 코드에서 요청하는 특권 모드를 나타내며, 인터럽트 발생시 cs 레지스터 내용은 발생하는 인터럽트 종류에 따라 OS 부팅 시 등록된 trap gate(page fault 등) 혹은 interrupt gate (division by zero 등) 에 등록된 code segement selector 내용으로 바뀌고, ss 레지스터 내용은 OS 부팅 시 초기화한 tss(task state segment) 구조체를 가리키는 tr 레지스터를 통해 ss 멤버 변수를 참조하여 RPL 0의 stack segment selector 내용으로 바꾸게 된다.

<h3>세그먼트 디스크립터</h3>
<image src="/assets/segment descriptor.png">

앞서 설명한 세그먼트 레지스터에 저장된 세그먼트 셀렉터가 GDT 혹은 LDT에 저장된 세그먼트 디스크립터를 가리킨다고 했는데, 위의 그림처럼 복잡하게 생겼다.

세그먼트 디스크립터가 가지고 있는 정보를 요약하자면,
1. 세그멘테이션의 기본 목적인 어떤 선형주소부터 어떤 선형주소까지 하나의 세그먼트인지 정보를 나타내게 된다(**base**, **limit**).
2. 해당 세그먼트에 접근할 수 있는 특권 레벨을 뜻 하는 **DPL**(**descriptor privilege level**)

16 비트 시절엔 세그멘테이션 기법을 통한 메모리 관리를 수행했지만, 32비트로 넘어오면서 세그멘테이션을 사용할 이유가 없어져 호환성 유지를 목적으로 기능을 남기고 있다. 각 프로세스마다 코드, 데이터, 스택 세그먼트의 범위를 구분해야하고, 유저 모드와 커널 모드 또한 구분해야하는 것이 16비트 시절 얘기라면, 지금 현재는 유저 모드 code, 유저 모드 data(stack 겸용), 커널 모드 code, 커널 모드 stack 4가지만 OS 부팅시 GDT에 초기화를 하고 모든 프로세스에서 같은 세그먼트 디스크립터를 사용하게 된다. 또한 base address와 limit를 지정하는 것이 의미 없어져 메모리의 모든 구간(0x00~0xffffffff)에 대해 참조 가능하도록 descriptor에 설정한다. 그래서 가상주소 -> 선형주소 과정에서 수치상 바뀌는 것은 전혀 없다.

32비트 기준 세그멘테이션 기법에서 유효한 기능은 **code segment의 DPL에 따른 현재 코드의 특권 모드 구분**이라 할 수 있다. 현재 실행 중인 코드가 커널 모드인지 유저 모드인지 구분하는 것은 코드 세그먼트 셀렉터가 가리키고 있는 GDT 상의 인덱스(이 gdt를 가리키는 레지스터를 gdtr이라고 한다)의 descriptor의 DPL이 0(kernel mode)인지 3(user mode)인지로 구분하게 되고, 이후 메모리 rw 권한 보호에 대해선 페이징 과정에서 이뤄지게 된다. 현재 코드의 특권 모드를 나타내는 이 DPL 값을 **CPL**(**current privilege level**) 이라고 한다.

물론, call gate니 뭐니 다른 기능도 있긴 하지만, 알아보지 않아서 pass
<br>

<h3>페이징을 통한 선형주소 -> 물리주소</h3>
많은 운영체제들이 페이징 기법을 통해 메모리 관리를 하며, 이는 사실 페이징을 통한 주소 변환은 하드웨어의 일이기 때문에 PC의 경우 인텔에서 제공하고 있는 아래의 페이징 옵션 중 운영체제가 어느 것을 고르는지에 따라 선형주소 -> 물리주소 변환 과정이 달라지게 된다.

1.  32bit (2-level paging)
2.  PAE(Physical addresss extension, 3-level paging)
3.  4-level

여기선 1번 옵션인 32bit paging 옵션 기준으로 설명하겠다. 나머진 어차피 확장이라..
아래 사진에서 32bit paging을 아주 잘 설명하고 있다.
<img src="/assets/paging.png">

CR3레지스터에 **PDT**(**page directory table**)을 저장하고 있고, PDT의 크기는 한 페이지의 크기인 4KB이다. 하나의 **PDE**(**page directory entry**)의 크기는 32bit 이므로 총 1024개의 PDE를 PDT에서 가질 수 있다.
하나의 PDE에서는 1024개의 **PTE**(**page table entry**)를 가지는 **PET**(**page entry table**) 를 가리키며, 각각의 PTE에 4KB크기의 물리 페이지 프레임을 나타내는 PFN(page frame number)를 저장한다. 32비트의 선형 주소 중 앞의 10bit는 PDT내에서 PDE의 index를 결정하는데에, 중간의 10bit는 해당 PDE가 가리키고 있는 page table 내에서 PTE의 index를 결정하고 해당 PTE에서 4KB 크기의 물리 페이지 번호가 결정된다. 나머지 12비트는 4KB 크기의 물리 페이지 내에서의 1바이트 단위의 memory access를 위한 offset으로 사용된다. 이렇게 하여 선형 주소가 물리 주소로 바뀌게 되는 것이다.

가상 메모리 주소 체계는 각 프로세스마다 서로 다른 paging table을 가짐으로써 프로세스간 서로 다른 독립적인 가상주소 공간을 갖게 한다. 각 프로세스마다 구분되는 PDT의 주소는 각 스레드를 구분하는 커널 스택에 PCB(process control block)형태로 저장되게 된다.

아래 사진에서는 PTE(혹은 PDE)의 구성을 나타낸다.

<image src="/assets/PTE.png">

아래는 각 주요 멤버들에 대한 설명이다.
- PFN : 20bit 크기로 PTE의 경우 사용될 실제 물리 페이지를 나타내며, PDT의 경우 그 다음 PET(page entry table)이 저장된 물리 페이지 넘버를 가리키게 된다.
- AVIL : 여분 비트다.
- PS : 이 비트가 활성화 되면 PDE에서 바로 4MB 크기의 page frame을 가리킬 수 있게 된다. 메모리 주소 변환 과정에서 메모리 참조 횟수가 줄어들어 오버헤드가 적어진다.
- D(dirty) : 변경 여부 flag 저장.
- A(access) : 접근 여부 flag 저장.
- US(user-supervisor) : 유저 프레임인지 커널 프레임인지 구분. 유저 모드에서 커널 프레임 접근 시 page fault 발생
- RW(read, write) : 읽기, 쓰기 권한. 권한 침범 시 page fault 발생
- P(present) : 현재 유효한 물리 페이지 번호를 할당 받았는지 여부를 나타냄. swapping 구현 시 이용됨

<h2>캐싱</h2>
메모리 참조는 CPU에서 여러차례 사이클을 기다려야하는 오버헤드가 큰 작업이다. 또한 페이징과 같은 주소 변환 과정에서 메모리 참조는 많이 일어나게 된다. 느린 메모리 참조를 계속 하는 것이 아닌, 좀 더 읽기와 쓰기가 빠른 캐쉬에다가 저장하고 사용하여 메모리 참조 오버헤드를 줄일 수 있다. 이러한 과정을 캐싱이라고 한다.
캐싱을 하드웨어적으로 구현하는 방법은 크게 아래 3가지이다.

1.  direct mapping
2.  fully associative mapping
3.  set associative mapping

### Direct mapping
- 동일한 라인번호면 동시 저장 불가
- 하드웨어적 구현 쉬움
- 비효율적
<image src="/assets/direct mapping.png">

### Fully associative mapping
- 메모리 주소 상관없이 동시 캐싱 가능
- 리스트 내에서 탐색해야함
- 위 과정은 하드웨어적 병렬처리로 구현
- 구현 복잡
- 캐시 히트율 높음
- TLB(translation lookaside buffer) 등에서 사용됨
<image src="/assets/fully associative mapping.png">

### Set associative mapping
- 위 2개의 절충안
- 가장 많이 차용됨
<image src="/assets/set associative mapping.png">

## 캐싱이 효과가 있는 이유
캐시 사용 시 캐시 히트율이 유의미한 수치로 나오는 이유는 공간 지역성(spacial locality), 시간 지역성(temporal locality) 으로 설명할 수 있다.
-  공간 지역성
    - 한번 참조 되었던 지역은 인접한 지역이 또 참조될 가능성이 높음
    - 코드 실행, 배열 참조, 지역 변수 참조 등
-  시간 지역성
    - 한번 참조 되었던 지역은 짧은 시간 내에 재참조 될 가능성이 높음
    - 반복문 실행 등

## swapping
프로세스를 올릴 수 있는 물리 메모리 크기는 한정적이다. 유휴 상태에 있는 프로세스 등은 다시 보조 기억 장치에 저장하여 새롭게 실행될 프로세스가 페이지 할당을 받을 수 있도록 해야한다. 아래에선 어떤 페이지가 스왑 아웃 되어야하는지 여러가지 생각해 볼 수 있는 정책들을 기술한다.
1. FIFO
    - 먼저 할당받은 페이지가 먼저 스왑 아웃됨
    - 페이지의 중요도, 참조율 등을 전혀 고려하지 않음
2. 랜덤
    - 최악은 막음
3. LRU
    - 참조율을 카운팅하여 가장 사용하지 않는 페이지 순으로 스왑 아웃 시켜버림
    - 가장 많이 사용됨
    - 실제 구현은 어려워 근사된 알고리즘인 시계 알고리즘으로 구현
### 스왑핑에서의 이슈
- thrashing
    - 프로세스가 요구한 페이지 총량이 물리 메모리 크기를 넘어서 운영체제가 끊임없이 스왑핑을 하는 과정에서 메모리 속도가 아닌 하드디스크 속도로 작동하는 현상
    - 실행되는 프로세스 수를 줄여서 선택과 집중으로 해결
    - 사실 이쯤 되면 물리 메모리 증설을 고려해야함

### 캐쉬 교체 정책
- LRU(least-recently-used)
  - 최저 빈도 정책
  - 그냥 제일 안쓰는거 먼저 교체해버리는거임
  - N개 크기의 캐쉬에서 n+1 크기의 배열 반복 접근하면 최악 히트율
- 랜덤
  - 최악은 막음

## 여러가지 고전 이슈
### 세그멘테이션에서의 이슈
메모리 청크를 관리해야함. base와 bound를 연결리스트로 관리할 수 있다. 이러한 상황에서 주어진 사이즈 만큼의 세그먼트를 할당해야할 때 어떤 전략을 생각해볼 수 있는지 알아보자
1. 최적 적합 (best fit)
    - 요청된 메모리 크기와 같거나 더 큰 메모리 청크를 찾는다
    - 리스트 전체 순회 해야한다
    - 아주 작은 메모리 청크들로 인한 외부 단편화 문제
2. 최악 적합 (worst fit)
    - 가장 큰 메모리 청크를 찾는다.
    - 리스트 전체 순회를 해야한다.
    - 남는 청크 자체의 메모리 크기가 커지긴 하는데, 외부 단편화 문제는 피할 수 없다.
3. 최초 적합 (first fit)
    - 요청된 메모리 크기를 할당할 수 있는 최초의 메모리 청크를 찾아서 할당한다.
    - 할당 속도가 빠르다. (전체 탐색 x)
    - 연결리스트 초반 작은 청크들의 쏠림 현상이 생길 수 있음
    - 메모리 주소 기반 정렬로 해결한다.
4. 다음 적합 (next fit)
    - 탐색 포인터 저장 후 환형 탐색
    - 작은 청크들이 분산됨

연결 리스트 말고 다른 자료구조는 아래와 같이 생각할 수 있다.

1. 개별 리스트
    - inode, lock 같은 객체들을 미리 초기화 하여 리스트로 관리해야함
    - 얼마나 초기화 해놔야하는지 모름
2. 슬랩 할당기 (slab allocator)
    - inode, lock 객체들을 초기화 하여 개별 리스트로 관리해야함
    - 요청이 많아지면 상위 할당기에 요청해서 더 많이 초기화해놓음
    - 요청이 0이 되면 상위 할당기가 회수해감
    - 객체당 잦은 초기화나 반납을 피할 수 있음
    - 말이 쉽지
3. 버디 할당
    - 처음에 2^n개 크기의 메모리를 만들고 요청된 size의 메모리 할당 위해 재귀적 반띵함
    - 내부 단편화는 잘 해결됨
    - 병합도 재귀적으로

### 다른 페이징 기법
1. 역페이징 기법(inverted page table)
    - 프로세스마다 구분된 페이지 디렉터리 테이블을 갖는 것이 아닌, 하나의 페이지 테이블을 관리해야함
    - 각 페이지 프레임마다 어떤 프로세스에서 사용하고 있는지, 가상 주소는 무엇인지 정보를 저장하고 있고, 탐색을 통해 매번 주소 변환 시 해당하는 페이지 프레임 주소를 찾으면서 주소 변환한다.
    - 탐색 과정은 hashing으로 최적화 가능

------------------------
## File System

### 파일이란?
운영체제를 통해 물리 장치들로 매핑되고, 일반적으로 비휘발적 특성을 지녀 전원이 끊어진 상황에서도 정보들을 영구히 보존 가능하다.

### 파일의 속성(metadata)
 * 이름 : 사람이 읽을 수 있는 형태로 유지되는 정보
 * 식별자 : 파일 시스템이 파일을 식별하는 고유의 번오 (Primary key)
 * 타입 : 여러 타입을 지원하는 시스템에 필요. 운영체제는 파일 타입을 통해 합당한 연산을 실행한다. 확장자는 파일이름을 통해 파일 타입을 나타내도록 한 것이다.
 * 위치 : 장치 내에 파일의 위치를 가리키는 포인터
 * 크기 : 파일의 크기
 * 보호 : 접근 제어 정보
 * 시간, 날짜, 사용자 식별 : 생성, 최근 변경, 최근 사용자 등의 대한 정보

 ## 파일 연산
 * 생성 : 사용할 수 있는 공간을 찾고 파일을 할당한다.
 * 쓰기 : 파일이름과 기록된 정보를 명시하는 시슽메 콜이 호출된다.
 * 읽기 : 시스템 콜을 통해 파일을 읽기 가능하다. 파일의 위치포인터를 통해 다양한 연산이 가능하다.
 * 위치 재설정 : 항목의 주소를 이용해서 현재 파일의 위치를 주어진 값으로 변경한다.
 * 삭제 : 지명된 파일을 디렉터리에서 찾고, 차지하고 있던 공간을 방출하고 디렉터리 항목을 삭제한다.
 * 절단 : 파일의 내용을 지우고 속성만을 남긴다.


 운영체제에서는 열린 파일의 정보를 갖는 **열린 파일 테이블(open file table)** 을 유지한다.
 시스템 콜 open()을 이용하여 테이블의 정보를 얻을 수 있다.


### 파일 접근 방법

1. 순차 접근
파일의 정보가 마치 테이프를 재생하는 것과 같이 레코드 순서로 처리된다. 편집기 혹은 컴파일러 등이 일반적으로 이러한 형식으로 파일을 접근한다.

- 읽기 : 파일의 다음부분부터 차례로 읽어 나가며 자동적으로 현재 위치를 추적하는 offset이 증가된다.
- 쓰기 : 파일의 끝에 추가하며 파일 포인터는 추가된 파일의 끝으로 이동한다. offset을 맨 앞 혹은 맨 뒤로 옮길 수 있고, 정수 n개의 레코드 만큼 앞 뒤로 건너 뛸 수 있다.

2. 직접 접근
파일의 어떠한 블록이라도 직접 접근할 수 있다. 직접 접근을 위해서는 파일은 고정 길이의 논리 레코드의 집합으로 정의되어야 한다.
디스크는 임의의 파일 블록에 임의적 접근을 허용하기에 직접 접근 방법은 파일의 디스크 모델에 기반한다. 이 방식에서 파일은 번호를 갖는 일련의 블록 또는 레코드로 간주된다.

3. 기타 접근 방법
직접 접근 파일에 기반을 두고 색인을 구축한다. 크기가 큰 파일을 입출력 탐색이 가능하게 한다.


### 저장 장치의 구조
범용 컴퓨터 시스템은 다수의 저장장치를 가지고 그 장치들은 파일 시스템으로 저장할 수 있는 볼륨으로 분할된다. 파일시스템이 없을 수도 있으며, 다양한 파일시스템을 가질 수도 있다.

* 볼륨 : 파일 시스템을 포함하고 있는 임의의 개체, 각 볼룸은 논리적인 가상 디스크로 취급될 수 있다. 하나의 볼륨에는 하나 이상의 운영체제를 저장하고 부팅, 실행시킬 수 있다.
* 디바이스 디렉터리(디렉터리) : 볼륨 내에 있는 모든 파일에 대한 이름, 위치 등의 속성(metadata)를 기록한다.
* 파티션 : 연속된 저장 공간을 하나 이상의 연속되고 독립적인 영역으로 나누어서 사용할 수 있도록 정의한 규약


### 디렉터리의 구조
1. 1단계(단일) 디렉터리
가장 간단한 구조의 디렉터리. 파일이 많아지거나 다수의 사용자가 사용할 경우 심각한 제약이 따른다. 각 파일은 서로 유일한 이름을 가진다.

2. 2단계 디렉터리
각 사용자에게 개별적인 디렉터리를 만들어 준다.
- UFD(User File Directory) : 자신만의 사용자 파일 디렉터리, 비슷한 구조를 가지고 있지만 오직 한 사용자만의 파일을 저장한다.
- MFD(Master File Directory) : 사용자의 이름이나 계정 번호로 색인(index)되어 있고, 각 엔트리는 사용자의 UFD를 가리킨다.

특정한 파일을 참조할 시 사용자의 UFD 에서만 탐색하므로 파일 이름이 충돌하는 문제가 사라진다.
다른 사용자의 파일에 접근해야 하는 경우는 단점이 된다.

3. 트리 구조 디렉터리
2단계 구조를 확장하여 만들 수 있다. 사용자들이 자신의 서브 디렉토리를 만들어서 파일을 구성할 수 있게 한다. 트리 구조는 하나의 루트 디렉터리를 가지며 시스템의 모든 파일은 고유 경로를 가진다. 각 항목은 한 비트를 이용하여 일반 파일인지 디렉터리인지 구분한다.

통산적으로 각 프로세스는 **현재 디렉터리**를 가진다.
디렉터리 경로명에는 절대 경로명과 상대 경로명이 있다.

4. 비순환 그래프
비순환 그래프는 디렉터리들이 버스 디렉터리와 파일들을 공유할 수 있도록 허용한다.
트리구조의 디렉터리를 공유가능하도록 한 형태


절대경로명/상대경로명을 이용하여 **링크** 라고 불리는 새로운 디렉터리 항목을 만들 수 있다.
단순한 트리 구조보다는 융통성이 있는 대신에 더 복잡하다.


파일을 삭제할 때 대상이 없는 포인터(dandling pointer) 를 남긴다.
참조되는 파일에 참조 계수를 두어 계산한다. 참조 계수가 0이 되면 현재 파일을 참조하는 링크가 존재하지 않으므로 파일을 삭제할 수 있다.


5. 일반 그래프 디렉터리
순환 그래프 형태의 구조. 순환이 허용되면 무한 루프에 빠질 가능성이 있다. 이런 문제를 해결하기 위해 하위 디렉터리가 아닌 파일에 대한 링크만을 허용하거나 가비지 컬렉션을 이용하여 전체 파일 시스템을 순회하여 접근 가능한 모든 것을 표시한다.


### 파일 시스템 마운팅
파일이 사용되기 전에 열려야 하는 것처럼 파일 시스템은 프로세스들에 의해 사용되기 전에 장착(mount) 되어야 한다.

**마운트 과정**
1. 운영체제에게 장치 이름과 파일 시스템을 부착할 수 있는 파일 구조 내의 위치가 주어진다. 일반적으로 마운트 포인트는 장착되는 파일 시스템이 부착될 비어있는 디렉토리이다.
2. 운영체제는 장치가 유효한 파일 시스템을 포함하는지 확인 한다. 그 과정은 장치 드라이버가 장치 디렉토리를 읽고 디렉토리가 유효한 포맷을 가지고 있는지 확인하도록 요청함으로써 이루어진다.
3. 운영체제는 파일 시스템이 지정된 마운트 포인트에 장착되었음을 디렉토리 구조에 기록한다. 이 기법은 운영체제가 디렉토리 구조를 순회하고 파일 시스템을 적절히 교체할 수 있게 한다.

### 파일 공유
디렉터리 구조가 사용자 간의 파일 공유를 허용한다면, 시스템은 파일 공유를 중재해야 한다. 대부분의 시스템은 파일/디렉터리의 소유자, 그룹이라는 개념을 사용하는 형태로 발전해 왔다.
UNIX 시스템의 소유자는 파일에 대한 모든 작업을 실행할 수 있지만 그룹 멤버는 일부 작업만을 실행할 수 있다.

### 접근 제어

- 타입
사용자가 어떤 접근 타입을 가지고 오는지에 따라 파일 연산을 통제시킬 수 있다.
* 읽기
* 쓰기
* 실행
* 추가
* 삭제
* 리스팅

파일과 디렉터리에 접근 제어 리스트를 둔다(ACL) 특정 사용자가 어떤 파일에 접근할 경우 리스트를 보고 허용 여부를 결정한다.

---

# MassStorage Management



#### Physical Disk Structure

- head : hard disk를 읽어주는 장치(하나의 플레터 위아래에 달려있음) - synchronous
- platter : hard disk를 구성할 때 달려있는 원판
- track & sector : track은 데이터를 저장하는 공간이고 이를 쪼갠 것이 sector이다. 보통 sector는 512byte이다. 각 트랙별로 sector의 갯수는 같음(편의상 이렇게 만듬)
- spindle motor : platter를 회전시켜주는 장치. 회전 수의 경우 보통 RPM단위로 표시함.
- cylinder : platter들의 track동심원 크기의 track의 집합. (파일 읽기 효율성을 위해서 보통 파일은 같은 실린더에 배치하는 것이 효과적)
- Seek, Rotation, Data Transfer
  - head를 옮겨가면서 찾아가는 과정이 Seek (delay가 가장 크다.)
  - platter가 도는 것을 rotation
  - 원하는 위치에서 head가 데이터를 읽는 것을 data transfer
- Disk bandwidth : 디스크의 성능을 나타내는 수단으로 단위 시간당 전송된 바이트 수 (Seek time을 줄이는 것을 목표로한다.)
  <img src="/assets/hard_disk_structure.png">



#### Scheduling

1. FCFS : 무조건 들어와있는 순서대로 읽어간다.
   <img src="/assets/disk_fcfs.png">
2. SSTF : seek time이 짧은 것을 먼저 읽는다. (starvation의 위험이 있음.)
   <img src="/assets/disk_sstf.png">
3. SCAN
   - 한방향으로 head를 진행시키고 이후 반대 방향으로 head를 진행시킴
   - 바깥 쪽은 1회, 가운데는 2회의 기회가 있음. unfair wait time
     <img src="/assets/disk_scan.png">
4. C-SCAN : 한방향으로만 계속해서 진행 (뒤에 작업이 없는데 계속 진행 - 손해 발생)
   <img src="/assets/disk_cscan.png">
5. C-LOOK : 한방향으로만 진행하면서 맨 마지막 작업 뒤 다시 초기 위치로 복귀
   <img src="/assets/disk_clook.png">



#### bad block & swap space

- bad block : 만약 block이 죽으면 다른 블럭(spare sector)으로 대체를 시키고 다음부터 요청이 들어오면 새로운 sector로 안내한다.
- swap space
  - 부족한 메인메모리의 부하를 줄여주기 위해서 존재
  - 가상의 메모리를 가지고 있는 것으로 보이게 하고 실제로 공간은 hard disk에 존재
  - 프로세스가 필요에 의해서 swap과 main을 왔다갔다 한다.
    <img src="/assets/swap_space.png">



#### RAID (redundant array of inexpensive disks)

- 하드디스크 용량이 부족할 경우 용량 증설을 위해서 사용.
- 하드디스크의 장애로 인한 데이터 손실을 예방하고자 데이터의 안정성을 확보.



1. RAID0

   - concatenate : 두개 이상의 데이터를 순차적으로 쓰는 방법
     - 장점 : 용량증설 가능
     - 단점 : 어떤 디스크라도 장애 발생시 복구 불가, 패리티(오류검출) 불가
   - stripe : 두개 이상의 디스크를 랜덤하게 쓰는 방법
     - 장점 : 여러 디스크를 분할 하여 사용. I/O performance 증가.
     - 단점 : 구성하려면 기존 데이터 모두 삭제 후 구성. 이외 concatenate방식과 동일

2. RAID1 (Mirror)

   - 중복하여 데이터를 보존하게 하여 최소 동일한 용량의 2개의 디스크 필요.
     - 장점 : 하나의 디스크 및 데이터가 장애가 생겨도 백업 데이터가 있어 문제 X
     - 단점 : 가용 용량이 절반이 되고 쓰기 속도가 오래 걸림.

3. RAID2

   - RAID0와 같이 stripe방식임.
   - 에러 체크와 수정을 위해 hamming code를 사용.
   - 하드웨어적으로 지원하지 않기에 별도의 드라이브에 ECC(error correction code)를 저장, 하지만 ECC를 위한 드라이브가 손상되는 문제 발생 가능.

4. RAID3, RAID4

   - RAID0와 같이 stripe 방식
   - 별도의 디스크에 패리티 정보를 저장하여 에러 체크 및 수정을 함.
   - RAID3은 데이터를 바이트 단위로 나누어 디스크에 동등하게 분산 기록. (동기화 필수)
   - RAID4는 데이터를 블록 단위로 나눠 기록하여 완벽하게 동일하지는 않음.

5. RAID5

   - stripe로 구성된 디스크내에서 패리티 정보를 저장하여 처리함.
   - 만약 한개의 하드가 고장나도 다른 하드들을 통해 복구 가능

6. RAID6

   - RAID5와 같은 개념
   - 2차 패리티를 넣어 2개의 하드가 고장나더라도 복구 가능. 더욱 안정

   <img src="/assets/RAID.png">


