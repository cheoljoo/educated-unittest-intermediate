1\.  [발표자 : Live Coding   (엄청 잘함)](#발표자:livecoding엄청잘함)  
2\.  [개발 환경](#개발환경)  
3\.  [강의 내용 1일](#강의내용1일)  
3.1\.  [실습](#실습)  
3.1.1\.  [테스트를 구성하는 방법 - 3A (TDD)  vs BDD (행위주도개발)](#테스트를구성하는방법-3atddvsbdd행위주도개발)  
3.1.2\.  [테스트 픽스쳐](#테스트픽스쳐)  
3.1.3\.  [예외 테스트 기능](#예외테스트기능)  
3.1.4\.  [비기능 테스트 (성능 / 시간)](#비기능테스트성능/시간)  
3.1.5\.  [test 비활성화](#test비활성화)  
3.1.6\.  [배열 비교](#배열비교)  
3.1.7\.  [Hamcrest Matcher](#hamcrestmatcher)  
3.1.8\.  [Suite Fixture setup/teardown  ex.Terminal Test](#suitefixturesetup/teardownex.terminaltest)  
3.1.9\.  [google test](#googletest)  
3.2\.  [- reflection을 써야하는데 ....](#-reflection을써야하는데....)  
4\.  [기타](#기타)  
5\.  [새로운 언어](#새로운언어)  
6\.  [강의 2일차](#강의2일차)  
6.1\.  [실습](#실습-1)  
6.1.1\.  [parameterized Test](#parameterizedtest)  
6.1.2\.  [테스트 대역 (Test Double) : 대신 : stunt double](#테스트대역testdouble:대신:stuntdouble)  
6.1.2.1\.  [Test Stub Pattern](#teststubpattern)  
6.1.2.2\.  [Fake Object](#fakeobject)  
6.1.2.3\.  [Test Spy](#testspy)  
6.1.2.4\.  [Mock Object](#mockobject)  
6.1.3\.  [mockito :  호출 여부 / 횟수/ 순서 (반드시 제공되어져야 하는 기능)](#mockito:호출여부/횟수/순서반드시제공되어져야하는기능)  
6.2\.  [정리 - effective unit test (SOLID 원칙)](#정리-effectiveunittestsolid원칙)  
6.3\.  [기타](#기타-1)  
7\.  [markdown syntax](#markdownsyntax)  



<a name="발표자:livecoding엄청잘함"></a>

# 1\. 발표자 : Live Coding   (엄청 잘함)
윤찬식 (server serviec / android / **iphone** 개발가능) : android는 파편화 이슈가 매우 큼
chansigi@imguru.co.kr

<a name="개발환경"></a>

# 2\. 개발 환경
JDK 8
IntelliJ IDEA CE

<a name="강의내용1일"></a>

# 3\. 강의 내용 1일
- 내부에 assertion이 꼭 있어야 한다. 
- 단위 테스트가 안되는 부분은 빼 놓고 unit test를 한다.  (ex. GUI는 unit test 못한ㄷ.)
- private methods는 검증할수 없다. (private은 public methods의 가독성을 높이기 위한 것이다.  private은 public에서 호출되게 되므로 , private로 public으로 올려서라도 test를 해야 한다.)
- Early Testing : 설계 부터 -> 설계 단계의 defect를 발견하는 것임.  
  - MS는 SW를 어떻게 test하는가?
  - Google은 SW를 어떻게 test하는가? 별도의 testing 팀 (SDET) 유지 : 이 팀은 초반에 **자동화된** testing 환경구축 / jenkins등 이용 
  - sprint단위로 testing 수행
- 7,8년 전에 자동으로 test case를 생성하는게 인기 있었지만, 버그를 다 잡을수 없기 때문에 **test case를 갱신하고 update하는 작업이 필요**하다.
- 단위 : 함수 / methods
- SUT (system under test) : test 대상 시스템 - 단위 test 를 통해서 검증하기 원하는 test 영역
- integration test를 할때도 우리는 unit test를 이용한다.
- 추천책 : The complete guide to software testing  (싸이의 병특책)
- 단위 테스트 작성 비용 : 초반에 단위 test를 작성하기 힘들다. 전체적인 sw 개발시간은 증가할수밖에 없지만, 유지보수의 시간이 줄어든다고 본다. 
  - 문제를 발견하는 시간이 매우 줄어든다.  문제 찾기 위한 debugging 시간이 매우 줄어들고 , **debugger 사용 시간이 줄어들면 확실한 효과**를 보는 것이다.
  - 추천책 : xUnit
  - 어설프게 unit test를 적용할바에는 하지 않는 것이 낳다. 의미없는 단위 test는 하지 마라.
- 기타 :  
  - RX   에릭 마이어 linq
  - fzf https://github.com/junegunn/fzf
  - https://github.com/junegunn/vim-plug
- unit test 가치 : failure point를 제어한다. 내가 작성하는 곳에서 failure point가 나와야 한다.
  - 이런 것을 위해서는 **테스트 대역 (mock)**이 필요 (4가지) : failure point를 하나로 격리하는 목적
  - 테스트 쪽에서 반드시 알아야 하는 기술 : google test가 C++에 대한 답 -> 가장 휼륭함.
  - gtest : 1.7 ->1.8 gmock이 gtest에 병합
- 문서로써의 test
- 단위 테스트 작성 방법
  - 테스트는 실행하기 쉬워야 한다.
    1. 완전 자동 테스트 : 수동 조정없이 돌려볼수 있어야 한다.  환경 설정 필요없이 해야 한다. docker이용이 좋은 예이다.
    1. 자체 검사 테스트 : 직접 검사해보지 않아도 에러를 찾아내 알려줄수 있어야 한다.
    1. 반복되는 테스트 : 여러번 돌려도 같은 결과
    1. 독립적인 테스트 : 테스트별로 돌려볼수 있어야 한다. 수동으로 돌릴수 있어야 한다.   이름에 대한 규칙이 중요하다. 예외처리 구문들에 대한 여러개의 test case가 나온다. 이를 필요한 것만 하기 위해서 rule을 잘만들면 좋다.
  - 만들고 유지보수가 쉬워야 한다. : 단위테스트는 작아야 하고 , 한번에 하나만 테스트해야 한다.
    - test code안에서는 반복문이나 분기문이 없어야 한다.
  - 필요한 유지보수 비용이 최소화 : 영향 최소화 / 테스트 환경에 영향을 받지 않아야 한다.
    - DB가 설치되지 않아도 test가 되게 해야 한다.   강사의견) docker를 잘 활용하자.
- travis-ci 로 jenkins 대체 가능 / circleci (1개의 project만 무료)
- __test-driven development는 어렵다.**__  현실에서 환상은 많이 깨졌다.
- BDD 방식은 밖에서 안으로 방식 추천 : 고객 중심 
- 테스트 견해
  - 상태 검증 : ASSERTION으로 내부 확인
  - 동작 검증 : 바뀌는 값이 없을때 , 내부 method의 호출에 기반을 두는 검증 (어떤 호출 순서 , 호출 횟수)  / 모의 객체나 test spy를 많이 사용
- test case가 자연어 처럼 부드럽게 나와야 한다.

- xUnit test framework (Creator : Kent Beck)
  - C / C++  : google test 추천  (xunit 지원 / arm x86등 이식성 좋음)
  - Test Runner / Test Case (상속) / Text Fixtures (일련의 상태에 대한 setting) / Test Suites (동일한 사전 상태를 가지는 것들)
  - Tex Execution (setup() , teardown()) / Test Result Formatter (web에 게시)
  - assertions : 이것이 없으면 의미없는 test가 된다.
- 추천책
  - **effective unit testing**
  - xunit
  - 실용주의 Junit
  - art of unit testing : .NET기준으로만 되어진게 아님


<a name="실습"></a>

## 3.1\. 실습
- http://github.com/imguru/   Unittest날짜
  - https://github.com/imguru/GoogleTest_0722
  - https://github.com/imguru/GoogleTest_0722
- 하나의 SUT(CUT)에 대한 테스트 메소드를 하나의 테스트 케이스 클래스 안에 전부 집어 넣는다
- library도 같이 다 올려주는게 맞다.  
- google test는 정적 library를 사용하는게 원칙
- JetBrain에서는 빨간색 뜨면 "Alt+Enter" 누르면 도움이 된다.
- throws Exception 을 넣는 이유는 try catch를 내부에 가지지 않기 위해서이다.
- import static org.junit.Assert.*;  -> 명시적 실패 fail method
- vscode : googleTest Adapter  plugin 활용

<a name="테스트를구성하는방법-3atddvsbdd행위주도개발"></a>

### 3.1.1\. 테스트를 구성하는 방법 - 3A (TDD)  vs BDD (행위주도개발)
  1. arrange (준비) - /Given : 객체를 생성하고 적절하게 설정한다.
  1. act (실행) - / When : 객체에 적용을 가한다. 원하는 메소드를 호출한다.
  1. assert (단언) - / Then : 기대하는 바를 단언한다.
- Test Double (Test 대역) 
  - BDD는 자연어에 가깝다. 
  - Mocha (JS) : http://mochajs.org
  - spock framework (Java)
- test code의 품질 - effective unit testing
  1. 가독성 : test method name / test fail message   ex) 대상메소드_시나리오_기대값
    - JAVA와 같이 한글로 쓰면 좋으나 , C++에서는 이름이 한글로 안된다.  
  1. 유지보수성 : 내부에서 제어 구문을 사용해서는 안된다.
  1. 신뢰성 : 

<a name="테스트픽스쳐"></a>

### 3.1.2\. 테스트 픽스쳐
- 픽스쳐 설치 방법 1. inline fixture setup
  - 모든 픽스쳐 설치를 테스트 메소드 안에서 수행한다.
  - Pros : 인과관계를 쉽게 파악
  - Cons : 모든 테스트 메소드 안에서 각각 설치해야 하므로    코드 중복  / 이해가 어렵다.
- 픽스쳐 설치 방법 2. delegate setup (위임 설치) - 공통되는 것들을 함수로 뽑아낸다.
  - 테스트의 인과 관계를 쉽게 파악할수 있고, 픽스쳐 설치에 대한 복잡함을 캡슐호함으로써 , 각 테스트 메소드에 대한 이해도 쉽게 할수 있다.
- 픽스쳐 설치 방법 3. implicit setup (암묵적 설치)
  - xUnit test framework 이 제공하는 기능을 사용합니다.
  - Pros : 테스트 코드 중복 제거 / 불필요한 상호 작용을 감출수 있다.
  - Cons : 인과관계 이해 어렵다. 
  - xUnit test framework :신선한 픽스쳐 전략 .. 항상   tc=new class()로 수행을 시켜준다.
    - 이전 test가 이후 test에 영향을 미치지 않게 하기 위함임.
    - 4단계 테스트 패턴
      1. 픽스쳐를 설치하거나 관찰하기 위해 필요한 것을 집어 넣는 작업 setup() : @Before
      1. SUT와 상호 작용을 한다.   (do)
      1. 기대 결과가 나왔는지 확인한다.  (assert)
      4. 픽스쳐를 해체해서 테스트 이전 단계로 되돌려 놓는다.  teardown() : @After   -> assert에 의해서 fail 발생시 이후 routine은 수행되지 않는다. 그러나, teardown은 수행됨

<a name="예외테스트기능"></a>

### 3.1.3\. 예외 테스트 기능
- parseInt라는 함수에 잘못된 형식의 문자열을 보냈을때 , NumberFormatException이 발생하는지 여부를 검증하고 싶다.
  - junit3에서는 try catch로 넣어서 처리
  - junit4에서는 @Test (expected = NumberFormatException.class)으로 처리
  - junit5에서는 assertThrows(NumberFormatException.class , ()-> { parseInt(bad); });
  - **gtest : ASSERT_THROW MACRO**

<a name="비기능테스트성능/시간"></a>

### 3.1.4\. 비기능 테스트 (성능 / 시간)
- gtest는 제공하지 않는다. 
- junit4 :  @Test(timeout = 2000)    : ms 단위
- junit5 : assertTimeout(Duration.?? , () -> {  ~~ } );

<a name="test비활성화"></a>

### 3.1.5\. test 비활성화
- 전체 test의 결과에 영향을 주지 않고 test가 존재해야 한다는 사실은 알아야 할때
- junit4 : @Ignore (value=~~)
- junit5 : @Disabled(value = "작성중.....")
- gtest :disabled
  - https://stackoverflow.com/questions/7208070/googletest-how-to-skip-a-test

<a name="배열비교"></a>

### 3.1.6\. 배열 비교
- asswertArrayEquals

<a name="hamcrestmatcher"></a>

### 3.1.7\. Hamcrest Matcher
- google mock도 이것의 영향을 받음.
- 비교 표현의 확장 라이브러리
  - test 단언문을 작성할때 , 문맥적으로 자연스럽고 우아한 문장을 만들수 있도록 해준다.
- 자연어에 가까운 테스트 단언 구문을 작성하도록 한다.
- jMock library에서 독립해서 , Junit 4.4 이후로 정식 포함되었습니다.
  - JUnit5에서는 기본으로 포함되지 않습니다.
- assertThat(~~~)

<a name="suitefixturesetup/teardownex.terminaltest"></a>

### 3.1.8\. Suite Fixture setup/teardown  ex.Terminal Test
- 만약 픽스쳐를 설치하거나 해체하는게 느리다면 , 테스트가 너무 느려서 개발자들이 SUT가 변경되어도 매번 테스트를 자동으로 수행하지 않는다.
  - 개발하면서 누리는 효과가 있어야하는데 , off 시켜쓰면 생산성 문제가 발생한다.
- 해결책 : Suite Fixture setup/teardown
  - 모든 test가 시작하기 전과 끝나는 시점에 1번씩만 수행한다.
- 객체가 생성되기 이전에 호출되어야 하므로 static으로 만들어야 한다.
  - public static void setUpTestCase()     @BeforeClass     @AfterClass

<a name="googletest"></a>

### 3.1.9\. google test
- scripts
  - fuse_gtest_files.py directory를 하면
  - 0923 directory안에 gtest-all.cc 와 gtest.h가 있다.   이것을 가져가서 cross compile해서 쓰면 된다.
  - g++ ./gtest/gtest-all.cc -c -I.   -> gtest-all.o
  - ar rcv libgtest.a gtest-all.o   정적 라이브러리로 만들기
- gmock을 쓰고 싶으면
  - scripts에 fuse_gmock_files.py   : 한 곳에 모아서 capsule화 해주는 것이다.
  - rm libgtest.a *.o
  - gmock-gtest-all.cc 만 컴파일 하면 됨.
  - g++ -> *.o
  - ar
  - gmock_main.cc 를 제공됨. 
- README.md 를 보면 사용법이 나옴.  # Build
- googletest/googlemock/scripts/generator/gmock_gen.py 를 이용하여 header를 지정해주면 자동으로 mock을 만들어줌.
  - public인 것을 만들어준다.
  - virtual로 선언되어져있어야만 된다.
<a name="-reflection을써야하는데...."></a>

  3.2\. - reflection을 써야하는데 ....
- 

<a name="기타"></a>

# 4\. 기타
- gmock-global 이라는 것을 참조하면  , C 함수들도 대체가능할 것으로 보인다고 강사님의 의견을 주심.

<a name="새로운언어"></a>

# 5\. 새로운 언어
- GO - class 없음.  python같은 C
- RUST

<a name="강의2일차"></a>

# 6\. 강의 2일차

<a name="실습-1"></a>

## 6.1\. 실습

<a name="parameterizedtest"></a>

### 6.1.1\. parameterized Test
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

<a name="테스트대역testdouble:대신:stuntdouble"></a>

### 6.1.2\. 테스트 대역 (Test Double) : 대신 : stunt double
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

<a name="teststubpattern"></a>

#### 6.1.2.1\. Test Stub Pattern
- 다른 컴포넌트로부터의 간접 입력에 의존하는 로직을 독립적으로 검증하고 싶다.
  - 실제 의존하는 객체를 테스트용 객체로 교체해서 , SUT가 테스트하는데 **필요한 결과를 보내도록 설계한다.**
  - 목적 : 특수한 상황을 시뮬레이션 한다. (시간 , 네트워크 , 환경)
  - ex. Connection class대신 BadConnection을 만들어서 , test할때는 new BadConnection을 만들어 넣어주면 된다. interface가 있어야 한다.
- C++에서는 모두 overriding을 해야 하므로 , virtual로 선언되어져야 한다.
  - 실제로도 원칙적으로 외부에서 호출하는 함수들은 모두 virtual이어야 하고 , google도 외부에서 호출하는 함수는  대문자로 시작하고 가상함수로 되어져있다.

<a name="fakeobject"></a>

#### 6.1.2.2\. Fake Object
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

<a name="testspy"></a>

#### 6.1.2.3\. Test Spy
- SUT의 method를 호출할때 , 발생하는 부수 효과를 관찰할 수 없어 테스트 안된 요구사항을 검증하고 싶다.
  - 목격한 일을 기록해두었다가 , 나중에 테스트에서 확인할수 있또록 만들어진 테스트 대역.
- target의 write가 호출되면 이 부분을 기록했다가 assertion하겠다고함.
  - SpyTarget::write에서는 하나의 문자열에 모든 내용을 적어둘 것이라고함.
  - SpyTarget::isReceived  와 같이 테스트를 위한 메소드를 제공해야 한다.
  - DlogTest  testcase { spy1,spy2를 넣어 수행한후에 assert로 확인 }

<a name="mockobject"></a>

#### 6.1.2.4\. Mock Object
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
  - example
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
      for (Target* e : targets){
      }
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
- [Google Eample](https://github.com/imguru/GoogleTest_0722)  <- 위 수업과 같은 내용에 대한 google test version

<a name="mockito:호출여부/횟수/순서반드시제공되어져야하는기능"></a>

### 6.1.3\. mockito :  호출 여부 / 횟수/ 순서 (반드시 제공되어져야 하는 기능)
- interface가 아닌 class에서도 사용할수 있다.   Point mokedPoint = mock(Point.class)
- 행위 기반 검증 : 관찰해야 하는 상태가 변하지 않아 ,  호출 여부 등만 확인 필요할 때
  - verify(mockedList).add("one");  // add("one")를 호출한 적이 있는가?  호출 여부만을 검증  
- 호출 횟수 &  :  verify(mockedList,times(1)).add("once");  verify(mockedList,times(2)).add("twice");
  - 기본 1번을 가정하므로 , 2번 호출되면 fail이다. 
  - time(?)
  - atLeast(N) : N번 이상
  - atMost(N) : N번 이하
  - verify(mockedList).add( anyString() ) : 인자 상관없이.    anyInt()
    - google test는 add(_) 로 표시하면됨.
- 호출 순서
  - 일반적으로 순서를 확인하지 않습니다.
  - InOrder 객체를 넣으면 순서를 확인한다.
    - InOrder inOrder = inOrder(mockedList);    inOrder.verify(mockedList).add("first"); ....
- stub 처리도 가능하다.
- mockito에서는
  - mock/ stub는 동일 합니다.  mock() , spy()
  - mock은 실제로 호출이 발생하지 않고 , spy는 호출이 발생합니다.
```cpp
#include <stdio.h>

class User {
private : 
int age;
public:
User(): age(42){}
};

#define private public    // 이렇게 넣으면 처리 public으로 처리 됨
#define class struct      // class 처음에 default private인 것을 이용할때
#include "add.c"        // add.c안에 함수 선언을 static 으로 했을때
#include "User.h"
class TestUser : public User {    // User.h안에 protected로 선언된 것이 있을때
public 
  using User::age;    // 부모의 멤버 변수 / 함수의 접근 레벨을 변경하는 방법
};

int main(){
User user;
printf("%d\n",user.age);   // fail
}
```

<a name="정리-effectiveunittestsolid원칙"></a>

## 6.2\. 정리 - effective unit test (SOLID 원칙)
- 인터페이스 단일 책임의 원칙
- 의존성 주입 방식 설계를 해야 한다.
- MVC -> MVP / MVVM 로 변경
  - MVC : M만 unit test 가능
  - MVP : M P
  - MVVM :  M VM 에 단위 test 적용 가능 - Data Binding을 통해 ~~~
- 복잡한 private method를 피하라.  public method의 가독성을 높이기 위한 모듈의 역할로 제안
- 정적 멤버 함수를 피하라.
- new는 신중하게 사용하라. 
- singleton을 피하라.
- 상속보다는 컴포지션을 사용하라. 
- 종속성을 줄여라.  객체 생성과 로직 수행을 분리하는 것이 좋다.  given when then처럼...
- 생성자는 간단하게 만들어라.


<a name="기타-1"></a>

## 6.3\. 기타
- cppcon : cpp conference
- bullseye  : coverage tool instead of gcov
- google test의 listener를 제공하여 , 각기 들어가는 단계마다의 callback을 등록하게 했다.  확장하게 좋게 되어져있다.
  - RecordProperty는 XML output에 추가가되는 것이다.
- TDD는 behaviour verification을 기준으로 하고 ,  mock을 해서 쓰는 것을 기본으로 한다.

  

<a name="markdownsyntax"></a>

# 7\. markdown syntax
  - __file__
  - **file**
  - \__file__
  - _\_file__
  - __file\__
  - __file_\_
  - _file_
  - \___file___
  - _\__file__
  - _\__file___
  - \_\_file\_\_
  
