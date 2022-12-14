# CPU 스케쥴링

## 1️⃣ CPU 스케줄링이란?

- 운영체제는 프로세스들에게 공정하고 합리적으로 CPU 자원을 할당하기 위해 어떤 프로세스에게 CPU를 할당할지, 어떤 프로세스를 기다리게 할지 결정한다.
- 이처럼 프로세스들에게 CPU 자원을 배분하는 것이 CPU 스케줄링이다

## 2️⃣ 스케줄링 발생 조건

<img src="https://user-images.githubusercontent.com/89509857/203510087-e3ef6514-2456-4266-994f-5c0049da723f.png" width="700">

- 1 - **프로세스가 실행상태에서 대기 상태로 전환될 때** : 입출력 요청이나 자식 프로세스 중의 하나가 종료되기를 기다릴 때
- 2 - **프로세스가 실행상태에서 준비 상태로 전환될 때** : 타이머 종료에 의한 외부 인터럽트가 발생할 때
- 3 - **프로세스가 대기 상태에서 준비 상태로 전환될 때** : 입출력이 종료될 때
- 4 - **프로세스가 수행을 마치고 종료될 때** : 작업을 종료할 때

1,2번 조건 하에서 스케줄링이 발생하면 '비선점형 스케줄링', 그렇지 않은 스케줄링을 '선점형 스케줄링'이라고 한다.

## 3️⃣ 선점형 스케줄링 vs 비선점형 스케줄링

- 선점형 스케줄링(preemptive scheduling)
  - 프로세스가 CPU 를 비롯한 자원을 사용하고 있더라도 운영체제가 프로세스로부터 자원을 강제로 빼앗아 다른 프로세스에 할당할 수 있는 스케줄링의 방식
  - 프로세스마다 정해진 시간만큼 CPU를 사용하고, 정해진 시간을 모두 소비하여 타이머 인터럽트가 발생하면 운영체제가 해당 프로세스로부터 CPU 자원을 빼앗아 다음 프로세스에 할당하는 방식이 선점형 스케줄링의 일종임
  - 장점 : 어느 한 프로세스의 자원 독점을 막고 프로세스에 골고루 자원을 배분할 수 있음
  - 단점 : 문맥 교환 과정에서 오버헤드가 발생할 수 있음
- 비선점형 스케줄링(non-preemptive scheduling)
  - 하나의 프로세스가 자원을 사용하고 있다면 그 프로세스가 종료되거나 스스로 대기 상태에 접어들기 전까지 다른 프로세스가 끼어들 수 없는 스케줄링 방식
  - 장점 : 문맥 교환에서 발생하는 오버헤드가 적다
  - 단점 : 모든 프로세스가 골고구 자원을 사용할 수 없음
- 현재 대부분의 운영체제는 선점형 스케줄링 방식을 차용하고 있음

## 4️⃣ 프로세스 우선순위

- 프로세스마다 우선순위가 다르고, 우선순위가 높은 프로세스는 빨리 처리해야하는 프로세스를 의미한다.
- 운영체제는 PCB에 우선순위를 명시하고 PCB에 적힌 우선순위를 기준으로 먼저 처리할 프로세스를 결정한다
- 대표적으로 입출력 작업이 많은 프로세스가 우선순위가 높은 프로세스이다
- CPU 집중 프로세스와 입출력 집중 프로세스가 동일한 빈도로 CPU를 사용하는 것은 비합리적이다
- 입출력 장치가 입출력 작업을 완료하기 전까지 대기 상태가 될 것이기 때문에 그동안 다른 프로세스가 CPU 를 사용할 수 있기 때문
- 입출력 집중 프로세스를 가능한 한 빨리 실행시켜 입출력 장치를 끊임없이 작동시키고, 그다음 CPU 집중 프로세스에 집중적으로 CPU 를 할당하는 것이 효율적


### 입출력 집중 프로세스 vs CPU 집중 프로세스

- 입출력 집중 프로세스 : 비디오 재생, 디스크 백업 작업
- CPU 집중 프로세스 : 복잡한 수학 연산, 컴파일, 그래픽 처리

#### 🔅 CPU burst(CPU 버스트) vs I/O burst(입출력 버스트)

- CPU 버스트 : CPU 를 이용하는 작업
- I/O 버스트 : 입출력 장치를 기다리는 작업
- 프로세스는 일반적으로 CPU 버스트와 입출력 버스트를 반복하며 실행된다.
- CPU 버스트가 많은 프로세스는 CPU 집중 프로세스, 입출력 버스트가 많은 프로세스가 입출력 집중 프로세스

## 5️⃣ 스케줄링 큐

- 매번 일일이 모든 PCB를 검사하는 것은 비효율적이기 때문에 '스케줄링 큐'를 구현하여 관리한다
- 큐는 선입선출 자료구조이지만, 스케줄링에서 이야기하는 큐는 반드시 선입선출 방식일 필요는 없다
- 준비 큐(ready queue) : CPU를 이용하고 싶은 프로세스 들이 서는 줄
- 대기 큐(waiting queue) : 입출력장치를 이용하기 위해 대기 상태에 접어든 프로세스 들이 서는 줄
- 운영체제는 PCB 들이 큐에 삽입된 순서대로 프로세스를 하나씩 꺼내어 실행하되, 그중 우선순위가 높은 프로세스를 먼저 실행한다
- 즉, 우선순위가 낮은 프로세스들은 먼저 큐에 삽입되어 줄을 섰다고 할지라도 우선순위가 높은 프로세스가 먼저 처리될 수 있다

<br>

# CPU 스케줄링 알고리즘

## 1️⃣ FCFS 스케줄링 (First Come First Served Scheduling, 선입 선처리 스케줄링)

