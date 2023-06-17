# 2장 의미있는 이름

## 의도를 분명히 밝혀라

변수나 함수 그리고 클래스 이름은 존재 이유?, 수행 기능?, 사용 방법은? 이 세가지 질문에 답해야 한다

잘못된 경우 : `int d`
올바는 경우 : `int elapsedTImeInDays`, `int daysSinceCreation`

잘못된 경우

```
public List<int[]> getThem() {
    List<int[]> list1 = new ArrayList<int[]>();
    for (int[] x: theList)
        if (x[0] == 4)
            list1.add(x)
    return list1;
}
```

올바른 경우

```
public List<int[]> getFlaggedCells() {
    List<int []> flaggedCells = new ArrayList<int[]>();
    for (int[] cell : gameBoard)
        if (cell.isFlagged())
            flaggedCells.add(cell);
    return flaggedCells;
}
```

## 그릇된 정보를 피하라

프로그래머는 코드에 그릇된 단서를 남겨서는 안된다.

## 의미있게 구분하라

1. 연속된 숫자를 덧붙이거나 불용어를 추가하는 방식은 적절하지 못하다.
2. 읽는 사람이 차이를 알도록 이름을 지어라

## 발음하기 쉬운 이름을 사용하라

잘못된 경우

```
class DtaRcred102 {
    private Date genymdhms;
    private Date modymdhms;
    private final String pszqint = "102";
}:
```

올바른 경우

```
class Customer {
    private Date generationTimestamp;
    private Date modificationTimestamp;
    private final string recordId = "102";
}
```

## 검색하기 쉬운 이름을 사용하라

잘못된 경우

```
for (int j=0; j<34; j++) {
    s += (t[j]*4)/5;
}
```

올바른 경우

```
int realDaysPerIdealDay = 4;
const int WORK_DAYS_PER_WEEK = 5;
int sum = 0;
for (int j=0; j < NUMBER_OF_TASKS; j++) {
    int realTaskDays = taskEstimate[j] * realDaysPerIdealDay;
    int realTaskWeeks = (realTaskDays / WORK_DAYS_PER_WEEK);
    sum += realTaskWeeks;
}
```

## 인코딩을 피하라

### 헝가리식 표기어

`PhoneNumber phoneString`

### 멤버 변수 접두어

멤버 면수에 `m_` 이라는 접두어를 붙일 필요도 없다.
클래스와 함수는 접두어가 필요없을 정도로 작아야 한다.

### 인터페이스 클래스와 구현 클래스

인터페이스 클래스 이름과 구현 클래스 이름 중 하나를 인코딩해야 한다면 구현 클래스 이름을 택해라.
`ShapeFactory, ShapeFactoryImp`

## 자신의 기억력을 자랑하지 마라

명료함이 최고다.

## 클래스 이름

클래스 이름과 객체 이름은 명사나 명사구가 적합하다.

올바른 경우
`Customer, WikiPage, Account, AdressParser`

잘못된 경우
`Manager, Processor, Data, info`

같은 단어는 피하고, 동사는 사용하지 않는다.

## 메서드 이름

메서드 이름은 동사나 동사구가 적합하다.

## 기발한 이름은 피하라

재미난 이름보단 명료한 이름을 선택하라.
의도를 분명하고 솔직하게 표현하라.

## 한 개념에 한 단어를 사용하라

1. 메서드 이름은 독자적이고 일관적이어야 한다.
2. 일관성 있는 어휘는 코드를 사용할 프로그래머가 반갑게 여길 선물이다.

## 말장난을 하지마라

1. 프로그래머는 코드를 최대한 이해하기 쉽게 짜야 한다.
2. 프래그래머 코드는 의도를 밝힐 책임이 저자에게 있는 잡지 모델이 적합하다.

## 해법 영역에서 가져온 이름을 사용하라

기술 개념에는 기술 이름이 가장 적합한 선택이다.

## 문제 영역에서 가져온 이름을 사용하라

문제 영역 개념과 관련이 깊은 코드라면 문제 영역에서 이름을 가져와야 한다.

## 의미 있는 맥락을 추가하라

클래스, 함수, 이름 공간에 넣어 맥락을 부여한다.

## 불필요한 맥락을 없애라

짧은 이름이 긴 이름보다 좋다. 단 의미가 분명한 경우에 한해서다.
이름에 불필요한 맥락을 추가하지 않도록 주의한다.
