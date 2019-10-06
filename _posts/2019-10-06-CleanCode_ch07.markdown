---
layout: post
title:  "Ch.7 오류 처리"
date:   2019-09-01 21:03:36 +0530
categories: CleanCode 오류처리
---

**\#오류 코드보다 예외를 사용하라**
- 예외를 사용하자. 
 : 오류 처리 코드를 따로 분리해 코드가 더 깔끔해진다.
 
**\#Try-Catch-Finally문부터 작성하라**
- 예외가 발생할 코드를 짤 때는 try-catch-finally문으로 시작하는 편이 낫다.
- try블록의 트랜잭션 범위를 정의하고 cath블록에서 범위 내 프로그램 상태를 일관성 있게 유지하도록 하자.

**\#미확인 예외를 사용하라**

**\#예외에 의미를 제공하라**
- 예외를 던질 때, 오류가 발생한 위치나 원인을 쉽게 찾을 수 있도록 오류 메시지에 정보를 담아 예외와 함께 던져라.

**\#호출자를 고려해 예외 클래스를 정의하라**

**\#정상 흐름을 정의하라**
- 클래스를 만들거나 객체를 조작해 예외적인 상황을 처리하는 방식을 특수 사례 패턴이라 한다. 

**\#null을 반환하지 마라**
```
 List<Employee> employees = getEmployees();
 if (employees != null){
   for (Employee e : employees){
     totalPay += e.getPay();
   }
 }
```  

```
 List<Employee> employees = getEmployees();
   for (Employee e : employees){
     totalPay += e.getPay();
   }
 }
 
 public List<Employee> getEmployees(){
   if (..직원이 없다면..)
     return Collections.emptyList();
 }
```
**\#null을 전달하지 마라**
