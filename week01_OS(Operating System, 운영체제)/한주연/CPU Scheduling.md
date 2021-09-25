# CPU Scheduling

## 스케쥴링 이란?

> Ready Queue에 있는 프로세스들 중 어떤 프로세스를 CPU에게 할당해야 하는지를 결정하는 일

스케쥴링이 필요한 이유는 CPU 이용율을 최대화 하기 위해서이다.

## CPU 스케줄링 척도

1) **CPU 이용률(Utilization)** : CPU 수행 시간 / 시스템 구동 시간 (%) (↑)

2) **처리율(throughput)** : 단위 시간당 완료되는 프로세스 수 (↑)

3) **반환 시간(turnaround time)** : 프로세스가 시스템에 진입하여 완료되기까지의 시간(↓)

4) **대기 시간(waiting time)** : 준비 큐에서 대기하는 시간 (↓)

-> CPU 스케쥴링 알고리즘에 따라 실질적으로 영향받는 요소

5) **반응 시간(response time)** : 작업을 제출한 후 첫 응답이 나올 때까지의 시간 (↓)

-> 대화식 시스템의 경우 반환 시간보다 적합

## 프로세스 상태

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e1a653a1-9019-4126-b98d-c7c58a74d7cd/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e1a653a1-9019-4126-b98d-c7c58a74d7cd/Untitled.png)

ready : 프로세스가 CPU를 기다리는 상태

running : 프로세스가 CPU를 할당받아 명령어를 수행중인 상태

waiting : 프로세스가 CPU를 할당 받아도 당장 실행할 수 없는 상태

- 비선점 스케줄링 : `I/O or Event wait`
- 선점 스케줄링 : `Interrupt`

### ready와 waiting의 차이?

ready도 waiting과 똑같이 상태의 변화를 기다리고 있는 것.

- ready는 단어에서 알 수 있듯 실행 준비가 다 된 상태에서 기다리는 것
- waiting은 I/O나 다른 이벤트가 발생이 끝나기를 기다리는 것.

waiting은 프로세스 A가 CPU를 할당받고(running상태) 명령어를 실행하다 I/O 작업을 해야 하는 경우, 디스크 I/O 작업은 CPU 처리 속도에 비해 오래 걸리는 작업이기 때문에 디스크 I/O 작업 동안은 CPU를 점유하고 있어도 다음 명령어를 수행하지 못합니다. ㅡ> CPU 낭비

때문에 디스크 I/O 작업을 하는 프로세스는 CPU를 반납하고 장치 큐에가서 줄을 서게 된다 (waiting → ready)

## 선점 / 비선점 스케줄링

- 선점 (preemptive) : OS가 CPU의 사용권을 선점할 수 있는 경우, 강제 회수하는 경우
- 비선점 (nonpreemptive) : 프로세스 종료 or I/O 등의 이벤트가 있을 때까지 실행 보장 (처리시간 예측 어려움)

### 비선점 스케쥴링

1. FCFS (First Come First Served)
    - 큐에 도착한 순서대로 CPU 할당
    - 실행 시간이 짧은 게 뒤로 가면 평균 대기 시간이 길어짐

    ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d3332d7c-73b3-4c75-b880-e5472fee21d0/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d3332d7c-73b3-4c75-b880-e5472fee21d0/Untitled.png)

2. SJF (Shortest Job First)
    - 수행시간이 가장 짧다고 판단되는 작업을 먼저 수행, 동일할 경우는 선입선출 스케쥴링을 적용
    - FCFS 보다 평균 대기 시간 감소, 짧은 작업에 유리

    ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/dfa64806-c291-4bda-b92e-edde0bc03e20/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/dfa64806-c291-4bda-b92e-edde0bc03e20/Untitled.png)

### 선점 스케쥴링

1. 선점 SJF 스케쥴링
    - 최소 잔여 시간 우선(Shortest Remaining Time First) 스케쥴링

    ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5229389b-7331-4803-a0bb-14b391cb1e66/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5229389b-7331-4803-a0bb-14b391cb1e66/Untitled.png)

2. Priority Scheduling
    - 정적/동적으로 우선순위를 부여하여 우선순위가 높은 순서대로 처리
    - 우선 순위가 낮은 프로세스가 무한정 기다리는 Starvation 이 생길 수 있음
    - Aging 방법으로 Starvation 문제 해결 가능
    에이징(Aging) - 체류 시간에 비례하여 우선순위를 높여 주는 방법
