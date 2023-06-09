# 9장 - 단위테스트

## TDD 법칙 세 가지

- **첫번째** 법칙: 실패하는 단위 테스트를 작성할 때까지 실제 코드를 작성하지 않는다.
- **두번째** 법칙: 컴파일은 실패하지 않으면서 실행이 실패하는 정도로만 단위 테스트를 작성한다.
- **세번째** 법칙: 현재 실패하는 테스트를 통과할 정도로만 실제 코드를 작성한다.

이런 방식으로 테스트 코드를 작성하다보면 사실상 전부 테스트하는 테스트 케이스가 나온다. 하지만 실제 코드와 맞먹을 정도로 방대한 테스트 코드는 심각한 관리 문제를 유발하기도 한다.

## 깨끗한 테스트 코드 유지하기

지저분한 테스트 코드는 테스트를 안하는 것보다, 오히려 더 못한 결과를 초래한다. 실제 코드가 변할수록 테스트 코드도 변해야 한다. 그런데 테스트 코드가 지저분할 수록 변경이 어려워지고, 테스트 코드가 복잡할 수록 실제 코드를 짜는 시간보다 테스트 케이스를 추가하는 시간이 더 걸리게 된다. 이렇게 반복된다면 실패하는 테스트 케이스를 점점 더 통과시키기 어려워지게 된다.

새 버전의 기능이 출시되면 팀이 테스트 케이스를 유지하고 보수하는 비용도 늘어난다. 그렇게 된다면 테스트 코드는 개발자들에게 불만으로 자리 잡히게 된다. 하지만 **테스트 슈트가 없다면 개발자는 자신이 수정한 코드가 제대로 동작하는지 확인할 수 있는 방법이 없다**. 결국 결함율이 높아지고, 개발자는 변경을 주저하게 되며, 코드의 변경이 득보다 해가 크다 생각해 더 이상 코드를 정리하지 않게 된다.

즉, **테스트 코드는 실제 코드 못지 않게 중요**하다.

### 테스트는 유연성, 유지보수성, 재사용성을 제공한다

코드에 유연성, 유지보수성, 재사용성을 제공하는 버팀목은 단위 테스트이다. 테스트 케이스가 존재하면 변경이 두렵지 않게 되기 때문이다. 또한 테스트의 커버리지가 높을수록 변경에 대한 공포는 사라지며 변경이 쉬워진다.

## 깨끗한 테스트 코드

깨끗한 테스트 코드를 만들기 위해서 가장 중요한 것은 바로 가독성이다. 오히려 실제 코드보다 테스트 코드에서의 가독성이 더 중요하다. 테스트 코드는 최소의 표현으로 많은 것을 나타내야 한다.

**BUILD - OPERATE - CHECK 패턴**이 테스트 구조에 적합하다. 첫 부분은 테스트 자료를 만든다. 두 번째로는 테스트 자료를 조작하고, 세 번째 부분은 조작한 결과가 올바른지 확인한다.

### [도메인에 특화된 테스트 언어](https://www.jetbrains.com/ko-kr/mps/concepts/domain-specific-languages/)

시스템 조작 API 를 사용하는 대신 API 위에 함수와 유틸리티를 구현한 후 그 함수와 유틸리티를 사용하기 때문에 테스트 코드를 짜기도 읽기도 쉬워진다. 구현한 함수와 유틸리티는 테스트 코드에서 사용하는 특수 API 가 된다.

즉, 테스트를 구현하는 당사자와 나중에 테스트를 읽어볼 독자를 도와주는 테스트 언어이다.

### 이중 표준

테스트 API 코드에 적용하는 표준은 실제 코드에 적용하는 표준과 확실히 다르다. **단순하고, 간결하고, 표현력이 풍부해야 하지만, 실제 코드만큼 효율적일 필요는 없다**. 실제환경에서 돌아가는 것이 아니라 테스트 환경에서 돌아가는 코드이기 때문이다.

실제 환경에서는 절대로 안 되지만 테스트 환경에서는 전혀 문제 없는 방식이 있다. 메모리나 CPU 효율과 관련 있는 경우이다. 코드의 깨끗함과는 철처하게 무관하다.

## 테스트 당 assert 하나

assert 문이 단 하나인 함수는 결론이 하나라서 코드를 이해하기 쉽고 빠르다.

**give - when - then** 이라는 관례를 사용하면 테스트 코드가 읽기가 쉬워진다. 하지만 **테스트를 분리하면 중복되는 코드는 많아진다**.

**TEMPLATE METHOD 패턴**을 사용하면 중복을 제거할 수 있다. give/when 부분을 부모 클래스에 두고 then 부분을 자식클래스에 두면된다.

아니면 독자적인 테스트 클래스를 만들어 `@Before` 함수에 given/when 부분을 넣고 `@Test` 함수에 then 부분을 넣어도 된다.

단일 assert 문은 좋은 방법이지만 **최대한 assert 문 개수를 줄이는 것으로 테스트 코드를 작성**하는 것이 저자는 좋다고 생각한다고 한다.

### 테스트 당 개념하나

이것저것 잡다한 개념을 연속으로 테스트하는 긴 함수는 피해야 한다.

새 개념을 한 함수로 몰아넣으면 독자가 각 절이 거기에 존재하는 이유와 각 절이 테스트하는 개념을 모두 이해해야 한다.

가장 중요한 규칙은 개념당 **assert 문 수를 최소로 줄이고, 테스트 함수 하나는 개념 하나만 테스트 하는 것**이다.

## F.I.R.S.T

깨끗한 테스트는 다음 다섯 가지 규칙을 따르며, 각 규칙에서 첫 글자를 따오면 FIRST 가 된다.

### 1. Fast

테스트는 빨라야 한다. 자주 돌리지 않으면 초반에 문제를 찾아내 고치지 못한다. 코드를 마음껏 정리하지도 못한다. 결국 코드 품질이 망가지기 시작한다.

### 2. Independent

각 테스트는 **서로 의존하면 안된다**. 한 테스트가 다음 테스트가 실행될 환경을 준비해서는 안된다. 각 테스트는 독립적으로 그리고 어떤 순서로 실행해도 괜찮아야 한다. 테스트가 서로에게 의존하면 하나가 실패할 때 나머지도 잇달아 실패하므로 원인을 진단하기 어려워지고, 후반 테스트가 찾아내야 할 결함이 숨겨진다.

### 3. Repeatable

테스트는 어떤 환경에서도 반복 가능해야 한다. 실제 환경, QA 환경, 네트워크에 연결되지 않은 노트북 환경에서도 실행할 수 있어야 한다.

### 4. Self-Validating

테스트는 Bool(true or false) 값으로 결과를 내야 한다. 통과 여부를 알기 위해 로그 파일을 읽거나 텍스트 파일들을 수작업으로 비교하게 만들어서는 안된다. 테스트가 스스로 성공과 실패를 가늠해야 한다.

### 5. Timely

단위 테스트는 테스트하려는 실제 코드를 구현하기 직전에 구현한다. 실제 코드를 구현한 다음에 테스트 코드를 만들면 실제 코드가 테스트하기 어렵다는 것을 발견할 수도 있다.

테스트 코드는 실제 코드만큼이나 프로젝트를 운영하는데 중요하다. 테스트 코드가 방치되어 망가지게 되면 실제 코드도 망가진다. 테스트 코드를 깨끗하게 유지해야 한다.
