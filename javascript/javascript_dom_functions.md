# 자바스크립트 DOM 조작 함수 정리

## 1. DOM 요소 선택

### document.getElementById() : ID로 요소 선택

```javascript
const element = document.getElementById("myId");
console.log(element);  // <div id="myId">...</div>
```

### document.querySelector() : CSS 선택자로 첫 번째 요소 선택

```javascript
const element = document.querySelector(".myClass");
const element2 = document.querySelector("#myId");
const element3 = document.querySelector("div");
const element4 = document.querySelector("div.myClass");
```

### document.querySelectorAll() : CSS 선택자로 모든 요소 선택 (NodeList 반환)

```javascript
const elements = document.querySelectorAll(".myClass");
console.log(elements);  // NodeList

// NodeList 순회
elements.forEach(el => {
  console.log(el);
});
```

### document.getElementsByClassName() : 클래스명으로 요소 선택 (HTMLCollection)

```javascript
const elements = document.getElementsByClassName("myClass");
console.log(elements);  // HTMLCollection

// HTMLCollection 순회 (배열 아님, 주의)
for (let i = 0; i < elements.length; i++) {
  console.log(elements[i]);
}
```

### document.getElementsByTagName() : 태그명으로 요소 선택 (HTMLCollection)

```javascript
const divs = document.getElementsByTagName("div");
const buttons = document.getElementsByTagName("button");
```

### document.getElementsByName() : name 속성으로 요소 선택 (NodeList)

```javascript
const inputs = document.getElementsByName("email");
```

---

## 2. 요소 생성 및 추가

### document.createElement() : 새 요소 생성

```javascript
const newDiv = document.createElement("div");
const newButton = document.createElement("button");
const newImg = document.createElement("img");
```

### appendChild() : 요소 끝에 자식 요소 추가

```javascript
const parent = document.getElementById("parent");
const newChild = document.createElement("div");
newChild.textContent = "Hello";

parent.appendChild(newChild);
// parent의 마지막 자식으로 추가됨
```

### insertBefore() : 특정 요소 앞에 자식 요소 추가

```javascript
const parent = document.getElementById("parent");
const newChild = document.createElement("div");
const referenceChild = parent.querySelector(".existing");

parent.insertBefore(newChild, referenceChild);
// newChild가 referenceChild 앞에 추가됨
```

### insertAdjacentHTML() : 특정 위치에 HTML 삽입

```javascript
const element = document.getElementById("myId");

// beforebegin: 요소 앞
element.insertAdjacentHTML("beforebegin", "<div>Before</div>");

// afterbegin: 요소 시작 다음
element.insertAdjacentHTML("afterbegin", "<div>Start</div>");

// beforeend: 요소 끝 앞
element.insertAdjacentHTML("beforeend", "<div>End</div>");

// afterend: 요소 다음
element.insertAdjacentHTML("afterend", "<div>After</div>");
```

### insertAdjacentElement() : 특정 위치에 요소 삽입

```javascript
const element = document.getElementById("myId");
const newElement = document.createElement("div");

element.insertAdjacentElement("beforebegin", newElement);
```

### insertAdjacentText() : 특정 위치에 텍스트 삽입

```javascript
const element = document.getElementById("myId");
element.insertAdjacentText("beforebegin", "Hello");
```

---

## 3. 요소 제거 및 클론

### removeChild() : 자식 요소 제거

```javascript
const parent = document.getElementById("parent");
const child = parent.querySelector(".item");

parent.removeChild(child);
```

### remove() : 요소 직접 제거

```javascript
const element = document.querySelector(".item");
element.remove();
```

### cloneNode() : 요소 복제

```javascript
const original = document.querySelector(".item");

// 자식 없이 복제
const clone = original.cloneNode(false);

// 자식 포함 복제 (깊은 복제)
const deepClone = original.cloneNode(true);
```

---

## 4. 텍스트 및 HTML 내용

### textContent : 요소의 텍스트 내용 (읽기/쓰기)

```javascript
const element = document.getElementById("myId");

// 읽기
console.log(element.textContent);  // "Hello World"

// 쓰기
element.textContent = "New Text";

// HTML 태그는 텍스트로 처리됨
element.textContent = "<div>Not HTML</div>";
// 실제로는 텍스트로 표시됨
```

### innerText : 요소의 보이는 텍스트 (읽기/쓰기)

```javascript
const element = document.getElementById("myId");
element.innerText = "New Text";
// textContent와 유사하지만 스타일 적용 범위 고려
```

### innerHTML : 요소의 HTML 내용 (읽기/쓰기)

```javascript
const element = document.getElementById("myId");

// 읽기
console.log(element.innerHTML);
// <span>Hello</span> <b>World</b>

// 쓰기
element.innerHTML = "<span>New</span> <b>Content</b>";

// 주의: XSS 취약점 위험
// 신뢰할 수 없는 사용자 입력으로는 사용하지 말 것
```

