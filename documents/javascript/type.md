

# Javscript Type

### 1. Javascript Type 종류

| Type      | Example      | Type of   | Category            |
| --------- | ------------ | --------- | ------------------- |
| Number    | 5            | number    | primitive type      |
| Boolean   | true, false  | boolean   | primitive type      |
| String    | 'Hi, there'  | string    | primitive type      |
| undefined | undefined    | undefined | primitive type      |
| null      | null         | object    | primitive type      |
| Symbol    | Symbol('hi') | symbol    | primitive type      |
| Object    | {}           | object    | none primitive type |
| Array     | []           | object    | none primitive type |
| Function  | function(){} | function  | none primitive type |

- undefined 는 정의되지 않았다는 의미이며 null은 값이 없다는 의미이다.

- array와 function은 object안에 속한다.

- Primitive type : 

  - 데이터가 메모리속에 오직 하나의 값만 나타낸다. 

  - `immutable` 하다 그렇기 때문에 var a = 5; 의 데이터에서 a = 7; 을 대입하고 싶다면 5를 메모리에서 아예 지우고 7를 대입시켜야한다.

  - `pass by value` : primitive 데이터 값은 다음과 같이 값이 전달 되기때문에 b++를 해도 기존의 a의 값이 변하지 않는다. 

    ```js 
    var a = 5;
    var b = a;
    
    b++;
    console.log(a); // 5
    console.log(b); // 6 
    ```

- None Primitive type: 

  - 메모리속에 해당 데이터의 pointer 주소가 저장되어 있다.

  - `pass by reference` : 해당데이터가 저장되어있는 주소의 참조값을 전달 하여 아래와 같이 obj2.password를 수정하면 원본데이터인 obj1.password 도 수정 된다.

    ```js
    let obj1 = {name: 'bam', password: '123'};
    let obj2 = obj1;
    
    obj2.password = 'abc123';
    
    console.log(obj1.password); //abc123
    console.log(obj2.password); //abc123
    ```

  - array clone 방법

    ```js 
    let a = [1, 2, 3];
    let b = [].concat(a);
    
    if(a === b) {
      console.log('fail');
    }else{
      console.log('success');
    }
    
    //success
    ```

  - object clone방법

    **shallow clone**

    ```js 
    let a = {a: 1, b: 2, c: 3};
    //shallow clone
    let b = Object.assign({}, a);
    let c = {...obj};
    if(a === b) {
      console.log('fail');
    }else{
      console.log('success');
    }
    
    if(a === c) {
      console.log('fail');
    }else{
      console.log('success');
    }
    
    //success
    //success
    ```

    **deep clone**

    ```js 
    let a = {a: 1, b: 2, c: {another: 'hehe'}};
    let clone = JSON.parse(JSON.stringify(a));
    
    clone.c.another = 'hohoho';
    console.log(clone.c.another); //hohoho
    console.log(a.c.another); //hehe
    
    ```



### 2. Tricky Example

```js 
const number = 100
const string = "Jay"
let obj1 = {
  value: "a"
}
let obj2 = {
  value: "b"
}
let obj3 = obj2;
 
function change(number, string, obj1, obj2) {
    number = number * 10;
    string = "Pete";
    obj1 = obj2;
    obj2.value = "c";
}
 
change(number, string, obj1, obj2);

console.log(number); 	// 10
console.log(string);		// Jay
console.log(obj1.value); // a
```

아마 `obj1.value` 값이 `c` 라고 생각 할 수도 있을 것이다 하지만 function change안의 obj1 은 `function scope`  에 있는 변수이다. 물론 obj1과 같은 값을 참조 하지만 다른 변수이다. 그렇기 때문에 function 내의 obj1 은 이제 obj2의 값을 참조하지만 `global` 에 있는 obj1은 변하지 않고 똑같은 값을 참조 하는 것이다. 

> [Javascript Built int Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects)



### 3.  Javascript Type Coercion(타입변환)

```js 
1 == '1'
```

위와 같은 코드를 javascript 에서 비교하면 `true` 가 나올 것이다. 바로 `Type Coercion` 덕분이다. `Type Coersion` 은 위의 코드와 같이 `==` 로 비교 할때 한쪽의 type을 다른 한쪽과 일치시키도록 변환시키는 것을 말한다.

```js 
false == ""   // true
false == []  //true
false == {}  // false
"" == 0      //true
"" == []     //true
"" == {}     //false
0 == []      //true
0 == {}      //false
0 == null  	//false
```



하지만 값을 비교할 경우 `===` 를 사용하는 것이 가장 좋다.

> 1.[JS Comparision Table](https://dorey.github.io/JavaScript-Equality-Table/)
>
> 2.[Equality comparisons and sameness](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Equality_comparisons_and_sameness)
>
> 3.[Equality comparisons and sameness