# Score와 Closure
## Scope
* JS 내에서 어떤 변수들에 접근할 수 있는지를 정의
* Global/Local의 두 가지가 있음
### Global Scope
* 변수가 메소드 밖이나 중괄호로 지정된 블록 밖에 선언된 경우 전역으로 정의되었다고 한다
```javascript
const global = 'global';

function test() {
    console.log(global);
}
```
* 같은 이름이 2개 이상이 되어 충돌할 경우 에러가 발생함
```javascript
let a = 1;
let a = 2; // Uncaught SyntaxError: Identifier 'a' has already been declared
```
* 단, var를 사용하면 두 번째 선언한 변수가 첫 번째를 덮어씌운다. ES6을 쓴다면 되도록 var은 쓰지 말자
* 애초에 전역변수는 안쓰는게 맞다
### Local Scope
* 대부분은 자연스럽게 로컬변수를 사용하게 되는데 Function 단위와 Block 단위로 나뉘어진다
#### Function Scope
* 메소드 내에서 변수를 선언하면 메소드 밖에선 사용할 수 없다
```javascript
function test() {
    const a = 1;
}
console.log(a); // error
```
#### Block Scope
* 메소드가 아닌 블록 내에서 선언한 변수도 마찬가지
```javascript
{
    const a = 1;
}
console.log(a); // error
```
### 함수 호이스팅과 스코프
* 함수가 만약 선언(function declaration)으로 선언되면 호이스팅이 된다
```javascript
test();
function test() {
    console.log("A");
}
// 요렇게도 쓸 수 있고

function test() {
    console.log("A");
}
test();
// 요렇게도 쓸 수 있다
```
* 그러나 표현식(function expression)으로 정의되면 호이스팅이 되지 않는다
```javascript
test(); // 이건 안된다
const test = function() {
    console.log("A");
}
```
* 혼란을 줄이려면 메소드를 사용하기 전에 항상 선언해두자
* Nested Scope
```javascript
function A() {
    const va = "VA";

    function B() {
        const vb = "VB";
        console.log(va); // 가능
    }
    console.log(vb); // 불가
}
```
## Closure
### 정의
* 독립적인 변수를 가리키는 메소드
* 클로저는 독립적이므로 실행 뒤 값이 그대로 보존되어있다
### Lexical(어휘적) Scope
```javascript
function init() {
  var name = "nira";
  function displayName() {
    alert(name);
  }
  displayName();
}
init();
```
* 위의 예제에서는 init이 호출되면 그 내부에서 displayName이 호출되는 방식을 가지고 있다.
* Nested scope이므로 name 변수는 displayName에서도 사용할 수 있다 (메소드 내부에서는 외부의 변수 접근이 가능함)
* Lexical 이란 변수가 어디서 사용가능한지 알기 위해 해당 변수가 어디에서 선언되었는지 고려한다는 것을 의미한다.
* 이 때 호출이 아닌 선언 순서에 따라 Scope가 변경된다는 것에 주의해야 한다
### 클로저
```javascript
function init() {
  var name = "nira";
  function displayName() {
    alert(name);
  }
  return displayName;
}
var myname = init();
myname();
// 혹은 이렇게도 사용 가능하다
init()();
```
* 앞의 예제와 역할은 동일하지만 위에서는 메소드를 실행한 반면, 여기서는 내부의 메소드 자체를 리턴하여 이를 사용한다
* 리턴된 것이 메소드이므로 이를 발동하려면 다시 한 번 괄호()를 붙여주어야 발동된다
### 사용하는 이유
#### 정보은닉과 캡슐화 제공
* 일반적인 프로그래밍에서 사용하는 private과 같은 접근지정자와 같은 효과를 낼 수 있다
```javascript
const a = (function() {
    var privatefunc = function() {
        alert('private');
    }

    return {
        publicfunc: function() {
            privatefunc();
        }
    }
})();
a.publicfunc();
```
* a.publicfunc()를 호출하면 a.privatefunc()가 호출되는데, 이는 closure에서만 접근되고 사용자가 직접 a.privatefunc()를 부를 수는 없다
```javascript
// counter example
<button onclick="updateCount()">Tap</button>

// case 1
let count = 0;
function updateCount() {
    count++;
}

// case 2
function updateCount() {
    let count = 0;
    count++;
}

// case 3
function updateCount() {
    let count = 0;
    function update() {
        count++;
    }
    update();
    return count;
}

// case 4
function countClosure() {
    let count = 0;

    return {
        updateCount: function() {
            count++;
            console.log(count);
        },
        getCount: function() {
            return count;
        }
    }
}
const updateCount = countClosure();
updateCount.updateCount(); // 실행
```
* case 1은 일반적인 구현이지만 count를 밖에서 제어 가능하다
* case 2는 매번 부를 때마다 0으로 초기화된다
* case 3도 마찬가지
* case 4처럼 클로저로 만들면 외부에서 count에 접근할 방법은 없다. count를 참조하지 않고 값을 리턴할 방법도 추가되었다.
```javascript
function person(_name) {
    let name = _name;

    return {
        get: function() {
            return name;
        },
        set: function(value) {
            name = value;
        }
    }
}
const p1 = person('a');
const p2 = person('b');
```
* 추가로 클로저 변수 끼리는 값을 공유하지 않기 때문에 p1과 p2는 별개의 객체이다.
* 호출 될 때 마다 새로운 지역변수를 갖는 클로저가 생성되기 때문이다.