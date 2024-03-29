# NormadCoder_React

- prop-types -> type checking

ReactJS: 어플리케이션이 interactive하게 만들어주는 라이브러리.  
ReactDOM: 모든 react element들을 HTML body에 둘 수 있도록 해줌.  
ReactDOM.render():
render의 의미 [React element를 가지고 HTML로 만들어서 배치한다는 뜻 -> show it to the user]

---

### 2.2 강의내용정리

```
<!-- This html is for practice ReactJS again -->

<!DOCTYPE html>
<html>
    <body>
        <div id="root"></div>
    </body>
    <script src="https://unpkg.com/react@17.0.2/umd/react.development.js"></script>
    <script src ="https://unpkg.com/react-dom@17.0.2/umd/react-dom.production.min.js"></script>
    <script>
        const root= document.getElementById("root");
        const span= React.createElement(
            "span",
            {id:"spanspan",style:{color:"red"}},
            "Hi I'm a span"
        );
        ReactDOM.render(span,root);
</script>
    </html>
```

위 코드는, 단지 빨간 span을 페이지에 두는 데 코드가 많다고 느낄 수 있다.  
즉 :
root를 생성하고, 두 가지를 import하고, root를 가져오고, element를 생성하고, element를 render해야한다.

`React.createElement("span",{span의 property}, "span의 내용")` 과 같이 작성한다. ->이때 property는 class name,id,style 가능

\* 바닐라JS : HTML ->JS 의 순서  
\* 리액트 : JS->HTML 의 순서

---

### 2.3 강의내용 정리

```
Warning: Each child in a list should have a unique "key" prop.
```

위와 같은 경고가 발생했는데, import한 패키지를 development에서 production.min.js로 변경하니 해결됨.

### 2.4 Recap: 강의내용정리

요약:  
이전까지는 React JS와 ReactDOM을 먼저 import하고 이후 createElement를 통해 코드를 작성하였다. props 안에서 event listener을 등록할 수 있다. 예를들어 on으로 시작하는 event를 작성하면 React JS가 event listener임을 알아챈다.

### 2.5 JSX 강의내용정리

목표:  
createElement를 대체하고자 한다(by JSX:JavaScript를 확장한 문법, HTML과 유사).  
예시:

```
const h3= React.createElement(
            "h3",
            {
                onMouseEnter: () => console.log("mouse enter!"),
            },
            "Hi I'm a span"
            );
```

를 JSX로 바꾸면 다음과 같다.

```
const Title = ( <h3 id="title onMouseEnter={() => console.log("mouse enter")}> Hello I'm a Title</h3>);
```

```
const btn = React.createElement(
    "button",
    {
        onClick: () => console.log("I'm cliked"),
    },
    "Click me"
);
```

위 코드 또한 아래와 같이 바꾸어 작성할 수 있다.

```
 const Button = <button style ={{backgroundColor:"tomato"}} onClick ={()=> console.log("I'm clicked")}>Click me</button>
```

-> JSX는 html문법과 유사하게 태그를 열고 닫으며, 내용은 그 사이에 담고 props는 태그를 연 이후 작성해주면 된다.(createElement가 불필요!)

그대신, 브라우저가 JSX를 이해할 수 있도록 `Babel`이라는 도구를 설치해야 한다. 더불어 Babel을 적용하기 위해 type을 text/babel로 작성해주어야 한다.

### 2.6 JSX part 2

- ()=> : arrow function

```jsx
function Title() {
    return (
        <h3 id="title" onMouseEnter{() => console.log("mouse enter")}>
        Hello I'm a span
        </h3>
    );
}
```

와 아래 코드는 동일하다.

```jsx
const Title = () => (
    <h3 id="title" onMouseEnter{() => console.log("mouse enter")}>
        Hello I'm a span
    </h3>
)
```

이러한 함수들을 일반적인 HTML태그인 것처럼 포함시켜주려면,  
<함수명 /> 와 같이 작성한다.  
예시: `const Contatiner = ( <div> <Title /> <Button /> </div>);`

- html 요소 : 소문자로 작성 `<button>`
- 직접만든 요소 : 대문자로 작성 `<Button />`

