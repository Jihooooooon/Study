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
> 어노테이션 안에 두개 이상의 메소드가 선언 될 경우 오류가 발생한다.

