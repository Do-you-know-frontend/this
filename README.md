# 자바스크립트의 this 

1. this가 뭐야?
* 자신이 속한 객체 또는 자신이 생성할 인스턴스를 가리키는 자기 참조 변수 
* 키워드로 분류되나 식별자 역할을 함 

2. 왜 필요해? 
* 일반 객체
: 객체는 상태를 나타내는 프로퍼티와 상태를 참조 및 변경 가능한 메서드로 이루어진 자료 구조
-> 메서드가 속한 객체의 상태를 참조, 변경하려면 해당 객체를 가리키는 식별자를 참조해야 함 
-> 그 역할을 this가 함! 
* 생성자 함수로 만들어진 객체 
: 생성자 함수 내부에서 프로퍼티, 메서드를 추가하려면 자신이 생성할 인스턴스를 참조해야 함 
-> 생성자 함수 정의 시점에는 인스턴스를 가리키는 식별자를 모름 
-> 이를 가리킬 특수한 식별자 this가 필요함! 

3. 문맥에서의 this
* 브라우저에서의 this: window 객체 (=globalThis)
* 일반 함수 내부에서의 this: window 객체 (=globalThis) / 'use strict'일 경우 undefined
* 생성자 함수, 클래에서의 this: 생성될 인스턴스 자체 

4. this 바인딩
* 바인딩: 식별자와 값을 연결하는 과정 
 (cf. 변수 선언: 변수 이름인 식별자와 확보된 메모리 공간의 주소를 바인딩하는 것)
* this바인딩은 this 식별자와 this가 가리킬 객체를 연결하는 것 

5. 동적 바인딩
* 자바 같은 다른 객체 지향 프로그래밍 언어에서 this는 항상 자신의 인슨턴스 자체를 가리킴 (변경 X)
* 자바스크립트는 호출자(caller)에 따라 this가 가리키는 것이 달라짐 = 동적으로 결정됨

```jsx
const obj = {
  bar: 'bar',
  foo() {
  console.log(`출력, ${this.bar}`)
 }
}

function print(callback) {
 callback(); 
}

print(obj.foo);

// undefined
```
* 특정 객체의 this를 참조하는 메서드를 콜백으로 전달했을 시, this 정보를 잃고 undefined 출력됨
* 이처럼 자바스크립트는 호출자에 따라 this가 변경, 사라짐 

6. 정적 바인딩 
1) bind로 수동 바인딩
```jsx
function foo(name){
...
this.print = this.print.bind(this)
...
} 
```
2) 화살표 함수 사용
* 화살표 함수는 생성되는 순간 화살표 함수 밖에서 제일 근접한 스코프의 this를 가리키고 기억함 
```jsx
function foo(name){
...
this.print = () => {
  console.log(`출력, ${this.bar}`)
}
...
} 
```


