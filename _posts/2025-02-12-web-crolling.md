---
title: 웹크롤링
layout: single
classes: wide
categories:
  - web crawling
tags:
  - html
  - beautifulsoup
  - selenium
---


## **1. HTML 기본 개념 소개**
HTML은 웹 크롤링의 기초입니다. 간단한 예제를 통해 확인하자.

### **(1) HTML 기본 구조**
```html
<!DOCTYPE html>
<html>
<head>
    <title>예제 페이지</title>
</head>
<body>
    <h1>환영합니다!</h1>
    <p id="intro">안녕하세요. 이것은 예제입니다.</p>
    <ul>
        <li class="item">첫 번째 항목</li>
        <li class="item">두 번째 항목</li>
    </ul>
</body>
</html>
```

- `<html>`: 문서의 시작과 끝.
- `<head>`: 메타 정보(예: 제목, 스타일 등).
- `<body>`: 실제 콘텐츠가 포함된 부분.
- `<h1>`, `<p>`, `<ul>`, `<li>`: 각각 제목, 단락, 목록, 항목을 나타내는 태그.
- `id`와 `class`: 특정 요소를 식별하거나 그룹화하는 속성.

---

## **2. BeautifulSoup 기본 사용법**
BeautifulSoup은 HTML을 파싱하고 원하는 데이터를 추출하기 위한 도구입니다. 

### **(1) 설치 및 임포트**
```bash
pip install beautifulsoup4
```
```python
from bs4 import BeautifulSoup
```

### **(2) 간단한 예제**
위에서 작성한 HTML 파일을 파싱해 보는 예제를 제공하세요.

```python
from bs4 import BeautifulSoup

# HTML 문서 (앞서 작성한 예제)
html = """
<!DOCTYPE html>
<html>
<head>
    <title>예제 페이지</title>
</head>
<body>
    <h1>환영합니다!</h1>
    <p id="intro">안녕하세요. 이것은 예제입니다.</p>
    <ul>
        <li class="item">첫 번째 항목</li>
        <li class="item">두 번째 항목</li>
    </ul>
</body>
</html>
"""

# BeautifulSoup 객체 생성
soup = BeautifulSoup(html, "html.parser")

# 데이터 추출(find()는 태그 이름, 클래스, ID, 속성 등 키워드 인자 기반)
title = soup.title.text  # <title> 태그의 텍스트
heading = soup.h1.text   # <h1> 태그의 텍스트
intro = soup.find(id="intro").text  # id="intro"인 요소의 텍스트
items = [item.text for item in soup.find_all(class_="item")]  # class="item"인 모든 요소의 텍스트

# 결과 출력
print("제목:", title)
print("헤딩:", heading)
print("소개:", intro)
print("항목들:", items)
```

---

## **3. 네이버 날씨 크롤링**
네이버 날씨 페이지에서 현재 온도를 가져오기.

```python
import requests
from bs4 import BeautifulSoup

# 네이버 날씨 페이지 URL
url = "https://weather.naver.com/"

# HTTP GET 요청
headers = {
    "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/115.0.0.0 Safari/537.36"
}
response = requests.get(url, headers=headers)

# HTML 파싱
soup = BeautifulSoup(response.text, "html.parser")

# 현재 온도 추출(select_one()은 CSS 선택자 기반)
current_temp = soup.select_one(".current").text.strip()

# 결과 출력
print("현재 온도:", current_temp)
```

---

## **4. HTML태그와 CSS선택자 비교**

### **(1) HTML 태그**
- **HTML 태그**는 웹 페이지의 구조를 정의하는 기본 요소입니다.
- 태그는 `<`와 `>`로 감싸져 있으며, 특정 콘텐츠를 나타내거나 의미를 부여합니다.

#### **예시**
```html
<h1>제목</h1>
<p>단락 텍스트입니다.</p>
<a href="https://www.example.com">링크</a>
```

- `<h1>`: 제목을 나타냅니다.
- `<p>`: 단락(문단)을 나타냅니다.
- `<a>`: 하이퍼링크를 나타냅니다.

#### **역할**
- 웹 페이지의 **구조**와 **콘텐츠**를 정의합니다.
- 각 태그는 고유한 의미를 가지며, 브라우저가 이를 해석하여 화면에 표시합니다.


### **(2) CSS 선택자**
- **CSS 선택자**는 HTML 문서 내에서 특정 요소를 선택하기 위한 규칙입니다.
- CSS 선택자는 스타일을 적용하거나 JavaScript/jQuery, BeautifulSoup 등을 통해 특정 요소를 찾을 때 사용됩니다.

#### **예시**
```css
/* 클래스 선택자 */
.highlight {
    color: red;
}

/* ID 선택자 */
#main-title {
    font-size: 24px;
}

/* 태그 선택자 */
h1 {
    text-align: center;
}
```

#### **종류**
1. **태그 선택자**: HTML 태그 이름을 직접 사용합니다.
   - 예: `h1`, `p`, `div`
2. **클래스 선택자**: 클래스 속성(`class`)을 사용합니다.
   - 예: `.highlight`, `.container`
3. **ID 선택자**: ID 속성(`id`)을 사용합니다.
   - 예: `#main-title`, `#footer`
4. **속성 선택자**: 특정 속성을 가진 요소를 선택합니다.
   - 예: `a[href]`, `input[type="text"]`
5. **계층 선택자**: 요소 간의 관계를 이용합니다.
   - 예: `div span`, `.container > p`


### **(3) 차이점 비교**

