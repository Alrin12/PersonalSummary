## Rest Operator

 ### Rest Parameter
 ES5의 arguments객체를 대신할 방법이다.

 ``` javascript
 function foo(...rest) {
     console.log(Array.isAarray(rest)); // true;
     console.log(rest); // [1,2,3,4,5]
 }
 
 foo(1,2,3,4,5);
 ```
 Rest Paremeter을 사용하면 인수를 함수 내부에서 배열로 전달받을 수 있다.
 ES5에서는 arguments 객체에 유사배열을 집어넣고 이를 apply 또는 call 메소드로 배열로 변환을 해야했다.
 이 때, Rest Parameter은 반드시 마지막 Parameter이어야 한다.
 * Parameter의 최대 갯수는 255개이다.
 * Rest Parameter 앞에 ...은 Spread Operator이다. 즉, Rest Parameter은 Spread연산을 한 Parameter이다.
 
## 배열에서 사용하는 경우
 
 ### concat
 ``` javascript

 // ES5
 var arr = [1,2,3];
 console.log(arr.concat[4,5,6])); // [1,2,3,4,5,6]

 // ES6

 const arr = [1,2,3];
 console.log([...arr, 4, 5, 6]); // [1,2,3,4,5,6]

 ```
 ### push
 ``` javascript

 // ES5
 var arr1 = [1, 2, 3];
var arr2 = [4, 5, 6];

// apply 메소드의 2번째 인자는 배열. 이것은 개별 인자로 push 메소드에 전달된다.
Array.prototype.push.apply(arr1, arr2);

console.log(arr1); // [ 1, 2, 3, 4, 5, 6 ]

```
 * Spread Oprator은 가독성이 좋지만 Performance가 좋지않다.(concat > push > ...) 그러니까 1000개 정도 되는 배열은 concat을 쓰자...
 * Attribute에서 요소를 가져오면 무조건 string형으로 가져온다

## Enhanced Object Property
 
 ### Property 축약 표현
 ES6에서는 Property 값으로 변수를 사용하는 경우, Property 이름을 생략할 수 있다. 이 때, Property 이름은 변수의 이름으로 자동 생성된다.

 

## Destructuring
 Destructuring은 기존에 구조로 가지고 있던 객체를 개별적인 변수에 할당하는 것이다. 배열 또는 객체 리터럴에서 필요한 값만을 추출하여 변수에 할당하거나 반환할 때 유용하다.

 ### Array destructuring
 ``` javascript
 const arr = [1,2,3];
 const [one, tow, three] = arr;
 console.log(one, two, three); // 1 2 3
 ```
 위와 같이 사용한다.
 
 ### Object destructuring
 ``` javascript
 const obj = { firstName: 'Ungmo', lastName: 'Lee' };
 const { firstName, lastName } = obj;
 console.log(firstName, lastName); // Ungmo Lee
 ```


## Class
 
 ES6에 도입된 Class는 사실 Function이다.
 
 ``` javascript
 // ES5로 구현한 클래스
 var Person = (function() {
     
     // Constructor의 역할을 하는 함수 생성
     function Person(name) {
         this._name = name;
     }

     // Method
     function sayHi() {
         console.log('Hi' + this._name);
     }

     return Person; // 내부에 선언된 Person함수를 리턴한다.
 }())// 즉시 실행 함수(외부함수)를 호출한다.
 
 var user1 = new Person('Json'); // Instance 생성
 user1.sayHi(); // 'Hi Json'
 ```

 위 코드는 변수 Person에 함수 Person을 할당하고, 이를 즉시 실행 함수(외부함수)에서 리턴하는 구조이다.
 즉, ES6에서 말하는 Class란 사실 즉시 실행 함수로 Instance를 생성할 함수를 감싸고, 해당 함수를 리턴해주는 '함수'이다.
 
 ### constructor
 constructor는 인스턴트를 생성하고 초기화하기 위한 Method이다.
 Class 내에 한 개만 존재할 수 있으며, 2개 이상의 constructor을 포함하면 SyntaxError가 발생하게된다.
 
 
 ### 멤버변수
 멤버변수는 Property를 의미하는데, Property의 값으로 data만 올 수 있다.(객체 리터럴에서 Property value는 undefined를 제외한 모든것을 쓸 수 있다.) 즉, Method를 제외한 모든것을 값으로 쓸 수 있다.
 멤버변수는 constructor() {} 내부에서만 쓸 수 있다.(멤버변수는 this를 앞에 붙인 변수이다.)

 ### getter & setter
 멤버 변수에 접근하기 위한 연산자이다.
 getter는 멤버변수를 참좋하여 값을 반환해야하므로 return이 있어야하고, setter는 멤버변수를 참조하여 값을 써야하므로 return이 없어야 한다. 또한 setter는 parameter을 가져야한다.

 ### static Method
 정적메소드는 new 연산자를 통한 인스턴스화 없이 실행 가능하다.
 일반 메소드(프로토타입)는 반드시 new를 통해 인스턴스화 한 후 호출이 가능하다.
 ``` javascript

 class Foo {
     constructor (prop) {
         this.prop = prop;
     }
     static staticMethod() {
         return 'staticMethod';
     }
     prototypeMethod() {
         return 'prototypeMethod';
     }
 }
 
 const foo = new Foo(123);

 console.log(Foo.staticMethod());
 console.log(foo.staticmethod()); // Type Error

 ```
 ES5에서 Staitc Method는 Object.creator() Method이다.

 ### Class의 상속
 class의 상속은 extends 명령으로 이루어진다.

 ### Super keyword
 부모 클래스의 constructor를 사용하겠다는 키워드로, 자식클래스의 선두에 사용하는것이 좋다.(부모클래스를 한번 호출하면 super키워드 없이도 부모클래스의 속성값을 이용할 수 있다. 이를 single-turn pattern이라 한다.)
 

 