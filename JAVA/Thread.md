Thread
==============

## 스레드(thread)란?

**스레드(thread)**란 프로세스 내에서 실질적으로 작업을 수행하는 단위이다. 

<aside>
💡 **프로세스(Process)**는 실행중인 프로그램으로 볼 수 있다.

</aside>

### **스레드의 상태**

| NEW | 스레드 객체가 생성, 아직 start() 메소드가 호출되지 않은 상태 |
| --- | --- |
| RUNNABLE | 바로 실행 가능한 상태, 대기 중… |
| WAITING | 다른 스레드가 통지할 때까지 기다리는 중… |
| TIME_WAITING | 정해진 시간 동안 기다리는 중… |
| BLOCKED | 사용하려는 객체의 Lock이 풀릴 때까지 기다리는 중…  |
| TERMINATED | 실행 완료하여 종료된 상태… |

## JAVA Thread

### 생성하는 법

1. **Thread 상속**
    - 다른 클래스를 상속하지 않을 경우 사용한다.
    
    ```java
    public class Sample extends Thread{
    		@Override // => 없어도 실행된다
        public void run(){
            System.out.println("Thread를 상속받아 실행한 스레드");
        }
    }
    ```
    
2. **Runnable 인터페이스 implements**
    - 다른 클래스를 상속받아 Thread 클래스를 상속받지 못하는 경우에 사용한다.
    
    ```java
    public class Sample2 implements Runnable{
        @Override
        public void run(){
            System.out.println("Runnable 인터페이스를 활용하여 실행된 스레드");
        }
    }
    ```
    
    **Main.class**
    
    ```java
    public class Main {
        public static void main(String[] args) throws InterruptedException {
    				// 스레드 생성 State
            Thread thread1 = new Sample();
            Thread thread2 = new Thread(new Sample2());
    				// 스레드 시작
            thread1.start();
            thread2.start();
    
    				// 스레드가 종료될 때 까지 대기
            thread1.join();
            thread2.join();
    				
    				// 스레드가 종료되었으면 출력
            if(!thread1.isAlive() && !thread2.isAlive())
                System.out.println("main 종료");
        }
    }
    ```
    
    **결과**
    
    ```bash
    Thread를 상속받아 실행한 스레드
    Runnable 인터페이스를 활용하여 실행된 스레드
    main 종료
    
    Process finished with exit code 0
    ```
    

### Thread Method

| 메서드 | 타입 | 설명 |
| --- | --- | --- |
| getId() | long | Thread의 id 반환 |
| sleep(long ms) | void | 지정한 시간 만큼 대기 |
| getName() | String | Thread의 이름 반환 (지정하지 않을 경우 Thread1 ~ ThreadN 번까지 이름으로 설정된다.) |
| setName(String name) | void | Thread의 이름 지정 |
| start() | void | Thread 시작(run() 메서드 호출) |
| getPriority() | int | Thread의 우선순위 반환 |
| setPriority() | void | Thread의 우선순위 지정 |
| getState() | string | Thread의 상태 반환 |
| isAlive() | boolean | Thread가 살아있는지 확인, 살아있으면 True, 죽었으면 False 반환 |
| join() | void | Thread가 종료될 때까지 대기 |
| run() | void | start() 시 실행되는 함수 |
| suspend() | void | Thread 일시정지 |
| resume() | void | 일시정지된 Thread 다시 시작 |
| yield() | void | 다른 Thread에게 실행 상태 양보 후, 준비 상태로 변환 |
| notify() | void | 대기 상태의 Thread를 실행 상태로 만든다. Waiting ⇒ Runnable |
| interrupt() | void | Thread 중단 |
| isInterrupted()  | boolean | Thread가 interrupt() 메서드를 통해 종료되었는지 반환, interrupt()에 의해 종료 되었으면 True, 아니라면 False |

## 스레드 안전

**스레드 안전**이란 멀티 스레드 프로그래밍에서 객체가 여러 스레드로부터 동시에 접근이 이루어져도 프로그램의 실행에 문제가 없는것을 의미한다.

메서드가 하나의 스레드에서 호출되어 **실행중**인 경우에 다른 스레드가 그 메서드를 호출하여 동시에 함께 실행되더라도 각 스레드에서의 스레드 수행 결과가 정확히 나오는 것을 의미한다.

