
# 이야기 추천 페이지 with ChatGPT
이야기 추천 페이지 with ChatGPT

* 목표
    * ChatGPT API 통해서 간단한 이야기 추천서비스 제공

* 사용방법
    1. https://mkdirlife.github.io/shortStoryRecommand 로 접속해주세요.
    2. input에 질문에 맞는 답을 입력하고, 버튼을 눌러주세요.

* 서비스 URL 정보
    * 실행 URL: https://mkdirlife.github.io/shortStoryRecommand
    * blog github repo: https://github.com/mkdirlife/shortStoryRecommand

* 개발환경
   * 개발 : VSCode
   * Frontend: HTML, CSS, JavaScript
   * 서비스 배포 : GitHub    

* 구조
```mermaid
graph LR
    %% Local Utils
    A[Client] -->|Load Utilities| B[JS/utils.js]
    A -->|스타일 로드| C[style/globalStyle.js]

    %% CDN
    A -->|Load Libraries| D[CDN/marked.min.js]
    A -->|Load Libraries| E[CDN/highlight.min.js]
    E -->|Highlight Syntax _ 현재 파이썬만 지원| F[CDN/python.min.js]
    A -->|Load Libraries| G[CDN/tailwind.css]
    
    %% Request
    A -->|Request| H[JS/config.js]
    H --> I[JS/URLparsing.js]
    I -->|데이터 초기화 _ 로컬/배포 상태에 따라 호출 다름| J[JS/initData.js]
    J --> K[JS/render.js]
    K -->|마크다운/노트북 체크| L[style/blogContentsStyle.js]
    L -->|노트북일 경우| M[JS/convertIpynbToHtml.js]

    %% Style
    K -.->|스타일 적용| C[style/globalStyle.js]
    L -.->|스타일 적용| C[style/globalStyle.js]
    M -.->|스타일 적용| C[style/globalStyle.js]
    
    A -->|Toggle Mobile Menu| Q[JS/mobileMenuToggle.js]
```

* 폴더 구조

  <img src="README%20image/폴더구조.png"> 

* 코드 컨벤션과 변수 컨벤션
    * 변수명(함수명): 역할
        * blogList(initDataBlogList): (fetch) repo에서 blog폴더에 있는 파일 명을 정규표현식으로 파싱, 데이터가 이미 있다면 다시 통신하지 않음.
        * blogMenu(initDataBlogMenu): (fetch) repo에서 menu폴더에 있는 파일 명을 파싱, 데이터가 이미 있다면 다시 통신하지 않음.
        * posts: (fetch) post의 정보를 가져와 데이터 저장, 재접속시 , 데이터가 이미 있다면 다시 통신하지 않음.
        * url
            * url: ChatGPT api 주소
        * isLocal: 로컬과 배포여부

* WBS
```mermaid
gantt
    title 이야기 추천 페이지 with ChatGPT
    dateFormat  YYYY-MM-DD
    section 계획
    프로젝트 범위 정의        :    des1, 2024-02-13, 1d
    section 설계
    와이어프레임 작성         :    des2, after des1, 12h
    section 개발
    기능 개발                :     dev1, after des2, 1d
    section 테스트
    테스트                  :     tes1, after dev1, 6h
    section 배포
    배포 준비               :     dep1, after tes1, 6h
```

* 화면 정의서
    <table>
        <tr>
            <th>메인화면</th>
            <th>설명</th>
        </tr>
        <tr>
            <td width="70%">
                <img src="README%20image/orm_project.jpg">
            </td>
            <td>
                <ul>
                    <li>필요 정보 입력 후</li>
                    <li>글 생성 버튼 클릭</li>
                    <li>하단에 짧은 글 추천</li>
                    <li>logo 클릭시 리셋</li>
                </ul>
            </td>
        </tr>
    </table>

* 애러와 애러 해결(트러블슈팅 히스토리)
    * 모바일 메뉴 설계
        * 모바일 메뉴와 데스스탑 메뉴를 2개 만드는 일을 이벤트 위임을 통해 해결해야 했으나 중복코드가 발생하더라도 시간을 절약하는 차원에서 모듈화 하지 않음.

* 참고
    * https://github.blog/category/engineering/ 스타일을 참고
    <table>
        <tr>
            <th>레퍼런스 이미지 메인</th>
        </tr>
        <tr>
            <td><img src="readme_img/레퍼런스.png" width="100%"></td>
        </tr>
    </table>
    <table>
        <tr>
            <th>레퍼런스 이미지 블로그</th>
        </tr>
        <tr>
            <td><img src="readme_img/레퍼런스2.png" width="100%"></td>
        </tr>
    </table>

