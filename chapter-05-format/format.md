# 형식 맞추기

# 목차

- 형식을 맞추는 목적
- 적절한 행 길이를 유지하라
  - 신문 기사처럼 작성하라
  - 개념은 빈 행으로 분리하라
  - 세로 밀집도
  - 수직 거리
  - 세로 순서
- 가로 형식 맞추기
  - 가로 공백과 밀집도
  - 가로 정렬
  - 들여쓰기
  - 가짜 범위
- 팀 규칙
- 밥 아저씨의 형식 규칙

# Intro

프로그래머라면 형식을 깔끔하게 맞춰 코드를 짜야 한다.
팀으로 일한다면 팀이 합의해 규칙을 정하고 그 규칙을 착실히 따라야 한다.
필요하다면 규칙을 자동으로 적용하는 도구를 활용한다.

# 형식을 맞추는 목적

코드 형식은 중요하다! 코드 형식은 의사소통의 일환이다. 의소 소통은 전문 개발자의 일차적인 의무이다.
맨 처음 잡아놓은 구현 스타일과 가독성 수준은 유지보수 용이성과 확장성에 계속 영향을 미친다.

# 적절한 행 길이를 유지하라

500줄을 넘지 않고 대부분 200줄 정도인 파일로도 커다란 시스템을 구축할 수 있다는 사실이다.
일반적으로 큰 파일보다 작은 파일이 이해하기 쉽다.

## 신문 기사 처럼 작성하라

이름만 보고도 올바른 모듈을 살펴보고 있는지 아닌지를 판단 할 정도로 신경 써서 짓는다.
첫 부분은 고차원 개념과 알고리즘을 설명한다.
아래로 내려갈수록 의도를 세세하게 묘사한다.
마지막에는 가장 저차원 함수와 세부 내역이 나온다.

## 개념은 빈 행으로 분리하라

각 행은 수식이나 절을 나타내고, 일련의 행 묶음은 완결된 생각 하나를 표현한다.
생각 사이는 빈 행을 넣어 분리해야 마땅하다.
빈 행은 새로운 개념을 시작한다는 시각적 단서다.

## 세로 밀집도

세로 밀집도는 연관성을 의미한다.

## 수직 거리

타당한 근거가 없다면 서로 밀접한 개념은 한 파일에 속해야 마땅하다.
이게 바로 `protected` 변수를 피해야 하는 이유 중 하나다.

- 변수 선언
  - 변수는 사용하는 위치에 최대한 가까이 선언한다.
- 인스턴스 변수
  - 인스턴스 변수는 클래스 맨 처음에 선언한다.
  - 중요한건 잘 알려진 위치에 인스턴스 변수를 모은다.
  - 변수 선언을 어디서 찾을지 모두가 알고 있어야 한다.
- 종속 함수
  - 한 함수가 다른 함수를 호출한다면 두 함수는 세로로 가까이 배치한다.
  - 호출하는 함수를 호출되는 함수보다 먼저 배치한다.
  - 상수를 알아야 마땅한 함수에서 실제로 사용하는 함수로 상수를 넘겨주는 방법이 더 좋다.
- 개념적 유사성
  - 친화도가 높을수록 코드를 가까이 배치한다.
  - 친화도가 높은 요인
    - 한 함수가 다른 함수를 호출
    - 변수와 그변수를 사용하는 함수
    - 명명법이 똑같고 기본 기능이 유사한 함수들

## 새로 순서

일반적으로 함수 호출 종속성은 아래 방향으로 유지한다.즉, 호출되는 함수를 호출하는 함수보다 나중에 배치한다.
그러면 소스 코드 모듈이 고차원에서 저차원으로 자연스럽게 내려간다.
가장 중요한 개념을 가장 먼저 표현한다.
가장 중요한 개념에서는 세세한 사항을 최대한 배제한다.
세세한 사항은 가장 마지막에 표현한다.

# 가로 형식 맞추기

프로그래머는 명백하게 짧은 행을 선호한다.
120자 정도로 행 길이를 제한해라.

