---
layout: post
title:  "Ch.3 함수"
date:   2019-07-31 21:03:36 +0530
categories: CleanCode 함수
---

**\# 작게 만들어라!**
 - 블록과 들여쓰기 : if 문/else 문/while 문 등에 들어가는 블록은 한 줄이어야 한다. 함수에서 들여쓰기 수준은 1단~2단이 적당하다.

**\# 한 가지 작업만 해라!**
 - 지정된 함수 이름 아래에서 추상화 수준이 하나인 단계만 수행한다면 그 함수는 한 가지 작업만 한다.
 - 함수 내 섹션이 여러 개로 나눠진다면 여러 작업을 한다는 증거이다. 


**\# 함수당 추상화 수준은 하나로!**
 - 함수 내 모든 문장의 추상화 수준이 동일해야 한다.
 - 위에서 아래로 읽혀야 좋은 코드다. (내려가면서 함수의 추상화 수준이 낮아진다.)


**\# 서술적인 이름을 사용하라!**  
  " 코드를 읽으면서 짐작했던 기능을 각 루틴이 그대로 수행했다면 깨끗한 코드라 불러도 되겠다. "
 - 모듈 내에서 함수 이름은 같은 문구, 명사, 동사를 사용한다. (일관성)
(ex)  includeSetupAndTeardownPages, includeSetupPages, includeSuiteSetupPage, includeSetupPage


**\# 함수 인수**
 - 이상적인 인수 개수는 0개(무항)이다. 인수가 많을 수록 함수를 이해하기 어렵다. 
 - 플래그 인수, 함수로 Boolean값을 넘기는 관례는 끔찍하다.
 - 인수가 2-3개가 필요하다면 일부를 클래스 변수로 선언할 가능성을 고려한다. 
    (ex) Circle makeCircle(double x, double y, double radius);
    -> Circle makeCircle(Point center, double radius);
 - 단항 함수는 함수와 인수가 동사/명사 쌍을 이뤄야한다.
    (ex) write(name) -> writeField(name)
 - 함수 이름에 인수를 추가하면 인수 순서를 기억할 필요가 없다.
    (ex) assertEquals -> assertExpectedEqualsActual(expected, actual);


**\# 명령과 조회를 분리하라!**
 - 객체상태를 변경하거나 아니면 객체 정보를 반환하거나 둘 중 하나만 해야 한다. 
    (ex) attribute인 속성을 찾아 속성값을 value로 설정하면 true, 실패하면 false를 반환한다.

```java
  //bad
  Public boolean set(String attribute, String value);
  if(set("usename", "unclebob"))…   //의미 모호
```
  
```java
//good
if(attributeExists("username")){
 setAttribute("username","unclebob"));
…}     
```

**\# 오류 코드보다 예외를 사용하라!**
 - Try/Catch를 사용해서 오류 처리 코드를 원래 코드에서 분리해라.
 - 오류 처리도 한 가지 작업이다. Try/Catch블록을 별도 함수로 뽑아내는 편이 좋다. 


**\# 반복하지 마라!**

**\# 구조적 프로그래밍**
 - 모든 함수와 함수 내 모든 블록에 입구와 출구가 하나만 존재해야 한다. 
 즉, 함수는 return문이 하나여야 되며, 루프 안에서 break나 continue를 사용해선 안된며 goto는 절대로, 절대로 사용하지 말자. 함수가 작게 만든다면 return, break, continue를 사용해도 괜찮다. Goto는 큰 함수에서만 의미가 있으므로 작은 함수에서는 피해야 한다. 


