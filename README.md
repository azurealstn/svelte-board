## 실행하기

1. 다운받아서 압축 풀기

```javascript
Download ZIP
```

2. VS code 열기

```javascript
확장 프로그램 설치:
Svelte for VS Code
```

3. 라이브러리 설치

```javascript
npm install
```

4. 실행하기

```javascript
npm run dev
```

# Svelte

Svelte(스벨트)는 컴파일러 기반으로 실행되는 프레임워크입니다. 이는 Virtual DOM이 없고, Runtime에 로드할 프레임워크가 없음을 의미합니다.

## Svelte 주요 특징과 장점

그러면 Svelte의 주요 특징과 장점을 알아봅시다.

### 1. Write less code!

적은 코드로 개발 시간을 단축시키고, 러닝 커브가 낮습니다. 다음은 프레임워크별로 코드 길이를 나타냅니다.

#### Svelte

```javascript
<script>
  let a = 1
  let b = 2
</script>

<input type="number" bind:value={a} />
<input type="number" bind:value={b} />
<p>{a} + {b} = {a + b}</p>
```

#### React

```javascript
import React, { useState } from 'react'

export default function () {
  const [a, setA] = useState(1)
  const [b, setB] = useState(2)

  function handleChangeA(event) {
    setA(Number(event.target.value))
  }
  function handleChangeB(event) {
    setB(Number(event.target.value))
  }

  return (
    <div>
      <input type="number" value={a} onChange={handleChangeA} />
      <input type="number" value={b} onChange={handleChangeB} />
      <p>{a} + {b} = {a + b}</p>
    </div>
  )
}
```

#### Vue

```javascript
<template>
  <div>
    <input type="number" v-model.number="a" />
    <input type="number" v-model.number="b" />
    <p>{{a}} + {{b}} = {{a + b}}</p>
  </div>
</template>

<script>
  export default {
    data: function() {
      return {
        a: 1,
        b: 2
      }
    }
  }
</script>
```

### 2. No Virtual DOM

Svelte는 Virtual DOM을 사용하지 않습니다. Virtual DOM은 필요한 부분만 DOM에 조작함으로써 충분히 빠르고 유용하지만 Svelte는 런타임이 아닌 컴파일 타임에 빌드되면서 DOM 구성이 완료된다. Virtual DOM을 생성하고 비교하는 연산과 실제 DOM에 업데이트해야 하는 과정이 생략되어 리액트보다 렌더링 속도가 빠르다.

> Virtual DOM이란 초기에 Virtual DOM을 생성하고 Snapshot으로 남겨서 이전 Snapshot과 비교한다. 변경이 생기면 변경된 부분(요소)만 Real DOM에 반영하게 된다.

### 3. 반응성

반응성은 변경된 값이 DOM에 자동으로 반영됨을 의미합니다. Svelte는 별도의 Setter 없이 값의 할당만으로 업데이트를 트리거할 수 있습니다. 이렇게 상태를 유지할 수 있는 이유는 컴파일시 스벨트라는 프레임워크가 대신 해줍니다. 따라서 개발자는 React의 `useState()`와 같은 Hook 내장 API를 따로 사용할 필요없이 순수 js 코드 짜는 것처럼 작성할 수 있습니다.

## 현재 프로젝트 구성

현재 프로젝트는 매우 단순하게 개발하였습니다.

### 1. Vite를 이용한 프로젝트 생성

Vite(비트)를 이용해서 프로젝트 초기 세팅을 하였습니다.

> Vite란 Vue 창시자가 만든 "빠르다"를 의미하며, 프로젝트 빌드 도구로써 기존 웹팩보다 수십배 빠릅니다. Vite는 로컬에서 번들링을 하지 않고 필요시 rollup.js를 사용합니다.

### 2. 컴포넌트 구성

`/src/components/` 디렉토리에 관리되며, 반복되는 부분이 있으면 컴포넌트를 만들어서 import하여 사용합니다.

### 3. 라우팅 설정

사용할 페이지들은 `/src/pages/` 디렉토리에 관리되며, 라우팅 설정 파일은 `routes.svelte`에 있습니다.

### 4. 기능 구현

REST API 통신하기 위해 `axios` 라이브러리를 사용하였고, 비동기 통신은 `async`, `await` 문법을 사용하였습니다. 현재 구현은 `/src/pages/DataModel.svelte`만 되어 있으며, 기능은 게시판 목록, 페이지네이션, 검색입니다.

[Data Hub swagger](http://222.107.32.38:48083/swagger-ui/index.html)에 있는 API는 CORS 에러가 나서 당장 사용을 못했고, 예시로 제공해주는 API를 가져다 사용하였습니다.

## 만들면서 어려웠던 점

### 1. 컴포넌트 구성

프론트 프레임워크 사용을 해본 경험이 적다보니 컴포넌트 분리를 어떻게 해야할지 고민

### 2. UI 프레임워크

- Flowbite
- Material UI
- Tailwind CSS

등등 많지만 실제 적용하는데 어려움이 있었음. 사용 방법이나 커스터마이징하기 쉽지 않았음.

### 3. API 통신

API 통신할 때 반복되는 코드들이 있는데 이를 어떻게 하면 통일해서 사용할 수 있는지 고민 필요

### 4. 상태관리

- 전역상태를 어떻게 관리할지 고민 필요 
- (스벨트에도 Store라는 API 제공하며, 전반적으로 학습이 필요함 - 패턴이 있는 것 같음)

### 5. 개발 환경

- 테스트 환경을 구축해야 하는데 현재 Swagger API 통신을 하면 CORS 에러가 발생해서 테스트가 힘듬.

## React VS Svelte

- Svelte가 구글 검색에 자료가 많이 없는 것은 사실입니다.
- 하지만 Svelte 역시 React, Vue와 같은 SPA 프레임워크로 사용하는 방법을 숙지하고, 하나의 페이지에 대해 컴포넌트를 만들고 CRUD 개발을 해놓으면 나머지 개발 역시 참고하여 해나갈 수 있을 것으로 보입니다.
- 요즘은 Svelte를 사용한다면 SvelteKit과 같이 사용합니다. (SvelteKit을 사용하면 다양한 플러그인도 제공)

> SvelteKit은 웹 애플리케이션을 구축하기 위한 프레임워크로써 서버 측 렌더링(SSR), 라우팅 및 API 호출을 쉽게 호출할 수 있습니다. 예를 들어 React의 Nextjs나 Vue의 Nuxtjs 같은거라고 생각하면 됩니다.