### **Re-entrancy(재진입성)**

- 어떤 메서드가 한 스레드에 의해 호출되어 실행 중일 때, 다른 스레드가 그 메서드를 호출하더라도 그 결과가 각각에게 올바로 주어져야 한다.

### **Thread-local storage(스레드 지역 저장소)**

- 공유 자원의 사용을 최대한 줄여 각각의 스레드에서만 접근 가능한 저장소들을 사용함으로써 동시 접근을 막는다.

### **Mutual exclusion(상호 배제)**

- Thread에 lock이나 semaphore를 걸어서 공유 자원에는 하나의 Thread만 접근 가능하게 한다.
    
    <aside>
    💡 세마포어(Semaphore) : 공유된 자원의 데이터에 여러 Thread가 접근하는 것을 막아준다.
    
    </aside>
    

### **Atomic operations(원자 연산)**

- 데이터 변경 시 실제로 데이터의 변경이 이루어지는 시점에 Lock을 걸고, 데이터를 변경하는 시간 동안 다른 스레드의 접근을 막는다.

## 동시성

### **동시성**

멀티 태스킹을 위해 여러 개의 스레드가 **번갈아가면서** 실행되는 성질

### **병렬성**

여러 스레드가 **동시에** 실행되는 성질

### 동시성 문제

동일한 메서드에 여러개의 스레드가 동시에 접근하면서 발생하는 문제

### 실습

실행할 메서드

```java
public class Util {

    static String userName;

    public void showUserName(String name) throws InterruptedException {
        userName = name;
        System.out.println(userName + "저장");
        Thread.sleep(1000);
        System.out.println(userName + "조회");
    }

}
```

생성할 Thread

```java
public class Sample3 implements Runnable{
    private final Util util;
    private final String userName;

    public Sample3(Util util, String userName) {
        this.util = util;
        this.userName = userName;
    }

    @Override
    public void run() {
        try {
            util.showUserName(userName);
        } catch (InterruptedException e) {
            throw new RuntimeException(e);
        }

    }
}
```

```java
public class Main {
    public static void main(String[] args) throws InterruptedException {
        Util util = new Util();

				// 스레드들 생성 "A", "B"
        Thread a = new Thread(new Sample3(util, "A"));
        Thread b = new Thread(new Sample3(util, "B"));

				// A 스레드 실행
        a.start();
				// B 스레드 실행
        b.start();
        Thread.sleep(3000);

        if(!a.isAlive() && !b.isAlive())
            System.out.println("main 종료");
    }
}
```

userName이란 변수에 이름을 저장하고 1초 뒤 조회해보는 로직을 구현한다고 쳐 보자.

위의 코드 처럼 A라는 유저와 B라는 유저를 저장 및 조회를 하려고 한다. 위 코드만 봐서는 

A가 먼저 저장 및 조회가 되고 그 다음에 B가 저장 및 조회가 되야한다고 예상할 수 있다.

**하지만 예상과 다르게 B유저가 두번 조회 되는 것을 볼 수 있다.**

```bash
A저장
B저장
B조회
B조회
main 종료

Process finished with exit code 0
```

<aside>
💡 **이유**

1. 스레드A와 스레드B가 동시에 실행이 되어 같은 showUserName이라는 메서드를 실행하였다. 

2. 먼저 스레드A가 “A”라는 userName을 먼저 저장하고 1초 쉬고있었다. 그때 스레드B가  userName을 B로 바꾸고 저장하였다.

3. A가 저장된 userName 조회를 실행 할 때 userName을 스레드B가 바꿔버린 후 이므로 “B”가 조회가 되게 되는 것이다.

</aside>

### Synchronized

synchronized 메서드는 특정 메서드 혹은 변수에 Lock을 걸어 하나의 Thread가 해당 메서드 혹은 변수를 사용하고 있는 동안 다른 Thread들의 접근을 막는 역할을 한다. synchronized로 동시성 문제를 해결할 수 있다.

한번 사용해 보자

```java
public class Util {

    static String userName;

    public **synchronized** void showUserName(String name) throws InterruptedException {
        userName = name;
        System.out.println(userName + "저장");
        Thread.sleep(1000);
        System.out.println(userName + "조회");
    }

}
```

