---
sidebar_position: 10
---

# 🍭 Chapter 9: 단위 테스트

## 🎃 TDD 법칙 세 가지
- 첫째 법칙: 실패하는 단위 테스트를 작성할 때까지 실제 코드를 작성하지 않는다.
- 둘째 법칙: 컴파일은 실패하지 않으면서 실행이 실패하는 정도로만 단위 테스트를 작성한다.
- 셋째 법칙: 현재 실패하는 테스트를 통과할 정도로만 실제 코드를 작성한다.

위 세 가지 규칙을 따르면 개발과 테스트가 대략 30초 주기로 묶인다. 테스트 코드와 실제 코드가 함께나올뿐더러 테스트 코드가 실제 코드보다 불과 몇 초 전에 나온다.   

이렇게 일하면 매일 수십 개, 매달 수백 개, 매년 수천 개에 달하는 테스트 케이스가 나온다. 이렇게 일하면 실제 코드를 사실상 전부 테스트하는 테스트 케이스가 나온다. 하지만 실제 코드와 맞먹을 정도로 방대한 테스트 코드는 심각한 관리 문제를 유발하기도 한다.

## 🎃 깨끗한 테스트 코드 유지하기
테스트 코드가 지저분할수록 변경하기 어려워진다. 테스트 코드가 복잡할수록 실제 코드를 짜는 시간보다 테스트 케이스를 추가하는 시간이 더 걸리기 십상이다. 실제 코드를 변경해 기존 테스트 케이스가 실패하기 시작하면, 지저분한 코드로 인해, 실패하는 테스트 케이스를 점점 더 통과시키기 어려워진다. 그래서 테스트 코드는 계속해서 늘어나는 부담이 되버린다.   

테스트 슈트가 없으면 개발자는 자신이 수정한 코드가 제대로 도는지 확인할 방법이 없다. 테스트 슈트가 없으면 시스템 이쪽을 수정해도 저쪽이 안전하다는 사실을 검증하지 못한다. 그래서 결함율이 높아지지 시작한다. 의도하지 않은 결함 수가 많아지면 개발자는 변경을 주저한다. 변경하면 득보다 해가 크다 생각해 더 이상 코드를 정리하지 않는다. 그러면서 코드가 망가지기 시작한다. 결국 테스트 슈트도 없고, 얼기설기 뒤섞인 코드에, 좌절한 고객과, 테스트에 쏟아 부은 노력이 허사였다는 실망감만 남긴다.   

내가 이야기가 전하는 교훈은 다음과 같다. **테스트 코드는 실제 코드 못지 않게 중요하다.** 테스트 코드는 이류 시민이 아니다. 테스트 코드는 사고와 설계와 주의가 필요하다. 실제 코드 못지 않게 깨끗하게 짜야 한다.   

### 🎈 테스트는 유연성, 유지보수성, 재사용성을 제공한다
테스트 코드를 깨끗하게 유지하지 않으면 결국 잃어버린다. 그리고 테스트 케이스가 없으면 실제 코드를 유연하게 만드는 버팀목도 사라진다. 맞다, 제대로 읽었다. 코드에 유연성, 유지보수성, 재사용성을 제공하는 버팀목이 바로 **단위 테스트**다. 이유는 단순하다. 테스트 케이스가 있으면 변경이 두렵지 않으니까! 테스트 케이스가 없다면 모든 변경이 잠정적인 버그다. 아키텍쳐가 아무리 유연하더라도, 설계를 아무리 잘 나눴더라도, 테스트 케이스가 없으면 개발자는 변경을 주저한다. 버그가 숨어들까 두렵기 때문이다.   

하지만 테스트 케이스가 **있다면** 공포는 사실상 사라진다. 테스트 커버리지가 높을수록 공포는 줄어든다. 아키텍처가 부실한 코드나 설계가 모호하고 엉망인 코드라도 별다른 우려 없이 변경할 수 있다. 아니, 오히려 안심하고 아키텍처와 설계를 개선할 수 있다.   

그러므로 실제 코드를 점검하는 자동화된 단위 테스트 슈트는 설계와 아키텍처를 최대한 깨끗하게 보존하는 열쇠다. 테스트는 유연성, 유지보수성, 재사용성을 제공한다. 테스트 케이스가 있으면 **변경**이 쉬워지기 때문이다.   

