- markdown syntax
  - __file__
  - **file**
  - \__file__
  - _\_file__
  - __file\__
  - __file_\_
  

# 발표자 : Live Coding   (엄청 잘함)
윤찬식 (server serviec / android / **iphone** 개발가능) : android는 파편화 이슈가 매우 큼
chansigi@imguru.co.kr

# 개발 환경
JDK 8
IntelliJ IDEA CE

# 강의 내용 1일
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


## 실습
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

### 테스트를 구성하는 방법 - 3A (TDD)  vs BDD (행위주도개발)
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

### 테스트 픽스쳐
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

### 예외 테스트 기능
- parseInt라는 함수에 잘못된 형식의 문자열을 보냈을때 , NumberFormatException이 발생하는지 여부를 검증하고 싶다.
  - junit3에서는 try catch로 넣어서 처리
  - junit4에서는 @Test (expected = NumberFormatException.class)으로 처리
  - junit5에서는 assertThrows(NumberFormatException.class , ()-> { parseInt(bad); });
  - **gtest : ASSERT_THROW MACRO**

### 비기능 테스트 (성능 / 시간)
- gtest는 제공하지 않는다. 
- junit4 :  @Test(timeout = 2000)    : ms 단위
- junit5 : assertTimeout(Duration.?? , () -> {  ~~ } );

### test 비활성화
- 전체 test의 결과에 영향을 주지 않고 test가 존재해야 한다는 사실은 알아야 할때
- junit4 : @Ignore (value=~~)
- junit5 : @Disabled(value = "작성중.....")
- gtest :disabled
  - https://stackoverflow.com/questions/7208070/googletest-how-to-skip-a-test

### 배열 비교
- asswertArrayEquals

### Hamcrest Matcher
- google mock도 이것의 영향을 받음.
- 비교 표현의 확장 라이브러리
  - test 단언문을 작성할때 , 문맥적으로 자연스럽고 우아한 문장을 만들수 있도록 해준다.
- 자연어에 가까운 테스트 단언 구문을 작성하도록 한다.
- jMock library에서 독립해서 , Junit 4.4 이후로 정식 포함되었습니다.
  - JUnit5에서는 기본으로 포함되지 않습니다.
- assertThat(~~~)

### Suite Fixture setup/teardown  ex.Terminal Test
- 만약 픽스쳐를 설치하거나 해체하는게 느리다면 , 테스트가 너무 느려서 개발자들이 SUT가 변경되어도 매번 테스트를 자동으로 수행하지 않는다.
  - 개발하면서 누리는 효과가 있어야하는데 , off 시켜쓰면 생산성 문제가 발생한다.
- 해결책 : Suite Fixture setup/teardown
  - 모든 test가 시작하기 전과 끝나는 시점에 1번씩만 수행한다.
- 객체가 생성되기 이전에 호출되어야 하므로 static으로 만들어야 한다.
  - public static void setUpTestCase()     @BeforeClass     @AfterClass

### google test
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
  - reflection을 써야하는데 ....
- 

# 기타
- gmock-global 이라는 것을 참조하면  , C 함수들도 대체가능할 것으로 보인다고 강사님의 의견을 주심.

# 새로운 언어
- GO - class 없음.  python같은 C
- RUST
