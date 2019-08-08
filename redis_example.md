Redis 사용법!!!
=======================
윈도우 version
-----------------------
### redis는 key-value 형태의 데이터 저장소를 제공해주는 NoSQL의 일종이다. 캐쉬로 많이 쓰인다고 한다!

## 설치
1. [Redis다운](https://github.com/microsoftarchive/redis/releases/tag/win-3.0.504)

2. 압축을 풀어주고 나면 redis-cli, redis-server exe파일이 있다. redis-server를 실행하자!

3. 요렇게 나오면 성공!
![redis_server](./img/redis_server.PNG)


## 적용해보기

1. 따로 패키지를 만든 후 SpringRdisConfig 클래스를 만들고 @Configuration 후 JedisConnectionFactory를 사용하기 위해
connectionFactory함수를 만들고 @Bean 설정 후 hostname과 port를 지정해준다.

2. RedisTemplate 사용을 위한 redisTemplate 함수를 만들고 @Bean 설정후 connectionFactory를 주입한다.

3. controller 부분에서 RedisTemplate을 선언한다. 그리고 resdisTemplate.opsForValue().get() 을 통해 key값으로 검색을 한다.

4. 만약 검색 결과가 null이라면 캐쉬에 값이 없다는 뜻이므로 service를 통해 데이터베이스에서 값을 가져온 후 캐쉬에 저장을 한다. null이
아니라면 데이터베이스에서 접속 할 필요 없이 캐쉬에서 값을 가져온다.


**캐쉬에 없을때**
![redis_server](./img/redis_null.PNG)

**캐쉬에 있을때**
![redis_server](./img/redis_notNull.PNG)

