# 큰 주제: OS(Operating System, 운영체제) <br>

## 소 주제1: 프로세스와 스레드<br>

## 소 주제2: (CPU) 스케쥴링 기법 ex) FCFS, SJF 등 <br>

참고1: https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/master/OS <br>
참고2 대학교 공부한 것 <br>
참고3: https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Operating%20System/Process%20vs%20Thread.md <br>

## 소 주제1: 프로세스와 스레드<br>

### 프로세스(Process)

- 프로세스는 실행 중인 프로그램으로 디스크로부터 메모리에 적재되어 CPU의 할당을 받을 수 있는 것이다.
- 운영체제(OS)로부터 주소 공간, 파일, 메모리 등을 할당 받으며 이것들을 총칭하여 프로세스라고 한다.
- 구체적으로 살펴보면 프로세스는 함수의 매개변수, 복귀 주소와 로컬 변수와 같은 임시 자료를 갖는 프로세스 스택과 전역 변수들을 수록하는 데이터 섹션을 포함한다. 또한 프로세스는 프로세스 실행 중에 동적으로 할당되는 메모리인 힙을 포함한다.

#### 프로세스 제어 블록(Process Control Block, PCB)

- kernel의 data structure(자료 구조), 큰 table 이라고 생각하면 된다.
- process의 state, pointer, PC(Program Counter), register 값, 우선 순위, 메모리 할당받은 양, Pid, file open 등을 기록한다.
- Pid는 서로 다른 process를 구분하기 위해 존재한다.

### 스레드(Thread)

- 스레드는 프로세스의 실행 단위이다.
- 한 프로세스 내에서 동작되는 여러 실행 흐름으로 프로세스 내의 주소 공간이나 자원을 공유할 수 있다.
- 스레드는 스레드 ID, 프로그램 카운터, 레지스터 집합, 그리고 스택으로 구성된다.
- 같은 프로세스에 속한 다른 스레드와 코드, 데이터 섹션, 그리고 열린 파일이나 신호와 같은 OS 자원들을 공유한다.
- 하나의 프로세스를 다수의 실행 단위로 구분하여 자원을 공유하고 자원의 생성과 관리의 중복성을 최소화하여 수행 능력을 향상시키는 것을 멀티스레딩이라고 한다. 이 경우 각각의 스레드는 독립적인 작업을 수행해야 하기 때문에 각자의 스택과 PC 레지스터 값을 갖고 있다.

#### 장점

- (Process에 비해) 응답성(Responsiveness)이 좋다, Context Switch가 짧다.
- resource sharing으로 인해 경제적이다. 다른 thread와 주소 공간, code, global variable, heap, OS resource 등을 공유하기 때문이다. (register, PC, SP, stack은 따로 가진다)

#### 프로세스와 스레드

좀 러프하게 예를 들면

- 곰플레이어: 1개의 프로세스
- 자막, 사운드, 영상: 각각 1개의 스레드

## 소 주제2: (CPU) 스케쥴링 기법 ex) FCFS, SJF 등

### FCFS(First Come First Served)

#### 특징

- FIFO, Run-Until-Done
- 먼저 온 고객을 먼저 서비스 해주는 방식, 즉 먼저 온 순서대로 처리
- 비선점형(Non-Preemptive) 스케쥴링: 일단 CPU를 잡으면 CPU burst가 완료될 때까지 CPU를 반환하지 않는다. 할당되었던 CPU가 반환될 때만 스케쥴링이 이루어진다.
- Overhead는 작은 편에 속한다.

#### 문제점

- convoy effect: 소요시간이 긴 프로세스가 먼저 도달하여 효율성을 낮추는 현상이 발생한다. 즉 순서에 따라 차이가 크다.

### SJF(Shortest - Job - First)

#### 특징

- 다른 프로세스가 먼저 (혹은 동시에) 도착했어도 CPU burst time이 짧은 프로세스에게 우선 할당한다.
- 비선점형(Non-Preemptive) 스케쥴링이다.

#### 문제점

- starvation: 효율성을 추구하는게 가장 중요하지만 특정 프로세스가 지나치게 차별받으면 안된다. 이 스케쥴링은 극단적으로 CPU 사용이 짧은 job을 선호하기 때문에 사용 시간이 긴 프로세스는 CPU를 할당받기가 힘들다.
- 또 누가 가장 짧은 process인지 알기 어렵다.

### SRTF(Shortest Remaining Time First)

#### 특징