결과

해당 showUserName 메서드에  synchronized가 붙어 Thread들이 하나씩 해당 메서드를 실행하게 하여 A스레드가 실행을 마친 후에 B스레드가 메서드를 실행 하는 것을 볼 수 있다.

```bash
A저장
A조회
B저장
B조회
main 종료

Process finished with exit code 0
```

### ConcurrentHashMap

**HashMap**

HashMap은 모든 메서드에 synchronized가 적용되어있지 않기 때문에 성능은 좋지만 동시성 문제가 발생할 수 있다.

**Hashtable**

Hashtable은 모든 메서드에 synchronized를 사용하여 스레드들의 동기화를 시켜주어 멀티 스레드 환경에서 동시성 문제를 방지할 수 있다.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/cb7d1515-18c8-476b-b39f-40fa103ae474/be0011ed-5115-4e36-99be-91ed5f59cda6/Untitled.png)

하지만 멀티 스레드 환경에서 동시에 작업을 할 때 메서드를 호출할 때 마다 Lock을 걸어 성능상으로 효율이 떨어진다.

**ConcurrentHashMap**

JAVA의 자료구조 중 하나로 멀티 스레드 환경에서 안전하게 데이터를 관리할 수 있는 자료구조이다.

**HashTable과의 차이점??**

HashTable과는 다르게 모든 메서드에 synchronized가 적용된게 아닌 일부분에만 적용되어있어

필요한 부분에만 Lock을 걸어 성능을 향상 시킨 자료구조이다.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/cb7d1515-18c8-476b-b39f-40fa103ae474/9bd34372-e082-43d6-8e36-3a9fd8dead6a/Untitled.png)

<aside>
💡 **조회(get())**의 경우 **sychronized**를 적용시키지 않아 동시성을 보장하지 않는다

</aside>

ConcurrentHashMap은 내부적으로 여러 개의 세그먼트(구간)로 나뉘어져 있다. 각 세그먼트는  각각 Lock을 가진다. 이를 통해 여러 스레드가 동시에 접근해도 서로 다른 세그먼트에서 작업하여 동기화가 된다.

## 데드락(DeadLock)

여러개의 Thread들이 서로가 가지고 있는 Lock이 해제되기를 계속 기다리는 상태가 생기는 상태를 **교착 상태(deadlock)** 라고 한다. 교착 상태가 되면 어떤 작업도 실행되지 못하고 서로 상대방의 작업이 끝나기만 바라는 무한정 대기 상태에 빠진다

<aside>
💡 예를 들어 스레드1과 스레드2가 동시에 실행중이다.

**스레드1**은 **A**라는 자원을 점유중이고 **B**라는 자원을 점유하기 위해 대기 중…
**스레드2**는 **B**라는 자원을 점유중이고 **A**라는 자원을 점유하기 위해 대기 중…

이럴 경우 교착 상태에 빠져버린다.

</aside>

### 발생하는 조건

1. **상호 배제**
    - Thread에 lock이나 semaphore를 걸어서 공유 자원에는 하나의 Thread만 접근 가능하게 한다.
2. **점유 대기**
    - Thread가 최소한 하나의 공유 자원을 점유 하는 중 다른 자원을 얻기 위해 대기하고있는 상태이다.
3. **비선점**
    - Thread가 한 자원을 점유중이면 다른 Thread가 점유할 수 없다.
4. **순환 대기**
    - 스레드들이 자원을 요구하는 방향이 원형을 이루는 상태
    - 스레드 A는 스레드 B가 점유한 자원이 필요하고 스레드 B는 C가 점유한 자원이 필요하며, 스레드 C는 스레드 A가 점유한 자원이 필요한 상태 처럼 순환 형태로 자원을 대기하고 있는 것
        
        ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/cb7d1515-18c8-476b-b39f-40fa103ae474/0bd4e737-af4c-4b06-9fc9-cf0e6524baaa/Untitled.png)
        

## 스레드 풀(Thread Pool)

스레드를 계속 생성, 회수하여 시스템적으로 무리가 갈 수 있어 이를 방지하기 위해 여러 스레드들을 미리 생성하여 작업이 들어올 때 생성한 스레드들에게 작업을 적절히 분배 시켜주는 것이다.

