# 마크업이 전달되는 과정 소개하기

    인사말~

## 네이버 '회원서비스' 업무 프로세스

1. 신규건이 발생
2. 기획문서 공유
3. 주간 회의때 논의
4. 디자인 시안 작업 진행 (기획서를 바탕으로 작업된 디자인 시안을 jpg or png 파일 공유)
5. 디자인 시안 컨폼 완료
6. 컨폼이 완료된 디자인 시안의 가이드 파일이 전달 (디자인 요소별 px,font,color 수치값 적용)
7. 마크업 가이드 작업 진행 (html,css 작업 후 git 저장소에 push)
8. 마크업 가이드 페이지 URL 공유, 디자인 검수 요청 & 검수 완료
9. 검수가 완료된 마크업 가이드 페이지 git lab을 통해 페이지 url 개발파트 전달
10. 개발 작업진행 & 개발 완룐
11. QA 진행 & QA 완료
12. 배포


## 마크업 개발이 진행되는 과정 소개

 ### 디자인 가이드 전달
 ![](img_desktop01.png)

 ### 마크업 가이드 진행
* 시맨틱한 마크업 구조 설계 (HTML 문서 작성) : 디자인이 적용되지 않은 상태이며, 가장 기초적인 골격의 형태로 내용의 선형성을 유지하고 의미론적으로 작성되며 접근성이 확보될 수 있도록 작성되어야 한다.

- DOCTYPE 정의 및 선언(DTD)이란

``` html
<!DOCTYPE html>
```        
- 주언어 lang 속성 선언
``` html
<html lang="ko">
```        
- head 요소는 문서의 선언을 포함하는 일반적인 정보, 제목과 스타일시트, 스크립트 링크를 제공

``` html
<html lang="ko">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0, user-scalable=no">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<title>네이버 회원정보</title>
	<link rel="stylesheet" href="css/join_global.css">
	<script type="text/javascript" src="http://code.jquery.com/jquery-latest.js"></script>
</head>
<body>
  <!-- 콘텐츠 영역 -->
</body>
</html>
```       
- viewport 소개
  - 스마트 기기에서 여러 단말기에 해상도에 대응하기위해 사용
  - 스마트 기기상에서 최초에 페이지를 로딩할때 확대정도, 최대 확대비율, 최초 확대비율을 다루는 meta data에 속하는 속성


- 스타일 시트 설계 (CSS 문서 작성) : HTML 문서위에 css로 스타일링 하여 디자인 시안과 동일한 UI로 화면을 구성한다.

- 테스트 및 유효성 검사 : HTML과 css에 대한 문법적 검사로 페이지 단위로 이루어진다. HTML W3c validator & firfox의 부가기능 firebug ot firebug 로 검사

- 웹접근성 테스트 n-wax 등등 테스트

- 검수 기준 브라우져, 모바일 기기에서 마크업 가이드의 화면과 디자인 가이드에 표기된 수치와 동일하게 노출되는지 테스트한다.

ex ) pc :  ie11 ~ ie8 (px 검수 브라우져 ie11)
        mobile : iphone 5  (inspector or X 코드 )


예시 페이지
- 점유인증 페이지 설명

- html 구조 설명
- input lable링 예시(접근성), blind 텍스트
- 미디어쿼리 ( one soure markup )
pc/ table / mobile  하나의 페이지로 마크업작성 . css 해상도별 분기 css
-이미지 스프라이트 사용된 부분 설명
