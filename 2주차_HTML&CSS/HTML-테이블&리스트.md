# [HTML] 테이블과 리스트

 

### ▣ 테이블

* 테이블 태그

  * '<table>' 태그	→	표를 담는 태그

  * '<tr>' 태그		→	표의 행					; table row

  * '<th>' 태그		→	표의 속성 제목		; table heading

  * '<td>' 태그		→	표의 속성 데이터	; table data

    ```html 
    <body>
        
        <table>
            <tr>
                <th>학년</th>
                <th>성별</th>
                <th>이름</th>
            </tr>
            <tr>
                <td>4</td>
                <td>남</td>
                <td>홍길동</td>
            </tr>
            <tr>
                <td>2</td>
                <td>여</td>
                <td>김영희</td>
            </tr>
        </table>
        
    </body>
    ```

* 속성

  * rowspan = "숫자"

    * 숫자만큼 셀이 행을 점유 (행 합치기)

  * colspan = "숫자"

    * 숫자만큼 셀이 열을 점유 (열 합치기)

    ```html
    <!-- |성별|___여___| -->
    <tr>
        <th>성별</th>
        <td colspan ="2">여</td>
    </tr>
    ```

    

### ▣ 리스트 (목록)

* 순서없는 목록 (Unordered List)

  ```html
  <ul>
      <li>리스트 아이템1</li>
      <li>리스트 아이템2</li>
  </ul>
  ```

* 순서있는 목록 (Ordered List)

  ```html
  <ol>
      <li>리스트 아이템1</li>
      <li>리스트 아이템2</li>
  </ol>
  ```

* 리스트 중첩 가능

  ```html
  <!-- To-Do 리스트
  	 1. 맛집 리스트
  		* 처갓집
  		* 피자알볼로		-->
  <ol> To-Do 리스트
      <li>맛집 리스트
      	<ul>
              <li>처갓집</li>
              <li>피자알볼로</li>
      	</ul>
      </li>
  </ol>
  ```

* 속성

  * '<ol>' 태그

    * start = "숫자"

      > 리스트가 시작되는 숫자를 정함
      >
      > ex. 2 부터 시작하도록 

      ```html
      <!-- 2. 롤 실버 탈출
      	 3. 맛집 탐방
      	 4. 과제 하기		-->
      
      <ol start = "2"> To-Do 리스트
          <li>롤 실버 탈출</li>
          <li>맛집 탐방</li>
          <li>과제 하기</li>
      </ol>
      ```

    * type = "문자"

      > 순서를 카운트 할 문자를 정함
      >
      > ex. 1,2,3 .... OR ㄱ,ㄴ,ㄷ...

      ```html
      <!-- A. 롤 실버 탈출
      	 B. 맛집 탐방
      	 C. 과제 하기		-->
      
      <ol type = "A"> To-Do 리스트
          <li>롤 실버 탈출</li>
          <li>맛집 탐방</li>
          <li>과제 하기</li>
      </ol>
      ```

    * reversed

      > 순서를 반대로 시작

      ```html
      <!-- 3. 롤 실버 탈출
      	 2. 맛집 탐방
      	 1. 과제 하기		-->
      
      <ol reversed> To-Do 리스트
          <li>롤 실버 탈출</li>
          <li>맛집 탐방</li>
          <li>과제 하기</li>
      </ol>
      ```

  * '<ul>' 태그

    * value = "숫자"

      > 해당하는 리스트 아이템의 번호를 지정

      ```html
      <!-- 1. 롤 실버 탈출
      	 5. 맛집 탐방
      	 6. 과제 하기		-->
      
      <ol> To-Do 리스트
          <li>롤 실버 탈출</li>
          <li value ="5">맛집 탐방</li>
          <li>과제 하기</li>
      </ol>
      ```

      