작업 처리에 사용되는 Thread들의 개수를 정해놓고 작업 큐(queue)에 들어오는 작업들을 생성한 스레드들에게 분배하여 처리하는 것이다.

**그림으로 표현하면 이런 느낌인거 같다.**

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/cb7d1515-18c8-476b-b39f-40fa103ae474/b755d4f0-b181-48a1-99ed-745c0e3ad797/Untitled.png)

### Single Thread Executor

- 단일 스레드, 즉 하나의 스레드를 생성하여 작업을 처리하는 스레드풀이다.
- 작업이 완료되면 다음 작업을 실행
    - 하나의 스레드가 작업을 완료하면 queue에 있는 다음 작업을 받아 실행한다고 함.

### Fixed Thread Executor

- 고정된 개수만큼 스레드 생성
- 일정한 스레드 수를 유지하며 작업 처리
- 작업 처리량을 제한할 때 사용
- 실패 시 새로운 스레드를 생성하여 대체

### Cached Thread Pool

- 필요에 따라 스레드를 동적으로 생성 및 종료
- 작업량에 따라 스레드 개수 조절, 사용하지 않으면 삭제
- 기본적으로 60초 동안 스레드가 유지된다
- 비동기 작업에 사용

### Scheduler Thread Pool

- 예약된 작업을 처리
- 특정 시간이나 주기적으로 실행하는 작업 관리

### Work Stealing Thread Pool

- 작업 스스로 스레드를 할당하여 처리
- 작업 큐가 비어있는 스레드가 다른 스레드의 작업 큐에서 작업을 가져와 처리 (쉬고 있는 스레드가 없도록 하는 듯)

**다른 스레드의 작업 큐?**

스레드 풀의 개념을 봤을 때에는 하나의 작업 큐에서 생성된 스레드들에 작업을 분배한다고 공부했었다. 그런데 Work Strealing Thread Pool의 개념에서는 **다른 스레드의 작업 큐**에서 작업을 훔쳐와 처리한다는 내용이 있다.

**Work Stealing Thread Pool에서는 Thread마다 각각 작업 큐를 가지고 있는걸까?**

<aside>
💡 **ForkJoinPool?**

Executor를 추가적으로 공부하다가 알게 된 ForkJoinPool이 Work Stealing Thread Pool인 것 같다. ForkJoinPool에 설명으로 보아 스레드들이 각자의 작업 큐를 가지고 있는 것 같다.

</aside>

## Executor Service

JAVA에서 Thread Pool을 생성하여 사용하고자 할때 사용되는 클래스이다.

Task를 지정해주면 Thread Pool을 이용하여 작업을 처리하고 관리해준다.

### Spring Default Executor

- Spring 기본설정으로 되어있는 TaskExecutor는 SimpleAsyncTaskExecutor이다.
- 어떤 스레드도 재사용하지 않고 호출 시 새로 스레드를 시작하기 때문에 자원 낭비가 심하다.

### ForkJoin Pool

- 큰 업무를 작은 업무로 배분하여, 작업을 한 후 결과를 취합한다.
- 작업의 크기에 따라 분할(Fork)하고, 분할된 작업이 처리되면 그것을 Join하여 리턴해준다.

**동작 방식**

1. 스레드A가 작업을 받아 자신의 로컬 큐에 1차 분할
2. 작업이 없는 스레드B가 스레드A의 로컬 큐에서 작업을 훔쳐 작업 진행
3. 스레드B가 훔쳐온 작업이 양이 많아 다시 세부적으로 분할
4. 세부적으로 작업을 분할하여 모든 스레드가 일을 종료하는 시간이 비슷함
5. 모든 작업 취합 후 리턴

**장단점**

- 작업이 오래걸리는 스레드가 존재하고 다른 스레드들은 작업 처리 속도가 빠를 때 효율이 좋다. (작업이 빨리 끝나 작업이 없는 스레드가 작업이 많은 스레드의 작업을 가져가기 때문)
- 스레드들에게 분할되는 작업이 거의 동일하다면 쓸데없는 스레드들을 생성하기 때문에 자원 낭비가 될 수 있다

# TODO

Thread  start()와 run()의 차이점을 한번 더 정리해 보자

