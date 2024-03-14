# JAVA Client & Server TCP 통신

# TCP

서버와 클라이언트간에 데이터를 신뢰성 있게 전달하기 위해 만들어진 프로토콜이다.

## 특징

1. 연결형 서비스로 연결이 성공하여야만 통신이 가능하다.
2. **3-way handshaking** 과정을 통하여 연결을 설정하고 4-way handshaking 과정을 통해 연결을 해제한다.
    1. 3-way handshaking 과정으로 발신지와 수신지를 확실하게 정해 정확한 전송을 보장하여 **높은 신뢰성**을 보장한다. 
3. 흐름 제어 및 혼잡 제어를 한다.
    - **흐름 제어**
        - 송신측이 수신측 보다 데이터 처리가 빠를 시 수신측에서 문제가 생길 수 있다.
        - Stop and Wait(정지 - 대기)
            - 전송한 패킷에 대한 확인 응답을 받아야 다음 패킷을 전송할 수 있게 한다.
4. 서버와 클라이언트는 1:1 통신을 한다.
5. 전송받는 데이터의 **신뢰성**과 **정확성**이 중요할 때 주로 사용하는 프로토콜이다.

## TCP State

| 상태 | 설명 |
| --- | --- |
| CLOSE | 커넥션이 없는 상태 |
| LISTEN | SYN을 기다리는 상태 |
| SYN-SENT | SYN을 보내고 ACK를 기다리는 상태 |
| SYN-RCVD | SYN_ACK를 보내고 ACK를 기다리는 상태 |
| ESTABLISHED | 커넥션이 생성된 상태, 데이터 전송 가능 |
| FIN-WAIT-1 | 첫 FIN을 보내고 ACK를 기다리는 상태 |
| FIN-WAIT-2 | 첫 FIN을 받고 2번째 FIN을 기다리는 상태 |
| CLOSE-WAIT | 첫 FIN을 받고 ACK를 보낸 상태, 애플리케이션 종료 대기 |
| TIME-WAIT | 2번째 FIN을 받고 ACK를 보낸 상태, 동일 포트와 IP로 커넥션이 생성되지 않도록 하는 시간을 기다리는 상태 |
| LAST-ACK | 2번째 FIN을 보내고 ACK를 기다리는 상태 |
| CLOSING | 양쪽이 동시에 닫기로 한 상태 |

## TCP flag

TCP 패킷 구조 중 하나인 flags이다. TCP의 여러가지 속성들을 설정할 수 있다.

| Flag | 표시 | 설명 |
| --- | --- | --- |
| SYN(Synchronization) | S | 연결 요청 플래그로 TCP에서 세션을 성립할 때 가장 먼저 보내는 패킷이다. 시퀀스 번호를 임의적으로 설정하여 세션을 연결하는데에 사용된다. |
| ACK(Acknowledgement) | Ack | 응답 패킷이다. 상대방에게 패킷을 받았다는 걸 알려주는 패킷. |
| RST(Reset) | R | 재설정을 하는 과정이다 양방향에서 동시에 일어나는 중단 적업이다. 즉시 연결을 끊을 때 사용. |
| PSH(Push) | P | 받은 데이터를 즉시 목적지인 OSI 7 계증의 응용 계층으로 전송한다. |
| URG(Urgent) | U | Urgent Pointer라는 전송하는 데이터 중에서 긴급히 전달해야 할 내용이 있을 때 사용. |
| FIN(Finish) | F | 세션 연결을 종료시킬 때 사용된다. |

## 3-Way Handshake (통신 연결)

**3-way HandShake**는 TCP 통신을 하는 프로그램이 데이터를 전송하기 전 정확한 전송을 보장하기 위해 상대방과 먼저 **세션**을 수립하는 과정이다.

1. 클라이언트는 서버에 접속을 요청하는 SYN 패킷을 보낸 뒤 SYN/ACK 응답을 기다리는 **SYN _SENT** 상태가 된다.
2. 서버는 SYN 요청을 받고 클라이언트에 요청 수락을 의미하는 ACK 패킷을 보낸 뒤 클라이언트가 다시 ACK로 응답하기를 기다리는 **SYN_RCVD** 상태가 된다.
3. 클라이언트는 서버에게 ACK 패킷을 보내고 연결이 되어 데이터의 송수신이 이루어진다. 이때 서버와 클라이언트는 **ESTABLISHED** 상태가 된다. 

