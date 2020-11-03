# JavaScript Basics
# Before read
* TypeScript나 새로운 기능은 제외한 JS만을 정리함
* 다른 언어에서 볼 수 있는 기초적인 내용은 제외함
# Definition
## JavaScript란 무엇인가
* 정적인 HTML 컨텐츠를 동적으로 만들어주고 사용자와 상호작용을 할 수 있게 해주는 스크립트 언어
## JS의 특징
* 오브젝트 기반의 스크립트 언어로 웹 브라우저상에서 해석되는 인터프리터 언어이다
* 동적이며 타입을 명시하지 않는다
* HTML/CSS에서 정의된 정적인 내용과 속성, 디자인을 변경할 수 있다
* *이벤트*를 처리하여 사용자와 상호작용을 가능하게 한다
* 필요에 따라 서버와 실시간으로 상호작용할 수 있다 (AJAX)
## ECMAScript
* JavaScript의 표준 규격으로 1997년부터 꾸준히 업데이트 되어왔음
* 최근에는 매년 업데이트되는 양상을 보이고 있음
* 모던 JS는 ES6 이상을 지칭한다
## TypeScript
* JS가 Type-strict 하지 않아 생기는 문제들을 해결하기 위해 만들어진 JS의 상위 확장 (Superset)
* 최근 만들어지는 대부분의 JS 라이브러리/플랫폼 등에서도 지원함
* 비슷한 것으로 CoffeeScript 등이 있음
# JS의 활용처
## Frontend
* 본래 JS는 HTML/CSS의 동적 활용을 위한 언어였던 만큼 프론트엔드 개발에 있어서는 필수적인 요소임
* AngularJS, React, Vue 등의 프론트엔드 프레임워크의 기반이 됨
## Backend (Node.js)
* JS를 백엔드 프로그래밍 개발에 사용할 수 있도록 만들어진 서버사이드 JS 런타임 엔진 (정확히는 Chrome V8 JS Engine에 기반)
* 경량의 빠른 웹서버 개발에 적합하지만 안정성 문제와 디버깅이 어렵다는 문제가 있음
* 이벤트 기반의 Non-Blocking I/O를 사용함
* 전용 패키지 매니저(npm)가 있으며 규모도 상당히 큰 편
## Application (Electron/React Native etc)
* JS를 사용하여 데스크탑/모바일용 앱을 만들 수 있게 해주는 플랫폼/라이브러리