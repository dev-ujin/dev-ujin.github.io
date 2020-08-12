---
layout: post
title:  "[정보보안기사/실기]UNIX/Linux 시스템 관리"
date:   2020-06-22 19:12:00 0800
categories: 정보보안기사실기
tags: 정보보안 시스템
---
> 

# [1] 시스템 시작과 종료
## 런 레벨(Run Level)
- 시스템의 운영 상태를 숫자 혹은 문자로 표현한 것
- /etc/inittab 파일에 정의되어 있음
- 서버용은 일반적으로 3 또는 5 레벨로 운영됨
- 시스템은 `init` 명령을 통해 런 레벨을 이동

|런 레벨|시스템의 운영 상태|
|:---:|---|
|0|PROM(Programmable Read Only Mode)|
|S,s|시스템 싱글 유저 모드, 로컬 파일 시스템이 마운트 되지 않은 상태|
|1|시스템 싱글 유저 모드, 로컬 파일 시스템이 마운트 된 상태|
|2|멀티 유저 모드(NFS 클라이언트 모드)|
|3|멀티 유저 모드(NFS 서버 모드), UNIX 기본 런 레벨|
|4|사용 안 함|
|5|시스템 power off 모드|
|6|시스템 리부팅|

## 시스템 시작
### 순서
1. 바이오스(Bios) 과정 : 시스템의 하드웨어 이상 유무 점검, 하드웨어 정보 수집
2. 부트(Boot)프로그램 과정 : 하드디스크에서 커널을 읽어 들여 메모리상에 적재
3. 커널(Kernel) 과정 : 시스템 운영을 위한 부가적인 커널 모듈을 하드디스크에서 메모리상으로 적재
4. init 프로세스 과정 : 사용자가 시스템을 사용할 수 있게 해주는 초기화 작업 진행

## 시스템 종료
- `shutdown` 명령은 시스템을 안전하게 종료할 때 사용
- `sync` 명령은 버퍼의 내용을 하드디스크로 옮길 때 사용

# [2] 사용자 관리
## 사용자 계정 추가
- `useradd` 명령
- 슈퍼 유저 root만 사용할 수 있음
```c
$ useradd test1 //새로운 사용자 text1 추가
```

## 사용자 계정 삭제
- `userdel` 명령
- 슈퍼 유저 root만 사용할 수 있음
```c
$ userdel test1 //test1 계정을 삭제
$ userdel -r test2 //test2 계정과 홈 디렉터리를 삭제
```

## 그룹 추가
- `groupadd` 명령
- 새로 추가한 그룹은 사용자 계정 정보 중 기본 그룹으로 사용됨
- 기존에 사용되지 않는 group_name을 지정해야 함
```c
$ groupadd study //그룹 study를 새로 추가
$ groupadd -g 100 study //GID가 100인 study 그룹을 새로 추가
```

## 그룹 삭제
- `groupdel` 명령
```c
$ groupdel study //그룹 study를 삭제
```

# [3] 파일 시스템 관리
## 파일 시스템 연결
- `mount` 명령은 보조기억장치에 설치된 파일 시스템을 UNIX 시스템이 인식하도록 특정 디렉터리에 논리적으로 연결시켜 줌
- /etc/mtab 파일에 마운트된 파일시스템의 정보를 관리
```c
$ mount //현재 시스템에 마운트된 정보를 출력
$ mount -a ///etc/mtab 파일에 정의된 모든 파일 시스템을 마운트함
$ mount /dev/cdrom /mnt/cdrom ///dev/cdrom 디바이스 파일을 /mnt/cdrom 디렉터리에 마운트
```

## 파일 시스템 연결 해제
- `unmount` 명령은 이전에 마운트된 파일 시스템의 연결을 해제
- 루트 디렉터리는 unmount 불가
```c
$ unmount -a //마운트된 모든 파일시스템을 언마운트
$ unmount /mnt/cdrom ///mnt/cdrom 디렉터리에 연결된 파일시스템의 연결해제
```

## 하드디스크 사용량
- `du`(Disk Usage) 명령은 디렉터리의 하드디스크 사용량을 확인

## 파일 시스템 용량 정보
- `df`(Disk Free) 명령은 파일 시스템의 전체 공간 및 사용가능 공간을 보여줌

# [4] 프로세스 스케줄 관리
## 정기적 스케줄 관리
- cron 데몬 프로세스는 시스템에서 기본적으로 지원하는 데몬 프로세스로 정기적인 작업을 지정시간에 처리하기 위해 사용
- 1) crontab파일 2) crontab 명령 3) cron 데몬 프로세스가 필요

### crontab 파일의 구조
|필드|의미|기술 방법|
|:---:|:---:|---|
|필드1|분|0-59의 숫자|
|필드2|시|1-23의 숫자|
|필드3|일|1-31의 숫자|
|필드4|월|1-12의 숫자|
|필드5|요일|0-6의 숫자(0 : 일요일)|
|필드6|작업|최대경로로 기술, 필요한 옵션과 인수 기술|

- \* : 모든 값
- \- : 범위
- , : 값을 구분
- / : 간격값

```c
*/5 * * * * batch.sh //매 5분 간격으로 batch.sh 실행
20 6 * * 1-5 /work/batch_job param1 //매월 매일 월~금요일 오전 6시 20분에 param1 인수와 함께 /work/batch_job 명령을 실행
```

### crontab 파일의 제어
- `crontab` 명령은 crontab 파일을 제어 
- crontab 파일은 사용자 계정별로 만들어짐
- 일반 사용자는 자신의 crontab 파일만 편집할 수 있고, root는 다른 사용자의 crontab 파일을 편집할 수 있음
- 옵션
  - \-e : crontab 파일을 편집(Edit)
  - \-l : crontab 파일을 출력(List)
  - \-r : crontab 파일을 삭제(Remove)
```c
$ crontab -u user01 -e //[Linux] user01 계정의 crontab 파일을 편집
$ crontab -e user01 //[UNIX/Solaris] user01 계정의 crontab 파일을 편집
$ crontab -e //자신의 crontab 파일을 편집
```

### crontab 명령 접근제어
- `/etc/cron.allow`와 `etc/cron.deny` 설정 파일을 사용
- cron.allow가 cron.deny보다 우선
- cron.allow는 화이트 리스트 방식으로 해당 파일에 등록된 사용자만 crontab 명령 실행 가능
- cron.deny는 블랙 리스트 방식으로 해당 파일에 등록되지 않은 사용자라면 crontab 명령 실행 가능

## 일시적 스케줄 관리
- `at` 명령은 정해진 시간에 작업을 한 번만 실행
- 옵션
  - \-t time_date: 작업시간을 지정
  - \-l : 현재 대기 중인 작업목록을 출력
  - \-r job_id : job_id에 해당하는 작업을 목록에서 삭제(UNIX)
  - \-d job_id : job_id에 해당하는 작업을 목록에서 삭제(Linux)
- atq : at -l과 같음
- atm job_id : at -r이나 at -d와 같음