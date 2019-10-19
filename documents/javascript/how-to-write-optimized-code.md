# How to Wrtie Optimized Code in Javascript

### 1. Optimized Code를 위해 피해야 할 Javascript 문법

> 참고문서 : [Optimization killers](https://github.com/petkaantonov/bluebird/wiki/Optimization-killers#3-managing-arguments)

- `eval()`
- `arguments`
- `for in`
- `with`
- `delete`
- `Hidden class`
- `Inline Caching`

### 2. Inline caching

```js 
function finduser(user) {
  return `found ${user.firstName} ${user.lastName}`;
}

const userData = {
  firstName: 'Johnson',
  lastName: 'Junior'
};

findUser(userData);
```

만약에 `findUser(userData)` function을 반복해서 부른다면 해당 function은 `Inline caching` 을 통해 `found Johnson Junior`로 대체 될 수 있다.

### 3. Hidden Class

```js 
function animal(x, y) {
	this.x = x;
  this.y = y;
}

const obj1 = new Animal(1, 2);
const obj2 = new Animal(3, 4);

obj1.a = 30;
obj1.b = 100;
obj2.b = 30;
obj2.a = 100;
```

- 위와 같이 obj2 에 값을 대입할때 obj1과 순서를 달리하면 같은 hidden class를 공유하지 않기 때문에 성능이 느려질 것이다. 이럴 경우 다음과 같이 두가지 옵션이 존재한다.
  - `constructor` 를 사용하여 값을 대입
  - 값을 대입하는  `순서` 를 똑같이 한다.

> 참고 문서 : [Javascript Hidden Classes and Inline Caching in V8](https://richardartoul.github.io/jekyll/update/2015/04/26/hidden-classes.html)

