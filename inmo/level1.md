# 문제풀이

## ID : level1
## PASSWORD : level1

1. ls -l 입력결과 hint 파일 발견
   cat 명령어를 사용해 파일의 내용을 확인한다.

hint 내용 : "level2 권한에 setuid가 걸린 파일을 찾는다"

- setuid 비트
  8진수 4000
  setuid 비트를 실행파일에 적용하면 실사용자(프로그램을 실제 실행중인 사용자)에서 프로그램 소유자의 ID로 유효사용자(EUID)가 변경됨
  setuid 비트가 설정된 파일을 실행순간만 그 파일의 소유자 권한으로 실행, 실행 순간만 권한을 빌려오는 개념이다. 슈퍼유저의 유효한 특권을 가지고 실행되므로 일반 사용자의 접근이 금지된 파일과 디렉토리들에 접근 가능하게함.
  따라서 일반 사용자가 setuid설정이 된 파일에 접근이 가능한 취약점이 있다.

setuid가 설정된 파일을 실행해 일시적으로 루트권한을 획득해 level2계정의 권한을 획득하는 것이다.

- find / -user level2 -perm -4000 2>/dev/null
  / : 전체를 검색한다
  -user level2 : level2 유저를 검색한다.
  -perm : 권한과 일치하는 파일
  -4000 : -(최소한),4(Setuid)가 걸려있는 000(모든파일)을 의미한다.
  2>/dev/null : 에러메시지를 출력하지 않는다.

## 결과

/bin/ExecuteMe

bin 디렉토리에 이동해 ExecuteMe 파일 실행결과 아래 문구출력
레벨 2의 권한으로 당신이 원하는 명령어를 한가지 실행시켜 드리겠습니다.
(단, my-pass와 chmod는 제외) 어떤 명령을 실행시키겠습니까?

/bin/bash 입력해 셸을 띄우면 level2의 셸을 획득할 수 있다.

my-pass(FTZ의 패스워드 확인명령어)를 입력해 level2계정의 비밀번호를 확인한다.

### level2 Password : "hacker or cracker"
