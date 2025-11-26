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
```

### document.querySelectorAll() : CSS 선택자로 모든 요소 선택

```javascript
const elements = document.querySelectorAll(".myClass");
elements.forEach(el => {
  console.log(el);
});
```

---

## 2. 요소 생성 및 추가

### document.createElement() : 새 요소 생성

```javascript
const newDiv = document.createElement("div");
const newButton = document.createElement("button");
```

### appendChild() : 요소 끝에 자식 요소 추가

```javascript
const parent = document.getElementById("parent");
const newChild = document.createElement("div");
newChild.textContent = "Hello";
parent.appendChild(newChild);
```

---

## 3. 텍스트 및 HTML 내용

### textContent : 요소의 텍스트 내용

```javascript
const element = document.getElementById("myId");
console.log(element.textContent);  // "Hello World"
element.textContent = "New Text";
```

### innerHTML : 요소의 HTML 내용

```javascript
const element = document.getElementById("myId");
element.innerHTML = "<span>New</span> <b>Content</b>";
```

---

## 4. 속성 조작

### getAttribute() : 속성 값 가져오기

```javascript
const element = document.querySelector("a");
console.log(element.getAttribute("href"));
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

---

## 5. 클래스 조작

### classList.add() : 클래스 추가

```javascript
const element = document.querySelector("div");
element.classList.add("active");
```

### classList.remove() : 클래스 제거

```javascript
const element = document.querySelector("div");
element.classList.remove("active");
```

### classList.toggle() : 클래스 토글

```javascript
const element = document.querySelector("div");
element.classList.toggle("active");
```

### classList.contains() : 클래스 포함 여부 확인

```javascript
const element = document.querySelector("div");
if (element.classList.contains("active")) {
  console.log("active 클래스가 있습니다");
}
```

---

## 6. 스타일 조작

### style 속성 : 인라인 스타일 설정

```javascript
const element = document.querySelector("div");
element.style.color = "red";
element.style.fontSize = "20px";
element.style.backgroundColor = "blue";
```

---

## 7. 이벤트 처리

### addEventListener() : 이벤트 리스너 추가

```javascript
const button = document.querySelector("button");
button.addEventListener("click", (event) => {
  console.log("Button clicked!");
});
```

### removeEventListener() : 이벤트 리스너 제거

```javascript
const button = document.querySelector("button");
const handler = () => console.log("Clicked");

button.addEventListener("click", handler);
button.removeEventListener("click", handler);
```

---

## 8. 요소 제거

### remove() : 요소 직접 제거

```javascript
const element = document.querySelector(".item");
element.remove();
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
