---
layout: post
title: "Error::Port 8080 was already in use."
date: 2020-11-17 21:10:00 0800
categories: Error
tags: Error
comments: 1
---
> 

> 기존에 실행중이던 프로그램이 종료되지 않은 상태에서 같은 포트로 서버 실행을 요구하면 다음과 같은 에러가 빈번히 일어난다.

> Windows에서의 해결방법이다.

# 에러메시지
```
Web server failed to start. Port 8080 was already in use.
```

# 해결방법
해당 포트를 담당하고 있는 프로세스를 찾아 종료해준다.

1. cmd창을 연다.
2. `netstat -ano` 명령어를 입력한다.
   - 옵션 a : 모든 연결과 수신 대기 포트를 표시
   - 옵션 n : 주소와 포트 번호를 숫자 형식으로 표시
   - 옵션 o : 각 연결의 소유자 프로세스 ID를 표시
3. 해당 포트에 사용중인 pid를 찾는다.
```
프로토콜  로컬 주소              외부 주소              상태            PID
...
 TCP    0.0.0.0:8080           0.0.0.0:0              LISTENING       29692
...
```
4. `taskkill -f /pid [pid]` 명령으로 프로세스를 kill한다.
   - 옵션 f : 강제 종료
```
taskkill -f /pid 29692
```