| start | run |
| --- | --- |
| 새로운 Thread가 생성되며 Thread가 시작되면 run() 메서드가 실행된다. | Thread가 생성되지 않으며 그냥 run() 메서드만 실행된다. |
| 동일한 객체에서 두 번 이상 호출 시 IllegalThreadStateException이 발생한다. | 호출수에 제한없이 계속 호출할 수 있다. |
| 병행 처리 가능 | 병행 처리 불가 |

## start()

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/cb7d1515-18c8-476b-b39f-40fa103ae474/7a942f7b-40be-4787-9e1e-9071c5c70204/Untitled.png)

<aside>
💡 **A zero status value corresponds to state "New”**

</aside>

threadStatus ≠ 0 즉 **스레드 객체가 생성된** 상태(**NEW**)가 아닌 경우에는 IllegalThreadStateException이 발생된다. (RUNNABLE, WAITING… 등)

즉 동일한 스레드는 두 번 이상 **start()**로 실행될 수 없다.

그 뒤 ThreadGroup에 추가 되어

 native 메서드인 start0()에 의해 내부적으로 run() 함수를 실행한다.

## run()

run()을 호출하면 스레드가 생성 되지 않고, 일반적인 메서드 처럼 실행된다.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/cb7d1515-18c8-476b-b39f-40fa103ae474/7d51d015-d686-4300-966d-b10eb2cfa166/Untitled.png)

새로운 스레드를 생성하지 않고 메인 스레드에서 호출이 된다 따라서 멀티 스레드와 같은 병렬 처리를 하지 못한다.

### 위에 동시성 문제 예제로 차이점 확인

run 먼저 실행 후 

1. run() 먼저 실행 후 start() 실행
    
    ```java
    **public class Main {
        public static void main(String[] args) throws InterruptedException {
            Util util = new Util();
    
            Thread a = new Thread(new Sample3(util, "A"));
    
            Thread b = new Thread(new Sample3(util, "B"));
    
            a.run();
    				b.run();
            a.start();
            b.start();
            Thread.sleep(3000);
    
            if(!a.isAlive() && !b.isAlive())
                System.out.println("main 종료");
        }
    }**
    ```
    
    결과
    
    ```bash
    A저장 // => run()으로 실행
    A조회
    B저장
    B조회
    A저장 // => start()로 실행
    B저장
    B조회
    B조회
    main 종료
    ```
    
    run으로 실행 할 경우에는 A가 작업이 끝난 뒤 B가 작업을 시작하여 동시성 문제가 발생하지 않았다. 반면 start로 실행하는 경우 A, B가 동시에 실행되어 동시성 문제가 발생한 것을 확인 할 수 있다.
    
    <aside>
    💡 run()은 스레드 객체를 생성하는게 아닌 **클래스에 정의된 함수**만을 실행하는 것, start()는 **스레드 객체**를 생성하고 실행되는 것이라고 결론 지을 수 있다.
    
    </aside>
    
    run 으로 실행 할 경우 작업을 병행하지 않아 run 메서드가 온전히 끝난 뒤에 start 메서드들이 멀티 스레드에서 동작하여 start 메서드로 실행한 결과에서 동시성 문제가 발생한 것을 확인할 수 있다.
    
2. start() 실행 후 run() 실행
    
    결과
    
    ```bash
    A저장 // a.start()로 추측
    B저장 // b.start()로 추측
    A저장 // a.run()으로 추측
    B조회 // a.run()의 결과로 추측
    B조회 // a.start()의 결과로 추측
    B저장 // b.run()으로 추측
    B조회 // b.run()의 결과로 추측
    B조회 // b.start()의 결과로 추측
    main 종료
    ```
    
    이건 대체 뭘까.. 스레드 이름을 함께 출력해 봤다
    
    ```bash
    main A저장
    Thread-1 B저장
    Thread-0 A저장
    Thread-0 B조회
    main B조회
    main B저장
    Thread-1 B조회
    main B조회
    main 종료
    ```
    
    결과를 봤을 때 a.run()이 먼저 실행된거 같지만 start()로직 상 start로 인해 실행되는 run()함수는 start 내부적으로 Thread가 생성된 후, 실행되기 때문에 결과는 늦게 출력이 됐지만 실행 자체는 a.start()가 먼저 실행된게 맞는거 같다.
