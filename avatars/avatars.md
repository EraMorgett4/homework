# 테킷 FES homework - Avatars 프로젝트

![죽겠어요..이미지](../images/image%20for%20md/EqHrn.webp)

~~"(5월 4일 자정이 5/4 00시인줄 알았던 사람의 최후)"~~

<details>
<summary>과제 요구사항</summary> 
<div markdown="1">

- ### 조건

  - 아바타 이미지는 배경색상이 아닌, 콘텐츠 이미지(`<img>` 요소)로 마크업 한다.
  - 아바타의 상태 정보를 알 수 있도록 정보를 제공한다.
  - 아바타 이미지의 크기 : 64px &#215; 64px
  - 아바타 이미지 간의 간격 : 20px
  - <span style="background-color:#DBDBDB">회색</span> 원 배경색 : `#DBDBDB`
  - <span style="background-color:#4CFE88">초록색</span> 원 배경색 : `#4CFE88`
    <br/>

- `float`를 사용하여 다음의 레이아웃을 구현하라.

![result1](../images/image%20for%20md/result1.png)
<br/>

- `flex`를 지원하는 환경에선 다음의 레이아웃을 구현한다.

![result2](../images/image%20for%20md/result2.png)

- 아바타 과제 수행에 대한 설명을 `avatars.md` 파일에 작성하고 `homework` 폴더에 있는 `README.md`에 링크로 연결한다.
- 과제는 `5월 4일 자정`까지 Github 저장소에 Push한다.

</div>
</details>

---

## 1. avatars.html

여러 아바타 이미지와 그 상태를 나타내는 인터페이스를 제공하는 파일로써, 다음과 같은 절차를 거쳤습니다.

- 각 아바타를 `<div>`로 감싸, `class`속성을 주어 구분할 수 있도록 하였습니다.
- `data-status` 속성을 통해, 각 아바타의 온라인/오프라인 상태를 구분하도록 하였습니다.
- 이미지는 `<img>` 태그, 온라인/오프라인 상태는 `<span>` 태그 안 `status-indicator` 클래스를 통해 나타냈습니다.
- 수업 시간에 강조하셨던 `alt`속성을 구분하였습니다.
- `<div class="avatars-container">`를 통해 모든 아바타를 포함하는 컨테이너를 구성하였습니다.
- `<div class="avatar" data-status="...">` 각 아바타를 개별적으로 감싸, `data-status`를 통해 현 상태를 표시하도록 하였습니다.

## 2. avatars.css

- `float`에서
  - `.avatars-container` 클래스를 통해 모든 아바타를 중앙에 배치하도록 하고, `width`를 고정하여 4&#215;2 형태를 유지하도록 하였습니다.
  - `.avatar ` 클래스를 통해 각 아바타의 기본 크기와 모양을 정의하고, 상태표시원이 제대로 나타나도록 `overflow: visible`로 설정하였습니다. 또한 스타일이 일관적으로 보이도록 `border-radius` 50%로 설정하였습니다.
  - 원형의 이미지는 `<img>` 자체도 `border-radius` 50%로 설정하여 원형의 이미지를 만들었습니다. 그리고 해당 이미지가 영역을 온전하게 커버하도록 `object-fit:cover`로 설정해주었습니다.
  - `.status-indicator`는 아바타의 상태표시원으로, 우측 하단에 배치하고 `border`를 설정해 흰 테두리를 설정하였습니다. 상태에 따라 다른 색상을 표시하도록 `background-color`를 `inherit`으로 설정해, `.avatar[data-status]` 에 따라 색상을 정할 수 있도록 하였습니다.
  - `flex` 지원환경에서 다르게 동작하도록 `@supports` 문법을 사용하였습니다.해당 브라우저가 `flexbox`모델을 지원하는지 확인하고, 지원하면 해당 스타일 블록 내의 규칙을 적용하여 보다 효율적으로 배치할 수 있도록 합니다.
  - `flex-wrap: wrap-reverse`를 통해 조건에 만족하도록 순서를 바꾸었습니다.

위 같은 내용을 구성하기 위해 참고한 사항들입니다.

<details><summary>참고사항</summary><div markdown="1">

![아 참고하라고~ ㅋㅋ](../images/image%20for%20md/endure.png)
<br/>
~~아 그냥 참고 하라고~ㅋㅋ... ㅠㅠ~~ 일뻔 했지만, 다음 사이트를 통해 개념을 복습하고 활용하였습니다.

1. [Inpa Dev](https://inpa.tistory.com/entry/JS-%F0%9F%93%9A-HTML-%EB%8D%B0%EC%9D%B4%ED%84%B0%EC%85%8Bdata-%EC%86%8D%EC%84%B1) 는 지난 수업시간 강조하셨던 crossorigin 개념을 공부하면서 찾아낸 기술 블로그로, 전반적인 FE 지식을 깔끔하게 정리한 곳입니다.<br/>
2. [Flexbox froggy](https://flexboxfroggy.com/#ko) 는 `flex`와 관련된 속성을 훈련할 수 있게 게임형태로 되어있던 사이트로, 학우분들의 추천으로 확인하게 되었습니다. 실제 특성을 연습해보는데에 도움이 되었습니다.<br/>
3. [heropy.dev](https://www.heropy.dev/p/Ha29GI) 또한 CSS Flex, Grid, SCSS 등 다양한 것들이 이해하기 쉬운 시각적 자료로 설명되어있던 개발블로그였습니다. flex 개념을 확고히 하는데에 도움이 되었습니다.<br/>
4. 그 외엔 구글링과, 정규 수업시간 중 슬비쌤께서 실습하신 부분을 복습 및 활용하였습니다.<br/>

</div>
</details>
