# 4월 29일 (수)

### UI를 트리 구조로 이해하기 Render트리

- React를 비롯한 많은 UI 라이브러리는 UI를 트리의 형태로 모델링을 합니다.

### 트리는 요소 사이의 관계 모델이며, UI는 이 트리 구조를 사용합니다.

- 브라우저는 HTML 과 CSS를 모델링하기 위해 트리 구조를 사용
- 모바일 플랫폼에서도 뷰의 계층 구조를 나타내는 데 트리를 사용

- 데이터가 흐르는 방식과 렌더링 및 앱 크기를 최적화하는 방법을 이해하는 데 유용한 도구입니다.
- 컴포넌트의 중요한 특징은 다른 컴포넌트들을 중첩해서 또다른 컴포넌트를 구성한느 것입니다.
- 컴포넌트를 중첩하면 부모 컴포넌트와 자식 컴포넌트의 개념이 생기게 됩나다.
- 이떄 각 부모 컴포넌트도 또다른 컴포넌트의 자식이 될 수 있습니다. 다만 자식 컴포넌트으 자식이 될 수는 없습니다.

## UI를 트리 구조로 이해하기 - 모듈 의존성 트리

- 모듈 의존성 트리는 React의 또다른 트리 구조 모델링 방법으로 모듈의 종속성을 나타냅니다.
- 컴포넌트와 로직을 별도의 파일로 분리하면 컴포넌트 뿐만 아니라 함수 또는 상수를 export할 구 있는 JS 모둘을 만들 수 있습니다.

- 트리의 루트 노드는 루트 모듈이며, 엔트리 포인트 파일이라고도 합니다.
  - 일반적으로 루트 컴포넌트를 포함하는 모듈입니다.

- 동일한 앱의 Render 트리와 비교하면 유사한 구조이지만 몇 가지 차이점이 있습니다.

1. 트리를 구성하는 노드는 컴포넌트가 아닌 모듈을 나타냅니다.
2. inspirations.js와 같은 컴포넌트가 아닌 모듈도 이 트리에 나타납니다.
3. Render 트리는 컴포넌트만 캡슐화 하지만 모듈 트리는 모듈도 포함합니다. (컴포넌트 + 모듈)

- Render 트리에서 Copyright 컴포넌트는 InspirationGenerator의 자식으로 나타나지만,  
  모듈 트리에서는 App.js 아래에 나타납니다.  
  → 이것은 InspirationGenerator가 Copyright를 자식 컴포넌트로 렌더링하지만  
   모듈을 가져오지는 않기 때문입니다.

- 의존성 트리는 React 앱을 실행하는 데 필요한 모듈을 결정하는 데 유용하게 이용됩니다.

- React 앱을 프로덕션으로 빌드할 때, 일반적으로 클라이언트에 제공할 때  
  필요한 모든 JavaScript를 번들로 묶는 빌드 단계가 있습니다.

- 이 작업을 담당하는 도구를 번들러라고 하며,  
  번들러는 의존성 트리를 사용하여 포함해야 할 모듈을 결정합니다.

- 일반적으로 앱이 커짐에 따라 번들 크기도 커집니다.

- 번들 크기가 커지면 클라이언트가 다운로드하고 실행하는 데 드는 비용도 커집니다.

- 또한 UI가 그려지는 데 시간이 지체될 수 있습니다.

- 앱의 의존성 트리를 파악하면 이러한 문제를 디버깅하는 데 도움이 될 수 있습니다.

## JSX에 스타일 적용하기

- JSX에 스타일을 적용하는 방법은 다음과 같이 매우 다양합니다.
  - 일반 CSS, 인라인 스타일, CSS-in-JS, CSS 프레임워크, CSS Module

- React에서 권장하는 방법은 CSS Module입니다.

- 실무에서는 Tailwind + 일부 CSS Modules 혹은 CSS Modules + SCSS의 조합으로 많이 사용합니다.

- 프로젝트의 특성에 따라 여러가지 방법을 사용할 수 있기 때문에  
  다른 방법에 관해서도 간단히 알아보도록 하겠습니다.

## 4. CSS 프레임워크

- 일반적으로 프론트엔드 개발에 많이 사용하는 방법입니다.

- Tailwind CSS(클래스 단위), Bootstrap(컴포넌트 단위), Bulma 등  
  유명한 CSS 프레임워크들이 많이 있습니다.

- React에서 추천하는 Tailwind CSS는 클래스를 조합하여 스타일을 작성합니다.

- 빠른 개발과 디자인의 일관성을 유지할 수 있다는 장점이 있습니다.

- 클래스를 조합하는 과정에서 클래스 선언이 길어지기 때문에  
  문서의 가독성이 떨어진다는 단점도 있습니다.

---

### 예제 코드

```jsx
export default function Button() {
  return <button className="bg-blue-500 text-white px-4 py-2">Click</button>;
}
```

## 5. CSS Module

