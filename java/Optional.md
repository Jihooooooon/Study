Optional이란
============================================ 
Optional는 “존재할 수도 있지만 안 할 수도 있는 객체”, 즉, “null이 될 수도 있는 객체” 감싸고 있는 일종의 래퍼 클래스이다.
원소가 없거나 최대 하나 밖에 없는 Collection이나 Stream으로 생각할 수 있다.


탄생배경
---------------------------

* 기존의 자바가 존재하지 않는 값을 표현하기 위해 null을 사용했다면, 스칼라나 히스켈 같은 함수형 언어들은 존재할지 안 할지 모르는 값을 표현할 수 있는 별개의
타입을 가지고 있었다. 
* 그리고 이 타입은 존재할지 안할지 모르는 값을 제어할 수 있는 여러가지 api를 제공하기 때문에 개발자들은 해당 api를 통해 간접적으로 그 값에 접근하게 된다.
* 이에 Java8에서는 함수형 언어의 접근 방식을 따와 java.util.Optional<T>라는 새로운 클래스를 도입하게 된다.


NPE 방어 예시
-------------------------------------------

주문을 하기 위한 정보가 저장되어 있는 다음과 같은 클래스들이 있다고 하자.
~~~
/* 주문 */
public class Order {
	private Long id;
	private Date date;
	private Member member;
	// getters & setters
}

/* 회원 */
public class Member {
	private Long id;
	private String name;
	private Address address;
	// getters & setters
}

/* 주소 */
public class Address {
	private String street;
	private String city;
	private String zipcode;
	// getters & setters
}
~~~

어떤 주문을 한 회원이 어느 도시에 살고 있는지 알아내기 위한 다음과 같은 메소드가 있다.

~~~
public String getCityOfMemberFromOrder(Order order) {
	return order.getMember().getAddress().getCity();
}
~~~

이 코드는 Null Point Exception(NPE)를 일으킬 소지가 다분한 문제가 있는 코드다.
* order가 null이면?
* order.getMember() 이 null 이면?
* order.getMember().getAddress() 가 null 이면?

Java8 이전에는 개발자들은 이러한 NPE를 회피하기 위해 다음과 같은 코딩 스타일을 사용했다.

~~~
public String getCityOfMemberFromOrder(Order order) {
	if (order != null) {
		Member member = order.getMember();
		if (member != null) {
			Address address = member.getAddress();
			if (address != null) {
				String city = address.getCity();
				if (city != null) {
					return city;
				}
			}
		}
	}
	return "Seoul"; // default
}
~~~

~~~
public String getCityOfMemberFromOrder(Order order) {
	if (order == null) {
		return "Seoul";
	}
	Member member = order.getMember();
	if (member == null) {
		return "Seoul";
	}
	Address address = member.getAddress();
	if (address == null) {
		return "Seoul";
	}
	String city = address.getCity();
	if (city == null) {
		return "Seoul";
	}
	return city;
}
~~~

코드가 아주 난잡해지고 차후에 유지보수가 어려워진다. 이러한 문제점들 때문에 Java8에서 Optional이 등장하게 된다!



Optional의 효과
---------------------------
* NPE를 유발할 수 있는 null을 직접 다루지 않아도 된다.
* 명시적으로 해당 변수가 null일 수도 있다는 가능성을 표현할 수 있다.

Optional의 기본 사용법
-------------------------
다음과 같이 선언을 한다
~~~
Optional<Order> maybeOrder; // Order 타입의 객체를 감쌀 수 있는 Optional 타입의 변수
Optional<Member> optMember; // Member 타입의 객체를 감쌀 수 있는 Optional 타입의 변수
Optional<Address> address; // Address 타입의 객체를 감쌀 수 있는 Optional 타입의 변수
~~~

Optional 객체를 생성하는 방법에는 3가지 방법이 있다.
* Optional.empty()
	- null을 담고 있는 비어있는 Optional 객체를 생성한다.
* Optional.of(value)
	- null이 아닌 객체를 담고 있는 Optional 객체를 생성한다. null이 넘어올 경우 NPE가 발생하므로 주의해야한다.
* Optional.ofNullable(value)
	- null인지 아닌지 확신할 수 없는 객체를 담고 있는 Optional 객체를 생성한다. null일 경우 Optional.empty()와 동일한 비어있는 객체를 얻어온다.
	

**Optional 객체 접근**

* isPresent()
	- 객체존재 여부를 bool 타입으로 반환한다
* get()
	- 비어있는 Optional 객체에 대해서, NoSuchElementException을 던진다.
* orElse(T other)
	- 비어있는 Optional 객체에 대해서, 넘어온 인자를 반환한다.
* orElseGet(Supplier<? extends T> other)
	- 비어있는 Optional 객체에 대해서, 넘어온 함수형 인자를 통해 생성된 객체를 반환한다. 비어있을때만 호출되므로 성능상 이점이 있다.
* orElseThrow(Supplier<? extends X> exceptionSupplier)
	- 비어있는 Optional 객체에 대해서, 넘어온 함수형 인자를 통해 생성된 예외를 던진다.


Optional 사용 예시
--------------------------------
위 NPE 방어 예시의 복잡한 코드를 Optional을 사용하여서 리팩토링한 코드이다. stream api 사용법과 유사하다.

~~~
/* 주문을 한 회원이 살고 있는 도시를 반환한다 */
public String getCityOfMemberFromOrder(Order order) {
	return Optional.ofNullable(order)
			.map(Order::getMember)
			.map(Member::getAddress)
			.map(Address::getCity)
			.orElse("Seoul");
}
~~~

이처럼 optional을 사용하면 직관적이고 깔끔한 코드를 만들 수 있다!
> https://www.daleseo.com/java8-optional-before/
