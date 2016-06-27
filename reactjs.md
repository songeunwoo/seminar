# React.js

![](assets/reactjs-301832.jpg)

 - home : https://facebook.github.io/react/  
 - repo : https://github.com/facebook/react

## Facebook은 React를 왜 만들었을까?

페이스북, 인스타그램 같은 크고 복잡한 애플리케이션 제작시,
기존 MVC는 끊임없이 변화하는 복잡한 UI에 적합하지 않았다.
그래서 재사용이 가능한 **UI 컴포넌트를 만드는 VIEW 전용 자바스크립트 라이브러리**를 만들어 주는 React가 탄생 하게 되었다.

 참고 url : https://facebook.github.io/react/blog/2013/06/05/why-react.html


![](assets/react_02_component1.jpg)
[출처:김태곤 개발자 발표자료](http://www.slideshare.net/taggon/react-js-46357445 "출처 : 김태곤 개발자 발표자료")


## google Trends

![](assets/googleTrends.jpeg)


## 특징

 * JUST THE UI

    ~~M : MODEL~~

      V : VIEW : 컴포넌트를 통한 view 표현만 담당

    ~~C : CONTROLLER~~                         


        >Separation of concerns?

        React.js 는 컴포넌트로써 마크업과 뷰의 로직을 createClass()의 안에 작성합니다.
        하지만, 기존의 다른 방식 처럼 마크업은 HTML이나 mustache로 작성하고 뷰의 로직은 자바스크립트로 나눠서 작성하지 않아 마음에 들지 않는 사람도 있을 것 같습니다.
        이 사안에 대해 React.js의 개발자인 Pete Hunt는 "그것은 관심사의 분리(Separation of concerns)가 아니라
        기술의 분리(Speparation of technologies)”라며 마크업과 뷰의 로직은 긴밀해야 한다고 언급했습니다.
        거기에 템플릿의 문법으로 불필요하게 코드를 작성하는 것 보다 자바스크립트로 작성하는 것이 더 좋다고 말하고 있습니다.

        >Separation of concerns vs Speparation of technologies

        HTML, CSS, 자바스크립트를 분리하는 건 관심사의 분리가 아니라 단순한 기술의 분리일 뿐, 그래서 React.js는 관심사를 컴포넌트 단위로 해석했다고 이해할 수 있습니다.

 * VIRTUAL DOM

        메모리에 가상의 DOM 트리를 구축 • 비교 후 실제 변경 사항이 있을 때 변경된 부분만 DOM에 반영.
        다시 그릴때(rerender)는 그 구조체의 전후 상태를 비교(diff)하여 최소한의 변경 사항을 실제 DOM에 반영합니다.
        따라서 무작위로 다시 그려도 변경에 필요한 최소한의 DOM만 갱신되기 때문에 빠르게 처리할 수 있습니다.

        - Ember는 Glimmer라는 Virtual DOM 기술 적용    
        - Google은 2015년 7월에 Incremental DOM이라는  Virtual DOM 라이브러리 발표   
        - Angular2 : http://goo.gl/k4pYbH
    
    - 참고 url : https://facebook.github.io/react/docs/reconciliation-ko-KR.html

 * DATA FLOW

        단방향 데이터 흐름 (One-way data flow) 으로 이해하고 관리하기 쉬운 애플리케이션을 만들 수 있습니다.
        상위 컴포넌트 -> 하위 컴포넌트 (하위 컴포넌트의 변화는 이벤트를 통해 감지한다.)

        - Props
           불변성을 갖는다.



        - State
            가변성을 갖는다.


 * JSX : JavaScript XML

        자바스크립트 안에 XML을 표현하는 문법

    변환 : React JSX는 XML같은 문법에서 네이티브 JavaScript로 변환됩니다.
    ``` javascript
    var Nav;
    // 입력 (JSX):
    var app = <Nav color="blue" />;
    // 출력 (JS):
    var app = React.createElement(Nav, {color:"blue"});
    ```        

    네임스페이스를 사용한 컴포넌트
    ```javascript
    // 이렇게 보기 어려운 코드를
    var Form = MyFormComponent;
    var FormRow = Form.Row;
    var FormLabel = Form.Label;
    var FormInput = Form.Input;

    // 직관성있게 아래와 같이 작성이 가능 합니다.
    var App = (
    <Form>
     <FormRow>
       <FormLabel />
       <FormInput />
     </FormRow>
    </Form>
    );

    // 더 간단하고 쉽게 네임스페이스를 사용한 컴포넌트를 사용해서, 다른 컴포넌트를 어트리뷰트로 사용할수 있습니다.
    var Form = MyFormComponent;

    var App = (
      <Form>
        <Form.Row>
          <Form.Label />
          <Form.Input />
        </Form.Row>
      </Form>
    );
    ```

    - 참고 url : https://facebook.github.io/react/docs/jsx-in-depth.html
 
 - Babel
    
        Babel transforms your JavaScript
        
    home : https://babeljs.io/
        

## React Native

![](assets/react_07_React_Native_logo.jpg)

 - repo : https://facebook.github.io/react-native/


 * Native Components

        React Native는 말 그대로 본래 제공하는 네이티브 속성을 그대로 이용할 수 있다.

 * Asynchronous Execution

        React Native는 자바스크립트 코드와 Native 코드를 별도 스레드로 분리한 뒤 둘 사이의 통신을 비동기식으로 만든다.
        이 때문에 네이티브가 자바스크립트 때문에 느려지는 현상이 없어진다.

    = 참고 url : http://www.slideshare.net/taggon/react-native 

## 함께해요 React!!
- 게시판의 댓글상자를 만들어 보겠습니다.

1. 시작은 간단하게
    - tutorial repo : https://github.com/reactjs/react-tutorial

2. 실제로 컴포넌트를 구성해 봅시다! (1,2,3,4)
    - 댓글상자 예제에서 아래와 같은 구조를 가질것 입니다.

    ```
    - CommentBox
       - CommentList
          - Comment
       - CommentForm
    ```

3. 컴포넌트 프로퍼티 (Component Properties) (5)
    - 이제 컨포넌트를 만들었으니, 여기에 글쓴이와 내용을 넘겨보도록 합시다.
    이렇게 함으로써 각 고유한 comment에서 같은 **코드를 재사용**할 수 있습니다.

4. Markdown 추가하기 (6,7)
    - remarkable 추가.
    ```
    <script src="https://cdnjs.cloudflare.com/ajax/libs/remarkable/1.6.2/remarkable.min.js"></script>
    ```

5. 데이터 모델 연결하기 (8,9,10)
   - json 데이터들을 댓글로 보내보자.

6. 동적으로 서버에서 받아오기 (11,12)
   - 서버에서 동적으로 받아서 처리하는 방식으로 바꿔봅시다.
   - 가변적인 state로 변경. private하므로 this.setState()으로 변경이 가능 하다.
     state가 업데이트 되면, 컴포넌트는 자신을 스스로 다시 렌더링합니다.
     동적 업데이트의 핵심은 this.setState()의 호출입니다.

7. state 업데이트하기 (13,14)
    -  jQuery를 사용해 서버에 비동기 요청을 통해 update.   

8. 새로운 댓글 추가 (15,16,17,18,19)
    - 새로운 폼의 추가 및 상호 작용


  
- 참고 url : https://facebook.github.io/react/docs/tutorial.html 


## 마치며...

    제가 소개한 내용은 핵심 개념과 아주 작은 부분 들일 뿐입니다.
    코드가 직관성이 좋다고 하지만 오히려 보기 더 어려워 졌다고 보여 집니다.
    하지만 UI요소를 컴포넌트화 하여 재 사용 한다는점, 가상의 DOM을 사용하는점 등 나름 신기하고 즐거웠습니다.
    여러분이 이 글을 통해서 React에 대해 조금이라도 관심을 가지고 흥미가 생기셨기를 바랍니다.


api : https://facebook.github.io/react/docs/top-level-api.html