### outerHTML : 요소 자신까지 포함한 HTML (읽기/쓰기)

```javascript
const element = document.querySelector("div.myClass");

// 읽기
console.log(element.outerHTML);
// <div class="myClass">...</div>

// 쓰기 - 요소 자체가 대체됨
element.outerHTML = "<span>Replaced</span>";
```

---

## 5. 속성 조작

### getAttribute() : 속성 값 가져오기

```javascript
const element = document.querySelector("a");
console.log(element.getAttribute("href"));
console.log(element.getAttribute("title"));
```

### setAttribute() : 속성 설정

```javascript
const element = document.querySelector("img");
element.setAttribute("src", "/path/to/image.jpg");
element.setAttribute("alt", "Description");
```

### removeAttribute() : 속성 제거

```javascript
const element = document.querySelector("button");
element.removeAttribute("disabled");
```

### hasAttribute() : 속성 존재 여부 확인

```javascript
const element = document.querySelector("img");
if (element.hasAttribute("alt")) {
  console.log("alt 속성이 있습니다");
}
```

### 직접 속성 접근

```javascript
const element = document.querySelector("input");

// 읽기
console.log(element.value);
console.log(element.checked);
console.log(element.disabled);

// 쓰기
element.value = "new value";
element.checked = true;
element.disabled = false;
```

---

## 6. 클래스 조작

### classList.add() : 클래스 추가

```javascript
const element = document.querySelector("div");
element.classList.add("active");
element.classList.add("highlight", "important");  // 여러 클래스 추가
```

### classList.remove() : 클래스 제거

```javascript
const element = document.querySelector("div");
element.classList.remove("active");
element.classList.remove("highlight", "important");
```

### classList.toggle() : 클래스 토글

```javascript
const element = document.querySelector("div");

// 없으면 추가, 있으면 제거
element.classList.toggle("active");

// 특정 상태로 설정
element.classList.toggle("active", true);  // 반드시 추가
element.classList.toggle("active", false); // 반드시 제거
```

### classList.contains() : 클래스 포함 여부 확인

```javascript
const element = document.querySelector("div");
if (element.classList.contains("active")) {
  console.log("active 클래스가 있습니다");
}
```

### classList.replace() : 클래스 교체

```javascript
const element = document.querySelector("div");
element.classList.replace("old-class", "new-class");
```

### className : 전체 클래스 문자열 (읽기/쓰기)

```javascript
const element = document.querySelector("div");

// 읽기
console.log(element.className);  // "active highlight"

// 쓰기 - 기존 클래스 모두 대체
element.className = "new-class";
```

---

## 7. 스타일 조작

### style 속성 : 인라인 스타일 설정

```javascript
const element = document.querySelector("div");

// CSS 속성명은 camelCase 사용
element.style.color = "red";
element.style.fontSize = "20px";
element.style.backgroundColor = "blue";
element.style.margin = "10px";
element.style.padding = "5px";

// 읽기
console.log(element.style.color);

// 제거
element.style.color = "";
```

### getComputedStyle() : 계산된 스타일 얻기 (읽기 전용)

```javascript
const element = document.querySelector("div");
const styles = getComputedStyle(element);

console.log(styles.color);
console.log(styles.fontSize);
console.log(styles.display);
```

---

## 8. 요소 네비게이션

### parentElement : 부모 요소 접근

```javascript
const element = document.querySelector(".child");
const parent = element.parentElement;
console.log(parent);
```

### children : 모든 자식 요소 (HTMLCollection)

```javascript
const parent = document.querySelector(".parent");
const children = parent.children;

for (let child of children) {
  console.log(child);
}
```

### childNodes : 모든 자식 노드 (텍스트 노드 포함)

```javascript
const parent = document.querySelector(".parent");
const nodes = parent.childNodes;

nodes.forEach(node => {
  console.log(node);
});
```

### firstChild / lastChild : 첫 번째/마지막 자식 노드

```javascript
const parent = document.querySelector(".parent");
console.log(parent.firstChild);  // 텍스트 노드일 수 있음
console.log(parent.lastChild);
```

### firstElementChild / lastElementChild : 첫 번째/마지막 자식 요소

```javascript
const parent = document.querySelector(".parent");
console.log(parent.firstElementChild);  // 첫 요소
console.log(parent.lastElementChild);   // 마지막 요소
```

### nextElementSibling / previousElementSibling : 다음/이전 형제 요소

```javascript
const element = document.querySelector(".item");
console.log(element.nextElementSibling);      // 다음 형제
console.log(element.previousElementSibling);  // 이전 형제
```

---

## 9. 이벤트 처리

### addEventListener() : 이벤트 리스너 추가

```javascript
const button = document.querySelector("button");

button.addEventListener("click", (event) => {
  console.log("Button clicked!");
  console.log(event);
});

// 여러 이벤트 타입
element.addEventListener("mouseover", handler);
element.addEventListener("mouseout", handler);
element.addEventListener("input", handler);
element.addEventListener("change", handler);
element.addEventListener("submit", handler);
element.addEventListener("load", handler);
element.addEventListener("scroll", handler);
```

