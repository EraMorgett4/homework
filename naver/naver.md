# 테킷 FES homework - NAVER 프로젝트

- ## 구조 설계

  HTML 손 마크업
  
   <img src="/images/image for md/markup.png" width="50%" title="HTML 손 마크업" alt="markupImage"></img><br/>

<details>
<summary>과제 요구사항</summary> 
<div markdown="1">

과제는 다음과 같은 조건을 만족할 수 있도록 구현한다.

`마크업`

- 로고 이미지는 배경이 아닌 `<img>` 요소로 마크업
  (svg를 지원하는 웹브라우저는 svg 형식으로 그렇지 않은 웹브라우저는 png 형식으로 보여지도록 구현)
- 웹접근성을 고려한 로그인 폼 서식 마크업
  (레이블 제공의 경우 WAI-ARIA가 아닌 HTML 네이티브 방식으로 구현)
- 아이디와 비밀번호는 필수 입력 서식임을 알 수 있도록 구현
- IP 보안 텍스트 클릭 시 미리 제공 된 ip_secruity.html 파일이 새창에 보이도록 구현
- 로그인 상태유지와 IP 보안 ON/OFF는 스위치는 키보드로도 조작 가능하도록 구현

`스타일링`

- 반응형으로 구현 (768px 미만 모바일 / 768px 이상 데스크탑)
- 모바일 퍼스트 (공통 스타일과 모바일 스타일을 먼저 구현한 후 데스크탑 스타일을 재정의 할 것)
- 글자 크기 및 여백(margin 및 padding)은 모두 rem 단위로 설정할 것
- 기본 글자 크기 및 색상
  16px,<span style="color:#fff; background-color:#181818;">#181818</span>
- 로고
  가로 230px, 가운데 배치
