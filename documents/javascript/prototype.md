# Prototype

### 1. `__proto__`

`__proto__` 란 object 의 상위 object를 의미한다.

아래의 코드를 살펴보자.

```js 
let dragon = {
  name: 'Tanya',
  fire: true,
  fight() {
    return 5
  },
  sing() {
    if (this.fire) {
      return `I am ${this.name}, the breather of fire`
    }
  }
}

let lizard = {
  name: 'Kiki',
  fight() {
    return 1
  }
}

lizard.__proto__ = dragon;
dragon.isPrototypeOf(lizard); //dragon은 lizard의 prototype이다.
console.log(lizard.fire)
console.log(lizard.sing())
```

위의 코드를 살펴보면 `lizard` 에는 `fire과 sing()` 이 없다. 하지만 `lizard.__proto__ = dragon` 으로 dragon properties들을 상속받았기 때문에 이후 `lizard` 에서 `fire 과 sing()` 을 사용할 수 있는 것이다. 하지만 직접적으로 `__proto__` 에 다른 object를 대입하는 것은 performance적으로 좋지 않기 때문에 지양 해야한다. 대신 `Object.create()` 사용하자.

```js 
var lizard = Object.create(dragon);
```



(참고) hasOwnProperty

아래와 같은 코드를 살펴보자

```js 
for( var param in lizard){
	console.log(param);
}
```

위의 코드를 실행시키면 name, fight뿐만 아니라 fire과 sing까지 param 값으로 출력 될 것이다. 하지만 아래와 같이 hasOwnProperty를 사용하면 lizard 내에 선언된 param들(name, fight) 만 출력 될 것이다.

```js 
for(  var param in lizard){
	if(lizard.hasOwnProperty(param)){
		console.log(param);
	}
}
```

### 2. `__proto__` 는 상속받는 `Object` 의 `prototype` 을 가리킨다.

```js 
function abc(){
	console.log('abc');
}

abc.__proto__;
//ƒ () { [native code] }
Function.prototype
//ƒ () { [native code] }

if(abc.__proto__ === Function.prototype){
	console.log('yes');
}

//yes
```

function abc의 `__proto__` 즉 상위 object는 `Function.prototype`이다 그렇기 때문에 `yes` 가 출력 되는 것이다.

앞서 말했듯이 Array와 Function은 모두 Object를 상속 받는다 그렇기 때문에 다음과 같은 코드도 `yes` 가 출력되는 것을 확인할 수 있다.

```js 
if(Array.__proto__.__proto__ === Object.prototype) {

	console.log('yes');
}
//yes

if(Function.__proto__.__proto__ === Object.prototype) {

	console.log('yes');
}
```

(참고) function 만 `prototype` 을 가질 수 있다.

```js 
typeof Object 
//function

Object.prototype // Object
{}.prototype // error
```

### 3. 예제

**예제1** : Date함수에 lastYear을 추가하여라

```js 
Date.prototype.lastYear = function() {
  return this.getFullYear() - 1;
}
```

**예제2** : map 함수를 재정의 해보자.

```js 
Array.prototype.map = function(){
   arr = [];
  for (let i = 0; i < this.length; i++) {
    arr.push((this[i]+'😊'));
  }
  return arr;
}
```

**예제3** : call 혹은 apply함수를 사용하여 bind를 재정의 해보자.

```js 
Function.prototype.bind = function(newThis){
  const self = this;
  return function(){
    return.self.apply(newThis, arguments);
  }
}
```



