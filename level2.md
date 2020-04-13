# 문제풀이

1. `su level2` 명령어를 입력해 `level2` 계정으로 로그인한다.
   비밀번호 : hacker or cracker

2. ls -l 입력
   hint 파일 확인결과 아래 문구를 발견했다.
   "텍스트 파일 편집 중 쉘의 명령을 실행시킬 수 있다는데..."

3. find / -user level3 -perm -4000 2>/dev/null 입력

## 결과

/usr/bin/editor

1. 해당 경로로 이동해 `editor`를 실행한다.
2. vi편집기 명령어는 아래와 같다.

- :q 저장하지 않고 종료
- :wq 저장하고 종료
- :q! 저장하지 않고 강제 종료(경고 무시)

3. ESC키를 누른 후 !my-pass 입력 결과 level3 비밀번호를 획득

password : can you fly?