- 포커스 스타일 커스텀 (색상 <span style="color:#24388d">#24388d</span>)
- 모바일 로그인 폼 로그인 폼의 가로 크기는 100%(좌/우 여백 각 20px 포함)
- 모바일 환경에서 IP 보안 ON/OFF 스위치는 사용자에게 제공되지 않도록 구현
- 데스크탑 로그인 폼의 가로 크기는 500px(좌/우 여백 각 20px 포함)
- 입력 서식 글자크기 및 세로 크기, 테두리 선 색상, 배경 색상
  기본 상태 : 14px, 45px, <span style="background-color:#dadada">#dadada</span>, <span style="color:#1b1b1b; background-color:#fff">#fff</span>
  포커스 상태 : <span style="background-color:#03cf5d">#03cf5d</span>, <span style="background-color:#e9f0fd">#e9f0fd</span>
- 로그인 버튼 글자 크기, 세로 크기, 글자 색상, 배경색상, 위쪽 여백
  16px, 45px, <span style="color:#1b1b1b; background-color:#fff">#fff</span>, <span style="background-color:#03cf5d">#03cf5d</span>, 20px
- 로그인 상태유지 및 IP 보안 ON/OFF 영역 위쪽 여백 10px
- 로그인 상태유지 체크박스 배경 이미지 및 크기와 여백
  선택안함 : unchecked.svg
  선택함 : checked.svg
  가로 _ 세로 : 24px _ 24px
  배경 이미지 오른쪽 여백 : 5px
- IP 보안 스위치의 글자 크기 16px, 글자 색상 <span style="color:#fff; background-color:#181818;">#181818</span>

</div>
</details>

---

## 1. naver.html

네이버 로그인 페이지를 클론코딩 한 파일로써, 주요 사항으로 다음과 같습니다.

1. **체크박스**와 **IP보안 ON/OFF 부분**을 각각 다른 방식으로 진행했습니다.
   <br/>
   1. **체크박스**는 `<span>` 을 이용하여 스타일을 적용하였습니다. 체크박스의 상태가 `checked` 상태일 때를 감지하여 `background-img`를 변경하여 이를 나타내었습니다.
      1. 하지만 이로 인해 탭을 눌렀을 때 해당 부분이 드러나도록 outline을 설정하긴 하였으나, **엔터키를 눌러도 상태가 변하지 않음을 확인**하였습니다. ON/OFF 부분은 JS로 이를 해결하였으나 조언을 구하고자 합니다.(::before, ::after를 활용한 부분도 동일하게 동작하는지?)
         <br/>
   2. **IP보안 ON/OFF 부분**도 동일하게 `<span>` 을 활용하였고, 체크박스 부분의 문제를 JS script를 활용해 이를 해결하였습니다.
      1. 클릭과 엔터키의 이벤트를 입력받아 ON/OFF 글자를 각각 다른 글자로 바꾸도록 JS script를 작성하였습니다. 색상부분은 CSS에서 녹색으로 처리하도록 설정하였습니다.
         <br/>
2. 접근성을 고려해 각 파트에 `label`을 삽입하고, `class="hidden"`을 부여해 이를 시각적으로 보이지 않게 하였습니다.
   <br/>
3. `tabindex`를 활용해 로그인 버튼 부분으로 바로 가지 못하도록 시도하였으나, 제대로 적용되지 않은 듯 합니다. 이 부분 조언 구하고자 합니다.
   <br/>
4. `onerror`를 활용하여 svg파일이 정상적으로 불러와지지 않을 때 png 파일을 불러오도록 하였습니다. JS를 사용하지 않고도 가능한 방법이 있는지 여쭙습니다.

## 2. naver.css

1. `.hidden`과 basic reset 부분을 제외한 모든 부분에서 절대 수치 대신 rem을 사용할 수 있도록 코드를 작성하였습니다. `html` 의 `--base-font-size` 를 기반으로 계산할 수 있도록 설정하였습니다. 색상, padding, margin 또한 변수화 하여 사용하였습니다.
   <br/>
2. `login-container` 클래스를 통해 내부 자식요소를 정렬하였습니다.
   <br/>

3. `input`의 속성을 지명하여 입력서식 및 포커스 상태시 요구사항에 맞도록 설정하였습니다. 수업시간에 배운 nesting을 활용하였습니다. `transition` 활용하여 시각적 효과를 주었습니다.
   <br/>

4. 체크박스 부분과 IP보안의 ON/OFF 부분이 제일 관건이었다 생각합니다. html 부분에서도 설명하였지만, 가상요소를 활용하려하였으나 위치 설정 문제로 다른 방도를 시도하였습니다.
   <br>

   1. 우선 모바일에선 오른쪽에 붙도록 `display: flex`, `justify-content: flex-end`로 설정하였습니다.
   2. 체크박스는 보이지 않게 하도록 `appearance: none`으로 설정하였습니다.
   3. 그 외적으론 수업시간에 진행하였던 체크박스 코드를 대부분 참고하였습니다. background 를 여지껏 background-image로 잘못 작성하여 에러가 났었고, 이는 확인 후 수정하였습니다. 때문에 정상적으로 unchecked.svg - checked.svg 가 바뀌도록 하였습니다.
   4. IP 보안 부분은 **모바일에선 보이지 않도록** `display:none` 으로 설정하였습니다.
      <br>

5. `.option` 으로 로그인상태 유지, IP보안을 묶어 관리하였습니다. `.ip-toggle` 에서 IP 보안 토글 ON/OFF 변환이 색상변환도 정상적으로 이뤄지도록 하였습니다. `:focus`와 `:focus-visible` 관리 또한 이부분에서 이루어졌습니다.
   <br/>

6. `@media` 를 통해 데스크톱 환경에서의 설정을 별도로 관리하였습니다. `options` 부분에서 오른쪽 정렬되었던 부분을 `space-between`으로 변경하여 요구사항과 같이 정렬하였습니다. IP보안 부분은 `text-decoration:none`을 이용하여 밑줄을 없앴습니다.
   <br/>

7. 반응형 레이아웃 gif 에서 요구하는 요구사항(화면 사이즈대로 조정되는 넓이)대로 포맷을 완성하였습니다.
   <br/>

#### 참고사항

- 대부분의 코드는 수업시간에 배운것을 토대로 하였습니다.
- JS 부분은 [생활코딩](https://opentutorials.org/course/1375/6761)을 참고하였습니다.

******

### 피드백 후 코드 수정 (24/05/15)

1. **로고 부분 마크업 방식 변경**

기존 JS의 onerror 특성을 활용하였던 방식에서, `<picture> ~ <img>` 구조로 시멘틱하게 활용하였습니다. 더불어 `<h1>` 요소 활용하여 대제목 자체를 로고로 설정하였습니다. 네이버 홈으로 연결되도록 하이퍼링크를 추가하였습니다. 그 외에 피드백 사항에 맞도록 수정하였습니다. 기존 이미지 파일의 해상도가 떨어져 더 높은 해상도로 figma에서 export 하여, 크기는 기존 크기에 맞게 조정하였습니다.

   - 변경 전 html
      ```html
      <img src="/naver.svg" alt="Naver" class="logo" onerror="this.onerror=null; this.src='/naver.png'">
      ```

   - 변경 후 html
      ```html
      <h1>
         <a href="https://www.naver.com" rel="noopener noreferrer">
            <picture class="picture-logo">
               <source srcset="/naver/naver.svg" type="image/svg+xml" />
               <img src="/naver/naver.png" alt="Naver_logo" class="logo" />
            </picture>
         </a>
      </h1>
      ```

   - 추가된 css
      ```css
      .picture-logo {
         display: inline-block;
         width: 14.375rem;
         height: auto;
         
         .logo{
            width: 100%;
            height: auto;
         }
      }
      ```

2. **ON/OFF 토글 구현방식 변경**

 기존엔 `<span>`을 활용하여 JS를 통해 구현하였으나, 피드백 내용을 바탕으로 checkbox, label, 가상선택자를 사용하여 이를 구현하도록 코드를 수정하였습니다. (prettier 설정때문에 css부분에서 의도와 다른 탭/엔터가 삽입되었을 수 있습니다.)

   - 변경 전 html

      ```html
      <div class="ip-security">
         <label for="toggle-status">
            <a href="/naver/ip_security.html" target="_blank" class="ip-security">IP 보안</a>
            <span id="toggle-status" class="ip-toggle" tabindex="0" role="button">OFF</span>
         </label>
      </div>
      ```

   - 변경 후 html

      ```html
      <span class="ip-toggle">
         <a href="/naver/ip_security.html" target="_blank" class="ip-security">IP 보안</a>
         <input type="checkbox" name="ip-toggle-checkbox" id="ip-toggle-checkbox" />
         <label for="ip-security"></label>
      </span>
      ```
   - 변경 전 css

      ```css
      .options {
         /* 중략 */

         /* ON/OFF 토글 */
         .ip-toggle.on {
            color: var(--bgcolor-naver-green);
         }

         .ip-toggle {
            color: var(--base-color);

            &:focus,
            &:focus-visible {
            border: var(--base-border-size) solid var(--focus-style-custom);
            }
         }
      }
      ```

   - 변경 후 css

      ```css
      @media (min-width: 48rem) {
         .ip-toggle {
         display: inline-block;
         position: relative;
         text-decoration: none; /* 밑줄 없애기*/

         input {
            appearance: none;
            position: absolute;

            &:focus-visible + label {
               outline: var(--base-border-size) solid var(--focus-style-custom);
               border-radius: var(--base-border-size);
            }

            &:checked + label {
               &::before {
               content: "";
               }

               &::after {
               content: "ON";
               color: var(--bgcolor-naver-green);
               }
            }
         }

         label {
            &::before {
               content: "OFF";
               color: var(--gray);
               }
            }
         }
      }
      ```



3. **로그인 상태 유지 코드 수정**

(수정 중)

4. **마이너한 수정**
   - 아이디 입력 서식의 type 속성을 text에서 email로 변경하였습니다.
   - 

(수정 중)

******
###### 피드백 기반 수정 후기
- 이제야 좀 시멘틱 마크업 구조가 눈에 들어오기 시작했고, 실습을 토대로 연습하여 경험이 쌓이면 스스로도 작성할 수 있을 듯한 자신감이 생겼다.
- 복습(이전 수업의 실습코드 탐색 및 관련 키워드 구글링)의 중요성을 여실히 느꼈다.
- 여지껏 포커스 상태에서 `<input>`부분의 동작은 모두 엔터키로 동작하는 줄 알았는데, checkbox의 경우 space 가 기본이었다.
- <details><summary>위 부분에 대한 GPT 답변</summary><div markdown="1">


   ## 스페이스바로 조작할 수 있는 HTML Input 요소

   HTML에서 접근성과 사용 편의성을 위해 스페이스바로 조작할 수 있는 여러 `input` 요소가 있습니다. 여기서는 이러한 요소들을 나열하고 스페이스바로 어떻게 조작할 수 있는지 설명합니다.

   ### 체크박스 입력

   - **요소**: `<input type="checkbox">`
   - **조작 방법**: 포커스가 있을 때, 스페이스바를 누르면 체크박스의 상태가 체크됨과 체크 해제됨 사이에서 전환됩니다.
   - **MDN 문서**: [MDN Web Docs - `<input type="checkbox">`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/checkbox)

   ### 라디오 버튼 입력

   - **요소**: `<input type="radio">`
   - **조작 방법**: 포커스가 있을 때, 스페이스바를 누르면 라디오 버튼이 선택됩니다. 라디오 버튼 그룹 내에서는 하나만 선택할 수 있습니다.
   - **MDN 문서**: [MDN Web Docs - `<input type="radio">`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/radio)

   ### 버튼 요소

   - **요소들**: `<button>`, `<input type="button">`, `<input type="submit">`, `<input type="reset">`
   - **조작 방법**: 포커스가 있을 때, 스페이스바를 누르면 버튼이 활성화되어 기본 동작(예: 폼 제출, 리셋 등)이 실행됩니다.
   - **MDN 문서**: 
   - [MDN Web Docs - `<button>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/button)
   - [MDN Web Docs - `<input type="button">`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/button)
   - [MDN Web Docs - `<input type="submit">`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/submit)
   - [MDN Web Docs - `<input type="reset">`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/reset)

   </div>
   </details>
