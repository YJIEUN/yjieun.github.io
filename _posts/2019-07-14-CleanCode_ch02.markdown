---
layout: post
title:  "Ch.2 의미있는 이름"
date:   2019-07-14 21:03:36 +0530
categories: CleanCode 변수명규칙
---

\** 이름을 잘 짓는 규칙 \**

**\# 의도를 분명히 밝혀라**
 - 이름에서 변수(함수 or 클래스)의 존재 이유, 수행 가능, 사용 방법을 파악할 수 있어야 한다.  
  (ex) 경과 시간 (단위:날짜)  
  int d; -> int elapsedTimeInDays;  
 - 명확하고 이해하기 쉽게 정보를 제공하자.  
 (ex) 지뢰찾기 게임
 
 ```java
 // Bad
 public List<int[]> getThem() {
    List<int[]> list1 = new ArrayList<int[]>();
    for (int[] x : theList) {
        if (x[0] == 4) {
            list1.add(x);
        }
    }
    return list1;
}
 ```
 
 ```java
 // Good
 public List<int[]> getFlaggedCells() {
    List<int[]> flaggedCells = new ArrayList<int[]>();
    for (int[] cell : gameBoard) {
        if (cell[STATUS_VALUE] == FLAGGED) {
            flaggedCells.add(cell);
        }
    }
    return flaggedCells;
}
 ```

**\# 그릇된 정보를 피하라**
 - 널리 쓰이는 의미 있는 단어나 비슷해 보이는 이름으로 해석에 혼란을 주지 말자.
	- accountList -> Accounts (실제 List가 아니라면)
	- 대문자 O or 소문자 L (숫자 0과 1)  

**\# 의미있게 구분하라**
 - 연속된 숫자 or 불용어(의미 없는 글자) 추가하지 말자
 - 읽는 사람이 각 변수의 차이를 알도록 이름을 지어라.
	- ProductInfo와 ProductData
	- a1, a2, .. aN
	- Name 과 NameString

**\# 발음하기 쉬운 이름을 사용하라**  
 (ex) genymdhns -> generation Timestamp

**\# 검색하기 쉬운 이름을 사용하라**
 - 변수나 상수를 코드 여러 곳에서 사용한다면 검색하기 쉬운 이름이 좋다. (길이가 긴 이름)

**\# 인코딩을 피하라**
 - 헝가리식 표기법 
  - 변수 이름에 타입을 적지 말자
 - 멤버 변수 접두어 : m_
 - 인터페이스 클래스와 구현 클래스  
   (둘 중 하나를 인코딩 한다면 구현 클래스 이름을 인코딩하자.     
      인터페이스 클래스 : ShapeFactory        
      구현 클래스 : IshapeFactory -> ShapeFactoryImP or CshapeFactory)

**\# 자신의 기억력을 자랑하지 마라**
 - 독자가 코드를 읽으면서 변수 이름을 자신이 아는 이름으로 다시 생각해야한다면 바람직 하지 않은 변수 이름이다.
 - 문자 하나만 사용하는 변수를 사용하지 말자
 (루프에서의 반복 횟수 변수 i,j,k 제외, l은 안됌)

**\# 클래스 이름**
 - 클래스, 객체 이름은 명사나 명사구를 사용하자.

**\# 메서드 이름**
 - 메서드 이름은 동사나 동사구가 적합하다. 
 - 접근자, 변경자, 조건자는 javabean 표준에 따라 get,set,is로 시작하자. 
 - 생성자를 중복 정의할 때는 정적 팩토리 메서드를 사용한다.

**\# 기발한 이름은 피한다**
 - 의도를 분명하게 표현하라.

**\# 한 개념에 한 단어를 사용하라**
 - 추상적인 개념 하나에 단어 하나를 선택해 이를 고수한다.
 	- fetch, retrieve, get
 	- controller, manager, driver

**\# 말장난을 하지 마라**
 - 한 단어를 2가지 목적으로 사용하지 마라

**\# 해법 영역에서 가져온 이름을 사용하라**
 - 코드를 읽는 사람도 프로그래머이다. 전산,알고리즘,패턴,수학 용어 등 프로그래머 용어를 사용해 정확한 뜻을 전달하는 것이 좋다.

**\# 문제 영역에서 가져온 이름을 사용하라**
 - 적절한 ‘프로그래머 용어’가 없다면 문제 영역에서 이름을 가져온다.
 - 문제 영역 개념과 관련이 깊은 코드라면 문제 영역에서 이름을 가져와야 한다.
 
**\# 의미있는 맥락을 추가하라**
 - 클래스, 함수, 이름 공간에 넣어 맥락을 부여한다. 
 - 마지막 수단으로 접두어를 붙인다.  
  (ex) addr -> addrFirstName, addrState
  
  ```java
  // Bad
private void printGuessStatistics(char candidate, int count) {
    String number;
    String verb;
    String pluralModifier;
    if (count == 0) {  
        number = "no";  
        verb = "are";  
        pluralModifier = "s";  
    }  else if (count == 1) {
        number = "1";  
        verb = "is";  
        pluralModifier = "";  
    }  else {
        number = Integer.toString(count);  
        verb = "are";  
        pluralModifier = "s";  
    }
    String guessMessage = String.format("There %s %s %s%s", verb, number, candidate, pluralModifier );

    print(guessMessage);
}
  ```
  
  ```java
  // Good
public class GuessStatisticsMessage {
    private String number;
    private String verb;
    private String pluralModifier;

    public String make(char candidate, int count) {
        createPluralDependentMessageParts(count);
        return String.format("There %s %s %s%s", verb, number, candidate, pluralModifier );
    }

    private void createPluralDependentMessageParts(int count) {
        if (count == 0) {
            thereAreNoLetters();
        } else if (count == 1) {
            thereIsOneLetter();
        } else {
            thereAreManyLetters(count);
        }
    }

    private void thereAreManyLetters(int count) {
        number = Integer.toString(count);
        verb = "are";
        pluralModifier = "s";
    }

    private void thereIsOneLetter() {
        number = "1";
        verb = "is";
        pluralModifier = "";
    }

    private void thereAreNoLetters() {
        number = "no";
        verb = "are";
        pluralModifier = "s";
    }
}
  ```
  
**\# 불필요한 맥락을 없애라**
 - 짧은 이름이 긴 이름보다 좋다. 단, 의미가 분명한 경우에 한해서다.



