## 라우팅이란?

라우팅은 네트워크에서 경로를 선택하는 프로세스를 의미한다.

## React-Router을 사용하는이유

#### a태그로 이동해도 무방한데 왜 궅이 라우터를 정의하고 사용할까?
-> 그냥 a 태그를 사용하면 페이지 전체가 깜빡이며 화면전환을 한다. 그래서 라우팅을 통해서 부드러운 화면전환을 하기 위해 사용한다.

#### 그냥 한주소 안에서 화면만 바꿔주면 되는거 아니야?
-> 그런방식으로 웹 페이지를 만들면 특정 페이지를 공유하거나 즐겨찾기를 하지 못한다, 그리고 브라우저의 뒤로가기 앞으로 가기를 하지 못한다, 만약 와이파이가 먹통이 돼서 새로고침이 되면 작업하던게 모두 날라간다. 이런 이유들 때문에 라우터를 사용한다.

## 라우터 종류

1.HashRouter

구조: ```https://mysite.com/#/about```

**특징**

주소에 #이 붙는다.    
검색엔진이 읽지 못한다.    
별도의 서버 설정을 하지 않아도 우류가 발생하지 않는다.     
history api를 사용하지 않아서 동적 페이지에 불리하다.

### 새로고침을 해도 404에러가 나지 않는이유

브라우저는 새로고침을 하면 # 뒷부분을 떼고 요청을 보낸다. 그래서 서버는 페이지를 잘 전달한다. 그후 페이지가 로드되면 # 뒤에 about이 붙어있는걸 보고 About컴포넌트를 띄운다

### 해시 라우터의 장단점

**장점**
* 배포가 매우 쉽다: 서버 환경을 마음대로 제어할 수 없는 무료 호스팅 사이트나 정적 파일 스토리지만 제공하는 환경에 좋다.    
* 안정적이다: 주소가 어떻게 바뀌든 무조건 서버는 루트만 바라봐서 경로 이탈 에러가 절대 나지 않는다.  
 
**단점**
* 주소가 못생김: 주소창 중간에 갑자기 # 이 들어가서 비전문적이고 지저분해 보일수있다.
* 검색엔진이 읽지 못함: 구글이나 네이버같은 검색로봇은 # 뒷부분을 인식하지 않거나 무시하는 경우가 많다.즉, 아무리 좋은글을 써도 검색엔진 결과에 안뜰수있다.

## history api란?

사용자의 방문기록을 조작할수있는 자바스크립트 기능이다. html5가 아닐때는 자바스크립트 코드로 마음대로 바꾸는 것이 불가능했는데 html5가 나오면서 페이지 새로고침없이 주소만 코드로 바꿀수 있는 기능이 추가되었는데 이게 **History API**이다.

2.BrowserRouter

구조: 
가장 표준라우터 # 을 붙이지 않는다, 우리가 흔히 보는 깔끔하고 직관적인 url을 만들어 준다.
브라우저 라우터는 html내장 기능인 history api를 사용한다. 별도의 서버설정이 없으면 새로고침시에 404에러가 뜬다.해결책은 에러를 내지말고 메인 파일을 보여달라는 **Fallback설정**을 추가해 주어야한다.

### 브라우저 라우터의 장단점

**장점**
* 주소가 깔끔하고 직관적    
해시 라우터와 달리 브라우저 라우터는 주소가 깔끔하게 떨어진다.
* 검색엔진에 유리함      
구글,네이버등의 검색 로봇들은 웹사이트의 주소 구조를 따라 페이지를 수집한다.브라우저 라우터같은 정석적인 주소 구조여야 검색 로봇이 각 페이지를 제대로 인식하고 결과에 노출한다.

**약점**
* 새로고침시 발생하는 404에러    
해결하기 위해서는 리다이렉션 설정을 추가해야한다.

Fallback이란: 원래 하려던 기능이나 계획이 실패하거나 작동하지 않을 때, 시스템 중단을 막고 서비스 연속성을 유지하기 위해 대신 사용하는 대체 동작, 값 또는 기술을 말함. 예를 들어, 5G에서 통화가 원활하지 않을때 LTE로 변환해서 통화가 안끊기게 하는 방법을 말함.


## React-Router-Dom
React로 생성된 SPA내부에서 페이지 이동이 가능하도록 만들어주는 라이브러리

## 세팅하기

```import { BrowserRouter, Routes, Route } from 'react-router-dom```

#### 가장 많이 사용되는 모듈 3가지

**BrowserRouter**
* history api를 활용해 history객체를 생성한다.
* history api는 내부적으로 **스택** 형태를 띄기 때문에 사용자가 방문한 url기록들을 쌓아놓는 형태로 저장한다고 생각하면 된다.
* 라우팅을 진행할때 컴포넌트 상위에 BrowserRouter 컴포넌트를 생성하고 감싸야한다. 라우팅을 적용할 부분을 감싸주는 울타리 역할을 한다.

