스트래티지 패턴
======================================

* 행위를 클래스로 캡슐화해 동적으로 행위를 자유롭게 바꿀 수 있게 해주는 패턴
  - 같은 문제를 해결하는 기능들이 클래스별로 캡슐화되어 있고 이들이 필요할 때 교체할 수 있도록 함으로써 동일한 문제를 다른 기능들로 해결할 수 있게 하는 디자인 패턴
  - 즉 전략을 쉽게 바꿀 수 있도록 해주는 디자인 패턴이다.
  - 특히 게임에서 캐릭터가 자신이 처한 상황에 공격이나 행동하는 방식을 바꾸고 싶을 때 스트래티지 패턴을 사용하는 것이 적합하다.
  
  ![strategy ex](../img/strategy.PNG)
  
  
* Strategy
  - 인터페이스나 추상 클래스로 외부에서 동일한 방식으로 객체를 호출하는 방법을 명시
* ConcreteStrategy
  - Strategy에서 명시한 기능들을 실제로 구현한 클래스
* Context
  - 스트래티지 패턴을 이용하는 역할을 수행
  - 상황에 따라 구체적인 전략을 바꿀수 있도록 setter메소드를 제공
  
  

예시
--------------------------------------
 ![고양이 만들기](../img/cat.PNG)
 
 ~~~
	public abstract class Cat{
		private String name;
		public Cat(String name) {
			this.name=name;
		}
		
		public String getName() {
			return name;
		}
		
		public abstract void attack();
		public abstract void move();
	}
	
	public class NormalCat extends Cat{
		public NormalCat(String name) {
			super(name);
		}
		public  void attack() {
			System.out.println("보통 냥냥펀치");
		}
		public  void move() {
			System.out.println("보통 뛰기");
		}
	}
	
	public class SuperCat extends Cat{
		public SuperCat(String name) {
			super(name);
		}
		public  void attack() {
			System.out.println("슈퍼 냥냥펀치");
		}
		public  void move() {
			System.out.println("슈퍼 뛰기");
		}
	} 


~~~
