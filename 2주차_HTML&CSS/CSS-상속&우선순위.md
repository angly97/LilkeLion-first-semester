# [CSS] 상속과 우선순위



### ▣ 상속

* 부모요소의 css 스타일을 자식요소가 물려받는 것

* 모든 CSS포로퍼티가 상속되진 X

  * 이때, inherit 사용하면 상속됨

    ```html
    margin: inherit;
    ```

    

### ▣ 우선순위

* CSS 적용 우선순위의 규칙

  * 중요도
    1. head태그 내 style 태그
    2. head태그 내 stype태그 내 @import문
    3. link태그로 연결된 CSS
    4. link태그로 연결된 CSS 내 @import문
    5. 문브라우저 디폴트 스타일시트

  * 명시도

    1. !important

       ```html
       p{color:red !important; }
       ```

    2. 인라인 스타일

       ```html
       <p style="color: blue;">
           ...
       </p>
       ```

    3. 아이디 선택자 (**→ 안쓰길 권장**)

    4. 클래스(class), 속성(attribute), 가상클래스 선택자(pseudo class selector)

    5. 태그 선택자(type selector)

    6. 전체 선택자(universal selector *)

    7. 상속(inherit)

  * 선언 순서
    * 나중에 선언된 스타일이 우선 적용