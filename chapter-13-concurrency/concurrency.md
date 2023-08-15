# 동시성

## 목차

- 동시성이 필요한 이유?
  - 미신과 오해
- 난관
- 동시성 방어 원칙
  - 단일 책임 원칙
  - 따름 정리: 자료 범위를 제한하라
  - 따름 정리: 자료 사본을 사용하라
  - 따름 정리: 스레드는 가능한 독립적으로 구현하라
- 라이브러리를 이해하라
  - 스레드 환경에 안전한 컬렉션
- 실행 모델을 이해하라
  - 생산자-소비자
  - 읽기-쓰기
  - 식사하는 철학자들
- 동기화하는 메서드 사이에 존재하는 의존성을 이해하라
- 동기화하는 부분을 작게 만들어라
- 올바른 종료 코드는 구현하기 어렵다
- 스레드 코드 테스트하기
  - 말이 안 되는 실패는 잠정적인 스레드 문제로 취급하라
  - 다중 스레드를 고려하지 않는 순차 코드부터 제대로 돌게 만들자
  - 다중 스레드를 쓰는 코드 부분을 다양한 환경에 쉽게 끼워 넣을 수 있게 스레드 코드를 구현하라
  - 다중 스레드를 쓰는 코드 부분을 상황에 맞게 조율할 수 있게 작성하라
  - 프로세서 수보다 많은 스레드를 돌려보라
  - 다른 플랫폼에서 돌려보라
  - 코드에 보조 코드를 넣어 돌려라. 강제로 실패를 일으키게 해보라
  - 직접 구현하기
  - 자동화
- 결론

### 서론

---

동시성과 깔끔한 코드는 양립하기 어렵다.

### 동시성이 필요한 이유?

---

동시성은 결합을 없애는 전략이다. 즉, 무엇과 언제를 분리하는 전략이다.  
무엇과 언제를 분리하면 애플리케이션 구조와 효율이 극적으로 나아진다.

#### 미신과 오해

- 동시성은 항상 성능을 높여준다.
  - 동시성은 **때로** 성능을 높여준다. 대기 시간이 아주 길어 여러 스레드가 프로세서를 공유할 수 있거나, 여러 프로세서가 동시에 처리할 독립적인 계산이 충분히 많은 경우에만 성능이 높아진다.
- 동시성을 구현해도 설계는 변하지 않는다.
  - 단일 스레드 시스템과 다중 스레드 시스템은 설계가 판이하게 다르다.
- 웹 또는 EJB 컨테이너를 사용하면 동시성을 이해할 필요가 없다.
  - 실제로는 컨테이너가 어떻게 동작하는지, 어떻게 동시 수정, 데드락 등과 같은 문제를 피할 수 있는지를 알아야만 한다.

반대로 다음은 동시성과 관련된 타당한 생각이다.

- **동시성은 다소 부하를 유발한다.** 성능 측면에서 부하가 걸리며, 코드도 더 짜야한다.
- **동시성은 복잡하다.**
- **일반적으로 동시성 버그는 재현하기 어렵다.**
- **동시성을 구현하려면 흔히 근본적인 설계 전략을 재고해야 한다.**

### 난관

---

동시성의 문제는 잘못된 결과를 내놓는것이 **일부** 경로이기 때문에, 발견하기 어렵다.

### 동시성 방어 원칙

---

##### 단일 책임 원칙

동시성 관련 코드는 다른 코드와 분리해야 하라

#### 따름 정리: 자료 범위를 제한하라.

공유 객체를 사용하는 코드 내 **임계영역**을 **synchronized** 키워드로 보호하라.  
이런 임계영역의 수를 줄이는 기술이 필요하다.  
**권장사항**: 자료를 캡슐화 하라. 공유 자료를 최대한 줄여라.

#### 따름 정리: 자료 사본을 사용하라

공유 자료를 줄이려면 처음부터 공유하지 않는 방법이 제일 좋다.  
공유 객체를 피하는 방법이 있다면 코드가 문제를 일으킬 가능성도 아주 낮아진다.

#### 따름 정리: 스레드는 가능한 독립적으로 구현하라

자신만의 세상에 존재하는 스레드를 구현하라.  
**권장사항**: 독자적인 스레드로, 가능하면 다른 프로세서에서, 돌려도 괜찮도록 자료를 독립적인 단위로 분할하라.

### 라이브러리를 이해하라

---

- 스레드 환경에 안전한 컬렉션을 사용한다.
- 서로 무관한 작업을 수행할 때는 executor 프레임워크를 사용한다.
- 가능하다면 스레드가 차단 되지 않는 방법을 사용한다.
- 일부 클래스 라이브러리는 스레드에 안전하지 못하다.

#### 스레드 환경에 안전한 컬렉션

ConcurrentHashMap 을 사용하라

### 실행 모델을 이해하라

---

