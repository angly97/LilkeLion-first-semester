# [CSS] 값과 단위



### ▣ 숫자값과 백분율

> 웹은 PC 뿐만 아니라 모바일 웹 브라우저나 테블릿PC 등
> 다양한 크기의 화면에서 보기 때문에
> 이에 반응하는 웹을 만들기 위해
> 상대길이(em, rem)사용
> → 그 중에서도 em은 상속문제로 인해서 지양하고, rem 권장

* 단위

  * px

    * 화소
    * 절대적인 길이

  * em

    * 상대적인 길이	
      →	현재 스타일이 지정된 요소의 폰트 크기 기준으로

  * rem

    * 상대적인 길이	
      →	최상위 요소의 폰트 크기 기준으로
      →	HTML에서 최상위 요소 = html 태그

  * 기본 상태 예시

    ```html
    <!-- 브라우저는 기본적으로 16px 가짐
    	 1em == 1rem == 16px로 지정됨	-->
    <head>
        <style>
            #px{
                width = 16px
                height = 16px
            }
            #em{
                width = 1em
                height = 1em
            }
            #rem{
                width = 1rem
                height = 1rem
            }
        </style>
    </head>
    
    <body>
        단위
        <div id="px">px</div>
        <div id="em">em</div>
        <div id="rem">rem</div>
    </body>
    ```

  * html 태그 폰트 크기만 변경한 예시

    ```html
    <!-- html 태그 폰트 크기 32px
    	 1rem == 32px
    	 현재 다른 폰트 크기 지정된 것 없고 html 문서 폰트 크기 32px로 정했으니까
    	 1em == 32px -->
    <head>
        <style>
            html {font-size = 32px}
            
            #px{
                width = 16px
                height = 16px
            }
            #em{
                width = 1em
                height = 1em
            }
            #rem{
                width = 1rem
                height = 1rem
            }
        </style>
    </head>
    
    <body>
        단위 ...
    </body>
    ```

  * html 태그 & em 폰트 크기 변경한 예시

    ```html
    <!-- html 태그 폰트 크기 32px, em 폰트 크기 24px
    	 1rem == 32px, 1em = 24px					 -->
    <head>
        <style>
            html {font-size = 32px}
            
            #px{
                width = 16px
                height = 16px
            }
            #em{
                width = 1em
                height = 1em
                font-size = 24px
            }
            #rem{
                width = 1rem
                height = 1rem
            }
        </style>
    </head>
    
    <body>
        단위 ...
    </body>
    ```

* % (퍼센트)

  * 상대 길이

  * 이미지나 레이아웃의 너비/높이를 지정

    ```html
    <!-- son 은 parent의 50% -->
    #parent{
    	width: 50%
    }
    #son {
    	width: 50%;
    }
    ```

    

### ▣ 색상

* hex code
  * color: #00ff0050
* RGB cod e
  * color: rgb(0,255,0)
  * 투명도 조절
    * rgba(0,255,0, .5)	→	마지막 요소는 0~1 사이 소수로 투명도