따라서 테스트 코드가 지저분하면 코드를 변경하는 능력이 떨어지면 코드 구조를 개선하는 능력도 떨어진다. 테스트 코드가 지저분할수록 실제 코드도 지저분해진다. 결국 테스트 코드를 잃어버리고 실제 코드도 망가진다.

## 🎃 깨끗한 테스트 코드
깨끗한 테스트 코드를 만들려먼? 세 가지가 필요하다. 가독성, 가독성, 가독성. 어쩌면 가독성은 실제 코드보다 테스트 코드에 더더욱 중요하다. 테스트 코드에서 가독성을 높이려면? 여느 코드와 마찬가지다. 명료성, 단순성, 풍부한 표현력이 필요하다. 테스트 코드는 최소의 표현으로 많은 것을 나타내야 한다.

```java
public void testGetPageHierarchyAsXml() throws Exception {
  makePages("PageOne", "PageOne.ChildOne", "PageTwo");

  submitRequest("root", "type:pages");

  assertResponseIsXML();
  assertResponseContains(
    "<name>PageOne</name>", "<name>PageTwo</name>", "<name>ChildOne</name>"
  );
}

public void testSymbolicLinksAreNotInXmlPageHierarchy() throws Exception {
  WikiPage page = makePage("PageOne");
  makePages("PageOne.ChildOne", "PageTwo");

  addLinkTo(page, "PageTwo", "SymPage");

  submitRequest("root", "type:pages");

  assertResponseIsXML();
  assertResponseContains(
    "<name>PageOne</name>", "<name>PageTwo</name>", "<name>ChildOne</name>"
  );
  assertResponseDoesNotContain("SymPage");
}

public void testGetDataAsXml() throws Exception {
  makePageWithContent("TestPageOne", "test page");
  submitRequest("TestPageOne", "type:data");

  assertResponseIsXML();
  assertResponseContains("test page", "<Test");
}
```

각 테스트는 명확히 세 부분으로 나눠진다. 첫 부분은 테스트 자료를 만든다. 두 번째 부분은 테스트 자료를 조작하며, 세 번째 부분은 조작한 결과가 올바른지 확인한다.   

잡다하고 세세한 코드를 거의 다 없앴다는 사실에 주목한다. 테스트 코드는 본론에 돌입해 진짜 필요한 자료 유형과 함수만 사용한다. 그러므로 코드를 읽는 사람은 온갖 잡다하고 세세한 코드에 주눅들고 헷갈릴 필요 없이 코드가 수행하는 기능을 재빨리 이해한다.   

## 🎃 테스트 당 assert 하나
JUnit으로 테스트 코드를 짤 때는 함수마다 `assert` 문을 단 하나만 사용해야 한다고 주장하는 학파가 있다. 가혹한 규칙이라 여길지도 모르지만, 확실히 장점이 있다. `assert` 문이 단 하나인 함수는 결론이 하나라서 코드를 이해하기 쉽고 빠르다.

```java
public void testGetPageHierarchyAsXml() throws Exception {
  givenPage("PageOne", "PageOne.ChildOne", "PageTwo");

  whenRequestIsIssued("root", "type:pages");

  thenResponseShouldBeXML();
}

public void testGetPageHierarchyHasRightTags() throws Exception {
  givenPage("PageOne", "PageOne.ChildOne", "PageTwo");

  whenRequestIsIssued("root", "type:pages");

  thenResponseShouldContain(
    "<name>PageOne</name>", "<name>PageTwo</name>", "<name>ChildOne</name>"
  );
}
```

위에서 함수 이름을 바꿔 `given-when-then`이라는 관례를 사용했다는 사실에 주목한다. 그러면 테스트 코드를 읽기가 쉬워진다. 불행하게도, 위에서 보듯이, 테스트를 분리하면 중복되는 코드가 많아진다.   

TEMPLATE METHOD 패턴을 사용하면 중복을 제거할 수 있다. `given/when` 부분을 부모 클래스에 두고 `then` 부분을 자식 클래스에 두면 된다. 아니면 완전히 독자적인 테스트 클래스를 만들어 `@Before` 함수에 `given/when` 부분을 넣고 `@Test` 함수에 `then` 부분을 넣어도 된다. 하지만 모두가 배보다 배꼽이 더 크다. 이것저것 감안해 결국 `assert` 문을 여럿 사용하는 편이 좋다고 생각한다.   

