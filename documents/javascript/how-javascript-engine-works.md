# Javascript Engine 작동방법



### 1. Javascript Engine이 필요한 이유

![javascript engine](https://raw.githubusercontent.com/Mia-jeong/TodayILearned/master/img/javascript/javascript-engine.png)

위의 그림과 같이 자바스크립트 파일을 컴퓨터에 전달 하면 컴퓨터는 0,1만을 해석하기 때문에 파일이 작동 하지 않는다. 그렇기 때문에 우리는 javascript 엔진을 통해 JS파일을 컴퓨터가 이해할 수 있도록 바꿔주어야 한다.



### 2. Javascript Engine 역할

![how javascript engine works](https://raw.githubusercontent.com/Mia-jeong/TodayILearned/master/img/javascript/javascript-engine-works.png)

1) `lexical analysis`: 우선 자바스크립트 엔진은 javascript keyword에 기반하여 해당 코드를 토큰으로 분해한다. 이후 해당 토큰이 무슨 동작을 실행시키려 하는지 파악한다. 이렇게 분해된 토큰을 `AST(Abstract Syntax Tree)` 라고 부른다.

> AST 를 직접 확인 할 수 있는 사이트 > [AST explorer](https://astexplorer.net/)

2) `Interpreter` : `AST` 를 전달 받고 `Bytecode` 를 추출 한다. 이후 Javascript engine은 해당 Bytecode를 해석하고 동작하게 만든다. 

3) `Profiler` : 일종의 `Monitor` 역할을 한다. 어떻게 코드를 `Optimization` 시킬까 지켜보는 역할을 수행한다. 만약에 `Optimization` 이 될 수 있는 코드를 발견하면 해당 코드는 `Compiler` 로 전달 된다.

4) `Compiler`: 컴파일러(`JIT Compiler`)는 애플리케이션이 작동되는것과 동시에 코드를 해석하여 `Bytecode` 를  `Optimized Code` 의 `Machine code`로 변형 한다.

### 3. Interpreter vs Compiler

1) `Interpreter`: 코드를 한줄 씩 일고 해석하여 bytecode로 변환 한 후 실행 Javascript는 Interpreter을 사용하여 코드를 해석하고 실행

2) `Compiler` : compiler는 코드 전체를 한번에 읽은 후 machine code로 변환 시킨다. 해당 코드는 CPU로 전달 되어 실행 된다. 컴파일러는 처음에 전체 코드를 읽어야하기 때문에 시작하기에 오래걸릴 수 있지만 반복되는 코드를 단순화 시켜(`Optimization`) 결국 인터프리터보다 더 빠르게 실행 될 수 있다.

3) `JIT Compiler(Just In Time Compiler)`: `Interpreter` 과 `Compiler` 을 합친 것