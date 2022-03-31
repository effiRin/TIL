
# Connection

## Socket = Connection = Session
- 데이터베이스에선 소켓(Socket)을 '커넥션'이라고 부르고, '세션'이라는 용어를 사용하기도 한다.  
- '커넥션을 맺는다'고 하는 동시에 '세션을 맺는다'고도 표현한다.  
<br>


## Connection 맺을 때 주의할 사항
1. 반드시 close()를 해준다.  
close()는 주로 네트워크 연결 중 '입출력'에서 주로 필요로 하는 작업이다. 연결을 맺고 모든 작업이 수행된 후, close()를 해줘야 DB가 죽는 것을 예방할 수 있다.  
  
<br>

2. 로컬 변수를 잡는다.  
데이터 베이스 관련된 사항은 대부분 로컬 변수로 잡아야 안전하다. 

<br>

## 스트레스 테스트 - close()의 여부   
  
팀원들이 사용자가 되어, 팀원 중 1명의 서버를 스레드로 계속해서 호출한다. 이때, close()를 닫지 않은 경우와 닫은 경우를 나누어 연결이 정상적으로 이루어지는지 확인해 본다.

<br>

### Close()를 닫지 않았을 때

```java
import org.junit.jupiter.api.Test;

import java.sql.Connection;
import java.sql.DriverManager;

public class JDBCTest {

    @Test
    public void test1() throws Exception {
        System.out.println("test1....");

        Class.forName("oracle.jdbc.driver.OracleDriver"); //

        String url = "jdbc:oracle:thin:@192.168.0.000:0000:XE"; // ip 주소

        for (int i = 0; i < 100; i++) {
            new Thread(()-> {
                try {
                    Connection con =
                            DriverManager.getConnection(url, "name", "password");
                    System.out.println(con);

                }catch(Exception e) {
                    e.printStackTrace();
                }
                }).start();
        }
    }
}
```

<br>

### Close()를 닫았을 때

```java
import org.junit.jupiter.api.Test;

import java.sql.Connection;
import java.sql.DriverManager;

public class JDBCTest {

    @Test
    public void test1() throws Exception {
        System.out.println("test1....");

        Class.forName("oracle.jdbc.driver.OracleDriver"); //

        String url = "jdbc:oracle:thin:@192.168.0.000:0000:XE";

        for (int i = 0; i < 100; i++) {
            new Thread(()-> {
                try {
                    Connection con =
                            DriverManager.getConnection(url, "name", "password");
                    System.out.println(con);
                    con.close();

                }catch(Exception e) {
                    e.printStackTrace();
                }
                }).start();
        }
    }
}
```
  <br>

- 실습 결과
1. close() 닫지 않았을 때 - 오류 발생
2. close() 닫았을 때 - 정상 가동

-> 즉, close()를 해야 DB가 터지지 않고 정상적으로 가동된다.

<br>