- css Module은 클래스명을 [클래스이름]\_[해쉬값]의 형태로 자동 변환하여, 고유한 이름의 로컬 스코프를 제공하는 기술입니다.
- 컴포넌트 기반의 프레임워크인 React나 Vue 등에서 채택하고 있는 이 기술은 스타일의 충돌을 완벽하게 방지할 뿐만 아니라 유지보수에도 유리합니다.
- 컴포넌트 단위로 스타일링 한다는 것이 가장 큰 특징으로 컴포넌트의 재사용에도 유리하게 작용합니다.

## CSS Module 사용방법

- 파일 이름의 규칙 : 파일 이름은 [컴포넌트 이름].module.css의 형태로 확장자는 반드시 .module.css로 합니다.
- CSS 작성 :
  - CSS의 내용은 일반 CSS의 작성법을 따릅니다.
  - class 선책자로 스타일을 선언합니다.
  - 아래 예제처럼 Tag 선책지를 사용하는 것은 특별한 경우가 아니라면 권장하지 않습니다.

## CSS Module 사용 방법

- 클래스에 적용하는 법 :
  - import의 변수명은 관행적으로 style을 사용합니다.
  - JSX에서는 class 키워드 대신 className을 사용 합니다.
  - class 이름은 객체를 사용할 때처럼 [변수 명].[클래스 명]의 형태로 작성합니다.
  - class 이름 전체를 중괄호로 감싸 줍니다.

- 관리 방법
  - CSS Module은 컴포넌트 단위로 CSS를 작성하여 재사용이 가능하도록 합니다.

### [ 실습 ]

```jsx
// ButtonCom
export default function ButtonCom() {
  return (
    <>
      <h1>ButtonCom</h1>
      <nav>
        <button>버튼1</button>
      </nav>
      <nav>
        <button>버튼2</button>
      </nav>
    </>
  );
}
```

```jsx
/// App.jsx
import ButtonCom from "./components/ButtonCom/ButtonCom";
export default function App() {
  return <ButtonCom />;
}
```

---

### 이벤트에 응답하기

- React애서는 JSP에 이벤트 핸들러를 추가할 수 있습니다.
- 이벤트 핸들러는 클릭, 마우스 호버, 폼 입력의 포커스 등 사용자와의 상호작용에 따라 유발되는 사용자 정의 함수 입니다.

### [ 실습 ]

```jsx
import style from "./ButtonCom.module.css";
function handleClick() {
  alert("버튼 클릭");
}
export default function ButtonCom() {
  return (
    <>
      <h1 className={style.title}>ButtonCom</h1>
      <nav className={style.navBar}>
        <button onClick={handleClick} className={style.myButton}>
          버튼1
        </button>
        <button onClick={handleClick} className={style.myButton}>
          버튼2
        </button>
      </nav>
    </>
  );
}
```

### 이벤트 핸들러 인라인 스타일 정의

- 이벤트 핸들러는 별도의 함수로 정의하는 것이 일반적이지만 JSX 내에 인라인으로 정의할 수 도 있습니다.
- 인라인 스타일은 함수가 아주 짧을 때만 예외적으로 사용할 것을 권장합니다.
- 가독성이 떨어지고 , 재사용화 하기에도 불편하기 때문입니다.

### 이벤트 핸들러 함수의 전달

- 이벤트 핸들러 함수는 호출하는 것이 아니라 전달하는 것입니다.
- 함수를 전달한다는 것은 다음 예와 같이 함수의 이름만 prop의 형태로 전달합니다.

```jsx
<button onclick={handleClick}>
```

#### 잘돗된 함수 사용법

```jsx
<button onclick={handleClick()}>
```

# 4월 15일 (수)

## [ 실습1 ]

```jsx
export const heroes = [
  {
    id: 0,
    casting: "스파이더맨",
    name: "피터 파커",
  },
  {
    id: 1,
    casting: "아이언맨",
    name: "토니 스타크",
  },
  {
    id: 2,
    casting: "배트맨",
    name: "브루스 웨인",
  },
  {
    id: 3,
    casting: "슈퍼맨",
    name: "클라크 켄트",
  },
  {
    id: 4,
    casting: "헐크",
    name: "브루스 배너",
  },
];
```

HeroesData

## 화살표 함수(Arrow Function)에 대하여

### 묵시적 반환 (Implicit Return)

화살표 함수는 `=>` 바로 뒤에 식이 오는 경우, 별도의 `return` 키워드 없이도 그 값을 **묵시적으로 반환**하므로 작성할 필요가 없습니다.

```jsx
const listItems = chemists.map(
  (person) => <li>...</li>, // 묵시적 반환
);
```

### 명시적 반환 (Explicit Return)

그러나 => 뒤에 **{ } (중괄호)**가 오는 경우에는 return을 명시적으로 작성해야 합니다.

```jsx
const listItems = chemists.map((person) => {
  // 중괄호 사용
  return <li>...</li>; // 명시적 반환
});
```