## 가로 공백과 밀집도

가로로는 공백을 사용해 밀접한 개념과 느스한 개념을 표현한다.
할당 연사자를 강조하려고 앞뒤에 공백을 준다.
함수 이름과 이어지는 괄호 사이에는 공백을 넣지 않는다. 왜냐하면 함수와 인수는 서로 밀접하기 때문이다.
연산자 우선순위를 강조하기 위해서도 공백을 사용한다.
연산자 우선순위를 고려햐여 공백을 넣든지, 않넣든지 해라

## 가로 정렬

선언문과 할당물을 별도로 정렬하지 않는다. 정렬하지 않으면 오히려 중대한 결함을 찾기 쉽다.

## 들여쓰기

계층에서 각 수준은 이름을 선언하는 범위이자 선언문과 실행문을 해석하는 범위다.
들여쓰기한 파일은 구조가 한눈에 들어온다.

- 들여쓰기 무시하기
  - 유혹에 빠질 때마다 나는 항상 원점으로 돌아가 들여쓰기를 넣는다.

## 가짜 범위

세미콜론(;)은 새 행에다 제대로 들여써서 넣어준다.

# 팀 규칙

팀에 속한다면 자신이 선호해야 할 규칙은 바로 팀 규칙이다.
좋은 소프트웨어 시스템은 읽기 쉬운 문서로 이뤄진다
스타일은 일괄적이고 매끄러워야 한다.

# 밥 아저씨의 형식 규칙

```java
public class CodeAnalyzer implements JavaFileAnalysis {
    private int lineCount;
    private int maxLineWidth;
    private int widestLineNumber;
    private LineWidthHistogram lineWidthHistogram;
    private int totalChars;

    public CodeAnalyzer() {
        lineWidthHistogram = new LineWidthHistogram();
    }

    public static List<File> findJavaFiles(File parentDirectory) {
        List<File> files = new ArrayList<File>();
        findJavaFiles(parentDirectory, files);
        return files;
    }

    public static void findJavaFiles(File parentDirectory, List<File> files) {
        for (File file : parentDirectory.listFiles()) {
            if (file.getName().endsWith(".java"))
                files.add(file);
            else if (file.isDirectory()) {
                findJavaFiles(file, files);
            }
        }
    }

    public void analyzeFile(File javaFile) throws Exception {
        BufferedReader br = new BufferedReader(new FileReader(javaFile));
        String line;
        while ((line = br.readLine() != null))
            measureLine(line);
    }

    private void measureLine(String line) {
        lineCount++;
        int lineSize = line.length();
        totalChars += lineSize;
        lineWidthHistogram.addLine(lineSize, lineCount);
        recordWidestLine(lineSize);
    }

    private void recordWidestLine(int lineSize) {
        if (lineSize > maxLineWidth) {
            maxLineWidth = lineSize;
            widestLineNumber = lineCount;
        }
    }

    public int getLineCount() {
        return lineCount;
    }

    public int getMaxLineWidth() {
        return maxLineWidth;
    }

    public int getWidestLineNumber() {
        return widestLineNumber;
    }

    public LineWidthHistogram getLineWidthHistogram() {
        return lineWidthHistogram;
    }

    public double getMeanLineWidth() {
        return (double)totalChars/lineCount;
    }

    public int getMedianLineWidth() {
        Integer[] sortedWidths = getSortedWidths();
        int cumulativeLineCount = 0;
        for (int width : sortedWidths) {
            cumulativeLineCount += lineCountForWidth(width);
            if (cumulativeLineCount > lineCount/2) {
                return width;
            }
        }
        throw new Error("Cannot get here");
    }

    private int getSortedWidths() {
        Set<Integer> widths = lineWidthHistogram.getWidths();
        Integer[] sortedWidth = (widths.toArray(new Integer[0]));
        Arrays.sort(sortedWidth);
        return sortedWidth;
    }
    private int lineCountForWidth(int width) {
        return lineWidthHistogram.getLinesforWidth(width).size();
    }
}
```
