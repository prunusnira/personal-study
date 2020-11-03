# JS의 자료형
## Primitive Type
* 기본적으로 JS는 이러한 자료형을 구분하지 않아 다른 자료형끼리도 비교나 연산이 가능하다. 이는 큰 문제를 야기할 수 있으며 이를 해결하기 위해 나온것이 TypeScript나 CoffeeScript등의 Superset이다.
* boolean: true/false
* null: 빈 값
* undefined: 변수는 있으나 값이 할당되지 않은 상태
* number: 정수, 부동 소수점, Infinity, NaN (NaN은 숫자로 처리되지 않음)
* string: 문자열
## Type간 비교 연산자
* ==/!=: Equality(동등) 연산자이며 연산이 되기 전에 피연산자들을 비교할 수 있는 형태로 변환 시킨 뒤에 연산을 수행한다
```javascript
254 == '254'              // true
true == 1                 // true
undefined == null         // true
'a' === new String('a')   // true
```
* ===/!==: Identity(일치) 연산자이며 피연산자의 형 변환 없이 있는 그대로 비교한다
```javascript
254 === '254'             // false
true === 1                // false
undefined === null        // false
'a' === new String('a')   // false
```
* 그래서 대부분은 ===나 !==를 쓰는게 낫다
* 다른 에시들
```javascript
0 == ''   // true
0 === ''  // false
NaN === NaN   // false
```
## Object Type
* 레퍼런스 타입
* 클래스, 배열, 함수, 사용자 정의 클래스를 모두 포함한다
* JSON(JavaScript Object Notation)은 Object를 기반으로 구성된다
# Variable
## 데이터 선언 방식
* var
    + 전통적인 JS의 변수 선언
    + 함수 범위에서 유효한 선언 방식
    + var를 선언하지 않으면 자동으로 전역변수가 됨
    ```javascript
    var a = 10;
    if(true) {
        var a = 20;
    }
    console.log(a); // 20
    ```
    + 위와 같은 문제가 있다
* let/const
    + ES6에서 새로 나온 block scope가 있는 변수 선언
    + let은 값을 재할당 할 수 있는 반면 const는 상수로 값을 바꿀 수 없음
    + (물론 const에 Object 타입을 넣으면 그 하위 데이터는 변경 가능, 재할당이 불가능한 것이다)
    + var의 예시와 같은 문제가 없이 일반적인 언어와 동일한 특성을 가진다
## Hoisting
* 변수나 메소드 등의 선언이 그 위치와 상관없이 어디서나 참조가 가능한 것을 말한다
* 단, 내부에 할당된 내용은 그 라인이 지나기 전에는 들어있지 않으며 값을 참조하면 undefined가 나오게 된다
```javascript
console.log(foo); // undefined
var foo = 'foo1';
console.log(foo); // foo1
```
## string 선언
* 일반적인 언어들이 ''는 char에 사용하고 ""는 string에 사용하는 반면,
* JS에서는 '', "" 모두 사용할 수 있다
# 특이한 제어문
## forEach
* ES5에서 추가되었다
* E를 대문자로 쓴다
```javascript
const data = [1, 2, 3];
data.forEach(function(value) {
    console.log(value);
});
```
* ES6에서 새로 도입된 arrow 연산자를 사용하면 이렇게 된다
```javascript
data.forEach(value => console.log(value));
```
## for-in, for-of
* C#이나 kotlin등에서 사용하는 방식으로 for문을 사용할 수 있다
* for-in은 키 값이나 인덱스로만 사용할 수 있고, 값을 가져오려면 for-of를 써야 한다
```javascript
for(var index in data) { console.log(data[index]); }
for(var value of data) { console.log(value); }
```
### for-in
* 객체의 모든 열거 가능한 속성에 대한 반복
* 객체의 키(key)에만 접근할 수 있으며 값(value)에는 접근할 수 없다
### for-of
* Iterable(반복 가능한) 객체의 값을 탐색
* 문자열, map, set(이 둘은 ES6에서 추가)에 대해서도 사용할 수 있다
# 자료구조
## Array
* [], new Array() 등으로 생성
* 크기의 제약이 없다
* 서로 다른 자료형을 한 배열에 넣을 수 있다
* JS객체도 넣을 수 있다
```javascript
var arr1 = [{"key":"value"}, 1, 'a']; // 이런게 가능하다
```
* 특히 객체가 들어간 배열은 JSON string이 되어서 서버와의 값 교환이나 내부 데이터관리에 이용할 수 있다
* 주요 메소드
    + push: 마지막에 값 추가
    + pop: 마지막 값 제거
    + shift: 맨 앞의 값 제거
    + splice: 배열값을 추가/제거하여 반환
    ```javascript
    const months = ['Jan', 'March', 'April', 'June'];
    months.splice(1, 0, 'Feb'); // index 1에서 0개를 지우고 "Feb"를 삽입
    console.log(months); // Array ["Jan", "Feb", "March", "April", "June"]
    months.splice(4, 1, 'May'); // index 4에서 1개를 지우고 "May" 삽입
    console.log(months); // Array ["Jan", "Feb", "March", "April", "May"]
    ```
    + reverse: 역순으로 만듦
    + sort: 정렬
    + concat: 두 배열 합치기
    + join: 배열 요소를 합쳐 문자열로 반환, 원하는 구분자를 추가할 수 있음
    + slice: 배열의 일부만 지정하여 반환
    + map: 각 배열 데이터에 대한 반복처리
    + filter: 특정 조건을 만족하는 데이터를 처리
    + reduce: 모든 데이터를 순회하면서 누적되는 연산을 수행