3. Round Robin
    - FCFS에 의해 프로세스들이 보내지면 각 프로세스는 동일한 시간의 `Time Quantum` 만큼 CPU를 할당 받음

        → `Time Quantum` or `Time Slice` : 실행의 최소 단위 시간

    - 시분할 시스템 성질을 가장 잘 활용함
    - 할당 시간(`Time Quantum`)이 크면 FCFS와 같게 되고, 작으면 문맥 교환 (Context Switching) 잦아져서 오버헤드 증가

    ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d25658f1-3e6c-4fa9-a924-437bb2255f06/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d25658f1-3e6c-4fa9-a924-437bb2255f06/Untitled.png)

4. Multilevel-Queue (다단계 큐)

    Ready Queue를 여러 개의 Queue로 분류하고, 각각의 Queue 내에 독립적인 스케쥴링 기법을 적용시키고, 각각의 Queue사이에도 별도의 스케쥴링 기법이 존재하는 스케쥴링 방식이다. 

    큐 사이의 스케쥴링 기법으로는 Priority 기법을 적용할수도, Time Slice 방식을 적용할수도 있다.

    ![https://user-images.githubusercontent.com/13609011/91695428-16a2f480-eba9-11ea-8d91-17d22bab01e5.png](https://user-images.githubusercontent.com/13609011/91695428-16a2f480-eba9-11ea-8d91-17d22bab01e5.png)

    - 작업들을 여러 종류의 그룹으로 나누어 여러 개의 큐를 이용하는 기법

        ![https://user-images.githubusercontent.com/13609011/91695480-2a4e5b00-eba9-11ea-8dbf-390bf0a73c10.png](https://user-images.githubusercontent.com/13609011/91695480-2a4e5b00-eba9-11ea-8dbf-390bf0a73c10.png)

    - 우선순위가 낮은 큐들이 실행 못하는 걸 방지하고자 각 큐마다 다른 `Time Quantum`을 설정 해주는 방식 사용
    - 우선순위가 높은 큐는 작은 `Time Quantum` 할당. 우선순위가 낮은 큐는 큰 `Time Quantum` 할당.
5. Multilevel-Feedback-Queue (다단계 피드백 큐)

    ![https://user-images.githubusercontent.com/13609011/91695489-2cb0b500-eba9-11ea-8578-6602fee742ed.png](https://user-images.githubusercontent.com/13609011/91695489-2cb0b500-eba9-11ea-8578-6602fee742ed.png)

    - 멀티레벨 큐와 비슷하나 프로세스가 다른 큐로 이동할 수 있음
    - **aging**기법을 구현가능, 낮은 우선순위에 있는 프로세스를 높은 우선순위 큐로 승격시키는 등.
    - 다단계 큐에서 자신의 `Time Quantum`을 다 채운 프로세스는 밑으로 내려가고 자신의 `Time Quantum`을 다 채우지 못한 프로세스는 원래 큐 그대로

        → Time Quantum을 다 채운 프로세스는 CPU burst 프로세스로 판단하기 때문

    - 짧은 작업에 유리, 입출력 위주(Interrupt가 잦은) 작업에 우선권을 줌
    - 처리 시간이 짧은 프로세스를 먼저 처리하기 때문에 Turnaround 평균 시간을 줄여줌

    ### 멀티프로세서 스케쥴링 ( Multiple-Processor Scheduling )

    프로세서 또는 코어가 여러개인 경우에 여러개의 CPU에 대해 다루어지는 스케쥴링

    ## 참고

    [CPU 스케쥴링](https://devsophia.tistory.com/entry/CPU-%EC%8A%A4%EC%BC%80%EC%A5%B4%EB%A7%81)

    [CPU Scheduling | 👨🏻‍💻 Tech Interview](https://gyoogle.dev/blog/computer-science/operating-system/CPU%20Scheduling.html)

    [[OS] Cpu 스케쥴링](https://velog.io/@secho/OS-Cpu-%EC%8A%A4%EC%BC%80%EC%A5%B4%EB%A7%81)

    [[운영체제] 5장 CPU 스케쥴링(CPU Scheduling)](https://m.blog.naver.com/three_letter/220334644682)