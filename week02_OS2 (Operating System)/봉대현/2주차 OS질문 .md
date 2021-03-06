# 2주차 OS



# 질문 후보

1. 외부 단편화에 대해서 설명하시고 어떤 방법으로 이것을 해결할 수 있나요??
- 메모리가 할당되고 해제되는 작업이 반복될때 작은 메모리 중간중간에 사용하지 않는 메모리가 많이 존재해서 총 메모리 공간은 충분하지만 실제로 할당할 수 없는 문제입니다.

→ compaction 방법으로 해결가능 : 작은 공간들을 모아서 연속적인 공간으로 만드는 작업 비용이 많이든다.

→ 이문제를 해결하는 방법 paging도 있다.

1. 스레싱이 뭔가요??
    - 하드디스크의 입출력이 너무 많아져 잦은 페이지 부재로 CPU Utilzation이 급격히 저하되는 현상
    - 방지하는 방법:
        - 각 프로세스가 필요로 하는 최소한의 프레임 갯수를 보장해주어야 합니다.
        - 지역교환 알고리즘 : 하나의 프로세스가 스래싱을 발생하게 되더라도 다른 프로세스로부터 프레임을 갖고 올 수 없게 되므로, 다른 프로세스를 스래싱 현상에 빠뜨릴 수 없게 됨
        - 우선순위 교환 알고리즘
2. 교착상태가 발생되는 조건이 무엇인가요??

점유 대기 (Hold and wait)	

- 최소한 하나의 자원을 점유하고 있으면서 다른 프로세스에 할당되어 사용하고 있는 자원을 추가로 점유하기 위해 대기하는 프로세스가 있어야 한다.
비선점 (No preemption)	

- 다른 프로세스에 할당된 자원은 사용이 끝날 때까지 강제로 빼앗을 수 없어야 한다.
순환 대기 (Circular wait)	

- 프로세스의 집합 {P0, P1, ,…Pn}에서 P0는 P1이 점유한 자원을 대기하고 P1은 P2가 점유한 자원을 대기하고 P2…Pn-1은 Pn이 점유한 자원을 대기하며 Pn은 P0가 점유한 자원을 요구해야 한다.
상호 배제 (Mutual exclusion)
- 자원은 한 번에 한 프로세스만이 사용할 수 있어야 한다