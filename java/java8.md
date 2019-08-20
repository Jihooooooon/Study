Java 8 변경점
============================
+ **Lambda Expression**
> 메소드를 하나의 식으로 표현 , 익명 함수라고도 부른다
> 클래스를 만들고 객체를 생성하지 않아도 메소드를 사용할 수 있다!
> 기존의 불필요한 코드를 줄여주고 가독성을 높일 수 있다.

+ **예제**
> 기존 코드
<pre><code>new Thread(new Runnable() {
    public void run() {
        System.out.println("전통적인 방식의 일회용 스레드 생성");
        }
    }).start();
    </code></pre>
> 람다식
<pre><code>new Thread(()->{
      System.out.println("람다 표현식을 사용한 일회용 스레드 생성");
    }).start();
</code></pre>
+ **함수형 인터페이스 예제**
>
~~~
public class Test {
	@FunctionalInterface
	interface Calc { // 함수형 인터페이스의 선언
	public int min(int x, int y);
	}	
	public static void main(String[] args) {
	// TODO Auto-generated method stub
		Calc test = (x,y)->x<y?x:y;
		System.out.println(test.min(4, 6));
		}
	}
~~~
> 어노테이션 안에 두개 이상의 메소드가 선언 될 경우 오류가 발생한다.
>
+ **Stream**
>기존의 iterator나 반복문의 경우 길고 가독성이 떨어진다는 단점이 있었고 정형화된 처리 패턴을 가지고 있지 않았기에 데이터마다 다르게 접근을 해야 했다.
> 이를 보완하기 위해 도입된 방법이 바로 stream!
+ **스트림 예제**
~~~
public class Test {
	public static void main(String[] args) {
		// TODO Auto-generated method stub	
	int[] arr = new int[] {1,2,3,4};
	IntStream stream = Arrays.stream(arr,1,3);
	stream.forEach(s->System.out.println(s));
	
	String[] temp = new String[] {"abc","def","ghi"};
	Stream<String> stream2 = Arrays.stream(temp);
	stream2.forEach(s->System.out.println(s));
	}

}
~~~
