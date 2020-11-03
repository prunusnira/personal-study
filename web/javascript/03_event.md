# Event와 DOM
## Event
### 정의
* 프로그래밍 언어에서의 이벤트: 사용자의 동작이나 프로그램에서 발생하는 특정 상황
* 이벤트가 발생하면 미리 정의된 코드가 실행되고 이에 따라 기능이 동작하거나 화면이 변경된다
### 주요 HTML 이벤트
* click: 마우스 클릭
* focus: 포커스를 얻었을 때 (text input 등)
* keydown/keyup: 키를 누르거나 키에서 손을 뗸 경우 발생
* load: 문서 로드가 완료되었을 때
* mouseover/mousedown/mouseout/mousemove/mouseup: 마우스 움직임에 대한 이벤트
* select/submit: 선택이나 요청 양식 제출 시 발생
* 기타 등등... 매우 많음
### 이벤트 핸들러
* 이벤트가 발생하면 이를 감지하고 처리할 코드가 필요한데 이를 이벤트 핸들러라고 함
* HTML상에서 속성으로 정의하거나 JS에서 직접 구현할 수 있음
```html
<input type="button" onclick="alert('클릭')"></input>
```
```javascript
document.getElementById("submitbtn").onclick = function() {
    alert("클릭");
};
```
## DOM (Document Object Model)
### 정의
* HTML이나 XML의 문서 표현 방식을 제공하는 표준 모델
* HTML에서는 JS로 DOM 구조에 접근하여 문서의 구조, 내용, 스타일을 변경할 수 있음
### 각 노드 타입
* Document Node: DOM에 접근하기 위한 최상위 document 객체
* Element Node: HTML 태그들이며 Attribute Node와 Text Node를 가짐
* Attribute Node: 객체화된 속성 노드
* Text Node: 태그의 값을 테스트로 객체화한 노드 (DOM 트리 구조의 최하단)
* Element Node는 다른 Element Node를 자식으로 가질 수 있다
### HTML element 선택
* getElement(s)By[ ] 와 같은 이름을 가진 메소드를 사용하여 각 HTML 요소를 가져올 수 있다
* s가 붙으면 Array 형태로 여러개가 오고 s가 없으면 맨 처음 찾아진 요소를 가져온다
* 사용할 수 있는 속성
    + Id: 아이디 값으로 가져온다. 아래 나머지는 getElements인 반면 이것만 getElement이다.
    + Name: 이름 값으로 가져온다
    + ClassName: 클래스 값으로 가져온다
    + TagName: 태그 명으로 가져온다
    + TagNameNS: 주어진 네임스페이스에 속하는 태그명을 갖는 element 목록을 가져온다. tag이름 외에 namespace가 파라미터로 들어간다
### querySelector
* 조건에 맞는 요소를 가져올 때 사용한다
* querySelector/querySelectorAll의 두 가지 종류가 있다 (첫 element, 여러개 반환의 차이)
* 이름, 아이디, 클래스이름 등 다양한 것을 사용 가능 (#id .class element)
### Element 컨트롤
* getElement나 querySelector로 가져온 DOM element를 사용하여 속성과 텍스트 노드에 접근가능하며 값을 변경하거나 이벤트 핸들러를 추가하는 등의 수정이 가능하다
```javascript
const inputButton = document.getElementById('btn');
inputButton.setAttribute('name', '[???]');
inputButton.onclick = function() { };
inputButton.addEventHandler("click", function() {});

// CSS 핸들링
inputButton.setAttribute('style', 'color:blue');    // 비추
inputButton..style.color = 'blue';                  // 추천
```