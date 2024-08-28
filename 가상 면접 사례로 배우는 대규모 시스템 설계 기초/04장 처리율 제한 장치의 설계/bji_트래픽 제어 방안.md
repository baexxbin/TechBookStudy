## Nginx 

### Rate Limiting 

- nginx는 rate limit 설정을 통해서 요청 횟수에 대해서 제한을 걸 수 있음 
- rate limit 알고리즘은 기본적으로 Leacky Bucket 알고리즘을 사용함 
  - 쉽게 말해서 요청이 통과될 때마다 Queue를 하나씩 쌓고 Queue가 꽉 차면 요청을 거부하는 방식

#### 적용 방식 

- 하나의 로케이션에 대해서 적용

```console
location / {
    limit_req zone=one burst=5 nodelay;
    proxy_pass http://localhost:8080;

    limit_req_status 429; # Ratelimit 제한에 걸리면 응답하는 Http Status
    limit_req_log_level error; # Ratelimit 제한에 걸렸을 때 로그 레벨
}
```

- 접속 대역대를 설정

```console
geo $limit {
    proxy_pass http://localhost:8080;
    proxy_pass http://localhost:8081;

    limit_req_status 429; # Ratelimit 제한에 걸리면 응답하는 Http Status
    limit_req_log_level error; # Ratelimit 제한에 걸렸을 때 로그 레벨
}

limit_req_zone $limit zone=one:10m rate=1r/s;
```

#### 설정 옵션

- rate 
  - 최대 요청률을 지정
  - rate=10r/s인 경우 1초에 10개의 요청을 허용하겠다는 의미
- burst
  - 최대 제한율을 넘어선 요청들을 잠시 보관해두는 큐 개념
- nodelay
  - brust를 사용할 때 brust 한도 내에서 요청을 바로 처리한다는 의미
  - 이 옵션을 사용하지 않으면 burst 한도 마저 초과했을 때 요청을 처리하지 않고 대기하게 됨
  - 이 옵션을 사용하면 rate + brust 한도를 초과한 요청을 **즉시 실패**로 처리함
- zone
  - 각 ip 주소의 상태와 요청 제한 URL에 액세스한 빈도를 저장하는데 사용되는 공유 메모리 영역
  - zone=one:10m은 one이라는 공간에 10MB의 공유 메모리 영역을 생성하겠다는 의미

## Redis + Spring Sliding Window Counter 구현

- https://github.com/Spring-Lab-s-Class/Sliding-Window-Counter-Algorithm

## Reference 

- [Nginx Rate Limit 적용해보기](https://willseungh0.tistory.com/191#Nginx%--Rate%--Limit%--%EB%-F%--%EC%-E%--%--%EB%B-%A-%EC%-B%-D)
- [요청 제한을 위한 ratelimit](https://m.blog.naver.com/pjt3591oo/223219393491)