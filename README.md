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
