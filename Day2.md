
# 강의 2일차

## 실습

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

### 테스트 대역 (Test Double) : 대신 : stunt double
- Stub : 외부 의존물이나 협력 객체를 간단하게 대신하기 위해 쓰이는 "제어가능한" 테스트 대역
- test 전반을 통제할수 있어야 한다.
- 강한 결함
  - 구체적인 타입을 직접 사용하는 경우 
- 약한 결합
  - 협력 객체를 이용할때 , 인터페이스나 추상 타입을 통해 이용해야 한다.
  - interface 기반으로 변환이 되어야 한다.  @override
  - 협력 객체를 직접 생성하면 안된다. new 연산은 강한 결합을 발생하는 연산이다.
    - 협력 객체를 외부에서 생성해서 전달 받아야 합니다. DI (Dependency Injection) 으로 사용해야 한다.
    1. 생성자 주입 : 협력 객체가 필수적일때
    1. 메소드 주입 : 협력 객체가  메소드를 호출할때만 필요할때
- DI (의존성 주입)의 문제점
  - 보일러 플레이트 : 반드시 필요하지만, 반복적으로 발행하는 코드
    - Logger -> FileSystemManager , LoggerManager 라면 , Logger를 생성하기 위해서는 의존하는 것 생성해서 주입하는 코드가 반복적으로 생성된다.
  - 보일러 플레이트의 문제를 해결하기 위해서 , 의존성 주입 framework을 사용하는 것이 좋습니다.  (C++ : boost library)
    - JAVA : Dagger (Dagger의 문제점은 성능) , **Dagger2** (compile time에 해결하여 많이 사용하고 있음)
    - [Dagger2](https://medium.com/@maryangmin/di-%EA%B8%B0%EB%B3%B8%EA%B0%9C%EB%85%90%EB%B6%80%ED%84%B0-%EC%82%AC%EC%9A%A9%EB%B2%95%EA%B9%8C%EC%A7%80-dagger2-%EC%8B%9C%EC%9E%91%ED%95%98%EA%B8%B0-3332bb93b4b9)
  - 틈새 만들기 : 가능하면 기존 code가 깨지지 않게... (art of unitest)
    - 생성자() 일때도 기존의 코드가 수정 없이 , 동작하도록 만들어 두어야 한다. 
- 결과가 정해져있는 테스트 애격 - Stub
  - 테스트 전용 클래스
- 외부 라이브러리를 사용할때는 강한 결함만 될텐데.. 이때는?  
- Mokito 라는 라이브러리를 이용하여 자동으로 mock 처리하는 방법이 있다. [mokito](https://github.com/tpounds/mockitopp)  [Medium](https://medium.com/@maryangmin/di-%EA%B8%B0%EB%B3%B8%EA%B0%9C%EB%85%90%EB%B6%80%ED%84%B0-%EC%82%AC%EC%9A%A9%EB%B2%95%EA%B9%8C%EC%A7%80-dagger2-%EC%8B%9C%EC%9E%91%ED%95%98%EA%B8%B0-3332bb93b4b9)
- Test Double Pattern
  1. test Stub
  1. Fake Object
  1. Test Spy
  1. Mock Object

#### Test Stub Pattern
- 다른 컴포넌트로부터의 간접 입력에 의존하는 로직을 독립적으로 검증하고 싶다.
  - 실제 의존하는 객체를 테스트용 객체로 교체해서 , SUT가 테스트하는데 **필요한 결과를 보내도록 설계한다.**
  - 목적 : 특수한 상황을 시뮬레이션 한다. (시간 , 네트워크 , 환경)
  - ex. Connection class대신 BadConnection을 만들어서 , test할때는 new BadConnection을 만들어 넣어주면 된다. interface가 있어야 한다.
- C++에서는 모두 overriding을 해야 하므로 , virtual로 선언되어져야 한다.
  - 실제로도 원칙적으로 외부에서 호출하는 함수들은 모두 virtual이어야 하고 , google도 외부에서 호출하는 함수는  대문자로 시작하고 가상함수로 되어져있다.

#### Fake Object
- 가볍게 컴포넌트를 만들어주어 대신 사용한다. (ex. Database)

1. **아직 만들어지지 않은 컴포넌트**에 의존하는 객체를 검증하고 싶다.
1. 의존 객체가 너무 느려서 , 테스트 하기 힘들다.
1. 의존 객체를 사용하기 어려울때 사용할수 있다.

- 보통 database 예제들이 많다
  - test에 필요한 최소한의 database기능을 만들어준다.
  - new UserManager ( new FakeDatabase() );
- 문제점 
  - test code의 유지보수성이 떨어질수 있다.
- assertEquals 일때는 연산자 override을 만들어주어야 한다.
- project Lombok : @Data만 class앞에 붙이면 자동으로 get/set 등을 모두 만들어준다. [Lombok](https://projectlombok.org/)

#### Test Spy
- SUT의 method를 호출할때 , 발생하는 부수 효과를 관찰할 수 없어 테스트 안된 요구사항을 검증하고 싶다.
  - 목격한 일을 기록해두었다가 , 나중에 테스트에서 확인할수 있또록 만들어진 테스트 대역.
- target의 write가 호출되면 이 부분을 기록했다가 assertion하겠다고함.
  - SpyTarget::write에서는 하나의 문자열에 모든 내용을 적어둘 것이라고함.
  - SpyTarget::isReceived  와 같이 테스트를 위한 메소드를 제공해야 한다.
  - DlogTest  testcase { spy1,spy2를 넣어 수행한후에 assert로 확인 }

#### Mock Object
- SUT의 method를 호출할때  발생하는 부수 효과를 관찰할 수 없어 테스트 안된 요구사항을 검증하고 싶다.
  - Mock Object (모의 객체)
- 테스트 수행 방법 2가지
  1. state verification (상태 검증)
    - test에 검증할수 있는 상태가 존재할때 사용하는 방법
  1. Behavior Verification (**행위 검증**)
    - 올바른 로직 수행의 판단의 근거로 특정한 동작의 수행 여부를 검증하는 방법
      - 호출 여부 / 횟수 / 순서 / 인자
      - Mock Framework
        - JAVA : jMock , EasyMock , **Mockito** , Spock (Groovy)
        - C++ : **Google Mock** , mokito가 있지만 사망한 프로젝트
- mockito
  - test double을 동적으로 생성할수 있습니다.
  - verify()로 확인 : assertion대신 verify사용하고 이것은 EXPECT처럼 동작함. (fail되어도 stop하지 않음)

- google mock을 이용한 같은 동작 (5분)
  - 
```cpp
<gmock/gmock.h>
<gtet/gtest.h>

struct Target {
virtual void write(const std::string& message) = 0;
};

class DLog {
std::vector<Target*> targets;

public:
void addTarget(Target* t) {
  targets.push_back(t);
}
void write(const std::string& message){
  for
};

```
  - googletest/googlemock/scripts/generator/gmock_gen.py Target.h
    - 알아서 추가됨.
  - TEST(... {
    - MockTarget mock1;
    - // expect 
    - EXPECT_CALL(
    - // act
    - add(mock1)
-
-
-
-
-
- 기타
  - cppcon : cpp conference
