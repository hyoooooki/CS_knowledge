# 웹 프로그래밍

*해당 자료는 [부스트코스 웹프로그래밍](https://www.edwith.org/boostcourse-web)에 기반을 두고 있음.*

<br>

### 목차

##### [1. 웹프로그래밍 기초 ](#웹프로그래밍-기초)

- [웹개발의 이해](#웹개발의-이해)

- [HTML](#html)

- [CSS](#css)

- [Servlet](#servlet)

  

<br>


## 웹프로그래밍 기초

### 웹개발의 이해



#### 프로그래밍 언어

- 저급언어
- 고급언어
- 컴파일러



##### 저급언어

- 2진수로 이뤄진 값으로 작성하는 프로그래밍 언어를 **기계어**라고 함.
- 기호로 작성된 언어를 **어셈블리어**라고 하며 이를 숫자로 바꿔주는 것을 **컴파일러**라고 한다.



##### 고급언어

- 사람 중심의 언어
- **컴파일러**를 이용하여 소스코드를 번역한다.



##### 웹관련언어

1. Python : 입문자가 읽기 쉽고 적은 코드를 사용하여 프로그램을 개발할 수 있음.
2. PHP : 웹의 80% 이상이 PHP로 만들어졌다고 함.
3. JavaScript : 초기에는 브라우저에서 동작하는 언어였으며 현재는 서버에서도 작성하는 프로그램으로 영역확대.
4. Java : 엔터프라이즈 소프트웨어 환경에 잘 맞는 언어
5. Ruby : 빠른 개발에 널리 사용되며, 단순함과 세련된 웹 어플리케이션을 만들 수 있음.



#### 웹의 동작(HTTP프로토콜 이해)



**인터넷(네트웍 통신)의 이해**

- 물리적인 하나의 컴퓨터에 여러개의 서버가 동작가능

- 각각의 서버는 각각의 포트를 가지고 있음
- TCP/IP라는 약속으로 연결되어 있는 경우가 많음.



**HTTP**

- HTTP는 서버와 클라이언트가 인터넷상에서 데이터를 주고 받기 위한 프로토콜(protocol)입니다.
- 현재는 version2까지 나옴.
- 기본 포트값 80번

- 작동방식
  - 서버/클라이언트 모델을 따름
  - 클라이언트가 요청을 서버에 요청을 보내고 서버가 응답을 보내는 것
  - 서버는 응답을 하고나면 연결을 끊어버림.
  - **장점** : 불특정 다수를 대상으로하는 서비스에 적합함. 계속적으로 연결된 상태가 아니기에 최대 연결 수보다 훨씬 많은 요청과 응답을 처리할 수 있음.
  - **단점** : 연결을 끊기에 클라이언트의 이전상황을 알 수 없음. 이러한 특징을 무상태(stateless)라고 함. 정보유지를 위해서 쿠키라는 개념도입.

<img src="C:/Users/Pink_HYOKI/Google 드라이브(학습)/스터디자료/web-programming/assets/http.png">



**URL**

- 인터넷 상 자원의 위치를 나타내기 위해서 사용
- 프로토콜의 종류 + 자원이 있는 서버의 **IP(도메인주소)** + 자원의 위치
  **총 3가지**로 구분이 되어 있음.



**HTTP - HTTPS의 차이**

https의 경우 보안이 강화된 http통신을 의미하며, 통신시 인증 및 암호가 요구된다. 그러므로 강력한 보안이 필요한 전자상거래 등에 이용된다.



#### 웹 Front-End, Back-End



##### 프론트엔드

사용자에게 웹을 통해 다양한 콘텐츠(문서, 동영상, 사진등)을 제공한다. 또한 사용자의 요청(요구사항)에 반응해서 동작한다.



**프론트 엔드 구조**

- 적절한 배치와 일관된 디자인등과같이 잘 구조화 하여서 만들어야함.
- 가독성이 좋게 디자인하는 것이 좋다. 사용자의 요청을 잘 반영해야함.
- HTML(구조를 결정함) 
- CSS(디자인적 요소 결정)
- JavaScript(요청 반영-동적제어) - 상대적으로 복잡한 interactive를 담고있음.



##### 백엔드

서버입장에서 개발이 진행, 프론트엔드로 부터 요청을 받고 그에 대한 결과를 넘겨주는 역할을 한다.



#### Browser의 동작

서버에서 전송한 데이터가 클라이언트에 도착해야 할 곳은 Browser이다.

- 서버와 HTTP로 정보를 주고 받을 수 있는 네트워크 모듈도 포함.

- 서버에서 받은 문서(html, css 등)를 해석하고 실행하는 parser도 있음.
- 브라우저 별로 각기 다른 엔진을 포함.



<browser component>

<img src="C:/Users/Pink_HYOKI/Google 드라이브(학습)/스터디자료/web-programming/assets/browser.png">



<browser flow>

<img src="C:/Users/Pink_HYOKI/Google 드라이브(학습)/스터디자료/web-programming/assets/browser_flow.png">



<예시 - 사파리 브라우저에서 처리되는 webkit 렌더링 엔진의 처리과정>

<img src="C:/Users/Pink_HYOKI/Google 드라이브(학습)/스터디자료/web-programming/assets/browser_main.png">



HTML + CSS = Render tree

만약 브라우저 탐색 시 스크롤이나 화면의 위치 변경이 일어나더라도 처음부터 모든 과정이 이루어지는 것이 아닌 render tree의 값을 변경하여 새로 display를 해준다. 여기서 캐시나 쿠키에 저장을 하면 더욱 효율적으로 사용 가능.



reference : https://www.html5rocks.com/en/tutorials/internals/howbrowserswork/



#### Browser에서의 웹 개발



- html코드 사이에 자바스크립트 코드와 css코드가 존재할 수 있다.

- HTML문서는 html태그로 시작해 html태그로 끝남.

- head는 HTML의 추가적인 설명(자세한 문서에 대한 정보)을 담고있음.

- body는 화면에 표현되어야할 정보가 포함.

- HTML은 계층적.

- HTML은 tag를 사용하여 표현한다.
- javascript코드는 보통 body아래에 위치시켜주는 것이 일반적
  (렌더링을 방해할 수 있기 때문에)
- css는 head에 위치시키는 것이 일반적임.





#### 웹서버

- 웹 서버는 소프트웨어를 말하지만, 웹 서버 소프트웨어가 동작한느 컴퓨터도 의미한다.

- 웹 서버의 가장 중요한 기능은 client가 요청하는 html문서나 각종 리소스를 전달하는 것입니다.
- 웹 브라우저나 웹 크롤러가 요청하는 리소스는 컴퓨터에 저장되어 있는 정적인 데이터이거나 동적인 결과가 될 수 있다.
- **웹크롤러** : 네이버나 구글 같은 포털에서 다른 웹사이트 정보를 읽어갈 때 사용하는 소프트웨어

<img src="C:/Users/Pink_HYOKI/Google 드라이브(학습)/스터디자료/web-programming/assets/web_server.png">



**웹 서버 소프트웨어의 종류**

* apache가 가장 대표적인 소프트웨어
  * 거의 대부분 운영체제에서 사용 가능
  * 오픈소스 소프트웨어
* nginx 지속적으로 성장을 하고 있는 소프트웨어
  * 차세대 웹서버로 불리면 더 적은 자원으로 더 빠르게 데이터를 서비스
  * 오픈소스 소프트웨어



#### WAS(web application server)



**클라이언트 / 서버 구조**

클라이언트 - 서비스를 요청하고 제공받는 대상

서버 - 요청된 서비스에 대한 처리를 하고 제공하는 대상

<img src="C:/Users/Pink_HYOKI/Google 드라이브(학습)/스터디자료/web-programming/assets/c_s.png">



**DBMS**

- 다수의 사용자들이 데이터베이스 내의 데이터를 접근할 수 있도록 해주는 소프트웨어

- 개발자들이 매우 편리하게 데이터를 관리할 수 있게 되었음.

<img src="C:/Users/Pink_HYOKI/Google 드라이브(학습)/스터디자료/web-programming/assets/d_s.png">

**미들웨어**

- 클라이언트와 DBMS사에 별도의 서버를 운영
- 클라이언트 쪽에 비즈니스 로직이 많을 경우, 클라이언트 관리 비용이 증가하는 문제 발생.
  => 미들웨어를 통해 클라이언트는 입,출력만 담당하면 된다.

<img src="C:/Users/Pink_HYOKI/Google 드라이브(학습)/스터디자료/web-programming/assets/mw.png">



**WAS**

- 일종의 미들웨어로 웹 클라이언트의 요청 중 보통 웹 애플리케이션이 동작하도록 지원하는 목적을 가짐.
- 초기에는 정적인 것만 제공하다가 동적인 것을 제공할 필요가 있어져 생겨남.



**WAS 기능**

1. 프로그램 실행환경과 DB접속 기능을 제공.
2. 여러개의 트랜잭션을 관리
3. 업무를 처리하는 비즈니스 로직을 수행
4. 웹서버의 기능도 제공
   (was tomcat만 설치하여 사용 가능한 이유)

<img src="C:/Users/Pink_HYOKI/Google 드라이브(학습)/스터디자료/web-programming/assets/was.png">

**웹서버, was의 차이점**

- was도 보통 자체적으로 웹 서버 기능을 내장
- 과거에는 was의 웹서버의 성능이 좋지 않아 별도의 웹서버를 설치했었음.
- 현재는 was가 가지고 있는 웹 서버도 정적인 컨텐츠를 처리하는데 있어 성능상 큰 차이가 없다.
- 규모가 커질수록 웹 서버와 was를 분리해야 관리적인 측면에서 유리하고 장애 극복 기능이 좋아진다.
  무중단 운영이 매우 중요해지는 경우에 특히 이렇게 구조화 해야함.
- 보통 웹서버를 먼저 위치시키고 그 뒤에 was를 위치시킨다.

<img src="C:/Users/Pink_HYOKI/Google 드라이브(학습)/스터디자료/web-programming/assets/was_web.png">

---

### HTML

**HTML태그**

태그는 그 의미에 맞춰서 사용해야 한다.



**layout태그**

<img src ="C:/Users/Pink_HYOKI/Google 드라이브(학습)/스터디자료/web-programming/assets/htmp_layout.png"> 



**HTML 구조설계**

문서를 쓴다고 생각하면 편함.

큰 영역으로 우선적으로 분리 후에 각 영역 안의 세부 구조를 잡아가는 것이 편리.

html이 가장 기초적인 뼈대가 되는 것이므로 초기 개발단계에서 잘 구조화시켜놓아야 후에 지속적으로 개발하기에 용이함.



**Class 와 Id**

class

- 하나의 HTML문서 안에 중복해서 사용 가능
- 하나의 태그에 여러 개의 다른 class이름을 공백을 기준으로 나열할 수 있음.
- 홈페이지 전반적인 스트일의 일관성을 주기 위해 class필수



id

- 고유한 속성으로 한 HTML 문서에 하나만 사용 가능
- 고유한 ID값이 있으면 하나하나에 특별한 제어를 할 수 있으며 검색 용이.



---

### CSS

selector(선택자), property(속성), value(값)으로 이루어진다.

```css
span{
	color : red;
}
```

span - selector

color - property

red - value



**사용 방법**

- inline 
  - html태그(body) 안에다가 작성 
  - 가장 우선선위를 가짐
- internal 
  - style 태그로 지정(head안에다가 넣는것
  - 별도의 css파일 관리 X
  - 구조와 스타일이 섞여 유지보수 어려움
- external 
  - 외부에 css파일을 별도로 관리
  - css가 매우 짧지 않다면 이와 같이 구성하는 것이 가장 좋음.
  - internal과 external의 우선순위는 동등함. 따라서 겹치는 선언이 있는 경우 나중에 선언된 속성이 반영.



동적으로 css코드를 수정하고 싶은 경우 class나 id값을 이용하여 css속성을 주어 동적으로 수정이 될 수 있도록 한다.



**상속과 우선순위 결정**

**상속**

- 매번 속성을 설정해주는 것은 매우 번거로운 작업

- 그러므로 부모의 속성을 자식이 물려받음.

- box-model이라고 불리는 속성들(width, height, margin, padding, border)과 같이 크기와 배치 관련된 속성들은  상속되지 않음.



**우선순위**

- css는 여러 스타일정보를 기반으로 최종적으로 **경쟁**에서 승리한 스타일 반영

- inline > internal = external
- id와 class를 모두 선언하게되면 id가 더욱 우선된다.
- 보통 구체적인 표현을 한 것이 우선순위가 높다.
- ID > CLASS > ELEMENT순으로 반영



**CSS Selector**

- HTML의 요소를 tag, id, class 태그 속성 등을 통해 쉽게 찾아주는 방법입니다.

- 그룹을 선택하여 여러개를 한번에 지정가능

- 자손 요소, 자식요소,n번째 자식요소를 선택 가능함

- p:nth-child(2) : 부모의 모든 자식중 2번째가 p태그이면.

  p:nth-of-type(2) :부모의 자식중에서 p태그 2번째.



**CSS Layout**

엘리먼트가 배치하는 것을 layout작업(rendering과정)이라고 함.

- 엘리먼트는 위에서 아래로 순서대로 블럭을 이루며 배치되는 것이 기본.
- 하지만 다양한 형태의 배치를 위해 css에서 추가적 속성을 제공
- 중요한 속성
  - display(block,inline,inline-block)
  - position(static, absolute,relative,fixed)
  - float(left,right)



**display**

- block, inline-block : 위에서 아래로 쌓임
- inline : 왼쪽에서 오른쪽으로 우선적으로 흐름. 아래쪽으로 빈자리 차지하면서 계속흐름



**position**

- 상하좌우로만 흐르며 쌓이면 다양한 배치가 어렵기에 상대적/절대적으로 특정위치에 배치시킬 수 있음. 

- 기본은 static, 그냥 순서대로 배치
- absolute는 기준점에 따라 특정 위치에 배치 가능 (top,left,right,bottom)
- relative는 원래 자신의 위치를 기준으로 상대적 위치 부여(top,left,right,bottom)
- fixed는 전체화면 좌축, 맨위를 기준으로 동작



**margin**

- margin으로 배치가 달라질 수 있음.
- 위/아래/좌/우 엘리먼트와 본인간의 간격



**float**

- 일반적인 배치를 float는 벗어난 형태로 특별히 배치됨.
- block엘리먼트가 float된 엘리먼트를 의식하지 못하고 중첩됨.
- 이러한 특성때문에 전체 레이아웃 배치에 유용하게 사용



**box-model**

- 블록 엘리먼트의 경우 box의 크기와 간격에 관한 속성으로 배치함.
- margin, padding, border, outline으로 생성
- box-shadow 속성도 box-model에 포함되어 설명할 수 있음.
- box-shadow : border 밖에 테두리를 그리는 속성



**엘리먼트 크기**

- block엘리먼트의 크기는 기본적으로 부모의 크기만큼을 가짐.



**box-sizing과 padding**

- padding 속성을 늘리면 엘리먼트의 크기가 달라질 수 있습니다.
- box-sizing 속성으로 이를 컨트롤 할 수 있음.
- border-box로 설정하면 엘리먼트 크기를 고정시킬 수 있음



**layout 구현방법**

- 전체 레이아웃은 float를 잘 사용해서 2단, 3단 컬럼 배치를 구현합니다.
- 최근에는 css-grid나 flex 속성 등 layout을 위한 속성을 사용하기 시작했으며 브라우저 지원범위를 확인해서 사용하도록 합니다.
- 특별한 위치에 배치하기 위해서는 position absolute를 사용하고, 기준점을 relative로 설정합니다.
- 네비게이션과 같은 엘리먼트는 block 엘리먼트를 inline-block으로 변경해서 가로로 배치하기도 합니다.
- 엘리먼트안의 텍스트의 간격과 다른 엘리먼트간의 간격은 padding과 margin 속성을 잘 활용해서 위치시킵니다.

---

### Servlet

**자바 웹 어플리케이션**

- WAS에 설치되어 동작하는 어플리케이션
- 자바 웹 어플리케이션에는 HTML,CSS,이미지,자바로 작성된 클래스(Servlet,package,인터페이스 등),각종 설정 파일 등이 포함된다.

<img src="C:/Users/Pink_HYOKI/Google 드라이브(학습)/스터디자료/web-programming/assets/jwa.png">



**Servlet**

- 자바 웹 어플리케이션의 구성요소 중 동적인 처리를 하는 프로그램의 역할
- 서블릿의 정의
  - 서블릿은 WAS에서 동작하는 java 클래스이다.
  - 서블릿은 HttpServlet클래스를 상속받아야 한다.
  - 서블릿과 JSP로부터 최상의 결과를 얻으려면, 웹 페이지를 개발할 때 이 두가지를 조화롭게 사용해야함.



**Servlet 작성방법**

1. 3.0이상에서 사용하는 방법
   - web.xml 파일 사용 X
   - 자바 어노테이션 사용
2. 3.0 미만에서 사용하는 방법
   - web.xml 파일에 등록



**Servlet의 생명주기**

<img src="C:/Users/Pink_HYOKI/Google 드라이브(학습)/스터디자료/web-programming/assets/servlet_life.png">

1. WAS는 서블릿 요청이 들어오면 메모리에 있는지 확인.
2. 메모리가 없을 시 init() 메소드 실행
3. 메모리가 있을 시 service() 메소드 실행
4. 요청 시에 동작하는 부분은 모두 service()에 구현해야함.
5. WAS가 종료되거나, 웹 어플리케이션이 새롭게 갱신될 경우 destroy()메소드가 실행.



**service 메소드**

- service메소드는 HttpServlet에 이미 구현
- HttpServlet에는 템플릿 메소드 패터으로 구현
- 요청이 get이면 doGet, post이면 doPost를 호출



**request & response**

<img src="C:/Users/Pink_HYOKI/Google 드라이브(학습)/스터디자료/web-programming/assets/res_req.png">

WAS는 웹 브라우저로부터 Servlet요청을 받으면

- 요청할 때 가지고 있는 정보를 HttpServletRequest객체를 생성하여 저장합니다.
- 웹 브라우저에게 응답을 보낼 때 사용하기 위하여 HttpServletResponse객체를 생성합니다.
- 생성된 HttpServletRequest, HttpServletResponse 객체를 서블릿에게 전달합니다.



**Request 객체**

- http프로토콜의 request정보를 서블릿에게 전달하기 위한 목적으로 사용

- 헤더정보, 파라미터, 쿠키, URI, URL 등의 정보를 읽어 들이는 메소드를 가짐.

- Body의 Stream을 읽어 들이는 메소드를 가지고 있음.

  

**Response 객체**

- WAS는 어떤 클라이언트가 요청을 보냈는지 알고 있고, 해당 클라이언트에게 응답을 보내기위해 객체를 생성해 서블릿에게 전달
- 서블릿은 해당 객체를 이용하여 content type, 응답코드, 응답 메세지등을 전송

---



## SUMMARY

**프론트엔드**

1. 프론트엔드와 백엔드의 역할과 관계
2. HTML로 웹페이지 구조 설계
3. CSS 레이아웃에 필요한 속성과 활용방법



**백엔드**

1. 웹 개발에 대한 이해
2. 서블릿(Servlet)