| **항목**         | **HTML 태그**                                   | **CSS 선택자**                              |
|------------------|-----------------------------------------------|--------------------------------------------|
| **정의**         | 웹 페이지의 구조와 콘텐츠를 정의               | HTML 문서 내 특정 요소를 선택하기 위한 규칙 |
| **사용 목적**     | 브라우저가 콘텐츠를 표시하기 위해 사용          | 스타일 적용 또는 특정 요소를 찾기 위해 사용 |
| **형식**         | `<태그명>`으로 작성                            | `.클래스`, `#아이디`, `태그명` 등으로 작성  |
| **예시**         | `<h1>`, `<p>`, `<a href="...">`               | `h1`, `.highlight`, `#main-title`          |
| **주요 도구**    | HTML 문서 작성                                | CSS, JavaScript, jQuery, BeautifulSoup     |

### **(4) 예제를 통한 비교**

#### **HTML 코드**
```html
<div id="header">
    <h1 class="title">환영합니다!</h1>
    <p class="description">이곳은 예제 페이지입니다.</p>
</div>
```

#### **HTML 태그**
- `<div>`: 컨테이너 역할을 하는 태그.
- `<h1>`: 제목을 나타내는 태그.
- `<p>`: 단락 텍스트를 나타내는 태그.

#### **CSS 선택자**
- `#header`: ID가 `header`인 `<div>`를 선택.
- `.title`: 클래스가 `title`인 `<h1>`을 선택.
- `.description`: 클래스가 `description`인 `<p>`를 선택.


### **(5) BeautifulSoup에서의 활용**
BeautifulSoup에서는 CSS 선택자를 사용하여 HTML 문서에서 원하는 요소를 쉽게 찾을 수 있습니다.

#### **예제**
```python
from bs4 import BeautifulSoup

html = """
<div id="header">
    <h1 class="title">환영합니다!</h1>
    <p class="description">이곳은 예제 페이지입니다.</p>
</div>
"""
soup = BeautifulSoup(html, "html.parser")

# HTML 태그로 접근
print(soup.h1.text)  # 출력: 환영합니다!

# CSS 선택자로 접근
print(soup.select_one("#header .title").text)  # 출력: 환영합니다!
print(soup.select_one(".description").text)    # 출력: 이곳은 예제 페이지입니다.
```

---

## **4. 주의사항: 크롤링 정책(`robots.txt`)을 준수**
**`robots.txt`**는 웹사이트의 관리자가 크롤러(예: 검색 엔진 봇)에게 어떤 페이지를 크롤링할 수 있고, 어떤 페이지를 크롤링하지 말아야 하는지를 지정하는 **텍스트 파일**입니다. 이 파일은 웹사이트의 루트 디렉토리에 위치하며, 크롤러가 웹사이트를 방문할 때 가장 먼저 확인하는 규칙 파일입니다.

### **(1) `robots.txt`의 목적**
- **크롤링 제어**: 특정 페이지나 디렉토리를 크롤링하지 못하도록 차단하여 서버 부하를 줄이고 보안을 강화합니다.
- **검색 엔진 최적화(SEO)**: 검색 엔진이 불필요하거나 민감한 데이터를 색인하지 않도록 합니다.
- **공개 정보 관리**: 특정 콘텐츠를 공개하지 않고 싶을 때 사용됩니다.


### **(2) 기본 구조**
`robots.txt` 파일은 다음과 같은 형식으로 작성됩니다:

```
User-agent: [봇 이름]
Disallow: [차단할 경로]

User-agent: [다른 봇 이름]
Allow: [허용할 경로]
```

#### **주요 키워드**
1. **`User-agent`**:
   - 특정 크롤러(봇)를 지정합니다.
   - 예: `Googlebot`, `Bingbot`, `*`(모든 봇).
   
2. **`Disallow`**:
   - 크롤러가 접근하지 못하도록 차단할 경로를 지정합니다.
   - 예: `/private/`, `/admin/`.

3. **`Allow`**:
   - 특정 경로에 대해 크롤링을 허용합니다(선택 사항).
   - 예: `/public/`.


### **(3) 예제**

#### **예제 1: 모든 봇 차단**
```
User-agent: *
Disallow: /
```

- 모든 크롤러가 웹사이트의 모든 페이지를 크롤링하지 못하도록 차단합니다.


#### **예제 2: 특정 디렉토리 차단**
```
User-agent: *
Disallow: /admin/
Disallow: /private/
```

- `/admin/`과 `/private/` 디렉토리는 크롤링하지 못하도록 차단합니다.

#### **예제 3: 특정 봇만 허용**
```
User-agent: Googlebot
Allow: /

User-agent: *
Disallow: /
```

- `Googlebot`만 전체 사이트를 크롤링할 수 있도록 허용하고, 다른 모든 봇은 차단합니다.


### **(4) 주의사항**
- **법적 강제력 없음**
- **보안 목적으로 사용 금지**
- **완전한 차단 방법**


### **(5) `robots.txt` 확인 방법**
웹사이트의 `robots.txt` 파일은 브라우저에서 직접 확인할 수 있습니다. 예를 들어:
- 네이버: `https://www.naver.com/robots.txt`
- 구글: `https://www.google.com/robots.txt`


### **(6) 결론**
- **`robots.txt`**는 웹사이트 관리자가 크롤러의 행동을 제어하기 위한 중요한 도구입니다.
- 크롤링 작업을 시작하기 전에 반드시 `robots.txt`를 확인하고, 이를 준수하여 윤리적이고 합법적인 크롤링을 수행해야 합니다.
