---
layout: post
title: "생성자 대신 정적 팩터리 메서드를 고려하라"
date: 2021-05-30
excerpt: "effective java 2장 item 01"
category: [effective java]
tags: [effective java, 생성자, 정적 팩터리 메서]
comments: true
---

# 생성자 대신 정적 팩터리 메서드를 고려하라.

클래스는 생성자와 별도로 정적 팩터리 메서드를 제공함
클래스의 인스턴스를 반환하는 단순 정적 메서드

정적팩터리 메서드가 생성자와 비교하였을 때의 장단점

장점
1. 이름을 가질 수 있다.
   생성자의 매개변수와 생성자 자체만으로는 반환될 객체의 특성을 제대로 나타내지 못한다.
   하지만 정적 팩터리 메서드는 네이밍을 통해 이 부분이 가능하다.
<br><br>하나의 시그니처로는 생성자를 하나만 생성할 수 있다. 물론 매개변수의 순서를 바꾸는 등으로 여러 개의 생성자를 추가 할 수 있지만 유지보수를 고려하였을 때, 좋지 않은 방법이다.
만약 여러개의 시그니처가 필요할 때에는 정적 팩터리 메서드를 사용하고, 각각의 차이를 나타내는 네이밍을 통하여 개발을 해야한다.
<br><br>
2. 호출될 때 마다 새로운 인스턴스를 생성하지 않아도 된다.
   대표적인 예로
   Boolean.valueOf(boolean) 는 메서드 객체를 아예 생성하지 않는다.
   같은 객체가 자주 요청되는 상황이라면 성능을 상당히 끌어올려준다.
<br><br>
3. 반환 타입의 하위 타입 객체를 반환 할 수 있음.
   반환할 객체의 클래스를 자유롭게 선택하는 유연성을 제공한다.
   자바 8 전에는 인터페이스에 정적 메서드를 선언 할 수 없었지만, 지금은 가능하다.
   <br><br>
4. 입력 매개변수에 따라 매변 다른 클래스의 객체를 반환할 수 있따.
반환 타입의 하위 타입이면 어떤 클래스의 객체를 반환하든 상관이 없다.
   <br><br>
5. 정적 팩터리 메서드를 작성하는 시점에는 반환할 객체의 클래스가 존재하지 않아도 된다.


단점
1. 상속을 하려면 public이나 protected 생성자가 필요해서 정적팩토리메서드만 제공하면 하위클래스를 만들 수 없다.
   <br><br>
2. 정적 팩터리 메서드는 프로그래머가 찾기 어렵다.


형이나 속성에 따른 명명방식이데 자주 개발할 때 사용하는 것들만 명시해두었다.

* from : 매개변수를 받아서 해당 타입의 인스턴스를 반환하는 형 변환 메서드
  >Date d = Date.from(instant);

* of : 여러 개의 매개변수를 받아 적합한 타입의 인스턴스를 반환하는 집계 메서드
  >Set<User> users = EnumSet.of(SANJI, JORO, NAMI);''''

* valueOf : from 과 of의 자세한 버전

* create or newInstance :  새로운 인스턴스를 생성해 반환하는 메서드
