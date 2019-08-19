싱글톤 패턴이란
======================================================
* 객체를 하나만 생성하도록 하며, 생성된 객체를 어디에서든지 참조할 수 있도록 하는 패턴
* 생성 패턴의 한 종류이다.
 ![싱글톤](../img/singleton.PNG)
* Singleton
  - 하나의 인스턴스만을 생성하는 책임이 있으며 getInstance 메서드를 통해 모든 클라이언트에게 동일한 인스턴스를 반환하는 작업을 수행한다.
  
프린터 예시
---------------------------------------------------
* 여러명이서 공유하는 프린터가 있다고 하자

~~~
public class Printer {
  public Printer() { }
  public void print(Resource r) { ... }
}

~~~
































>https://gmlwjd9405.github.io/2018/07/06/singleton-pattern.html