- 새로운 프로세스가 도착할 때마다 새로운 스케줄링이 이루어진다.
- 선점형(Preemptive) 스케줄링: 현재 수행 중인 프로세스의 남은 burst time보다 더 짧은 CPU burst time을 가지는 새로운 프로세스가 도착하면 CPU를 뺐긴다.
- 제대로 동작한다면 이상적이지만, overhead 등이 높고, 실제로 어떤 process가 짧은지 매번 계산하기가 힘들어서 구현이 사실상 불가능하다.

#### 문제점

- starvation
- 새로운 프로세스가 도달할 때마다 스케줄링을 다시하기 때문에 CPU burst time(CPU 사용 시간)을 측정할 수가 없다.

### Priority Scheduling

#### 특징

- 우선순위가 가장 높은 프로세스에게 CPU를 할당하는 스케줄링이다. 우선순위란 정수로 표현하며, 숫자가 작을 수록 우선순위가 높다.
- 선점형 스케줄링 방식: 더 높은 우선순위의 프로세스가 도착하면 실행 중인 프로세스를 멈추고 CPU를 선점한다.
- 비선점형 스케줄링 방식: 더 높은 우선순위의 프로세스가 도착하면 Ready Queue의 Head에 넣는다.

#### 문제점

- starvation
- 무기한 봉쇄(Indefinite blocking): 실행 준비는 되어있으나 CPU를 사용 못하는 프로세스를 CPU가 무기한 대기하는 상태이다.

#### 해결책

- aging: 아무리 우선순위가 낮은 프로세스라도 오래 기다리면 우선순위를 높여준다.

### Round Robin(RR)

#### 특징

- 현대적인 CPU 스케줄링
- 각 프로세스는 동일한 크기의 할당 시간(Time Quantum)을 갖는다.
- 할당 시간이 지나면 프로세스는 선점당하고 ready queue의 제일 뒤에 가서 다시 줄을 선다.
- RR은 CPU 사용시간이 랜덤한 프로세스들이 섞여있을 경우에 효율적이다.
- RR이 가능한 이유는 프로세스의 context를 save할 수 있기 때문이다.

#### 장점

- Response time이 빨라진다: n개의 프로세스가 ready queue에 있고 할당시간이 q(time quantum)인 경우 각 프로세는 q 단위로 CPU 시간의 1/n을 얻는다. 즉, 어떤 프로세스도 (n-1)q time unit 이상 기다리지 않는다.
- 프로세스가 기다리는 시간이 CPU를 사용할 만큼 증가한다. 공정한 스케줄링이라고 할 수 있다.

#### 주의할 점

- 설정한 time quantum이 너무 커지면 FCFS와 같아진다. 또 너무 작아지면 스케줄링 알고리즘의 목적에는 이상적이지만 잦은 context switch로 overhead가 발생한다. 그렇기 때문에 적당한 time quantum을 설정하는 것이 중요하다.

---

Q1. 1종류 이상의 스케쥴링 기법의 종류와 그에 대한 설명 가능할까요?<br>
A1. 위의 설명 참고

Q2. 멀티 스레드가 필요한, 유용한 분야가 있을까요? 있다면 이유를 함께 설명해주세요<br>
A2.

- 웹 브라우저에 적용할 수 있습니다. 예를 들어 웹 브라우저에서 영상 하나를 로딩하는데 오래걸릴 때, 멀티스레드 환경이라면 다른 스레드가 이미지나, 텍스트 등을 로딩하여서 사용자와 상호작용이 가능하게 됩니다.<br>
  (출처: https://ko.wikipedia.org/wiki/%EB%A9%80%ED%8B%B0%EC%8A%A4%EB%A0%88%EB%94%A9)
- 반복적인 작업이 필요한 곳에 유용할 것 같습니다. 예를 들어 비행기 날개를 부분으로 쪼개서 계산한다거나, 날씨를 지역 별로 쪼개서 계산하는 등입니다. (이유는 내가 안적어둬서 모르겠다, 검색해도 안나옴)
  (출처: 대학교 수업시간)
- 안정성이 중요한 곳에 활용할 수 있을 것 같습니다. 공장에서 어떤 파트에 문제가 난다면 라인스톱이 발생할 것인데, 이를 멀티 스레드를 활용하여 생산하고 있었다면, 문제가 생겨도 다른 부분이 이를 우회하여 처리할 수 있기 때문입니다.
  (출처: 검색결과 https://gall.dcinside.com/mgallery/board/view/?id=war&no=1799133 여기 안에 상세한 출처가 적혀있음)

---

### to 최민수 피드백

1. 잘못된 지식(뮤택스, 멀티 프로세스 등)
2. 예시는 좋았다.
