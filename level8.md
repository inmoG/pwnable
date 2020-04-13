# 문제풀이

level9의 shadow 파일이 서버 어딘가에 숨어있다.
그 파일에 대해 알려진 것은 용량이 "2700"이라는 것 뿐이다.

`find / -size 2700c 2>/dev/null`

실행 결과 `/etc/rc.d/found.txt` 파일을 찾았다. 파일을 열어보니 shadow 파일구조로 되어있다. 숨겨진 shadow 파일로 의심된다.
shadow 구조를 복사해 txt파일을 생성한 다음 `john the ripper`를 사용해 복호화 한 결과 `password`를 획득하였다.

password : apple

## shadow 구조

root:$6$5H0QpwprRiJQR19Y\$bXGOh7dIfOWpUb/Tuqr7yQVCqL3UkrJns9.7msfvMg4ZO/PsFC5Tbt32PXAw9qRFEBs1254aLimFeNM8YsYOv. : 16431 : 0 : 99999 : 7 : : :
|-1–|———————————–2——————————————————————————————————————————————————————
——————————————————————————————————————————|—3————|-4-|—5–————|-6-|7|8|

1.Login Name : 사용자 계정각 항목별 구분은 :(콜론) 으로 구분되어있으며 콜론과 콜론 사이 각 필드에는 다음과 같은 구조로 구성되어 있습니다.
2.Encrypted : 패스워드를 암호화시킨 값
3.Last Changed : 1970년부터 1월 1일부터 패스워드가 수정된 날짜의 일수를 계산
4.Minimum : 패스워드가 변경되기 전 최소사용기간(일수)
5.Maximum : 패스워드 변경 전 최대사용기간(일수)
6.Warn : 패스워드 사용 만기일 전에 경고 메시지를 제공하는 일수
7.Inactive : 로그인 접속차단 일 수
8.Expire : 로그인 사용을 금지하는 일 수 (월/일/연도)
9.Reserved : 사용되지 않음

## find 명령어

find ./_ -size +[volume] >> [volume] 이상 크기의 파일 검색
find ./_ -size -[volume] >> [volume] 이하 크기의 파일 검색
find ./\* -size [volume] >> [volume] 크기의 파일 검색

사이즈 단위
b : 블록단위
c : 바이트단위
k : 키로 바이트단위
w : 2바이트 워드
m : 메가 바이트
g : 기가 바이트
