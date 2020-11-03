# Object와 Class
## Object
* 현실의 사물의 속성과 행위를 코드로 나타낸 것
```javascript
const me = {
    name: 'nira',
    hobby: 'game'
}
```
* 속성: 콤마로 구분되는 각각의 특성
    + 위의 예제에서는 name: 'nira' 라는 특성과 hobby: 'game'이라는 2가지 속성이 존재
* Key-Value
    + Key: name, hobby와 같은 속성의 이름
    + Value: 해당 속성이 갖는 실제 값
* JS의 Object에는 어떤것이든 들어올 수 있으므로 속성의 값으로 메소드를 넣을 수 있다
```javascript
const test = {
    testvalue: [1, 2, 3],
    calc: function() {
        let sum = 0;
        this.testvalue.forEach( value => sum += value );
        console.log(sum);
    }
}
test.calc(); // 6
```
* ES6에서 Class가 도입되기 전에는 Object를 사용하여 클래스처럼 사용하기도 했다
```javascript
function Person(name, hobby) {
    this.name = name;
    this.hobby = hobby;
    this.getData = function() {
        return this.name + " " + this.hobby;
    }
}
const me = new Person('nira', 'game');
console.log(me.getData()); // nira game
```
## Class
* ES6부터 공식적으로 지원하기 시작하였으며 좀 더 객체지향적인 사용이 가능해졌다
* 위의 Person에서 this.getData와 같이 메소드를 구현하였는데, 이는 매번 new로 객체를 만들때 마다 새로 생성되어 코스트가 많이 드는 문제가 있다 (물론 class로 해결)
```javascript
class MyClass {
    constructor(name, hobby) {
        this.name = name;
        this.hobby = hobby;
    }

    getData() {
        return this.name + " " + this.hobby;
    }

    get data() {
        return this.name + " " + this.hobby;
    }

    set newhobby(newhobby) {
        this.hobby = newhobby;
    }
}
const myobj = new MyClass('nira', 'programming');
console.log(myobj.getData()); // nira programming
console.log(myobj.data); // nira programming
myobj.newhobby = 'game';
console.log(myobj.data); // nira game
```
* 메소드와 마찬가지로 JS에서는 클래스도 객체 취급이므로 익명선언이나 변수할당 등 모든것이 가능하다
* 클래스의 new 연산에서는 constructor가 호출된다
* 아직은 클래스 멤버 선언은 constructor에서만 가능하며 각 인스턴스는 this로 가리킨다
* 위의 getData는 일반 메소드고 get data는 getter이다. 이 경우에는 사용 시 ()를 붙이지 않으며 setter도 마찬가지이다