**Routes**
* 여러 개의 후보(Route) 주소들중에, 현재 주소창에 입력된 주소와 맞아떨어지는 하나만골라낸다.
* 브라우저 주소창이 ```/profile```로 바뀌면 Routes는 자신의 자식 즉,Route를 쭉 훑는다.
그후 매치되는 값을 찾아 화면을 보여준다

**Route**
* Route혼자는 아무것도 못 하고,부모인 Routes와 함께 쓰인다.
```<Route path="주소경로" element={<보여줄컴포넌트 />} />```    
* path: 브라우저의 주소창의 주소와 비교할 **기준 주소**이다.    
* element: 주소창과 path가 일치하면 화면에 띄워줄 컴포넌트 이다.


```const Router = () => {
  return (
    <BrowserRouter>
        <Routes>
          <Route path="/" element={<GalleryPage />} />
          <Route path="/gallery" element={<DetailCardPage />}>
            <Route path=":cardId" element={<DetailCard />} />
          </Route>
        </Routes>
    </BrowserRouter>
  );
};
```

위 코드가 기본설정 코드인데 해석을 해보면    
1. ```<BrowserRouter>``` -> 브라우저 라우터 기능을 사용할거라고 울타리 치기
2. ```<Routes>``` -> 아래에 있는 여러 주소중, 형재 사용자의 주소창에 적인 주소와 일치하는 하나를 고르기 위해 기다리는 태그   

**Route**

* ```<Route path="/" element={<GalleryPage />} />```     
사용자가 홈 주소(mysite.com/)로 들어오면, GalleryPage페이지를 출력해라는 뜻이다.

```
 <Route path="/gallery" element={<DetailCardPage />}>
  <Route path=":cardId" element={<DetailCard />} /> 
</Route>
```

* path="/gallery" -> 사용자가 ```mysite.com/gallery```주소로 들어오면 일단 ```DetailCardPage```컴포넌트를 화면에 띄웁니다.
* path=":cardId" -> 이것은 부모 주소뒤에 붙는 자식 주소이다. 콜론이 붙어있으므로 어떤 글자든 다 들어올수있는 변수 주소이다. 만약 주소창이 ```/gallery/5```에서 ```/gallery/6```으로 바뀔때 부모는 가만히 놔두고 자식만 바꿔서 화면을 출력한다.

위와 같이 Router컴포넌트를 생성한후,

```
import Router from "./Router";

const App = () => (
  <>
      <Router />
  </>
);

export default App;
```
상위 랜더링 요소에 컴포넌트를 붙여준다.


이것도 코드해석을 해보면     
* ```import Router from "./Router";```
-> 전에 만든 BrowserRouter, Routes, Route 파일들을 통째로 들고 온다는 뜻이다.    
* ```<Router />```
-> 들고 온 주소 부품들을 App이라는 곳에 올린것이다. 이렇게 해두면 웹사이트가 켜지자마자 주소가 ```/```이면 갤러리 메인을, ```/gallery/5```이면 상세 카드를 자리에 알아서 그려주게 된다.

이렇게 상위 렌더링 요소에 컴포넌트를 붙여준다.


## Link

Link컴포넌트란 라우터 내에서 직접적으로 페이지 이동을 하고자 할때 사용되는 컴포넌트이다.


```
import React from 'react';
import {Link} from 'react-router-dom';

function Nav(){
  return (
    <div>
      <Link to='/'> Home </Link>
      <Link to='/about'> About </Link>
    </div>
  );
}

export default Nav;
```
위 같은 방식으로 ```to```속성에 경로를 넣어주는 방식으로 사용한다.

### Link컴포넌트 특징

1. Relative
* 현재 있는 위치를 기준으로 이동하는것, 예를 들어 현재 주소가 ```/board```인데 ```<Link to="/login">로그인</Link>``` 이코드를 만나면 무조건 ```/login```으로이동한다.        
그리고 만약 ```/```이 없고 그냥 ```detail```이라고 쓰여있으면 ```/board/detail```이 된다.      
마지막으로 ```.```이나```..```을넣으면 리눅스와 윈도우 폴더와 같기 때문에 ```.```은 현재주소 ```..```은 한단계 전 화면으로 돌아간다

2. preventScrollReset
* 페이지를 이동했을 때 스크롤 위치를 맨 위로 초기화하지 않을지 정하는 속성이다.    
기본적으로 React Router는 다른 페이지로 이동하면 스크롤이 위로 올라가는 방식으로 동작할 수 있다.    
그런데 특정 상황에서는 이동 후에도 현재 스크롤 위치를 유지하고 싶을 수 있다. 그럴 때 사용한다.

