## [Django] Git사용법

> Git: 내 공간
>
> GitHub: 공유공간

### ▣ Git 명령어

* echo "# firstproject" >> README.md

  * README.md파일에 # firstproject 적어서 저장

* git init

  * 현제 디렉토리를 새로운 git저장소로 초기화하겠다
  * 참고, 독립적인 project마다 git init해줘야 함

* git add 파일1 파일2 파일3 ... / git add .

  * 파일들을 staging area에 올림

  * 근데 올리고 싶지 않은 파일 설정은?

    * .gitignore 파일 생성

    * 이 파일에 올리지 말아야할 파일 이름 적기

      > 어떤 파일 올리지 말아야 해?
      >
      > - gitignore.io에 들어가서 검색창에 django 입력
      > - 검색 결과를 .gitignore에 복붙

* git commit

  * staging area에 올라온 파일을 저장

* git branch 새브런치명

  * git status  
    * 일단 내가 어느 브런치에 있는지 확인

* git checkout 옮길 브런치 명

  * 브런치 이동

* git remote add origin 레퍼지토리주소
  * 레퍼지토리 주소를 origin이라는 이름으로 연결
  * 이 후부터는 레퍼지토리 주소를 origin으로 사용 가능
* git push origin 올릴 브랜치명
  * origin에 브런치 업로드



### ▣ GitHub 업로드 순서

1. git init
2. git add
3. git commit -m "message"
4. git remote add [remote 이름] [repository 주소]
5. git push [remote이름] [올릴 branch 이름]





![image-20210604100137002](C:\Users\angly\AppData\Roaming\Typora\typora-user-images\image-20210604100137002.png)

* 프로젝트 수정 시엔 7~9 만 수행