즉, JSX문법을 통해 각각의 요소를 만들고(함수를 작성) 한꺼번에 이들을 rendering 해주면 된다.

### 3.0 Understanding State

React.Js는 UI에서 바뀐부분만 update해준다.(반면 바닐라JS는 바뀐부분을 담고 있는 내용도 함께 update됨)  
index2.html에 작성한 코드와 같이 counterUp을 해줄 때 마다 렌더링을 통해 카운터를 작동시키는 방법을 배웠다.  
But, 이 방식은 매번 렌더링(리렌더링) 해주어야 하기 때문에 최고의 방법이 아니다.

- 변경된 부분만 update 해주는 것에 대한 장점 :[사이트 이동](https://nomadcoders.co/react-for-beginners/lectures/3265)
  > 일반 JS를 쓴 브라우저는 노드정보가 바뀔 때마다 노드트리를 5계에 걸쳐 처음부터 생성하. but 리액트는 가상돔을 사용하여 우리 시야에 보이는 부분만 수정하여 보여주고, 모든 update가 끝나면 일괄로 합쳐서 실제 돔에 던져줌. -> 면접 때 많이 물어봄! 브라우저 작동원리와 연관 O

### 3.1 setState part one

매번 렌더링을 해주는 일을 기억해야하는 번거로움이 있기 때문에, 자동으로 리렌더링을 일으킬 수 있는 방법에 대해 배웠다.

> useState

```
const data = React.useState();
console.log(data);
```

라고 작성하여 console에 찍히는 내용을 보면, `[undefined, f]` 라고 출력된다.  
여기서 undefined는 우리가 담을 data를, f는 data 값을 바꿀 때 사용할 modifier를 의미한다.

예를들어,  
`const food = ["apple", "banana"];` 와 같이 작성하면 ` const food1 = food[0];` 과 ` const food2 = food[1];` 과 같이 작성을 해주어 배열 안에 담긴 요소에 접근할 수 있는데.  
이를 좀 더 편리하게 사용하기 위해서는 다음과 같이 작성하면 된다.  
`const [food1, food2] = food ;` 이때 food에는 apple과 banana가 담겨있는 상태이다.

### 3.2 setState part two

```js
const [counter, modifier] = React.useState(0);
const onClick = () => {
  modifier(23984);
  // counter = 23984;
  // ReactDOM.render(<App />,root);
};
```

위의 코드에서 modifier 함수는 counter을 설정한 수로 바꾸로, 자동으로 렌더링을 해준다.

- 참고로 modifier의 이름은 set~ 으로 지어주는 것이 general 하다.

### 3.3 Recap

React.Js는 데이터가 바뀔 때마다 컴포넌트를 리렌더링 하고 UI를 리렌더링한다. 즉, usteState()에서 modifier 함수로 state를 바꿀 때 컴포넌트 전체가 재생성된다(with new value).

``const [counter, modifier] = React.useState(0)` 에서 counter의 초기값이 0으로 설정되어 있는 이유는, useState(0)과 같이 설정해주었기 때문이다.

### 3.4 State Function

state를 변경해주는 방법에는 크게 두 가지가 존재한다.

첫째. modifier을 통해 직접 값을 설정해주는 방법 (ex. setCounter(999))  
둘째. 이전 값(state)를 통해 현재 값(state)을 계산해주는 방법 (ex. setCounter(counter+1))  
But, 이전 값을 통해 현재 값을 구하고 싶다면 setCounter 함수 내부에 `counter +1`보다 `(current)=> current + 1`과 같이 작성해주는 것이 더욱 안전한 방법이다.

- 어떠한 부분에서 더욱 안전하다는 것인지 잘 모르겠따..  
  아직 current + 1과 current => current + 1의 차이를 잘 이해하지 못함.

### 3.5 Input and State

for -> JavaScript용어이다.  
JSX는 HTML문법과 유사하나, label과 input을 연결해주기 위해서 for과 id를 작성해주면 안된다.  
이 경우, production.min.js 를 import한 경우 오류가 뜨지 않지만 development.js로 import하여 사용하는 경우에는 오류가 발생한다.  
**-> 따라서 for은 htmlFor로, class는 className으로 사용해주어야 한다.**

해당 강의 comment란에 따르면,

> react,reactdom을 import하는 script tag에서 production -> development로 변경하는데 production는 배포 모드이고 development는 개발모드를 의미한다.  
> 개발모드는 버그로 이어질 수 있는 요소들을 미리 경고하고 검증하는 코드가 포함되어 있다.

라고 되어있음을 확인할 수 있다.

- input 태그 안에서 사용자가 입력하는 value의 값을 모르기 때문에, 이 값을 uncontrolled 라고 한다.  
  따라서, state를 만들어주는데 이 state를 통하여 input 태그 안에 value값을 설정 할 수 있다.  
  => value 값을 넣어주는 input이 존재하고, 그 값은 state가 된다.

```jsx
function App() {
  const [minutes, setMinutes] = React.useState();
  const onChange = (event) => {
    setMinutes(event.target.value);
  };
  return (
    <div>
      <h1 className="Hi">Super Converter</h1>
      <label htmlFor="minutes">Minutes</label>
      <input
        value={minutes}
        id="minutes"
        placeholder="Munutes"
        type="number"
        onChange={onChange}
      />
      <h4>U want to convert {minutes}</h4>
      <label htmlFor="hours">Hours</label>
      <input id="hours" placeholder="Hours" type="number" />
    </div>
  );
}
```

위 코드에서 onChange라는 event를 발생시키고자 onChange 함수를 생성하고 이를 input태그 안에 추가해주었다.  
onChange 함수 내에서는 setMinutes 라는 modifier을 가지고 input value값이 change될 때마다 modifier를 실행시킨다.

### 3.6 State Practice part One

\*참고: arrow function을 사용할 때, 한 줄로만 나타낼 수 있다면 {}를 생략할 수 있다. 함수 내용이 여러 줄일 경우에는 {}로 묶어주고, return되는 내용은 ()로 묶어서 나타낼 수 있다.

### 3.7 State Practice part Two

목표: [flip function 만들어보기]  
-> 한 가지 option을 선택하면, 다른 한 가지는 disable하게 만듦.  
Minutes input과 Hours input이 존재하는데, 두 input에 disabled속성을 주고 이 속성의 default 값에 따라 disable과 enable이 바뀐다.

- 삼항연산자를 통해 Minutes에서, ` value={flipped ? amount*60 : amount}` 라고 적어줌으로써 flipped(false)가 true이면 minutes입력란이 활성화 된 상태이므로 분을 입력 받는다.
- 반대로 Hours에서 ` value={flipped ? amount : Math.around(amount/60)}` 와 같이 적어줌으로써 flipped(false)가 true이면 Hours입력란이 활성화 된 상태이므로 시를 입력 받는다.
- flip 버튼을 누르면, 입력한 값이 그대로 가져와지므로 onFlip 함수에 reset()을 넣어주어 flip버튼이 클릭되었을 때 0으로 세팅되게 한다.

### 3.9 Final Practice and Recap

- select 태그 안에는 option을 가지고 있다.

예시)

```html
<select>
  <option>Minutes & Hours</option>
  <option>Km & Miles</option>
</select>
```

select는 html이므로 React JS를 사용할 필요가 없다.  
option이 바뀔 때 이 이벤트를 감지하기 위해서는 select태그 안에 event를 리스닝 해줘야 한다.

- {} 중괄호 안에는 JS를 작성할 수 있다.

```jsx
function KmToMiles() {
  const [amount, setAmount] = React.useState();
  const [inverted, setInverted] = React.useState(false);
  const onChange = (event) => {
    setAmount(event.target.value);
  };
  const reset = () => {
    setAmount(0);
  };
  const onInvert = () => {
    reset();
    setInverted((current) => !current);
  };

  return (
    <div>
      <div>
        <label htmlFor="km">Km </label>
        <input
          value={inverted ? amount / 1.609 : amount}
          id="km"
          placeholder="Km"
          type="number"
          onChange={onChange}
          disabled={inverted}
        />
      </div>
      <div>
        <label htmlFor="miles">Miles </label>
        <input
          value={inverted ? amount : amount * 1.609}
          id="miles"
          placeholder="Miles"
          type="number"
          onChange={onChange}
          disabled={!inverted}
        />
      </div>
      <button onClick={reset}>reset</button>
      <button onClick={onInvert}>{inverted ? "Turn Back" : "Invert"}</button>
    </div>
  );
}
```

다음과 같은 코드를 작성하여 Km<->Miles 변환기를 만들었다.  
이는 Minutes To Hours의 논리를 가지고 분리된 컴포넌트를 작성한 것이다.(분할 및 정복) -> index4.html 의 내용이다.

### 4.0 Props

목표: 부모 컴포넌트로부터 자식 컴포넌트로 데이터를 보내는 방법 연습 & 리액트 컴포넌트를 재사용하는 방법

따라서, 먼저 각각의 버튼마다 컴포넌트(함수,function)를 생성한다. ex) Save Chages 버튼과 Confirm 버튼이 존재하는데, 이 두 버튼이 text를 제외하고 모두 동일한 속성을 가질 때 같은 속성을 두 컴포넌트에 모두 적어주기보다, 한 가지의 컴포넌트만 만들어서 쓸 수 있다면 코드의 복잡성을 줄여줄 것이다.

```jsx
function SaveBtn() {
  return (
    <button
      style={{
        backgroundColor: "skyblue",
        color: "black",
        padding: "10px 20px",
        border: 0,
        borderRadius: 10,
      }}
    >
      Save Changes
    </button>
  );
}
function ConfirmBtn() {
  return (
    <button
      style={{
        backgroundColor: "darkgreen",
        color: "white",
        padding: "10px 20px",
        border: 0,
        borderRadius: 10,
      }}
    >
      Confirm
    </button>
  );
}
function App() {
  return (
    <div>
      <SaveBtn />
      <ConfirmBtn />
    </div>
  );
}
```

{props.xxx} 과 같이 작성하는 것 대신, 재사용하고자 하는 함수에 중괄호를 사용하여 {xxx} 로 받는다.

- 어떠한 prop이든 Btn컴포넌트에 보내게 되면, Btn 함수의 첫 번째 argument(인자) 속으로 들어간다.

```jsx
function Btn({ text, big }) {
  return (
    <button
      style={{
        backgroundColor: "skyblue",
        color: "black",
        padding: "10px 20px",
        border: 0,
        borderRadius: 10,
        fontSize: big ? 18 : 16,
      }}
    >
      {text}
    </button>
  );
}

function App() {
  return (
    <div>
      <Btn text="Save Changes" big={true} />
      <Btn text="Continue" big={false} />
    </div>
  );
}
```

### 4.1 Memo

- html요소 안에다가 onClick과 같은 evnt를 작성하면, 이는 EventListner이고 내 커스텀 컴포넌트에 작성하면 prop일 뿐이다.  
  즉, 내가 작성한 컴포넌트에 style을 적용하고 싶다면 prop을 가져와서 적용시켜야 한다.

- React.memo() :  
  컴포넌트가 React.memo()로 감싸져있을 때, 컴포넌트를 렌더링하고 그 결과를 memo한다. 다음 렌더링이 일어날 때 prop이 같으면 memo된 내용을 재사용한다.

### 4.2 Prop Types

- text에 숫자를 입력받거나, fontSize에 숫자가 아닌 text를 입력하는 등(잘못된 타입을 받는 경우) 이를 교정하기 위해 PropTypes패키지를 사용한다.  
   [PropTypes] : 어떤 type의 prop을 받고 있는지 check 해줌.
  ->따리사, 최소한의 경고를 받을 수 있다.

```
    Btn.propTypes = {
      text: PropTypes.string.isRequired, // isRequired를 통해 필수로 입력해야함을 알 수 있음.
      fontSize: PropTypes.number,
    };
```

다음과 같이 작성하여 prop type을 지정해줄 수 있다.  
(이때 PropTypes 에서 대문자,s붙이는 것에 유의하자)

### 4.3 Recap

-컴포넌트의 prop에 접근할 수 있는 방법은, 컴포넌트 함수의 첫 번째 인자 안에서 가능하다. (전달된 prop을 하나의 오브젝트로서 받는다->중괄호 안에 prop을 적어줌. 그냥 괄호 안에 props를 적어주고 중괄호에는 props.text , props.fontSize ...하는 것과 동일한 방법임)

### 5.0 & 5.1

css 파일을 작성 한 후 index.js에 import하게 되면 모든 속성에 css가 적용된다. style prop을 이용하면 이러한 문제(global한 css)를 해결할 수 있으나 이러한 방식은 사용하지 않을 것이다. 따라서, css파일을 작성하나 이를 모~든 부분에 import하지 않게 하기 위해서 .module.css 파일을 생성하고 이를 import하여 사용한다. => 여기서 스타일은 className or id로 import한 스타일 객체의 property를 전달하여 적용된다.

_react 컴파일 과정 중 random class or id가 생성되므로 .css 파일의 class or id 이름을 외울 필요가 없다_

### 6.1 useEffect

- useEffect -> 두 개의 argument를 가지는 function.  
  첫 번째 argument는 딱 한 번만 실행하고자 하는 코드 + 두 번째 argument는 []배열을 넣어줌  
  두 번째 argument에 []배열을 넣어주는 이유:  
  useEffect가 컴포넌트의 첫 번째 render 시점에 IRunOnlyOnce 함수를 호출 한 후, 상태를 변화 시키면 IRunOnlyOnce함수는 호출되지 않는다, 즉 한 번만 rendering된다.

  > memo : state가 변할 때 컴포넌트의 렌더링을 방지하기 위해 새로운 컴포넌트에 부여하는 속성  
  > useEffect : state가 변할 때 컴포넌트의 렌더링이 아닌, 코드의 재실행을 방지하기 위한 함수(argument)

  ### 6.2 Deps(언제 코드가 실행될지 결정하는 방법에 대해 알기)

problem: 내 코드의 특정한 부분만이 변화했을 때 렌더링 하고 싶다.  
solution: useEffect를 사용하여 control 해준다.

- useEffect의 두 번째 인자에서 react.js가 지켜볼 대상을 넣어주면 된다. ([] -> 아무것도 없기에 한 번만 실행됨. [keyword] -> keyword가 변화할 때 실행됨.)

```C
import { useState, useEffect } from "react";
import Button from "./Button";
import styles from "./App.module.css";

function App() {
  const [counter, setValue] = useState(0);
  const [keyword, setKeyword] = useState("");
  const onClick = () => setValue((prev) => prev + 1);
  const onChange = (event) => setKeyword(event.target.value);
  useEffect(() => {
    console.log("I run only once");
  }, []);
  useEffect(() => {
    console.log("I run when 'keyword' changes.. ");
  }, [keyword]);
  useEffect(() => {
    console.log("I run when 'counter' changes.. ");
  }, [counter]);
  useEffect(() => {
    console.log("I run when keyword&counter changes..");
  }, [keyword, counter]);
  return (
    <div>
      <input
        value={keyword}
        onChange={onChange}
        type="text"
        placeholder="Search here..."
      />
      <h1>{counter}</h1>
      <button onClick={onClick}>click me</button>
    </div>
  );
}
export default App;
```

정리: useEffect는 API를 매번 새로 호출하지 않고 한 번만 호출해준다(변화(update)감지도 가능)

### 6.3 Recap

💬 React.js를 사용하는 이유: 최소 단위의 redering을 위해  
💬 useState(): 변수와 변수를 제어하는 함수로 구성되며 변하는 값을 제어, 해당 부분의 리렌더링을 위함  
💬 props: 태그의 속성 값을 함수의 argument처럼 컴포넌트에 값을 전달해줌
💬 useEffect(): 코드의 실행 시점을 관리할 수 있는 선택권을 얻는 방어막 같은 존재. 디펜더시([]와 같은 두 번째 인자)가 없을 경우 최초 1회 실행하고 존재할 경우, 해당 값이 변할 때에 실행됨  
💬 부모컴포넌트에서 리렌더링이 일어날 경우 모든 자식들이 리렌더링 된다.(we can use memo)  
💬 propType을 설치하고 props의 타입을 지정해줄 수 있다.(isRequired로 필수값 지정 가능)

### 6.4 Cleanup

컴포넌트가 destroy될 때도 코드를 실행할 수 있는데, 이는 return 함수로 만들어주면 된다.  
useEffect는 함수를 받고, 이 함수는 dependency가 변화할 때 호출된다.
-> dependency가 비어있는 경우 컴포넌트가 처음 생성될 때 함수가 호출된 후 다시 호출되지 않는다. So 컴포넌트가 파괴될 때도 함수를 실행하고 싶다면 useEffect 함수가 새로운 함수를 return 하게 해야한다.

- deps가 비어있으면 자동으로 컴포넌트가 파괴될 때 cleanup함수가 실행되는데 그 과정이 리렌더링으로 useEffect함수가 실행되고 클린업하면서 이전에 있던 effect가 삭제- 새 effect 함수인 return함수가 실행
  > 즉, rerendering - 이전 effect cleanup - effect 실행

### 7.0 To Do List part One

- state를 직정 수정하지 않는다. 즉 modifier을 통하여 state를 변화시킬 뿐이다.

form은 submit 이벤트를 갖고 있다.
따라서, event.preventDefault()함수를 통해 기본 동작을 막아야 한다.

여러 개의 toDo를 받을 수 있는 배열 생성:  
const [toDos, setToDos] = useState([]); ->기본 값은 비어있는 배열이다.  
state는 직접적으로 수정이 불가능 하므로(ex. toDo="") 함수를 가져와서 수정하도록 만들어야 한다(ex. setToDo=(""));.

`setToDos(currentArray=>[toDos,...currentArray]);`
... 을 사용하여 currentArray 배열에 toDo를 추가해준다.

어플리케이션이 시작될 때는 비어있는 배열을 가진다.
첫 번째 toDo 입력시 비어있는 currentArray를 받아오고 새로운 toDos가 input을 통해 작성한 toDo와 아무것도 들어있지 않은 빈 배열의 element가 더해진다.  
1st toDo에 hello라 적고 submit한 후 byebye라 적고 submit -> currentArray에는 Hello가 이미 존재하고, toDo는 byebye가 된다. 그리고 currentArray는 hello와 byebye를 가지고 있는 배열이 된다.

### 7.1 To Do List part Two

map(): js함수. array 안의 요소들을 바꿀 수 있다.
이때 () 안에 함수를 넣을 수 있는데 배열의 모든 item에 대해 실행된다. 즉, 배열에 6개의 item이 있다면 6번 함수가 실행된다.
그리고 그 함수로부터 return한 값은 새로운 배열에 들어가게 한다.
['a','b','c','d','e','f'].map( ()=> ":)" ) -> [':)',':)',':)',':)',':)',':)']인 새 배열을 만들어준다.  
_다만, 기존의 배열에 접근할 수 없게된다._
But, amp은 함수의 첫 번째 argument로 현재의 item을 가지고 올 수 있다.
map(item)->item 이나 원하는 어떤 변수명을 넣으면 item 그 자체를 리턴하는 것도 가능하다.  
map( (item)=>item.toUpperCase() ) 와 같이 작성하면 item이 대문자로 바뀐 새로운 배열을 만들어준다.

리액트는 기본적으로 list에 있는 모든 item을 인식하므로 'key'를 넣어 고유하게 만들어주어햐 한다. map의 첫 번째 argument는 값이고, 두 번째는 index 즉 숫자를 의미한다.
{toDos.map((item.index)=>{item})} -> {{item},{item},{item}}

### 7.2 Coin Tracker

useState를 이용하여 coin tracker을 만드는데, loading중일 때와 그렇지 않은 경우로 나누어 실행결과를 다르게 하였다.  
useEffect에서 fetch를 통해 coin tracker의 사이트를 가져오고(F12-네트워크 에서 확인 가능), 그 안에서 key값과 coin의 name, symbol, USD price까지 가져왔다.

1. map함수와 \<ul>,\<li> 태그를 통해서 얻어온 결과를 보여주는 방법 구현
2. map함수와 \<select>,\<option> 태그를 통해 얻어온 결과를 보여주는 방법 구현  
   -> 위 두 가지 방법으로 간단한 coin tracker를 만들어보았다.

### 7.3 Movie App part One (페이지 전환 방법 배우기)

```C
import { useState, useEffect } from "react";

function App5() {
  const [loading, setLoading] = useState(true);
  const [movies, setMovies] = useState([]);
  useEffect(() => {
    fetch(
      `https://yts.mx/api/v2/list_movies.json?minimum_rating=9&sort_by=year`
    )
      .then((response) => response.json())
      .then((json) => {
        setMovies(json.data.movies);
        setLoading(false);
      });
  }, []);
  return <div>{loading ? <h1>Loading ... </h1> : null}</div>;
}

export default App5;
```

-> then 대신 async-await을 사용하면 아래와 같다.

```C
import { useState, useEffect } from "react";

function App5() {
  const [loading, setLoading] = useState(true);
  const [movies, setMovies] = useState([]);
  const getMovies = async() => {
    const response = await fetch(
      `https://yts.mx/api/v2/list_movies.json?minimum_rating=9&sort_by=year`
    );
      const json = await response.json();
        setMovies(json.data.movies);
        setLoading(false);
  };
  useEffect(() => {
    getMovies();
  }, []);
  return <div>{loading ? <h1>Loading ... </h1> : null}</div>;
}
export default App5;

```

이를 한 번 더 await으로 묶어주면,

```C
 const getMovies = async () => {
    const json = await (
      await fetch(
        `https://yts.mx/api/v2/list_movies.json?minimum_rating=9&sort_by=year`
      )
    ).json();

    setMovies(json.data.movies);
    setLoading(false);
  };
```

와 같이 작성이 가능하다.

\*리스트에 있는 내용을 보여주기 위한 방법 : map함수 사용  
(오래된 array를 가져가서 그 array의 각각의 item을 변형시킨다. 변형돼서 return 된 것들을 새로운 array에 넣어준다.)
예시) [1,2,3,4,5,6].map(x=>x\*2) 라고 입력시 [2,4,6,8,10,12]를 return한다.

또한 map을 사용할 때마다 우리는 key를 element에 주어야 한다. (key값이 존재하지 않는 경우 설정한 Argument값을 key값으로 써주어도 된다. 단, 그 argument가 고유한 값일 경우에만 가능)

### 7.4 Movie App part Two

Movie.js 파일을 새로 생성하여 기존의

```c
<div key={movie.id}>
      <h2>{movie.title}</h2>
      <img src={movie.medium_cover_image}/>
      <p>{movie.summary}</p>
      <ul>
        <li>
          <b>year: </b>
          {movie.year}
        </li>
        {genres.map((g) => (
          <li key={g}>{g}</li>
        ))}
      </ul>
    </div>
```

부분을 Movie.js에 가져오고, div 태그 안의 key값을 삭제하였다.  
이 경우 movie.~에서 movie가 정의되지 않았기 때문에 오류가 발생한다. (+ medium_cover_image, title, summary, genres,year또한 정의되지 않음)

따라서 props obeject를 열어 Movie component가 해당 정보들을(image,title...) parent component로부터 받아오게끔 작성한다.

이후 App5.js에 movie를 render해준다.

```c
{movies.map((movie) => (
            <Movie
              coverImg={movie.medium_cover_image}
              title={movie.title}
              summary={movie.summary}
              genres={movie.genres}
              year={movie.year}
            />
          ))}
```

-> movie component로 property를 보내기 위해 coverImg={movie.medium_cover_image} ...와 같이 작성해준다.

**모든 이미지 element들은 alt 속성을 가지기 때문에 작성을 따로 해주어야 한다.**

**key는 React.js 에서만 , map안에서 component들을 render할 때 사용한다**

---

[Router] - home route는 모든 영화를 보여주고, movie route는 영화 하나만을 보여준다. 즉 이렇듯 route별로 생각해야한다.

이번 chapter 7.4에서는 routes와 components 폴더를 새로 생성하고, Movie.js를 components로 이동한 다음 Home.js 파일을 routes폴더에 생성한다.  
이후 기존의 App5.js의 내용을 Home.js로 가져오고(export default Home; 작성), App5.js에는 `return null;`을 해준다.
-> **그렇다면 기존의 App5.js는 어떤 역할을 하는가?**  
: **router를 render한다.**
(router는 URL을 보고 있는 component고(home.js), 우리가 만약 URL을 변경하게 되면 router은 Detail component를 보여준다-> 새로운 component를 render한다.)

### 7.5 React Router

- Switch가 하는 일: Route 찾고 컴포넌트 렌더링  
  _이때 Route는 URL을 의미_
- ***

[isuue] : import를 했을 때,
`Module not found: Error: You attempted to import ../routes/Detail which falls outside of the project src/ directory. Relative imports outside of src/ are not supported.
You can either move it inside src/, or add a symlink to it from project's node_modules/.` 와 같은 에러가 발생하였다.  
이 에러는 경로가 다르기 때문에 발생하는 문제였고, src 폴더 외부에다 잘못 생성한 routes, components 폴더를 내부로 옮기니 해결되었다.

---

- link 컴포넌트 : 화면 전체를 재실행 하지 않고, 즉 브라우저 새로고침 없이도 유저를 다른 페이지로 이동시켜준다.

[복습]

0. App컴포넌트에 만들었던 모든 logic을 별개의 장소(Home)로 옮겼다.
1. react-router-dom을 import함으로써 Router,Switch,Route 등의 컴포넌트들을 사용한다.
2. 처음에 Router 컴포넌트를 통해 렌더링해주고, 그 안에 들어가는 내용은 유저가 있는 url에 따라 유저에게 보여주고자 하는 내용이다.
3. switch 컴포넌트는 한 번에 하나의 Route만 렌더링 하기 위해 사용하였다.

-> url을 바라보고 있다는 말을 제대로 이해하지 못했으나, url 변경에 따라 컴포넌트들이 작성한대로 실행하는 것(유저에게 보여주고자 하는 것)을 알고 점차 이해함.

### 7.6 parameters

props는 object일 뿐이고, 우리는 그것을 열어서 작성해놓은 item을 꺼내어 쓴다.  
이번 강의에서는 url을 변경함으로써 유저에게 보이는 페이지를 다르게 로딩하는 방법에 대해서 배웠다.

Movie.js에서 `` <Link to={`/movie/${id}`}><{title}></Link> `` 과 같이 작성해준 부분을 살펴보자.  
url에서 movie 이후에 id가 들어가게 될 것이다.  
이 url에 오는 id 값을 알아내기 위해 _url에 있는 값을 반환해주는 함수로서 react router에 존재하는 [useParam]이라는 함수를 불러와야 한다._

```C
import { useParams } from "react-router-dom";

  const { id } = useParams();
  const getMovie = async () => {
    const json = await (
      await fetch(`https://yts.mx/api/v2/movie_details.json?movie_id=${id}`
      )
    ).json();

    console.log(json);
  };

  useEffect(() => {
    getMovie();
  }, []);
```

다음과 같이 작성하면, 해당 id에 속하는 url을 가져와 이동하게 된다.

이후 코드챌린지과정을 통해 Detail.js에서 해당 영화제목을 클릭하면, 해당 url로 이동을 하게 되고 정보를 가져오기 전까지는 loading... 문구가 화면에 보여지며 정보를 가져온 후에는 유저화면에 해당 영화와 관련된 세부 정보들을 보여준다.

### 7.7 Publishing

1. npm i gh-pages
2. package.json에서 디버그 부분에 deploy,predeploy추가
3. package.json에서 맨 아래 부분에 "hompage"~ 추가하여 깃허브주소와 연결
4. npm run deploy (build폴더가 생김)

-> 이후 무엇인가를 수정하고 업데이트를 하고 싶으면, `npm run deploy`만 해주면 된다. (자동으로 프로젝트가 build되고, 폴더가 자동으로 Github pages에 push된다)