<aside>
💡 **MTU, MSS?**
TCP 3-way HandShaking 과정에서 연결 확립 뿐만 아니라 한번에 보낼 수 있는 패킷의 최대 크기까지 정한다

**MTU (Maximum Transmission Unit)**
- 전송할 수 있는 패킷의 최대 크기

**MSS (Maximum Segment Size)
-** TCP 상에서 전송할 수 있는 사용자 데이터의 최대 크기 (MTU값에 의해 결정)

</aside>

## 4-Way Handshake (통신 해제)

1. 클라이언트에서 서버로 연결 종료 요청인 FIN을 보내고, ACK를 기다리는 FIN-WAIT-1 상태가 된다. ⇒ **1번째**
2. 서버는 FIN 요청을 받고 ACK를 보낸 뒤에 남아있는 통신 작업을 처리하는 CLOSE-WAIT 상태가 된다. ⇒ **2번째**
3. 클라이언트는 ACK를 받고 서버의 FIN 응답을 기다리는 FIN-WAIT-2 상태가 된다.
4. 서버는 남은 작업을 모두 처리하고 연결을 종료하겠다는 FIN을 보내고 LAST-ACK 상태가 된다. ⇒ **3번째**
5. 클라이언트는 FIN을 받은 후 일정 시간 대기하는 TIME-WAIT 상태가 되며 서버에 ACK를 보낸다. ⇒ **4번째**
6. 서버는 ACK를 받은 후 연결을 종료한다. ⇒ 종료

## TCP Socket 프로그래밍

클라이언트와 서버간의 1대1 소켓 통신으로 서로 통신하기 위해서 서버가 먼저 실행 상태로 클라이언트의 연결 요청을 기다려야 한다.

## Socket 클래스

### 생성

- Socket socket = new Socket(host, port);
    
    ```java
    Socket socket = new Socket("192.168.50.24", 1234);
    ```
    

### 메서드

| 메서드 | 타입 | 설명 |
| --- | --- | --- |
| getInputStream() | InputStream | 소켓이 사용하는 입력 Stream 반환 |
| getOutputStream() | OutputStream | 소켓이 사용하는 출력 Stream 반환 |
| getLocalAddress() | InetAddress | 연결중인 로컬 주소 반환 |
| getInetAddress() | InetAddress | 연결중인 원격 주소 반환 |
| getLocalPort() | int | 연결중인 로컬 포트 반환 |
| getPort() | int | 연결중인 원격 포트 반환 |

**직접 실행해본 결과**

```bash
getInetAddress() : /192.168.50.24
getLocalAddress() : /192.168.50.24 => 로컬 호스트에서 서로 연결중이기 때문에 결과가 같다.
getLocalPort() : 62010
getPort() : 1234
```

### PrintWriter

다양한 출력 메서드를 지원하는 클래스

| 생성자 | 설명 |
| --- | --- |
| PrintWriter(OutputStream out) | OutputStream out을 인자로 전달받아 PrintWriter 객체를 생성한다. |
| PrintWriter(OutputStream out, boolean autoFlush) | OutputStream out을 인자로 전달받아 PrintWriter 객체를 생성한다.  autoFlush를 true로 지정하면 출력 시에 자동으로 flush() 메소드를 호출한 효과가 발생한다. (TCP Socket 통신 시에는 AutoFlush가 먹혔는데, HTTP 통신할 때 는 안먹힘..) |

# ++

## Netty ByteBuffer VS ByteBuf

### ByteBuffer

바이트 데이터를 저장하고 읽는 저장소이다.

배열을 멤버 변수로 가지고 있으며, 배열에 대한 읽기/쓰기 지원을 한다.

- **position**
    - 현재 읽거나 쓸 버퍼에서의 위치 값, 인덱스이기 때문에 0부터 시작한다.
- **limit**
    - 버퍼에서 읽거나 쓸 수 있는 position의 한계를 나타낸다.
- **capacity**
    - 버퍼가 사용할 수 있는 메모리 크기를 나타낸다.

**예제**

```java
import java.nio.ByteBuffer;

public class Main {
    public static void main(String[] args) {
        var byteBuffer = ByteBuffer.allocate(5); // 5바이트 까지 담을 수 있는 힙 버퍼 생성
        System.out.println(byteBuffer);

        byteBuffer.put((byte) 3);
        System.out.println(byteBuffer);
        
        System.out.println(byteBuffer.get());
    }
}
```

**결과**