- 비선점형 스케줄링
- 단순히 준비 큐에 삽입된 순서대로 프로세스들을 처리하는 방식
- 프로세스들이 기다리는 시간이 매우 길어질 수 있다는 단점이 있음
- 호위 효과가 발생할 수 있음

🔍호위효과 : 먼저 도착한 프로세스가 CPU에서 수행되는 버스트 시간이 매우 길면, 그 다음 도착한 프로세스가 첫 번째 프로세스가 끝날 때까지 매우 긴 시간을 기다리게 되는 것

## 2️⃣ SJF 스케줄링 (Shortest Job First Scheduling, 최단 작업 우선 스케줄링)

- 기본적으로 비선점형 스케줄링, 선점형으로 구현될 수도 있음.
- 호위 효과를 방지하기 위해 나온 스케줄링
- 준비 큐에 삽입된 프로세스들 중 CPU 사용 시간(버스트 시간)이 짧은 프로세스부터 실행하는 스케줄링 방식
- FCFS 스케줄링 기법보다 평균 대기시간을 감소 시킨다
- 큰 작업에 대해서는 FCFS 스케줄링에 비하여 예측하기가 어렵다
- 긴 작업보다 은 작업에 더 유리하다

## 3️⃣ 라운드 로빈 스케줄링(Round Robin Scheduling)

- 선점형 스케줄링
- 선입 선처리 스케줄링(FCFS스케줄링)에 타임슬라이스 개념이 더해진 스케줄링 방식
- 타임 슬라이스 : 프로세스가 CPU를 사용할 수 있는 정해진 시간
- 즉, 큐에 삽입된 순서대로 정해진 타임 슬라이스만큼의 시간 동안 돌아가면서 CPU를 이용함
- 정해진 시간을 모두 사용하였음에도 아직 프로세스가 완료되지 않았다면 다시 큐의 맨 뒤에 삽입되고 문맥 교환이 발생한다.
- 시분할 시스템에 효과적이다
- 타임 슬라이스가 지나치게 크면 FCFS 스케줄링과 동일하여 호위효과가 생길 수 있고, 지나치게 작으면 문맥 교환에 발생하는 비용이 클 수 있다. 타임슬라이스의 크기는 10~100ms 가 보통이다. 

## 4️⃣ SRT 스케줄링(Shortest Remaining Time, 최소 잔여 시간 우선 스케줄링)

- 선점형 스케줄링
- 최단 작업 우선 스케줄링(SJF 스케줄링) 알고리즘과 라운드 로빈 알고리즘을 합친 스케줄링 방식
- 정해진 타임 슬라이스 만큼 CPU 를 사용하되, CPU를 사용할 다음 프로세스로는 남아있는 작업 시간이 가장 적은 프로세스를 선택한다
- 현재 실행 중인 프로세스라도 남은 처리시간이 더 짧다고 판된되는 프로세스가 준비 큐에 생기면 언제라도 실행 중인 프로세스가 선점될 수 있다

## 5️⃣ 우선순위 스케줄링(Priority Scheduling)

- 비선점형 스케줄링
- 프로세스들에 우선순위를 부여하고, 가장 높은 우선순위를 가진 프로세스부터 실행하는 스케줄링 알고리즘
- 우선순위가 같은 프로세스들은 선입 선처리로 스케줄링 된다.
- 우선 순위가 낮은 프로세스는 계속해서 연기되는 **기아 현상**이 발생할 수 있다.
- 기아 현상을 방지하기 위해 오랫동안 대기한 프로세스의 우선순위를 점차 높이는 **에이징 기법**을 사용할 수 있다.

## 6️⃣ 다단계 큐 스케줄링(Multilevel Queue Scheduling)
<img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRlZCUb-xS-nQBVrIWRbgvtPKUd3HLtyb4c8zmNHo3idvqNR6QsGxN-gquSK3bMqHt1cOQ&usqp=CAU" width="500" />

- 선점형 스케줄링
- 우선순위 별로 준비 큐를 여러개 사용하는 스케줄링 방식
- 우선순위가 가장 높은 큐에 있는 프로세스들을 먼저 처리하고, 우선순위가 가장 높은 큐가 비어있으면 그다음 우선순위 큐에 있는 프로세스들을 처리한다
- 각 큐는 자신만의 독자적인 스케줄링을 갖고 있다
- 상위 단계 큐에 작업이 들어오면 CPU를 내주어야 하므로 선점형이다
- 한 큐에서 다른 큐로의 작업 이동이 불가능하다.
- 우선순위가 낮은 프로세스는 계속 연기되는 **기아현상**이 발생할 수 있다

## 7️⃣ 다단계 피드백 큐 스케줄링(Multilevel Feedback Queue Scheduling)

<img src="https://hyuntaekhong.github.io/assets/images/os/os18.png" width="700" />

- 다단계 큐 스케줄링이 기아현상이 발생할 수 있다는 점을 보완한 스케줄링 알고리즘
- 프로세스들이 큐 사이를 이동할 수 있다는 점이 차이점
- 새로 준비 상태가 된 프로세스가 있다면 우선순위가 가장 높은 큐에 삽입이 되고, 일정시간(타임 슬라이스)동안 실행된다. 해당 큐에서 실행이 끝나지 않았을 경우 다음 우선순위의 큐에 삽입되어 실행된다.
- 즉, CPU를 오래 사용해야 하는 프로세스는 점차 우선순위가 낮아진다
- 마찬가지로 낮은 우선순위 큐에 너무 오래 있는 프로세스가 있다면 에이징 기법을 적용하여 기아 현상을 예방할 수 있다.
