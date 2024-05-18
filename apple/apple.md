# apple 제품 카드

그리드를 사용하여 구현하고 구현 결과를 움직이는 이미지로 생성하여 삽입해주세요.

GIF파일이 너무 용량이 커서 아래와 같이 링크 첨부합니다.

![결과물](https://youtu.be/Nubkvpzw_0Y?si=jqCZbD14k0plbw5z)

# 테킷 FES homework - Apple 프로젝트

- ## 구조 설계

  HTML 손 마크업

  <img src="/images/image for md/마크업1.jpg" width="100%" title="HTML 손 마크업1" alt="markupImage"></img><br/>
  <img src="/images/image for md/마크업2.jpg" width="100%" title="HTML 손 마크업2" alt="markupImage"></img><br/>

<details>
<summary>과제 요구사항</summary> 
<div markdown="1">

과제는 다음과 같은 조건을 만족할 수 있도록 구현한다.

- `CSS Grid`를 사용하여 **반응형 레이아웃**을 구현한다.
- 중단점(breakpoint)은 `1024px` 로 지정한다.
  (Small Screen - 1024px 이하 / Large Screen - 1024px 이상)
- `theme.css` 파일에 제공 된 값(색상, 텍스트 크기, 여백 등)을 사용한다.
- 이미지는 배경으로 마크업(viewport의 width에 따라 배경 이미지가 달라질 수 있도록 구현)

</div>
</details>

---

### 0. HTML 구조

보이는 HTML 구조는 다음과 같습니다.

```html
<body>
  <h1 class="sr-only">제품 카드 목록</h1>
  <div class="card-container">
    <!-- 상단 섹션 묶음 -->
    <div class="upper-section">
      <!-- 첫번째 카드 -->
      <div class="card-wrapper">
        <article class="card card-1 dark">
          <h2 class="product-name">iPad Pro</h2>
          <p class="explanation">
            놀라우리만치&nbsp;얇다.<br class="small" />
            엄청나게&nbsp;강력하다.
          </p>
          <p class="release-date">출시일 추후 공개</p>
          <ul>
            <li class="more"><a href="#" class="btn">더 알아보기</a></li>
            <li class="price"><a href="#" class="btn price">가격 보기</a></li>
          </ul>
        </article>
      </div>
      (후략)...
    </div>
  </div>
</body>
```

- `<h1>`에 `sr-only` 클래스를 부여하여 시각적으론 보이지 않지만 접근성을 고려하여 선언하였습니다.

- 카드 컴포넌트를 화면에 배치할 때, `div.upper-section`, `div.lower-section`으로 나누어 크기에 따라 다른 화면을 구성할 수 있도록 나누었습니다.
  <br/>

- 카드 컴포넌트를 묶는 `div.card-wrapper`를 통해 컨테이너의 크기에 따라 출력되는 이미지, 폰트가 달라질 수 있도록 하였습니다. 더불어 카드마다의 이미지를 달리 불러오기 위해 `card-$`형태의 클래스를 각각 선언하였습니다.
  <br/>

- `article`의 클래스에 `dark` 또는 `light`를 부여하여, 해당 클래스에 따라 버튼, 폰트색상 등이 변화할
  수 있도록 기준점을 설정하였습니다.
  <br/>

- 첫번째 카드의 경우 화면 크기에 따라 `<br>` 부분이 나타나고 사라짐에 따라 이를 구현하기 위해 `class`를 할당하였습니다.
  <br/>

- 버튼 형태를 `ul`로 구성하였으나, 제출 이후 버튼으로 재구성할 계획입니다. 현 단계에선 `li` 요소 속에 `a`를 할당하여 구성하였습니다.
  <br/>

### 1. 카드 컴포넌트 (`card-component.css`)

손 마크업 순서대로, 우선 **카드컴포넌트를 설계**하였습니다. `card-component.css` 파일을 별도로 생성하여 `apple.css`에 `@import`하여 사용할 수 있도록 설정하였습니다.

<br/>

- 컨테이너를 선언하여 이후 선언될 카드 컴포넌트가 그 크기에 따라 배경이미지, 폰트 등 변화할 수 있도록 하였습니다.
  ```css
  /* Small Screen 기준 먼저 */
  .card-wrapper {
    container-type: inline-size;
    ...;
  }
  ```

<br/>

- 카드 컴포넌트 부분입니다. 먼저 디폴트로 다크테마를 적용한 카드를 선언하였습니다. 카드 내 서식은 요구사항에 따라 **Grid 로 선언**하였으며, 가운데로 정렬하였습니다. 카드 내 배경이미지는 반복되지 않으면서 가운데 정렬되고, 컨테이너 크기에 맞도록 `cover`로 선언하였습니다. 기본 폰트 색상은 **화이트**로 선언하였습니다.

  ```css
  /* 카드 공통 기본 서식 설정(디폴트: 다크) */
    .card {
      padding-top: var(--large-spacing);

      height: var(--size);
      block-size: var(--size);

      /* 카드 내 서식 */
      display: grid;
      grid-template-rows: repeat(12, 1fr);
      grid-template-columns: 1fr;
      justify-items: center;
      gap: var(--small-spacing);

      /* 카드 내 배경이미지 */
      background-repeat: no-repeat;
      background-position: center;
      background-size: cover;
      color: var(--white);
  ```

<br/>

- 카드 내부요소(제목, 부제목, 출시예정)에 관련된 부분입니다. 그리드 상 순서에 따라 배치될 수 있도록 `order` 속성을 사용하여 정렬될 수 있도록 하였습니다. 제목, 부제목, 출시일은 각각 요구사항에 따른 폰트크기와 자간, 색상을 적용하였습니다.

  ```css
  /* 카드 내부 요소 스타일 정의 */
  /* 제품명 */
  h2 {
    order: 1;
    font-size: var(--large-text);
  }

  /* 설명, 출시일 */
  p {
    order: 2;

    &.explanation {
      font-size: var(--base-text);
      line-height: var(--line-normal);
    }

    &.release-date {
      order: 3;
      font-size: var(--small-text);
      color: var(--gray);
    }
  }
  ```

<br/>

- 버튼 관련 요소입니다. 앞서 말씀드린대로 `li` 안에 `a`요소로 선언한 탓에 `li`크기를 버튼사이즈로 설정하여 구성하였습니다. 이 때문에 `a`요소의 크기만큼만 하이퍼링크가 먹히고 있습니다. 이 부분도 그리드를 활용하느라 스스로 한계에 부딪혔던 것 같습니다. (`div` 속 `button`으로 선언하여 `flex`를 활용하였다면 바로 했을수 있었겠으나, 이번 과제 목적과는 다르다고 생각해 우선 `grid`로 시도하였습니다.)

  ```css
  ul {
    order: 4;
    display: grid;
    grid-template-columns: 1fr 1fr;
    align-items: center;
    justify-items: center;

    gap: var(--base-spacing);
    font-size: var(--xx-small-text);

    /* 기본 포맷 설정 */
    li {
      padding: var(--x-small-spacing) var(--small-spacing);
      background-color: var(--blue-300);
      border: 1px solid var(--blue-300);
      border-radius: 1rem;

      &:hover {
        background-color: var(--blue-200);
      }
    }

    li.price {
      background-color: transparent;
      a {
        color: var(--blue-200);
      }

      &:hover {
        background-color: var(--blue-200);
        a {
          color: var(--white);
        }
      }
    }
  }
  ```

  - `Grid`로 선언하여 포맷을 배치하였고, `li`(더 알아보기) 요소의 기본포맷을 설정하였습니다.
  - `hover`를 통해 마우스를 올라면 색상이 변화하도록 설정하였고, `li.price`(가격 보기) 부분은 별도의 색상을 띌 수 있도록 하였습니다.

<br/>

- 카드 컴포넌트의 테마를 `light`로 설정하였을 때 다른 색상을 띄도록 설정한 코드 부분입니다.

  ```css
  /* 라이트 모드 카드 기본 서식 설정  */
  .light {
    color: var(--black);

    /* 카드 내부 요소 스타일 정의 */

    /* 버튼들 */
    ul {
      li {
        background-color: var(--black);
        border: 1px solid var(--black);
        border-radius: 1rem;
        color: var(--white);

        &:hover {
          background-color: var(--black-focused);
        }
      }

      li.price {
        background-color: transparent;
        a {
          color: var(--black);
        }

        &:hover {
          background-color: var(--black-focused);
          a {
            color: var(--white);
          }
        }
      }
    }
  }
  ```

<br/>

- 카드 종류에 따라 다른 배경이미지를 띄도록 설정하였습니다.

  ```css
  /* 카드 종류 따른 변화 */
  .card-1 {
    background-image: url(/apple/products/ipad_pro.jpeg);
  }

  .card-2 {
    background-image: url(/apple/products/ipad_air.jpeg);
  }

  .card-3 {
    background-image: url(/apple/products/iphone15_pro.jpeg);
  }
  ```

  <br/>

- 컨테이너의 크기에 따라 보여지는 결과가 달라질 수 있도록 `@container`를 사용하였습니다.

  ```css
  /* 컨테이너 사이즈에 따른 배경이미지 조절 */
    @container (min-width: 1024px) {
      .card {
        padding-top: var(--extra-large-spacing);
      }
      .card h2 {
        font-size: var(--extra-large-text);
      }

      .card .explanation {
        font-size: var(--medium-text);
      }

      .card ul {
        font-size: var(--x-small-text);
      }

      .card-1 {
        background-image: url(/apple/products/ipad_pro_wide.jpeg);
      }
      .card-2 {
        background-image: url(/apple/products/ipad_air_wide.jpeg);
      }
      .card-3 {
        background-image: url(/apple/products/iphone15_pro_wide.jpeg);
      }

  ...(후략)
  ```

<br/>

### 2. `apple.css` 의 upper-section, lower-section

`apple.css`에선 카드컴포넌트의 배열만 처리할 수 있도록 설계하였습니다. 때문에 `upper-section`에선 상단 부분(상위 카드 3개 부분)의 디스플레이만을, `lower-section`에선 2행 2열로 배열되는 부분의 디스플레이만을 담당하고 있습니다.

- 카드 레이아웃 부분입니다. 각 섹션의 기본구조를 정의하였습니다.

  ```css
  /* 카드 레이아웃 */
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  .upper-section {
    display: grid;
    gap: 1rem;
    padding-bottom: 1rem;
  }

  .lower-section {
    display: grid;
    /* 임시 지정 */
    gap: 1rem;
  }
  ```

<br/>

- 중단점 기준으로 레이아웃에 변화를 줄 수 있도록 `@media`를 사용하였습니다. `minmax`를 사용하여 최소 레이아웃에서 카드가 그 크기를 유지할 수 있도록 `200px`로 설정하였습니다. 더불어 중단점 기준으로 첫번째 카드의 내용 부분이 **두줄에서 한줄로 변화하는 부분**을 구현하였습니다.

  ```css
  /* 중단점 설정 */

  @media (max-width: 1024px) {
    .upper-section {
      grid-template-columns: minmax(200px, 1fr);
    }

    .lower-section {
      grid-template-columns: minmax(200px, 1fr);
    }

    br.small {
      display: inline;
    }
  }

  @media (min-width: 1024px) {
    .lower-section {
      grid-template-columns: 1fr 1fr;
    }

    br.small {
      display: none;
    }
  }
  ```

---

#### 참고사항

수업시간에 워낙 해당 과제 관련한 비슷한 실습을 많이 해주셔서, 큰 도움이 되었습니다.
그 외에 참고한 사이트는 다음과 같습니다.

- [애플 공식 홈페이지](https://www.apple.com/kr/)에서 개발자 도구를 통해 구현되어있던 레이아웃을 파악하였습니다. `upper-section`과 `lower-section` 구분하는 데에 힌트를 이를 통해 얻었습니다.
- [Inpa Dev](https://inpa.tistory.com/entry/%F0%9F%8C%9F-css-container-%EC%82%AC%EC%9A%A9%EB%B2%95)사이트를 통해 미디어쿼리와 컨테이너쿼리에 대해 조금 더 자세히 살펴볼 수 있었습니다.
- [1분코딩](https://studiomeal.com/archives/533)의 '이번에야말로 CSS Grid를 익혀보자' 에서 Grid와 관련된 속성들을 좀 더 탐구할 수 있었습니다.

---

#### 배운 것들 및 추가 공부가 필요한 것들

- `@container` 부분을 복습을 통해 알았다고 생각했는데, 결과물에서 제대로 적용되지 않은 것을 보아 조금 더 학습이 필요한 것 같습니다.
- `minmax()` 는 `grid-template-rows/columns` 에서만 사용되고 있다.
- `gap`은 그리드나 플렉스 내부의 컨텐츠 간의 간격을 설정한다.
- `@container`의 `screen`을 선언하는 부분은 범위로도 나타낼 수 있는지 확인이 필요하다. `@media`에선 `(min-width: 601px) and (max-width: 1024px)`처럼 나타낼 수 있지만 컨테이너 쿼리에서도 동일하게 작동하는지 확인이 필요하다. 더불어 `>`, `<`같은 연산자가 동작하는지 확인이 필요하다. 안되는 것으로 알고있기는하다. 스크린 크기를 나타내기 위해 수치입력 부분에 `var()`를 사용하려했으나 먹지 않는 것을 확인하였다.
- 속성 선택자에 대해 조금 더 공부할 수 있는 시간이었다. 분명 접근 가능할 것이라 생각했던 요소에 접근하지 못하는 상황이 자주 발생하였다. 어느 요소에 선언해야 올바르게 접근할 수 있는지 다시 돌아보는 시간이었다.
- Web Developer 애드온을 최대한 활용할 기회였다.하지만 CSS부분에서 가끔 동작이 멈추는 경우가 잦았다.
- 코드가 번잡해질수록 접근성에 관해 고려하는게 많이 어렵습니다. 아직 WAI-ARIA 관련 속성사용에 미숙하여 연습이 필요한 듯 합니다.

---

#### 질문사항

- 쿼리에서 스크린의 범위를 지정하는 값으로 `var()`값이 적용되지 않는 이유
- 배경에서는 `picture`와 `img`에서처럼 `srcset`으로 여러 브라우저에 대해 적용가능한 이미지셋을 세팅가능한데 `background`에선 이는 어려운 것으로 알고 있습니다. 이번 과제에선 이를 어떻게 활용했어야했는지 여쭙습니다. 그냥 이미지의 크기에 따라 중단점을 생성하여 구현했어야했는지 여쭙습니다.

---