```
<Link to="/gallery" preventScrollReset={true}>
  갤러리로 이동
</Link>
```

이렇게 쓰면 `/gallery`로 이동하더라도 스크롤 위치를 무조건 맨 위로 보내지 않는다.

3. replace
* 이동 기록을 새로 쌓지 않고, 현재 주소 기록을 바꿔치기하는 속성이다.    
보통 Link를 누르면 브라우저 방문 기록에 이전 페이지가 남는다. 그래서 뒤로가기 버튼을 누르면 이전 페이지로 돌아갈 수 있다.    
하지만 `replace`를 사용하면 이전 기록을 남기지 않고 현재 기록을 새 주소로 교체한다.

```
<Link to="/login" replace>
  로그인 페이지로 이동
</Link>
```

예를 들어 사용자가 `/signup`에서 `/login`으로 이동했는데, 뒤로가기를 눌렀을 때 다시 `/signup`으로 돌아가면 안 되는 상황이라면 `replace`를 사용할 수 있다.

4. state
* 주소에는 보이지 않는 데이터를 다음 페이지로 같이 넘길 때 사용하는 속성이다.    
주소창에는 `/gallery/5`처럼 보이지만, 실제로는 클릭한 카드의 정보 같은 데이터를 함께 넘길 수 있다.

```
<Link
  to="/gallery/5"
  state={{ title: "첫 번째 카드", cardId: 5 }}
>
  상세보기
</Link>
```

넘긴 데이터는 이동한 페이지에서 `useLocation`으로 받을 수 있다.

```
import { useLocation } from "react-router-dom";

function DetailCard() {
  const location = useLocation();

  console.log(location.state);

  return <div>상세 페이지</div>;
}
```

이때 `location.state` 안에 `{ title: "첫 번째 카드", cardId: 5 }`가 들어있다.    
다만 새로고침을 하거나 직접 주소를 입력해서 들어오면 `state` 값이 없을 수도 있기 때문에, 중요한 데이터는 주소 파라미터나 서버 데이터로 관리하는 것이 더 안전하다.

5. reloadDocument
* React Router 방식이 아니라 일반 `a` 태그처럼 페이지 전체를 새로고침하면서 이동하고 싶을 때 사용하는 속성이다.

```
<Link to="/gallery" reloadDocument>
  갤러리로 이동
</Link>
```

보통은 잘 사용하지 않는다.    
React Router를 쓰는 이유가 새로고침 없이 화면을 바꾸기 위해서이기 때문이다.    
하지만 정말로 문서 전체를 다시 불러와야 하는 특별한 상황에서는 사용할 수 있다.

## 중첩 라우팅

React-router-dom 내장 기능 중 가장 유용하게 사용되고 있는 기능이다. 특정 페이지 내에서 하위 페이지를 만들 수 있고, 해당 페이지마다 경로를 이용한 데이터 전달도 가능하다.

또한 중첩 라우팅을 구현할 경우 해당 하위 페이지 이외에는 컨텐츠가 바뀌지 않는다.

```
<Route path="/about" element={<About />}>
  <Route path="location" element={<Location />}></Route>
</Route>
```

라우터 내부에 위와 같이 자식 요소 Route를 만들어준다.  설정해도 라우터 내부적으로는 `/about` 주소 하위에 `/location` 이라는 하위 라우팅이 되었다고 판단한다. 따라서 우리가 `/about/location`으로 주소를 이동할 경우, 주어진 `Location` 컴포넌트가 렌더링되는 것이다. 물론 `About` 컴포넌트도 같이 렌더링된다.

물론 라우터에서 위와 같이 설정한 것 만으로는 아무런 변화가 생기지 않는다.

실제로 해당 라우팅이 발생하는 부모 요소인 `About` 페이지에 하위 라우팅 발생 시 컴포넌트를 렌더링할 자리를 명시해주어야 하기 때문이고, 이때 사용되는 것이 `Outlet` 컴포넌트이다.

## Outlet

```
import { Outlet } from 'react-router-dom';

function About() {
  return (
    <div>
      <div>
        <h2>여기는 About 페이지입니다.</h2>
        <p>대충 쇼핑몰 페이지라는 뜻</p>
      </div>
      <Outlet />
    </div>
  );
}
```

이처럼 `About` 컴포넌트 내부에 `Outlet` 컴포넌트를 렌더링해주면 라우터에서 이를 인식하고 `Outlet` 자리에 `Location` 컴포넌트를 렌더링하게 되는 것이다. 물론 주소가 일치하는 경우이다.

## Outlet 없이 중첩 라우팅 구현하기

`Outlet` 없이도 중첩 라우팅을 구현할 수 있다.

우선 라우터에서 중첩 라우팅을 하고자 하는 주소에 다음과 같이 `*`을 추가해주어 중첩 라우팅이 발생할 주소임을 명시해준다.

