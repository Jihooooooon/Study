Java 8 변경점
============================
+ **Lambda Expression**
> 메소드를 하나의 식으로 표현 , 익명 함수라고도 부른다
> 클래스를 만들고 객체를 생성하지 않아도 메소드를 사용할 수 있다!
> 기존의 불필요한 코드를 줄여주고 가독성을 높일 수 있다.

+ **예제**
> 기존 코드
    new Thread(new Runnable() {

    public void run() {

        System.out.println("전통적인 방식의 일회용 스레드 생성");

    }

    }).start();
> 람다식
    new Thread(()->{

      System.out.println("람다 표현식을 사용한 일회용 스레드 생성");
  
    }).start();
