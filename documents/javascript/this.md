# this

### 1. this 란?

> `this` is a object that the function is a property of

즉 해당 function이 property로 속해있는 object를 `this` 라고 의미한다.

```js 
const obj = {
  name: 'bam'.
  sing() {
  	return 'mung mung ~ ' + this.name; 
	},
  singAgain(){
  	return this.sing()+'!';  
  }
};

obj.sing();
```

위의 코드에서 sing 의 this는 obj이다 왜냐하면 sing은  obj 속해 있기 때문이다. `this` 는 해당 함수에대해 자신이 속해있는 object에 접근 할 수 있게 해준다.

```js 
function person() {
  console.log(this.name);
}

var name = 'bam';
const obj1 = {
  name: 'mung',
  person: person
};

const obj2 = {
  name: 'mong',
  person: person
};

person();			//bam
obj1.person();	//mung
obj2.person();	//mong
```

위와 같이 `this` 는 같은 코드를 상황에 알맞게 여러번 사용할 수 있게 해준다.

다음과 같은 코드의 this를 맞춰 보아라.

```js 
const a = function() {
  console.log('a ', this);
  const b = function() {
    console.log('b ', this);
    const c = {
      hi: function() {
        	console.log('c ', this);
      }
    }
    c.hi();
  }
	b();
}
a();
```

- a : global(==window)
- b: global(==window)
- c.hi = c

아마 a, c 는 이해가 가지만 b가 이해가 가지 않을 수 있다. b를 자세히 살펴보면 a()가 실행되고 나서 그 다음 실행 되는 함수이다. 하지만 해당 b는 a의 property에는 속하지 않기 때문에 global에 속한다. 즉 this는 어떻게 function 이 invoke되는지에 따라 정해진다. 

아래의 코드를 또 살펴보자.

```js 
const obj = {
  name : 'bam',
  barking() {
    console.log('a ', this);
    var func = function(){
      console.log('b', this);
    }
    func();
  }
}

obj.barking();
```

위와 같이 함수를 작성하고 실행 시키면 다음과 같은 결과가 나올 것이다.

- obj.sing: this === obj;
- func : this === window;

즉 func는 window(global) 에 의해 호출되고 실행 된다.

만약 `arrow function` 을 사용하면 어떻게 될까?

```js 
const obj = {
  name : 'bam',
  barking() {
    console.log('a ', this);
    var func = () => {
      console.log('b', this);
    }
    func();
  }
}

obj.barking();
```

위와 같이 `arrow function` 으로 바꾸면 lexically binding을 하기 때문에 둘다 this === obj 로 설정 된다.
(참고)
`arrow function`은 `scope`을 생성하지 않는다, 따라서 this를 바인딩 하지 않음.

```js 
const obj = {
  name : 'bam',
  self: this, // window
  barking: () => {
    console.log(this) //window  
  },
  barking2() {
    var func = () => {
      console.log('b', this); //obj barking2()의 scope에대한 this가 obj이기 때문에 arrow function은 새로 scope을 생성하지 않아 this를 바인딩하지 않으므로 barking2의 this를 따라간다.
    }
    func();   
  }    
}

obj.barking();
```

### 2. self 사용법

```js 
const obj = {
  name : 'bam',
  barking() {
    console.log('a ', this);
    var self = this;
    var func = function(){
      console.log('b', self);
    }
    func();
  }
}

obj.barking();
```

위와 같이 self를 생성하여 this를 대입시키면 func내에서도 self를 통해 this == obj를 접근 할 수 있다.

### 3. call(), apply()

call 과 apply는  함수를 invoke하는데 사용하는 함수이다.

```js 
function a(){
  console.log('hello~');
}

a.call();
a();
```

위와 같이 모든 함수를 실행시킬때 a() 이런식으로 부르면 안에서 call() 함수를 부른다. 즉 a()는 a.call() 를 줄인 버전이다.

call은 다음과 같이 다른 object에 있는 함수를 빌리는데 사용 할 수 있다.

```java 
const instrument = {
  name: 'piano',
 	volume: 40,
  up(){
    return this.volume = 100;
  }
};

const device = {
  name: 'radio',
  volume: 20
};

console.log('before', device);
instrument.up.call(device);
console.log('after', device);
///////return ///////
before {name: "radio", volume: 20}
after {name: "radio", volume: 100}
```

위와 같이 call 함수에 device를 this로 넣어주면 instrument에 있는 up 함수를 빌려서 사용할 수 있다.

call함수는 this말고 또다른 인자값을 받을 수 있다.

```js 
const instrument = {
  name: 'piano',
 	volume: 40,
  up(num1, num2){
    return this.volume += num1+num2;
  }
};

const device = {
  name: 'radio',
  volume: 20
};

console.log('before', device);
instrument.up.call(device, 12, 19);
console.log('after', device);
///////return ///////
before {name: "radio", volume: 20}
after {name: "radio", volume: 51}
```

`apply` 는 인자값을 `Array`로 받는 다는 사실 빼고는 call과 동일하다.

```js 
console.log('before', device);
instrument.up.apply(device, [12, 19]);
console.log('after', device);
///////return ///////
before {name: "radio", volume: 20}
after {name: "radio", volume: 51}
```

(문제)

```js 
const array = [1,2,3];
 
function getMaxNumber(arr){
  return Math.max(arr);
}
 
getMaxNumber(array); // NaN
```

위와 같은 코드를 실행하면 `NaN` 이 실행 될것이다. 왜냐하면 Math.max에서 `this` 는 global object를 바라보는데 global 에는 `arr` 변수명을 가진 데이터가 존재하지 않기 때문이다. 그렇기 때문에 아래와 같이 apply로 Match.max함수를 빌려 this를 null 시켜주면 원하는 값인 `3` 이 나올 것이다.

```js 
const array = [1,2,3];
 
function getMaxNumber(arr){
  return Math.max.apply(null, arr);
}
 
getMaxNumber(array); // 3
```



### 4. bind()

```js 
console.log('before', device);
instrument.up.bind(device, 12, 19);
console.log('after', device);
///////return ///////
before {name: "radio", volume: 20}
after {name: "radio", volume: 20}
```

위의 코드와 같이 bind를 넣을 경우 volume값이 변하지 않는 것을 확인 할 수 있다. bind는 해당 조건을 가진 새로운 function을 return 한다 그렇기 때문에 다음과 같이 코드를 변경하면 값이 적용 되는 것을 확인 할 수 있다.

```js 
console.log('before', device);
const upFunc = instrument.up.bind(device, 12, 19);
upFunc();
console.log('after', device);
///////return ///////
before {name: "radio", volume: 20}
after {name: "radio", volume: 51}
```

**function curring**

```js 
function multiply(a, b){
  return a * b;
}

let multiplyByTwo = multiply.bind(this, 2);
console.log(multiplyByTwo(4)); // 8
let multiplyByTen = multiply.bind(this, 10);
console.log(multiplyByTen(4)); // 40
```



### 5.Tricky Example

```js 
var b = {
  name: 'jay',
  say() {console.log(this)} // this === b
}

var c = {
  name: 'jay',
  say() {return function() {console.log(this)}}  //this === window
}

var d = {
  name: 'jay',
  say() {return () => console.log(this)} // this === d
}
```

