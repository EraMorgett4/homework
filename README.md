# homework

테킷 프론트엔드 스쿨 10기 과제 저장소

1. [`avatars.md` 링크](https://github.com/EraMorgett4/homework/blob/main/avatars/avatars.md)
2. [`naver.md` 링크](https://github.com/EraMorgett4/homework/blob/main/naver/naver.md)
3. [`apple.md` 링크](https://github.com/EraMorgett4/homework/blob/main/apple/apple.md)

## 피드백

<details>
<summary>1차 과제 피드백</summary> 
<div markdown="0">

- 마크업
  - Avatar1이 적절한 대체텍스트라고 볼 수 없음. 유저명 또는 사용자의 이름을 제공하는 것을 고려해보기 바람.
  - data-status 속성에 지정된 online과 offline이라는 값만으로 상태정보를 알 수 없음.
- 스타일링
  - overflow: visible의 경우 기본값이므로 선언할 이유가 없음.
  - float: left를 지정하면 display가 block으로 렌더링되기때문에 float 속성과 display: block을 함께 선언할 필요는 없음.
  - flex-wrap: wrap-reverse로 설정할 경우 8번 이미지부터 1번 이미지 순서로 배치됨. 5 ~ 8번 / 1 ~ 4번 순으로 배치되어야 함.

</div>
</details>

<details>
<summary>2차 과제 피드백</summary> 
<div markdown="0">

- 마크업
  - 대제목이 없음. 로고를 `<h1>` 요소로 제공하는 것이 적절.
  - `<picture>`, `<source>`, `<img>` 요소를 사용하여 로고를 마크업 하고 네이버 홈으로 연결되도록 하이퍼 링크를 추가할 것.
  - 대체 텍스트는 “네이버” 또는 “Naver”가 적절함
  - 아이디 입력서식의 type 속성 값이 text로 제공되고 있음. email 값을 지정하여야 함.
  - 로그인 버튼과 로그인 상태 유지 영역의 마크업 순서가 변경되는 것이 바람직 함.
  - 로그인 버튼은 로그인 텍스트가 접근 가능한 이름 즉 레이블의 역할임. 따로 <label> 요소를 제공할 필요 없음.
  - `<a>` 링크가 새창으로 열릴 경우 `rel="noopener noreferrer”`를 함께 명시하는 것을 추천함.
  - ON/OFF는 체크박스 임. 자바스크립트로 해당 기능을 구현하였는데 이 경우 상태값을 저장하기 위한 추가작업이 필요하고 동적으로 변경된 값을 스크린 리더가 읽을 수 있도록 aria-live 속성등의 사용이 필요해짐
- 스타일링
  - 변수를 사용한 부분은 Good!
  - 컴포넌트와 레이아웃을 분리하여 작성하는 것을 고민해 보기 바람.
- 과제 구현 과정에 대한 설명
  - 구조를 직접 그려본 점에 대해 칭찬하고 싶어요. 다만 과제를 해결하는 과정만 적지말고 회고처럼 느낀점 또는 앞으로 성장해야 할 방향 등에 대해 더 적었으면 좋았을 것 같아요.
  - 이제 마지막 과제가 남아있으니 해당 과제에서 이런 부분이 기재되어 있기를 기대해볼께요.

</div>
</details>

<details>
<summary>3차 과제 피드백</summary> 
<div markdown="0">

</div>
</details>
