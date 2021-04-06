# [HTML] 멀티미디어와 관련된 태그

 

### ▣ 이미지 태그

* <img>

  * <img src = "">

    *  종료 태그 없음	→	빈 요소

  * 속성 종류

    * src

      ```html
      <img src = "snowman.jpg">
      ```
      
    * alt
    
      > 불러올 이미지가 없거나, 실패할 경우
      >
      > 대신 표시되는 문장 (alternative text)
    
      ```html
      <img src = "snowman.jpg" alt = "snowman photo">
      ```
    
    * weight, height
    
      > weight = "수치"	→	너비
      >
      > height = "수치"	→	높이
      >
      > But, css가 꾸미는 언어니까 html로 이미지 조정하는 건 지양
    
      ```html
      <img src = "snowman.jpg" height = "300" weight = "30%">
      ```
    



### ▣ YouTube 영상 삽입

* 방법
  1. YouTube 영상의 공유하기 버튼
  2.  <> 표시가 된 퍼가기 버튼
  3. iframe 태그로 감싸진 코드 복사 후 붙여넣기