- Block Body: => { 처럼 중괄호를 사용하는 화살표 함수는 **"block body"**를 가지고 있다고 말합니다.
- 유연성: 이 형식을 사용하면 함수 내부에서 한 줄 이상의 복잡한 코드를 작성할 수 있습니다.
- 주의사항: 중괄호를 열었다면 반드시 return 문을 작성해야 합니다.
- 결과: return 문을 작성하지 않으면 아무것도 반환되지 않습니다 (undefined).

- 경고 메세지

```
Each child in a list should have a unique "key" prop.
```

### 리스트 랜더링

- 컴포넌트에서 여러 개의 데이터로 같은 햘식으로 출력해야 하는 경우가 있습니다.
- 이럴 떄는 JavaScript의 배열관련 함수를 사용해서, 배열을 컴포넌트의 기능에 맞게 랜더리할 수 있습니다.

## Key prop을 사용하는 이유

React에서 리스트를 렌더링할 때 다음과 같은 경고를 마주할 수 있습니다.

> **Warning:** Each child in a list should have a unique "key" prop.

### 경고가 발생하는 이유

이 경고는 목록(배열)의 각 자식 요소가 고유한 **'key' prop**을 가져야 하는데, 설정되지 않아서 발생합니다.

- 배열의 각 항목은 다른 항목들과 명확히 구분되는 **고유한 문자열 혹은 숫자**를 key로 지정해야 합니다.
- 이것을 **key prop**이라고 합니다.
- 데이터 설계 시 고려사항: HeroesData 컴포넌트의 데이터에 id 값을 미리 포함시킨 이유는 바로 이 key prop으로 사용하기 위해서입니다.
- 핵심 규칙: map() 함수를 사용할 때 내부의 JSX 엘리먼트에는 반드시 key prop이 필요합니다.

# 프래그먼트(Fragment)와 key prop

### 여러 개의 태그를 반환해야 할 때

#### 각 항목이 하나가 아닌 **여러 개의 DOM 노드**를 렌더링해야 하는 경우(반환해야 하는 태그가 여러 개일 경우) 어떻게 처리해야 할까요?

- 보통 **프래그먼트(`<>...</>`)** 구문을 사용하거나, `<div>` 태그 등으로 묶어서 하나로 노드로 만들어 반환해야 합니다.

## 컴포넌트를 순수하게 유지하기

- **순수 함수란 무엇인가?**
  - 같은 입력 값을 넣으면 항상 같은 결과를 반환하는 함수를 말합니다.
  - 외부의 상태를 변경하지 않는 즉, 사이드 이펙트(side effect)가 없는 함수를 의미합니다.

- **다음 두 함수를 비교해 보세요. 어떤 것이 순수함수 일까요?**

```jsx
function add(a, b) {
  return a + b;

```

```jsx
let count = 0;

function increase() {
  count++;
}
```

```jsx
// kiosk.jsx
import OrderUp from "./OrderUp";

export default function Kiosk() {
  return (
    <section>
      <h2>치즈버거 세트 메뉴를 주문하세요.</h2>
      <p>일반 세트</p>
      <OrderUp order={1} />
      <p>패밀리 세트</p>
      <OrderUp order={2} />
      <p>이용해 주셔서 감사합니다.</p>
    </section>
  );
}
```

```jsx
// OderUp.jsx
export default function OrderUp({ order }) {
  return (
    <section>
      <p>
        치즈버거{order}개/콜라{order}개 + (이벤트)프렌치 프라이{2 * order}개
      </p>
    </section>
  );
}
```

## 사이드 이펙트: 의도하지(않은) 결과

```jsx
/* eslint-disable*/
let guest s= 0;

function Cup() {
  // 이미 존재했던 변수를 변경하고 있습니다!
  guest = guest + 1;
  return <h2>Tea cup for guest #{guest}</h2>;
}

export default function TeaSet() {
  return (
    <>
      <Cup />
      <Cup />
      <Cup />
    </>
  );
```

## 지역 변경(local mutation)

- 잘못된 예제의 문제점은 컴포넌트가 **외부에 있는 기존 변수**를 렌더링 중에 변경했다는 것입니다.
- 이런 사이드 이펙트를 **"변경(Mutation)"**이라고 부르기도 합니다. Mutation은 돌연변이라는 뜻도 가지고 있습니다.
- 순수 함수는 **함수 스코프 외부의 변수**나 호출 전에 생성된 객체를 변경하지 않습니다.
- 그러나, **렌더링하는 동안에 생성된 변수와 객체**를 변경하는 것은 전혀 문제가 되지 않습니다.

## [ 실습 ]

```jsx
function Cup({ guest }) {
  return <h2>Tea cup for guest #{guest}</h2>;
}

export default function TeaGathering() {
  const cups = [];
  for (let i = 1; i <= 12; i++) {
    cups.push(<Cup key={i} guest={i} />);
  }
  return cups;
}
```

## UI를 트리 구조로 이해하기 - Render 트리

- React를 비롯한 많은 UI 라이브러리는 UI를 **트리의 형태**로 모델링합니다.
- 애플리케이션을 트리로 생각하면 **컴포넌트 간의 관계**를 이해하는 데 도움이 됩니다.
- 또한 향후 성능이나 상태 관리와 같은 개념을 파악하는 데도 많은 도움이 됩니다.

---

### 트리 구조의 활용

트리는 요소 사이의 관계 모델이며, UI는 이 트리 구조를 사용하여 표현됩니다.

- **브라우저**: HTML(DOM)과 CSS(CSSOM)을 모델링하기 위해 트리 구조를 사용합니다.
- **모바일 플랫폼**: 뷰(View)의 계층 구조를 나타내는 데 트리를 사용합니다.

# 4월 8일 (수)

### 조건부 렌더링

- 컴포넌트는 조건에 따라 다른 항목을 표시해야 하는 경우가 많습니다.
- React는 If문, 삼항 연산자와 같은 자바스크입트 문법을 사용하여 조건부로 JSX를 랜더링할 수 있습니다.

## [ 실습 ]

```jsx
import PackingList from "./PackingList";

export default function Profile() {
  return (
    <>
      <PackingList />
    </>
  );
}
```

App.jsx

```jsx
export default function Items({ name, isPacked }) {
  if (isPacked) {
    return <li>{name}✅</li>;
  }
  return <li>{name}</li>;
}
```

Items.jsx

```jsx
import Items from "./Items";

export default function PackingList() {
  return (
    <>
      <section>
        <h1>여행 짐 리스트</h1>
        <ul>
          <Items name="여분 옷" />
          <Items name="노트북" />
          <Items name="컵라면" isPacked={true} />
        </ul>
      </section>
    </>
  );
}
```

PackingList.jsx

### 논리 연산자 AND(&&) 사용하기

if문이나 삼항 연산자를 사용하는 방법외에 일반적으로 사용하는 또 다른 방법은 JavaScript 논리 연산자 AND('&&')를 사용하는 것입니다.

```jsx
export default function Items({ name, isPacked }) {
  return (
    <li>
      {name}
      {isPacked && " ✅"}
    </li>
  );
}
```

Items.jsx

- && 윈쪽에 숫자를 두면 안 됩니다.
- JavaScript는 조건을 테스트하기 위해 표현식 왼쪽을 자동으로 부울(bool)로 변환합니다.

### 변수에 존건부로 JSX를 할당하기

- let으로 정의된 변수는 재할당할 수 있으므로 표시할 기본 내용인 name을 먼저 대입합니다.

```jsx
let itemContent = name;
```

- 다음으로 if 문을 사용하여 isPacked가 true인 경우 JSX 표현식을 itemContent에 다시 할당합니다.

```jsx
if (isPacked) {
  itemContent = name + " ✅";
}
```

- return문의 JSX 트리에 중괄호를 사용하고, 위의 if문에서 계산된 변수 itemContent를 JSX 내부에 중첩하여 포함시킵니다.

```jsx
<li>{itemContent}</li>
```

```jsx
const heroes = [
  "스파이더맨: 피터 파커",
  "아이언맨: 토니 스타크",
  "베트맨: 브루스 웨인",
  "슈퍼맨: 클라크 켄트",
  "헐크: 로버트 브루스 배너",
];

export default function MovieHeroes() {
  const listHeroes = heroes.map((hero) => <li key={hero}>{hero}</li>);

  return (
    <section>
      <h1>영화 속 영웅들</h1>
      <ul>{listHeroes}</ul>
    </section>
  );
}
```

MovieHeroes.jsx

```jsx
import MovieHeroes from "./MovieHeroes";

export default function Profile() {
  return (
    <>
      <MovieHeroes />
    </>
  );
}
```

App.jsx

# 4월 1일 (수)

### Props (Properties) 이해하기

-**Props란 무엇인가?**

- 부모 컴포넌트가 자식 컴포넌트에 전달하는 데이터입니다. (마치 함수의 '인자'와 같은 역할)

- Props는 **읽기 전용(Read-only)**이며, 자식 컴포넌트 내부에서 수정할 수 없습니다.

-**Props 전달하고 사용하기 [ 실습 ]**

```jsx
// 부모 컴포넌트 (App.jsx)
import Welcome from "./Welcome";

export default function App() {
  return (
    <>
      <Welcome name="이동교" color="blue" />
      <Welcome name="리액트" color="red" />
    </>
  );
}
```

```jsx
// 자식 컴포넌트 (Welcome.jsx)
export default function Welcome(props) {
  return <h1 style={{ color: props.color }}>안녕하세요, {props.name}님!</h1>;
}
```

-**2. Props 구조 분해 할당 (Destructuring)**

- props.name 처럼 매번 props를 붙이지 않고, 중괄호 { }를 사용해 필요한 값만 바로 꺼내 쓸 수 있습니다.

```jsx
export default function Welcome({ name, color }) {
  return <h1 style={{ color: color }}>안녕하세요, {name}님!</h1>;
}
```

- 기본값 설정 (Default Props): 부모가 값을 주지 않았을 때 사용할 기본값을 지정할 수 있습니다.

```jsx
export default function Welcome({ name = "손님" }) {
  return <h1>환영합니다, {name}님!</h1>;
}
```

-**3. JSX에서 자바스크립트 사용하기 (중괄호 { })**

- JSX 내부에서 자바스크립트 변수나 표현식을 사용하려면 **중괄호 { }**로 감싸야 합니다.

-**[ 실습 ] 자바스크립트 객체와 스타일 전달**

```jsx
const user = {
  name: "Lee Dong-gyo",
  imageUrl: "https://example.com/photo.jpg",
  imageSize: 90,
};

export default function Profile() {
  return (
    <>
      <h1>{user.name}</h1>
      <img
        className="avatar"
        src={user.imageUrl}
        alt={"Photo of " + user.name}
        style={{
          width: user.imageSize,
          height: user.imageSize,
          borderRadius: "50%",
        }}
      />
    </>
  );
}
```

- 주의사항: style={{ ... }} 에서 바깥쪽 중괄호는 JSX 표현식을 위한 것이고, 안쪽 중괄호는 자바스크립트 객체임을 나타냅니다.

-**4. 자식 컴포넌트를 Props로 전달하기 (children)**

- 태그와 태그 사이에 넣은 내용은 children이라는 특별한 prop으로 전달됩니다.

```jsx
function Card({ children }) {
  return <div className="card-container">{children}</div>;
}

export default function App() {
  return (
    <Card>
      <h1>카드 제목</h1>
      <p>카드 내용입니다.</p>
    </Card>
  );
}
```

# 3월 25일 (수)

### 차세대 자바스크립트 빌드 도구 (Oxc & SWC)

- Rust 언어로 작성되어 기존 도구들보다 압도적인 속도를 제공하는 차세대 개발 도구들이다.

#### SWC (Speedy Web Compiler)

- **바벨(Babel)의 강력한 대체제**
  - 자바스크립트 및 타입스크립트 코드를 이전 버전의 자바스크립트로 변환(Transpiling)하거나 하나로 묶는(Bundling) 작업에 특화되어 있다.
- **현대적 프레임워크의 표준**
  - 속도가 매우 빨라 Next.js와 같은 최신 웹 프레임워크에서 기본 컴파일러로 채택하여 사용하고 있다.

#### Oxc (Oxidation Compiler)

- **고성능 툴체인(Toolchain) 모음**
  - 단순히 컴파일뿐만 아니라 ESLint, Prettier, TypeScript 변환 등을 하나로 통합하여 대체하려는 프로젝트이다.
- **압도적인 성능과 정적 분석**
  - 파싱(Parsing) 속도가 SWC보다 3배 이상 빠르며, 린팅(Linting) 작업에서는 기존 ESLint보다 100배 이상 빠른 성능을 보여준다.
  - 코드의 오류를 잡아내거나 구조를 분석하는 정적 분석 기능에 매우 강력한 강점을 가진다.

### React 컴포넌트 만들기 (실습)

---

```jsx
import Profile from "./Profile";

export default function App() {
  return (
    <>
      <Profile />
    </>
  );
}
```

App.jsx

```jsx
import reactLogo from "./assets/react.svg";

export default function Profile() {
  return (
    <>
      <img className="button-icon" src={reactLogo} alt="" />
    </>
  );
}
```

Profile.jsx

---

### 리액트 프로젝트의 기본 단위인 컴포넌트의 생성 과정과 사용 방법을 정리하면 다음과 같다.

#### 컴포넌트의 생성

1. **파일 생성**
   - 컴포넌트의 이름과 동일한 이름의 파일을 생성한다.
2. **외부 노출 설정 (Export)**
   - `function` 구문 앞에 `export default` 키워드를 사용하여 외부에서 이 컴포넌트를 불러와 사용할 수 있도록 한다.
3. **로직 구현**
   - `function` 구문의 중괄호 `{ }` 내부에 컴포넌트가 수행할 비즈니스 로직을 구현한다.
4. **UI 반환 (Return)**
   - `return` 구문의 소괄호 `( )` 내부에 컴포넌트가 화면에 렌더링할 JSX 문구를 작성한다.

#### 컴포넌트의 사용

1. **컴포넌트 불러오기 (Import)**
   - 사용하고자 하는 위치에서 해당 컴포넌트를 `import` 한다.
2. **태그 형태로 사용**
   - `import` 할 때 정의한 이름을 사용하여 `<컴포넌트명 />`과 같은 구조로 원하는 곳에 배치한다.

---

## 컴포넌트의 중첩(Nesting)

- React에서의 중첩은 특정 컴포넌트를 다른 컴포넌트 안에서 호출하는 것을 의미한다.

- 중첩을 특정 컴포넌트 안에 다른 컴포넌트를 선언하는 것으로 이해해서는 안 된다.

```jsx
export default function Gallery() {
  function Profile() {
    // ...
  }

  return (
    <div>
      <Profile />
    </div>
  );
}
```

```jsx
function Profile() {
  // ...
}

export default function Gallery() {
  // 외부에서 선언된 컴포넌트를 필요한 위치에서 호출하여 사용한다.
  return (
    <div>
      <Profile />
    </div>
  );
}
```

---

### 컴포넌트 중첩[ 실습 1]

```jsx
import Profile from "./Profile";

export default function Gallary() {
  return (
    <>
      <Profile />
      <Profile />
      <Profile />
    </>
  );
}
```

Gallary.jsx

## 컴포넌트 중첩[ 실습 2]

```jsx
export default function MyTile() {
  return (
    <>
      <h1>My Gallary</h1>
    </>
  );
}
```

MyTile.jsx

```jsx
import Profile from "./Profile";
import MyTile from "./MyTile";

export default function Gallary() {
  return (
    <>
      <MyTile />
      <Profile />
      <Profile />
      <Profile />
    </>
  );
}
```

Gallary.jsx

---

### Named Export의 다양한 사용법 [ 실습 ]

```jsx
export function NamedComponent1() {
  return (
    <>
      <h1>네임드 1</h1>
    </>
  );
}
export function NamedComponent2() {
  return (
    <>
      <h1>네임드 2</h1>
    </>
  );
}
export function NamedComponent3() {
  return (
    <>
      <h1>네임드 3</h1>
    </>
  );
}
```

NamedComponent.jsx

```jsx
import {
  NamedComponent1 as Foo,
  NamedComponent3 as Bar,
} from "./NanemdComponent";

export default function NamedComponentTest() {
  return (
    <>
      <h1>Named Component Test</h1>
      <Foo />
      <Bar />
    </>
  );
}
```

NamedComponentTest.jsx

```jsx
import Gallary from "./components/Gallary";
import NamedComponentTest from "./components/NamedComponentTest";

export default function App() {
  return (
    <>
      <NamedComponentTest />
      {/* <Gallary /> */}
    </>
  );
}
```

App.jsx

```jsx
import * as Foo from "./NanemdComponent";

export default function NamedComponentTest() {
  return (
    <>
      <h1>Named Component Test</h1>
      <Foo.NamedComponent1 />
      <Foo.NamedComponent2 />
      <Foo.NamedComponent3 />
    </>
  );
}
```

NamedComponentTest.jsx ( 모두 가져오기 )

## 2. 컴포넌트의 분리와 관리

### 컴포넌트를 다른 파일로 분리해서 사용하는 방법을 정리하면 다음과 같습니다.

1. 컴포넌트를 추가할 JSX 파일을 생성합니다.
2. 새로 만든 파일의 컴포넌트를 외부에서 사용할 수 있도록 export 합니다.
3. 사용할 컴포넌트에 새로 만든 컴포넌트를 import 하고 사용합니다.

### 컴포넌트를 분리하면 프로젝트 루트에 너무 많은 파일들이 생성돼서 관리하기가 어렵습니다.

### 따라서 컴포넌트는 다음과 같이 관리하고, 사용하는 것이 편리합니다.

- App.jsx는 루트 컴포넌트로 최종적으로 렌더링할 컴포넌트를 모아두는 곳으로 가능하면 App이외의 다른 컴포넌트를 정의하지 않는 것이 좋습니다.
- 컴포넌트는 /src/components/와 같은 별도의 디렉토리를 만들어 관리하는 것이 좋습니다.
- 프로젝트가 커져서 다양한 컴포넌트가 있다면, /src/components/ 디렉토리에 기능별로 하위 디렉토리를 만들어 사용해도 됩니다.

## 3. Default Export와 Named Export의 차이

- JavaScript에서는 default와 named export라는 두 가지 방법으로 값을 export 합니다.

- 두 가지 선언 방식의 차이는 default 키워드의 사용 여부입니다.

- 두 가지 방법 모두 한 파일에서 사용할 수도 있습니다.

- 주의할 점은 하나의 파일에는 하나의 default export만 존재할 수 있고, named export는 여러 개가 존재할 수 있다는 것입니다.

- Export 하는 방식에 따라 import 하는 방식이 정해져 있습니다.

## 3. Default Export와 Named Export의 차이

**[ Default import의 사용 ]**

- import 키워드 다음에 다른 이름으로 변수명을 선언할 수 있습니다.

- 이 이름을 로컬 식별자 혹은 변수명이라고 합니다.

- 예를 들어 import Banana from './Button' 라고 선언하면, 이 파일안에서는 Banana라는 이름으로 사용할 수 있습니다.

- 변수명은 대문자로 시작해야 합니다.

**[ named import를 사용 ]**

- export하는 곳과 import하는 곳의 컴포넌트의 이름이 같아야 합니다.

- 모듈에 여러 개의 named 컴포넌트가 있을 경우 전부 혹은 일부만 import해서 사용할 수 있습니다.

## 1. 개요

**JSX란 무엇인가?**

- JSX는 JavaScript를 확장한 문법으로, JavaScript 파일을 HTML과 비슷한 형태의 마크업을 작성할 수 있도록 해줍니다.

- 컴포넌트를 작성하는 다른 방법도 있지만, JSX의 간결함 때문에 대부분의 React 개발자가 선호합니다.

- HTML, CSS, JavaScript 코드는 일반적으로 분리된 파일로 관리합니다.

- 그러나 Web이 더욱 인터랙티브 해지면서, 로직이 내용을 결정하는 경우가 많아졌습니다.

- 따라서 효율적인 렌더링을 위해서는 로직을 담당하는 JavaScript가 HTML을 담당하는 것이 좋습니다.

- React의 컴포넌트가 좋은 예입니다.

## 1. 개요

- Form.jsx 처럼 버튼(input 태그)의 렌더링 로직과 마크업이 함께 있으면, 매번 변화가 생길 때마다 서로 동기화 상태를 유지할 수 있습니다.

- 반대로 버튼의 마크업과 사이드바의 마크업처럼 관련이 없는 항목들은 서로 분리되어 있기 때문에 각각 개별적으로 변경할 수 있어 안전한 관리가 가능합니다.

- 즉 React 컴포넌트는 JavaScript 함수로 작성되며, 이 로직과 함께 JSX라는 확장된 문법으로 마크업을 작성합니다.

- JSX는 HTML과 비슷해 보이지만 조금 더 엄격하게 적용되며, 동적으로 정보를 표시할 수 있습니다.

### 2. JSX의 3가지 규칙

1. 하나의 루트 엘리먼트로 반환해야 합니다.
2. 모든 태그는 닫아줘야 합니다.
3. 속성(attribute)은 카멜 케이스(camelCase)로 작성합니다.

**파스칼 케이스(PascalCase)** : 첫 단어부터 대문자로 시작합니다. React 컴포넌트의 이름에 사용됩니다.

**카멜 케이스(camelCase)** : 첫 단어는 소문자로 시작하고, 다음 단어부터는 대문자로 시작합니다. JSX의 속성 이름에 사용됩니다.

---

# 3월 18일 (수)

## 10. React Project의 구조 및 역할

### node_modules/

- 초기 의존성 패키지 및 새로 설치하는 패키지가 저장됩니다.
- 이 디렉토리는 git으로 관리하지 않습니다. .gitignore에서 확인할 수 있습니다.
- npm install 명령으로 재설치가 가능합니다.

### public/

- 정적(static) 파일을 저장하는 디렉토리입니다.
- 빌드 시 그대로 dist 디렉토리로 복사됩니다. Dist는 빌드 시에 자동으로 생성됩니다.
- Vite가 특별한 처리를 하지 않습니다. 파일 이름도 그대로 사용합니다.
- import 필요 없이 프로젝트에서 사용할 수 있습니다.
- 고정 파일, favicon, robots.txt 등의 파일을 보관할 때 사용합니다.

### src/

- React 프로젝트의 주요 코드가 위치하는 디렉토리입니다.
- 개발하면서 대부분의 작업이 이 곳에서 이루어지는 곳입니다.

## 10. React Project의 구조 및 역할

### src/main.jsx

- React 앱의 진입 점(entry point)으로 최종 렌더링이 되는 곳입니다.
- App.jsx 컴포넌트를 전달받아 렌더링합니다.
- 최종 적으로 /index.html 전달되어 마운트됩니다.

### index.html

- React 앱이 마운트 되는 HTML 파일입니다.
- 마운트 지점은 id값이 root인 div태그 안입니다.
- `<div id="root"> [마운트 지점] </div>`

#### 프로젝트의 디렉토리 구조를 확인해 두면 개발을 진행하는데 큰 도움이 됩니다.

#### 중요한 것은 App.jsx의 내용이 main.jsx로 전달되고, 이것은 최종적으로 index.html로 전달되어 출력 된다는 것입니다.

## 6. 의존성 관리와 package.json

**[ 의존성을 관리하는 이유 ]**

### 손쉬운 설치 및 업데이트

- npm install 또는 yarn install 한 줄로 모든 의존성을 자동 설치 가능.
- 특정 버전의 라이브러리를 쉽게 업데이트 가능.

### 일관된 개발 환경 유지

- 팀원들과 같은 라이브러리 버전을 유지할 수 있음.
- package-lock.json을 활용하면 동일한 패키지를 정확한 버전으로 설치 가능.

### 중복 설치 방지

- 필요 없는 라이브러리를 제거하여 프로젝트를 가볍게 유지할 수 있음.

#### package.json은 이런 의존성을 체계적으로 관리하는 역할을 합니다.

#### 프로젝트에 필요한 라이브러리를 쉽게 설치, 업데이트, 유지할 수 있도록 도와주는 시스템입니다.

## 의존성 관리와 package.json

**[ package.json의 의존성 내용의 종류 ]**

- dependencies : 실제 코드에서 사용하는 라이브러리 (예: React, Express 등)

- devDependencies : 개발할 때만 필요한 라이브러리들 (예: Webpack, ESLint 등)

- peerDependencies : 필요한 라이브러리만, 직접 설치하지 않고 사용자에게 설치를 맡기는 경우

- optionalDependencies : 있어도 되고 없어도 되는 선택적 의존성.

## 의존성 관리와 package.json

**[ package.json을 유지해야 하는 이유 ]**

1. 프로젝트의 의존성 정보 제공
   - 프로젝트에서 어떤 패키지를 사용하는지 정의하는 역할을 합니다.
   - 어떤 패키지를 설치해야 하는지 알 수 있는 기준이 됩니다.

2. 버전 범위 설정 가능
   - ^18.0.0처럼 최신 패치 버전을 허용할 수도 있고, 18.2.0처럼 정확한 버전만 고정할 수도 있습니다.
   - 개발자가 원하는 방식으로 유연하게 관리할 수 있습니다.

3. 스크립트와 메타데이터 저장
   - "scripts" 속성을 이용해 빌드, 테스트, 실행 등의 명령어를 저장할 수 있습니다.
   - 프로젝트 실행을 위해서는 반드시 필요 합니다.

4. 새로운 패키지 설치 및 관리
   - 패키지를 설치하면 package.json에 추가되고, package-lock.json에는 정확한 버전이 기록됩니다.
   - 만약 package.json이 없으면, 새로운 패키지를 추가할 수 없습니다.

## 13. node module의 재설치

**[ package-lock.json을 삭제하는 이유 ]**

1. package-lock.json이 손상되었거나, 잘못된 의존성이 있을 때
   - 가끔씩 package-lock.json이 의존성 충돌 때문에 이상한 상태가 될 때가 있습니다.
     · 예를 들면 패키지를 여러 번 업데이트하면서 충돌이 발생하는 경우
     · 수동으로 package.json을 수정해서 package-lock.json에 영향을 미치는 경우
   - 이런 경우, package-lock.json을 삭제하고 새로 생성하면 충돌이 해결될 수도 있습니다.

2. 최신 버전의 패키지를 다시 받고 싶을 때
   - 최신 버전의 패키지를 다시 다운로드하고 싶다면, 삭제하는 것이 효과적입니다.
   - 재설치 하면 최신 버전의 종속성을 기반으로 새로운 package-lock.json이 생성됩니다.

3. 팀 프로젝트에서 다른 팀원이 이상한 상태로 package-lock.json을 업데이트했을 때
   - 팀원 중 누군가가 로컬에서 이상한 상태로 package-lock.json을 변경했다면 파일을 삭제하고 다시 설치하는 것이 더 깨끗할 수도 있습니다.

#### 문제가 없다면 package-lock.json을 유지하는 것이 좋지만, 의존성 충돌이나 패키지 문제로 인해 에러가 발생한다면 삭제 후 재설치 하는 것이 좋습니다.

# 3월 11일 (수)

### Git 기본 사용법

- 프로젝트 버전 관리와 협업을 위해 필수적으로 사용하는 Git의 기본 명령어와 작동 원리를 상세히 정리

#### 명령어

```
git init
git add .
git commit -m "여기에 메모 작성"
```

# ch00

### Node.js란 무엇인가

-

#### node.js가 인기를 끄는 이유

- 빠른 성능으로 고성능 처리 가능
- 활발한 생태계, 실시간 애플리케이션에 강함

#### node.js는 앞으로 발전 할까?

- es 모듈 자원 강화
- 클라우드 및 서버리스

#### Node.js 장점

- **비동기 논블로킹 (Asynchronous Non-blocking I/O)**
  - 하나의 작업이 끝날 때까지 기다리지 않고 다음 작업을 바로 실행한다. 덕분에 채팅이나 스트리밍처럼 동시에 수많은 요청을 처리해야 할 때 처리 속도가 매우 빠르다.
- **프론트엔드와 백엔드 언어 통일**
  - 자바스크립트(JavaScript) 언어 하나만 알면 웹 화면과 서버를 모두 개발할 수 있어서 학습과 개발이 효율적이다.
- **방대한 오픈소스 생태계 (npm)**
  - 전 세계 개발자들이 만들어둔 수백만 개의 유용한 기능(패키지)들을 명령어 한 줄로 가져와서 레고 블록처럼 쉽게 프로젝트에 적용할 수 있다.

#### Node.js 단점

- **CPU 집약적인 작업에 불리**
  - 일하는 일꾼(스레드)이 기본적으로 하나뿐인 '싱글 스레드' 방식이기 때문에, 복잡한 수학 계산이나 동영상 인코딩처럼 연산량이 많은 무거운 작업에는 불리하다.
- **비동기 처리로 인한 코드 복잡도 (콜백 지옥)**
  - 기다리지 않고 다음 일을 처리하다 보니, 순서대로 실행해야 할 때 코드가 안쪽으로 계속 파고드는 복잡한 형태가 되기 쉽다.
- **에러 발생 시 서버 다운 위험**
  - 스레드가 하나뿐이라서 코드에 치명적인 에러가 발생했을 때 예외 처리를 철저하게 해두지 않으면 서버 전체가 멈춰버릴 위험이 있다.

---
