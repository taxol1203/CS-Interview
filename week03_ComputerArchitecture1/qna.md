3주차 질문 리스트입니다.

## 대연

- C코드에서 바이너리로 이어지는 과정
  - 전처리 과정에서는 무엇을 하나요?
  - 왜 바이너리 포맷의 구조를 가지게 만들죠?
- CPU레지스터에 대한 설명, 레지스터 vs 캐쉬 비교
- 해저드에 대한 설명
- 인터럽트 설명, 인터럽트에 적합한 핸들러를 선택하는 과정
- Java의 -Integer.MIN_VALUE 결과는?
- 리틀 엔디안이 무었이며. 리틀 엔디안을 어디다가 쓰면 좋은가요??

## 예상 질문 1.

Q. 메모리 레이아웃에서 BSS 영역에 대해 설명하시오  
A.

- 초기화되지 않은 Data Segment이다.
- Read-write
- 프로그램 실행 전 OS 커널에 의해 0으로 초기화됨.

## 예상 질문 2.

Q. 리틀/빅 엔디언의 장단점에 대해 설명하시오  
A.

- 빅 엔디언
  - 장점
    - 디버깅이 편하다. 사람과 숫자를 읽고 쓰는 법이 같기 때문이다.
    - 비교 연산이 비교적 빠르다. 맨 윗자리부터 비교하면 되기 때문
  - 단점 : 하위 바이트 값을 사용할 때 리틀 엔디언에 비해 추가 연산이 필요하다.
- 리틀 엔디언
  - 장점
    - 메모리에 저장된 값의 하위 바이트들만 사용할 때 별도의 계산이 필요 없다.
    - 계산 연산이 비교적 빠르다. 아랫자리부터 계산을 하면서 올림하면 되기 때문

## 예상 질문 3.

Q. 해저드가 무엇인지 설명하고, 왜 발생하는지 설명해주세요  
A. 해저드(Hazard): 처리 시간이 일정하지 않고, 처리 단계가 균등하지 않으면 발생하는 문제
(답 대충적었음 ㅈㅅ)

## 주연

- 분기 예측에 대해서 알려주세요
  - 정적 분기 예측과 동적 분기 예측 중 어느 것이 더 효율적인라고 생각?
- 프로시저의 호출과정에 대하여 알려주세요
- 예외 발생시 cpu가 어떻게 처리하는지?
