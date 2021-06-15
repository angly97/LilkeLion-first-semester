## [Django] 배포 사전 준비



### ▣ 배포 전 할 일

* 환경변수 설정

  * 시스템에 저장된 변수
  * 비밀키 등 유출되면 안되는 정보 / 환경에 차이를 둘 때 사용
  * os.environ에서 dic형식으로 불러올 수 있음
  * os.environ.get('변수명', '기본값')으로 사용

* requrements.txt

  * 내 파이썬(쟝고) 앱 실행을 위해 우선 설치되어야하는 패키지들
  * Django, Pillow 등
  * 패키지면 == 버전 으로 저장
  * 보통 requirements.txt 에 저장
  * pip freeze 명령어는 해당 환경에 설치된 모든 패키지를 보여줌
  * '>' 는 프로그램 출력을 파일에 저장한다는 의미
    * pip freeze > requirements.txt 로 생성

* AWS

  * IAM
    * Identity and Access Management의 준말
    * IAM에서 계정을 만든 후 해당 계정 로그인정보(엑세스키 & 시크릿 키)로 AWS의 API 활용
    * 보안을 위해 권한을 최대한 보수적으로 설정
  * S3
    * Simple Storate Service의 준말
    * AWS에서 제공하는 구글 드라이브 느낌
    * 최초 용량 지정 없이 사용한 만큼만 과금됨 → 용량 예측 필요 없음
    * 여러 서버에서 동시 접속 가능

  

### ▣ 실습하기

1. settings.py

   - 시크릿 키를 환경변수로 바꿈

     ```python
     import os	# 추가
     
     # 기본값은 선택적으로 작성
     SECRET_KEY =  os.environ.get('SECRET_KEY','django-insecure-v_51g&+dujd%yw7rtw6-yl4avzsb=nn-jc#5pjyo+7-u=a8ltt')
     
     ```

2. requirements.txt 생성

   - pip freeze > requirements.txt

3. aws 홈페이지 접속

   1. 클라우드 서비스 | 클라우드 컴퓨팅 솔루션| Amazon Web Services](https://aws.amazon.com/ko/)

   2. 지역 - 서울로 설정
   3. 사용자 추가
   4. 사용자 이름은 암거나; likelion-django-lesson
   5. AWS 액세스 유형 - 프로그래밍 방식 엑세스
   6. 권한 설정
      1. 기존 정책 직접 연결
      2. s3 검색 후, AmazonS3FullAccess 선택
   7. 태그는 건너 뛰고
   8. 사용자 만들기 버튼 클릭
   9. 엑세스키는 언제나 볼 수 있지만, 시크릿 키는 이 페이지에서만 볼 수 있음
      - .csv 다운로드 해놓기

4. S3 연동

   1. 구글에 django-storages 검색 후 첫번째 링크 들어가

   2. 페이지에 installation 코드 있음

      - ```
        pip install django-storages
        pip freeze > requirements.txt
        ```

   3. Amazon S3 카테고리 들어가서 Settings 설정 코드 나옴

      - settings.py

        ```python
        DEFAULT_FILE_STORAGE = 'storages.backends.s3boto3.S3Boto3Storage'
        ```

   4. 버킷 만들기

      - S3에서 사용하는 폴더

      1. AWS console 들어가서 S3 검색
      2. 버킷 카테고리에서 버킷 만들기 누름
      3. 버킷 이름 = likelion9th-django-lesson
      4. AWS Region = 서울
      5. 모든 퍼블릭 액세스 차단 ; Block all public access 체크 해제
      6. 빨간 세모 안 느낌표는 체크

   5. settings.py 마저 설정

      ```python
      
      # AWS 설정
      DEFAULT_FILE_STORAGE = 'storages.backends.s3boto3.S3Boto3Storage'
      
      # 다운받은 .CSV 엑셀 파일에서 복붙
      AWS_ACCESS_KEY_ID = 'AKIA32NLL4DS6EVL7OXX'
      AWS_SECRET_ACCESS_KEY = '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'
      
      AWS_STORAGE_BUCKET_NAME = 'likelion9th-django-lesson'
      
      AWS_S3_SIGNATURE_VERSION = 's3v4'
      AWS_S3_REGION_NAME = 'ap-northeast-2'
      
      ```

   6. pip install boto3

      - AWS 관련 API를 파이썬에서 사용하게 하는 패키지

