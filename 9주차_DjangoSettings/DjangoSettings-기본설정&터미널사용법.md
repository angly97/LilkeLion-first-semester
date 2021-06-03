## [Django Settings] 기본 설정 & 터미널 사용법



### ▣ Windows 환경설정

1. 크롬 설치
2. 파이썬 설치
3. Git 설치
   1. 설치된 Git Bash에서 
   2. git config --global user.name "angly97"
   3. git config --global user.email "angly97@naver.com"
   4. git config --list   -> 사용자 이름과 이메일이 정상 등록되었는지 확인
4. VS Code 설치



### ▣ 터미널 사용법

* 터미널?
  * CLI를 GUI환경에서 사용하게 함
    * CLI가 GUI보다 성능 좋게 작동해서 CLI를 GUI로 편리하게 사용하고 싶음
* 터미널 창에서 노란색 
  * 현재 디렉토리 위치
  * ~ 
    * 홈 디렉토리
    * 터미널 구동 시 처음 위치
  * .
    * Working 디렉토리
    * 작업중인 현재 위치
  * /
    * 루트 디렉토리
    * 모든 디렉토리의 시작
  * ..
    * 상위 디렉토리
  * 절대경로
    * 루트 / 부터 시작
  * 상대경로
    * 현재 . 부터 시작
* 터미널 필수 명령어
  * 명령어 [옵션] [인자...]
    * 옵션: ex. ls-a , ls-l , ls-al(a+l효과)
    * 인자: 대상 파일이나 디렉토리
  * pwd (print working directory)
    * 현재 위치 알려줌
  * man (manual)
    * 명령어 설명서
    * ex. man pwd -> 설명 페이지에서 나가기 = :q
  * ls (list)
    * 디렉토리 목록 출력
    * ls 경로
    * ls -a: 숨김파일까지 출력
    * ls -l: 상세하게 출력
    * ls -F: 파일인지 디렉토리인지 출력
  * cd (change directory)
    * 현재 위치 이동
    * cd 경로
      * ex. cd .. : 상위 디렉토리로 이동
  * clear
    * 터미널 창 깔끔히

* 터미널에서 알면 좋은 거
  * history
    * 지금까지 수행한 명령어들 출력
  * 어느 정도 타이핑 후에 Tab 누르면 -> 자동 완성