```
<Routes>
  <Route path="/" element={<Home />}></Route>
  <Route path="/about/*" element={<About />}></Route>
  <Route path="/products" element={<Products />}></Route>
</Routes>
```

이후 해당 `About` 컴포넌트에서 본래 `Outlet`이 들어갔던 자리에 마치 라우터를 구현했던 것처럼 중첩 라우팅을 진행해주면 된다.

```
function About() {
  return (
    <div>
      <div>
        <h2>여기는 About 페이지입니다.</h2>
        <p>대충 쇼핑몰 페이지라는 뜻</p>
      </div>
      <Routes>
        <Route path="/location" element={<Location />}></Route>
      </Routes>
    </div>
  );
}
```

위와 같이 작성하면 `Outlet`과 동일한 기능을 하는 중첩 라우팅을 구현할 수 있다.

## Params

주소 경로 내부에 특정 데이터를 넣어 전달하는 것을 말하는데, 크게 url 파라미터와 쿼리스트링으로 나누어진다.

### url 파라미터

주소: `http://hello.com/new/1234`

```
<Route path="/new/:id" element={<NewId />} />
```

여기에서 `:`으로 구분해준 `id`라는 값은 파라미터로 전달되어 이후 우리가 `NewId` 컴포넌트 내부에서 `useParams`훅을 통해 추출하고 사용할 수 있다. 이때 전달된 값은 `1234`가 된다.

### 쿼리스트링

`?`, `&`을 기준으로 key와 value를 나눠 데이터를 전달받는다. 이렇게 전달 받은 값은 이후 `useLocation`훅을 통해 추출하고 사용할 수 있다.

이전까지는 `?`, `&`을 직접 분리해 추출해야하는 번거로움이 있었는데, `useSearchParams`를 사용하면 쉽게 해결할 수 있다.

### url 파라미터 VS 쿼리스트링

| url 파라미터 | 쿼리 스트링 |
| --- | --- |
| ID, 이름, 특정 데이터를 조회할때 사용 | 키워드 검색, 페이지네이션, 정렬방식 등 데이터 조회에 필요한 옵션을 전달할 때 사용 |
| 일반적인 변수, 상수 값들을 전달하기 용이 | key, value 형태의 데이터이므로 json이나 객체 형태의 데이터를 전달하기 용이 |

## useParams

위에서 말한 것처럼 url 파라미터를 조회할 때 사용한다.

실제 사용 예시를 살펴보자.

```
import React from 'react';
import { useParams } from 'react-router-dom';

const NewId = () => {
  let { id } = useParams();

  return (
    <div className="test">
      <p>현재 유저의 아이디는 { id } 입니다.</p>
    </div>
  )
}

export default NewId;
```

이처럼 `http://hello.com/new/1234`의 주소로 이동하여 렌더링된 `NewId` 컴포넌트 내부에서 `useParams`를 이용해 아이디 값을 받아올 수 있다.

`http://hello.com/new/1234/1212`와 같은 주소에 라우팅을 `/new/:id/:lastId`와 같은 방식으로 해준다면 여러 개의 값도 한 번에 전달받을 수 있다.

## useSearchParams

위에서 언급한 것처럼 쿼리스트링을 추출하는 데 사용된다. 현재 위치에 대한 url의 쿼리스트링을 읽고 수정할 때 사용한다.

`useState`와 사용법이 유사하므로 처음 적용하기 어렵지 않다.

```
const [searchParams, setSearchParams] = useSearchParams();
```

`searchParams`는 `URLSearchParams` 객체이면서 쿼리스트링을 다루기 위한 다양한 메서드를 내장하고 있다.

`setSearchParams`는 함수의 인자에 객체와 문자열을 넣어주면 현재 url의 쿼리스트링을 변경하는 기능을 제공한다.

자주 사용하는 메서드를 살펴보자.

### 값을 읽어오는 메서드

* `searchParams.get(key)`: 특정한 key의 value를 가져오는 메서드, 해당 key의 value가 두 개 이상이라면 처음의 값을 반환한다.
* `searchParams.getAll(key)`: 특정 key에 해당하는 모든 value를 가져오는 메서드

### 값을 변경하는 메서드

* `searchParams.set(key, value)`: 인자로 전달한 key 값을 value로 설정한다. 만일 기존에 key에 대한 값이 존재했다면 덮어씌운다.
* `searchParams.append(key, value)`: 기존 값을 변경 혹은 삭제하지 않고 추가한다.

`searchParams`를 변경하는 메서드로 값을 변경하더라도 실제 url에는 이 정보가 반영되지 않는다. 만일 이를 반영하고자 한다면 `setSearchParams`에 `searchParams`를 인자로 전달해주어야 한다.





 

 .0.
 




































