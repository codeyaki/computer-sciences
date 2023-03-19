# 싱글톤 패턴 (Single Ton)

### 싱글톤 패턴이란?
싱글톤은 클래스를 구현할때 메모리상에 하나의 인스턴스만 존재하게 하여 사용하는 패턴

### 왜 사용 하나요?
1. 객체를 구현할때 메모리 리소스가 사용된다. 한개의 전역 객체로 만들어 둔다면 이러한 리소스낭비를 줄일 수 있기 때문입니다!
2. 어디에서나 접근 가능하도록 만들기 위함입니다.

### 언제 사용하나요?
데이터베이스 커넥트 풀과 같이 같은 객체를 자주 사용하는 경우에 사용하면 좋아요!

### 문제점
싱글톤에 많은 역할들이 담기게 되면 객체지향원칙에 어긋나게 된다.  
  => 유지보수가 힘들어 진다.  
만약 멀티 스레드 환경에서 동기화 문제를 처리하지 않는다면 2개가 생기는 문제가 발생할 수 있습니다.

### 구현 방법 (자바)
1. 다른 객체들이 싱글턴 클래스와 함께 new 연산자를 사용하지 못하도록 디폴트 생성자를 private으로 설정  
2. 생성자 역할을 하는 정적 생성 메서드 생성
    내부적으로 이 메서드는 최초 호출 시 객체를 만들기 위하여 비공개 생성자를 호출한 후 객체를 정적 필드에 저장 
    그 이후 호출들은 모두 저장되어있는 객체를 반환

### 구현 예시
1. 기본 방법
<pre>
  <code>
public class Singleton(){
    private static Singleton instance;

    // 생성자를 private로 만들기
    private Singleton(){
    }

    public static Singleton getInstance(){
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}
  </code>
</pre>

2. JDBC template 만들기 ( 세션 관리 )
<pre>
<code>
import java.io.IOException;
import java.io.InputStream;

import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;

public class Template {
	
	private static SqlSessionFactory sqlSessionFactory;
	
	public static SqlSession getSqlSession() {
		
		if(sqlSessionFactory == null) {
			
			String resource = "mybatis-config.xml";
			
			try {
				InputStream inputStream = Resources.getResourceAsStream(resource);
				sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
			} catch (IOException e) {
				e.printStackTrace();
			}
		}
		
		return sqlSessionFactory.openSession(false);
	}
}
</code>
</pre>