## Map
* ES6에서 Set과 함께 추가되었음
* 일반적인 언어들의 Map과 동일하게 key-value로 이루어져 있음
* Object와의 차이점
    + Object는 문자열만 key로 갖지만 Map은 어떤 값이든 가능
    + Object의 크기는 수동으로 판단하지만 Map은 내부 메소드를 지원
    + 데이터가 추가된 순서대로 iteration을 수행
    + 들어가는 key들과 value들이 각각 모두 동일한 타입이라면 Map을 쓰고 그게 아니라면 Object를 쓰자
## Set
* 일반적인 언어의 Set과 마찬가지로 중복 값은 허용하지 않는다
* Array가 splice로 삭제를 진행해야 하는 것과 달리 자체적인 삭제 메소드가 있다
* Array와 Set은 상호 변환이 가능하다 (Array -> Set의 경우 중복값은 자동 제거)
# Function
* JS는 메소드 자체를 변수로 할당할 수 있어 이를 사용해 인자로 메소드를 전달하거나 콜백을 구현하는 등의 활용이 가능
* 이러한 특징을 활용하여 함수형 프로그래밍의 개념도 어느정도 지원된다
## First Class Object
```
[참고](https://bestalign.github.io/2015/10/18/first-class-object/)
1급시민: 변수에 담을 수 있고, 파라미터로 전달할 수 있으며, 메소드에서 리턴될 수 있는 것

1급객체: 특정 언어에서 Object를 1급 시민으로 취급하는 것

1급함수: 함수를 1급시민으로 취급하는것, 아래의 추가 요건을 요구하기도 한다
- 런타임 생성이 가능해야 할 것
- 익명(anonymous) 생성이 가능해야 할 것
```
* JS는 모든 객체를 1급시민으로 취급하며 메소드도 객체로 관리하므로 메소드 또한 1급 객체이다
* 보통 JS에서의 1급객체는 아래의 조건을 만족한다
    + 변수나 데이터 구조에 담을 수 있다
    + 파라미터 전달이 가능하다
    + 리턴값으로 사용할 수 있다
    + 할당에 사용된 이름과 관계없이 고유 구별이 가능하다
    + 동적 속성 할당이 된다
## 익명 메소드 (Anonymous Function)
* 이름이 없이 variable로 구현하거나 리턴하는 형태의 메소드를 의미한다
* 이를 이용하여 콜백 구현이 가능하다
```javascript
const anonfunc = function(a, b) {
    return a+b;
}

function test(method) {
    console.log(method(1, 2));
}

console.log(anonfunc(1, 2));
test(anonfunc);
```
## 콜백 메소드 (Callback Function)
```javascript
function test(a, callback) {
    /* 비즈니스 로직이 들어가는 부분 */
    setTimeout(callback, 10, a);
}

test(1, function(n) {
    console.log(n);
});
```
* 메소드의 파라미터로 메소드를 넣어서 원하는 동작이 끝난 후 호출시킬 수 있다
* 익명 메소드를 만들어서 파라미터로 활용해도 되고 위의 예제처럼 파라미터에 바로 메소드 정의를 넣어도 된다
## 자료구조에 사용
* JS는 모든 것이 객체라고 하였으므로 당연히 메소드도 자료구조의 멤버로 사용 가능하다
* Array, Map/Set, Object 모두 사용 가능하다
```javascript
const funcarr = [function(v) { console.log(v); }];
funcarr[0]('a');
```