```bash
java.nio.HeapByteBuffer[pos=0 lim=5 cap=5]
java.nio.HeapByteBuffer[pos=1 lim=5 cap=5]
0
```

읽기와 쓰기 인덱스가 분리되어 있지 않아 byteBuffer.get() 을 통하여 읽기를 시도했지만 0이 출력됐다

### flip()

ByteBuffer의 모드를 변경하는 메서드이다.

**flip을 사용하여 모드 변경 후 get() 메서드 실행 시**

```java
import java.nio.ByteBuffer;

public class Main {
    public static void main(String[] args) {
        var byteBuffer = ByteBuffer.allocate(5);
        System.out.println(byteBuffer);

        byteBuffer.put((byte) 3);
        System.out.println(byteBuffer);

        byteBuffer.flip(); // byteBuffer의 모드를 읽기 모드로 변경한다.
				System.out.println(byteBuffer);
        System.out.println(byteBuffer.get());
    }
}
```

**결과**

```bash
java.nio.HeapByteBuffer[pos=0 lim=5 cap=5]
java.nio.HeapByteBuffer[pos=1 lim=5 cap=5]
java.nio.HeapByteBuffer[pos=0 lim=1 cap=5] // 모드가 변경 되었음을 확인
3
```

아까 넣었던 ‘3’이라는 데이터가 출력되는 것을 볼 수 있다. 쓰기 모드였다가 읽기 모드로 변경 시 pos를 0으로 초기화하고 lim을 현재 pos인 1로 바꾼다. **1byte만 put()** 했기 때문에 **lim**을 **1**로 바꾸는 것이다.

**추가 사항**

이런 식으로 입력 모드 변환 후 다시 출력 모드로 변환하였을 때 값을 확인해 보면

```java
				**var byteBuffer = ByteBuffer.allocate(5);
        System.out.println(byteBuffer);

        byteBuffer.put("hel".getBytes());
        System.out.println(byteBuffer);

        byteBuffer.flip(); // 읽기** **모드로 변환
        System.out.println(byteBuffer);
        byteBuffer.flip(); // 쓰기 모드로 변환
        System.out.println(byteBuffer);**
```

**결과**

이런 식으로 결과가 나온다

```java
java.nio.HeapByteBuffer[pos=0 lim=5 cap=5] // 기본(쓰기 모드)
java.nio.HeapByteBuffer[pos=3 lim=5 cap=5] // put()으로 값 할당 후
java.nio.HeapByteBuffer[pos=0 lim=3 cap=5] // 읽기 모드로 변환 후
java.nio.HeapByteBuffer[pos=0 lim=0 cap=5] // 쓰기 모드로 다시 변환 후
```

filp()으로 읽기 모드로 변환 시 lim가 넣었던 byte 크기(pos) 만큼으로 변환 되는것을 볼 수 있었다.

그리고 다시 한번 filp()을 실행할 때 lim이 다시 pos로 변환되어 0이 되는 것을 볼 수 있다.

뭔가 모드 변경이라고 보긴 애매한 느낌이 든다.

### rewind()

rewind()를 사용할 시에

```java
      	var byteBuffer = ByteBuffer.allocate(5);
        System.out.println(byteBuffer);

        byteBuffer.put("hel".getBytes());
        System.out.println(byteBuffer);

        byteBuffer.rewind(); // 읽기 모드로 변환
        System.out.println(byteBuffer);
        System.out.println(byteBuffer.get());
```

**결과**

lim 값이 유지 되는 것을 볼 수 있다.

```java
**java.nio.HeapByteBuffer[pos=0 lim=5 cap=5]
java.nio.HeapByteBuffer[pos=3 lim=5 cap=5]
java.nio.HeapByteBuffer[pos=0 lim=5 cap=5]
104**
```

### ByteBuf

바이트 데이터를 읽고 쓰는 저장소이다.

읽기와 쓰기에 대한 인덱스가 나눠져있다.

### 차이점

ByteBuffer는 flip을 통해 읽기와 쓰기를 변경하는데에 있어 계산을 해가면서 개발을 해야 하지만 ByteBuf는 filp을 하지 않아도 read index와 write index가 있기 때문에 읽고 쓰는 작업이 편리하다.

TODO 

1. nio Socket 통신(비동기) 
    1. Stream 기반 데이터 송수신
2. netty
    1. EventLoop
    2. ByteBuffer는 왜 netty에서 사용되지 않을까?
3. Channel
4. Executor
5. OSI 7계층에 대해 공부하자