### removeEventListener() : 이벤트 리스너 제거

```javascript
const button = document.querySelector("button");

const handler = () => {
  console.log("Clicked");
};

button.addEventListener("click", handler);

// 나중에 제거
button.removeEventListener("click", handler);
```

### onclick 등 : 이벤트 핸들러 직접 지정 (권장하지 않음)

```javascript
const button = document.querySelector("button");

button.onclick = () => {
  console.log("Clicked");
};
```

---

## 10. 폼 처리

### value : 입력 요소의 값

```javascript
const input = document.querySelector("input");
const textarea = document.querySelector("textarea");
const select = document.querySelector("select");

// 읽기
console.log(input.value);
console.log(textarea.value);
console.log(select.value);

// 쓰기
input.value = "new value";
textarea.value = "new text";
select.value = "option2";
```

### checked : 체크박스/라디오 버튼의 상태

```javascript
const checkbox = document.querySelector('input[type="checkbox"]');
const radio = document.querySelector('input[type="radio"]');

// 읽기
console.log(checkbox.checked);  // true/false

// 쓰기
checkbox.checked = true;
radio.checked = false;
```

### disabled : 요소 비활성화

```javascript
const button = document.querySelector("button");
const input = document.querySelector("input");

button.disabled = true;
input.disabled = false;
```

### form : 폼 요소 접근

```javascript
const input = document.querySelector("input");
const form = input.form;
console.log(form);
```

---

## 11. 데이터 속성

### dataset : data-* 속성 접근

```html
<div id="myDiv" data-user-id="123" data-role="admin"></div>
```

```javascript
const element = document.getElementById("myDiv");

// 읽기
console.log(element.dataset.userId);  // "123"
console.log(element.dataset.role);    // "admin"

// 쓰기
element.dataset.userId = "456";
element.dataset.newAttribute = "value";

// 읽기: getAttribute 사용도 가능
console.log(element.getAttribute("data-user-id"));
```

---

## 12. 요소 위치 및 크기

### getBoundingClientRect() : 요소의 위치 및 크기 정보

```javascript
const element = document.querySelector("div");
const rect = element.getBoundingClientRect();

console.log(rect.top);      // 요소 위쪽 위치
console.log(rect.left);     // 요소 왼쪽 위치
console.log(rect.bottom);   // 요소 아래쪽 위치
console.log(rect.right);    // 요소 오른쪽 위치
console.log(rect.width);    // 요소 너비
console.log(rect.height);   // 요소 높이
```

### offsetWidth / offsetHeight : 요소의 너비와 높이

```javascript
const element = document.querySelector("div");
console.log(element.offsetWidth);   // 테두리 포함
console.log(element.offsetHeight);
```

### clientWidth / clientHeight : 요소의 내용 너비와 높이

```javascript
const element = document.querySelector("div");
console.log(element.clientWidth);   // 패딩 포함, 스크롤바 제외
console.log(element.clientHeight);
```

### offsetLeft / offsetTop : 부모 요소 기준 위치

```javascript
const element = document.querySelector("div");
console.log(element.offsetLeft);   // 왼쪽 위치
console.log(element.offsetTop);    // 위쪽 위치
```

### scrollWidth / scrollHeight : 스크롤 가능한 전체 크기

```javascript
const element = document.querySelector("div");
console.log(element.scrollWidth);   // 전체 너비 (스크롤 포함)
console.log(element.scrollHeight);  // 전체 높이
```

### scrollLeft / scrollTop : 스크롤 위치

```javascript
const element = document.querySelector("div");

// 읽기
console.log(element.scrollLeft);
console.log(element.scrollTop);

// 쓰기
element.scrollLeft = 0;
element.scrollTop = 0;  // 맨 위로 스크롤
```

---

## 요약 테이블

| 함수/속성 | 설명 |
|----------|------|
| `getElementById()` | ID로 요소 선택 |
| `querySelector()` | CSS 선택자로 첫 요소 선택 |
| `querySelectorAll()` | CSS 선택자로 모든 요소 선택 |
| `createElement()` | 새 요소 생성 |
| `appendChild()` | 자식으로 추가 |
| `removeChild()` | 자식 제거 |
| `remove()` | 요소 제거 |
| `textContent` | 텍스트 내용 |
| `innerHTML` | HTML 내용 |
| `getAttribute()` | 속성 값 가져오기 |
| `setAttribute()` | 속성 설정 |
| `classList.add()` | 클래스 추가 |
| `classList.remove()` | 클래스 제거 |
| `classList.toggle()` | 클래스 토글 |
| `style` | 인라인 스타일 설정 |
| `addEventListener()` | 이벤트 리스너 추가 |
| `dataset` | data-* 속성 접근 |
| `getBoundingClientRect()` | 위치 및 크기 정보 |