나는 단일 `assert` 문이라는 규칙이 훌륭한 지침이라 생각한다. 대체로 나는 단일 `assert`를 지원하는 해당 분야 테스트 언어를 만들려 노력한다. 하지만 때로는 주저 없이 함수 하나에 여러 `assert` 문을 넣기도 한다. 단지 `assert` 문 개수는 최대한 줄여야 좋다는 생각이다.

### 🎈 테스트 당 개념 하나
이것저것 잡다한 개념을 연속으로 테스트하는 긴 함수는 피한다. 각 절에 `assert` 문이 여럿이라는 사실이 문제가 아니다. 한 테스트 함수에서 여러 개념을 테스트한다는 사실이 문제다. 그러므로 가장 좋은 규칙은 *개념 당 `assert` 문 수를 최소로 줄여라*와 *테스트 함수 하나는 개념 하나만 테스트하라*라 하겠다.

## 🎃 F.I.R.S.T
깨끗한 테스트는 다음 다섯 가지 규칙을 따르는데, 각 규칙에서 첫 글자를 따오면 FIRST가 된다.   

**빠르게**: 테스트는 빨라야 한다. 테스트는 빨리 돌아야 한다는 말이다. 테스트가 느리면 자주 돌릴 엄두를 못 낸다. 자주 돌리지 않으면 초반에 문제를 찾아내 고치지 못한다. 코드를 마음껏 정리하지도 못한다. 결국 코드 품질이 망가지기 시작한다.   

**독립적으로**: 각 테스트는 서로 의존하면 안 된다. 한 테스트가 다음 테스트가 실행될 환경을 준비해서는 안 된다. 각 테스트는 독립적으로 그리고 어떤 순서로 실행해도 괜찮아야 한다. 테스트가 서로에게 의존하면 하나가 실패할 때 나머지도 잇달아 실패하므로 원인을 진단하기 어려워지며 후반 테스트가 찾아내야 할 결함이 숨겨진다.   

**반복가능하게**: 테스트는 어떤 환경에서도 반복 가능해야 한다. 실제 환경, QA 환경, 버스를 타고 집으로 가는 길에 사용하는 노트북 환경에서도 실행할 수 있어야 한다. 테스트가 돌아가지 않는 환경이 하나라도 있다면 테스트가 실패한 이유를 둘러댈 변명이 생긴다. 계다가 환경이 지원되지 않기에 테스트를 수행하지 못하는 상황에 직면한다.   

**자가검징하는**: 테스트는 부울(bool) 값으로 결과를 내야 한다. 성공 아니면 실패다. 통과 여부를 알려고 로그 파일을 읽게 만들어서는 안 된다. 통과 여부를 보려고 텍스트 파일 두 개를 수작업으로 비교하게 만들어서도 안 된다. 테스트가 스스로 성공과 실패를 가늠하지 않는다면 판단은 주관적이 되며 지루한 수작업 평가가 필요하게 된다.

**적시에**: 테스트는 적시에 작성해야 한다. 단위 테스트는 테스트하려는 실제 코드를 구현하기 직전에 구현한다. 실제 코드를 구현한 다음에 테스트 코드를 만들면 실제 코드가 테스트하기 어렵다는 사실을 발견할지도 모른다. 어떤 실제 코드는 테스트하기 너무 어렵다고 판명날지 모른다. 테스트가 불가능하도록 실제 코드를 설계할지도 모른다.

## 🎃 결론
테스트 코드는 실제 코드만큼이나 피로젝트 건강에 중요하다. 어쩌면 실제 코드보다 더 중요할지도 모르겠다. 테스트 코드는 실제 코드의 유연성, 유지보수성, 재사용성을 보존하고 강화하기 때문이다. 그러므로 테스트 코드는 지속적으로 꺠끗하게 관리하자. 표현력을 높이고 간결하게 정리하자. 테스트 API를 구현해 도메인 특화 언어(DSL)를 만들자. 그러면 그만큼 테스트 코드를 짜기가 쉬워진다.   

테스트 코드가 방치되어 망가지면 실제 코드도 망가진다. 테스트 코드를 깨끗하게 유지하자.