|한정된 자원(Bound Resource)|다중 스레드 환경에서 사용되는 자원으로, 크기나 숫자가 제한적이다.|
|상호 배제(Mutual Exclusion)|한 번에 한 스레드만 공유 자료나 공유 자원을 사용할 수 있는 경우를 가리킨다.|
|기아(Starvation)|한 스레드나 여러 스레드가 굉장히 오랫동안 혹은 영원히 자원을 기다린다. 예를 들어, 항상 짧은 스레드에게 우선순위를 준다면, 짧은 스레드가 지속적으로 이어질 경우, 긴 스레드가 기아 상태에 빠진다.|
|데드라(Deadlock)|여러 스레드가 서로가 끝나기를 기다린다. 모든 스레드가 각기 필요한 자원을 다른 스레드가 점유하는 바람에 어느 쪽도 더 이상 진행하지 못한다.|
|라이브락(Livelock)|락을 거는 단계에서 각 스레드가 서로를 방해한다. 스레드는 계속해서 진행하려 하지만, 공명(resonance)으로 인해, 굉장히 오랫동안 혹은 영원히 진행하지 못한다.|

#### 생산자-소비자

생산자 스레드와 소비자 스레드가 사용하는 대기열은 **한정된 자원**이다.  
생산자 스레드는 대기열에 정보를 채운 다음 소비자 스레드에게 "대기열에 정보가 있다"는 시그널을 보낸다.  
소비자 스레드는 대기열에서 정보를 읽어들인 후 "대기열에 빈 공간이 있다"는 시그널을 보낸다.  
따라서 잘못하면 생산자 스레드와 소비자 스레드가 둘 다 진행 가능함에도 불구하고 동시에 서로에게서 시그널을 기다릴 가능성이 존재한다.

#### 읽기-쓰기

일기 스레드를 위한 주된 정보원으로 공유 자원을 사용하지만, 쓰기 스레드가 이 공유 자원을 이따금 갱산한다고 하자.  
이런 경우 처리율이 문제의 핵심이다. 처리율을 강조하면 **기아 현상**이 생기거나 오래된 정보가 쌓인다.  
갱신을 허용하면 처리율에 영향을 미친다.

#### 식사하는 철학자들

### 동기화하는 메서드 사이에 존재하는 의존성을 이해하라

공유 클래스 하나에 동기화된 메서드가 여럿이라면 구현이 올바른지 다시 한 번 확인해라
**권장사항**: 공유 객체 하나에는 메서드 하나만 사용하라.
만약에 공유 객체 하나에 여러 메서드가 필요한 상황이라면, 다름 세 가지 방법을 고려하라.

- 클라이언트에서 잠금
- 서버에서 잠금
- 연결 서버

### 동기화하는 부분을 작게 만들어라

---

임계영역은 반드시 보호해야 한다. 따라서, 코드를 짤 때는 임계영역 수를 최대한 줄여야 한다.
**권장사항**: 동기화하는 부분을 최대한 작게 만들어라.

### 올바른 종료 코드는 구현하기 어렵다.

---

**권장사항**: 종료 코드를 개발 초기부터 고민하고 동작하게 초기부터 구현하라. 생각보다 오래 걸린다. 생각보다 어려우므로 이미 나온 알고리즘을 검토하라.

### 스레드 코드 테스트하기

---

**권장사항**: 문제를 노출하는 테스트 케이스를 작성하라. 프로그램 설정과 시스템 설정과 부하를 바꿔가며 자주 돌려라. 테스트가 실패하면 원인을 추적하라. 다시 돌렸더니 통과하더라는 이유로 그냥 넘어가면 절대로 안 된다.

#### 말이 안되는 실패는 잠정적인 스레드 문제로 취급하라

**권장사항**: 시스템 실패를 '일회성'이라 치부하지 마라.

#### 다중 스레드를 고려하지 않는 순차 코드부터 제대로 돌게 만들자

**권장사항**: 스레드 환경 밖에서 생기는 버그와 스레드 환경에서 생기는 버그를 동시에 디버깅하지 마라. 먼저 스레드 환경 밖에서 코드를 올바로 돌려라.

#### 다중 스레드를 쓰는 코드 부분을 다양한 환경에 쉽게 끼워 넣을 수 있게 스레드 코드를 구현하라.

**권장사항**: 다양한 설정에서 실행할 목적으로 다른 환경에 쉽게 끼워 넣을 수 있게 코드를 구현하라.

#### 다중 스레드를 쓰는 코드 부분을 상황에 맞게 조율할 수 있게 작성하라

#### 프로세서 수보다 많은 스레드를 돌려보라

#### 다른 플랫폼에서 돌려보라

#### 코드에 보조 코드를 넣어 돌려라. 강제로 실패를 일으키게 해보라.

보조 코드 : `wait(), sleep(), yield(), priority()` 등

#### 직접 구현하기

스레드를 전혀 모르는 POJO와 스레드를 제어하는 클래스로 프로그램을 분할하면 보조 코드를 추가할 위치를 찾기가 쉬워진다.

#### 자동화

코드를 흔드는 이유는 스레드를 매번 다른 순서로 실행하기 위해서다.
**권장사항**: 흔들기 기법을 사용해 오류를 찾아내라.

### 결론

---

1. SRP 를 준수하라.
2. 동시성 오류를 일으키는 잠정적인 원인을 철저히 이해하라.
3. 사용하는 라이브러리와 기본 알고리즘을 이해하라.
4. 보호할 코드 영역을 찾아내는 방법과 특정 코드 영역을 잠그는 방법을 이해하라.
5. 공유하는 객체 수와 범위를 최대한 줄여라.