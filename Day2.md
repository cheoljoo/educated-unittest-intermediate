
# 강의 2일차

# 실습

### parameterized Test
- xUnit test framework 에서 지원해야 사용할수 있습니다.
- 정의 : 입력 데이터를 바꿔가면서 , 수차례 반복 검사하는 테이터 중심 테스트의 중복을 업애주는 기법
  - 단언 메소드는 실패할 경우 이후의 코드를 수행하지 않는다.
  - 하나의 테스트 메소드 안에서 여러개의 단언문을 사용할 경우 , 죽은 단언문 문제가 발생합니다.
- 하나의 test case안에는 하나의 단언문(assert)만을 사용하는 것이 좋다. 
- Junit4
  1. Test Runner가 다르게 동작합니다.
    - @RunWith(value = Parameterized.class)
  1. 생성자에 대해서 전달되는 데이터는 static이어야 한다.
    - public static Collection<object[]> data()    : object[] - reflection을 통해 객체를 생성할때 , 생성자의 인자를 전달하는 타입
    - 반드시 생성자를 정의해야 한다. 한개씩 넘어오는 것이 생성자의 인자로 한개씩 넘어오게 된다.
  1. 입력된 데이터를 기반으로 다양한 테스트 메소드를 작성하면 된다.
- 단점
  1. 복잡하다. : xUnit Test Framework마다 사용하는 방법이 다르다
  1. 테스트의 실패의 경우 원인 데이터가 무엇인지 알기 어렵다. 
    - @Parameterized.Parameters(name="index} - v:{0}, e:{1}")
  1. TestCase 클래스를 별도로 작성해야 한다.
    - SUT에서 일반적으로 테스트와 파라미터화 테스트가 동시에 필요한 경우, 별도 작성 필요
- JUnit5
  - @TestFactory : stream 사용 (network or file로부터 읽을수도 있다)
    - dynamicTest : runtime에 테스트를 생성할수 있는 함수
  - Parameterize와 아닌 것을 합쳐서 쓸수 있다. 
- gootle test : 단언문 대신 EXPECT라는 것을 만들었다.
  - EXPECT_TRUE(isPrime(2))
  - TIDL 예제에 이렇게 사용한 것이 있다. 분석 필요하다.
  - parameterized와 일반 test case를 합쳐서 사용할수가 없다. 별도로 Test class를 생성해주어야 한다.
  - EXPECT를 많이 사용한다. 
- CI가 github에 통합되고 있다고함.  (살펴봐야 할 내용임)
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
- 
