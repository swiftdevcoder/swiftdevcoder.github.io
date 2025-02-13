---
title: Selelium 사용하기
layout: single
classes: wide
categories:
  - web crawling
tags:
  - html
  - beautifulsoup
  - selenium
---


## **1. Selenium의 기본 개념**
- **WebDriver**: 브라우저를 제어. selenium 4부터 자동으로 chrome을 설정(수동 다운로드 불필요)
- **요소 선택**: `find_element`와 `find_elements`를 사용하여 HTML 요소를 찾는 방법.
- **동작 수행**: 클릭, 입력, 스크롤 등의 기본 동작.
- **대기(Wait)**: 페이지 로딩이나 요소가 나타날 때까지 기다리는 방법.


## 2. **로그인(login) 연습**
로그인 페이지에서 사용자 이름과 비밀번호를 입력하고 로그인 버튼을 클릭하는 방법을 연습할 수 있습니다.

### URL: [https://the-internet.herokuapp.com/login](https://the-internet.herokuapp.com/login)

```python
from selenium import webdriver
from selenium.webdriver.common.by import By

# WebDriver 설정, 

driver = webdriver.Chrome()

try:
    # 로그인 페이지 접속
    driver.get("https://the-internet.herokuapp.com/login")

    # 사용자 이름과 비밀번호 입력
    username_input = driver.find_element(By.ID, "username")
    password_input = driver.find_element(By.ID, "password")

    username_input.send_keys("tomsmith")  # 올바른 사용자 이름
    password_input.send_keys("SuperSecretPassword!")  # 올바른 비밀번호

    # 로그인 버튼 클릭
    login_button = driver.find_element(By.CSS_SELECTOR, "button[type='submit']")
    login_button.click()

    # 로그인 성공 메시지 확인
    success_message = driver.find_element(By.ID, "flash").text
    print(success_message)

finally:
    # WebDriver 종료
    driver.quit()
```

#### **학습 포인트**
1. **웹 요소 조작**: `find_element`와 `send_keys`, `click`을 사용하여 입력 필드에 데이터를 입력하고 버튼을 클릭하는 방법 학습.  
2. **데이터 추출**: `text` 속성을 활용해 웹 페이지에서 텍스트 데이터를 추출하고 결과를 확인하는 방법 익히기.  
3. **특정 요소 선택**: `By.ID`, `By.CSS_SELECTOR` 등 다양한 로케이터 전략을 사용하여 원하는 웹 요소를 정확히 선택하는 기술 습득.  
4. **자동화 프로세스 구현**: 로그인과 같은 일련의 작업을 자동화하여 실용적인 웹 상호작용을 구현하는 방법 학습.  
5. **리소스 관리**: `try-finally` 구문과 `driver.quit()`을 통해 WebDriver 세션을 안전하게 종료하고 리소스를 정리하는 중요성 이해.


## **3. 데이터 수집 연습**

```python
from selenium import webdriver
from selenium.webdriver.common.by import By
import time

# ChromeDriver 설정
driver = webdriver.Chrome()

try:
    # Wikipedia 접속
    driver.get("https://en.wikipedia.org/wiki/Squid_Game_season_2")
    time.sleep(2)  # 페이지 로딩 대기

    # 제목과 내용 추출
    title = driver.find_element(By.TAG_NAME, "h1").text
    contents = driver.find_elements(By.CSS_SELECTOR, "#mw-content-text p")
    print(f"제목: {title}")
    for i, content in enumerate(contents):
        if i in [1, 2, 3]:
            print(content.text)       

finally:
    # WebDriver 종료
    driver.quit()

```

#### **학습 포인트**
1. **데이터 추출**: `text` 속성을 사용하여 텍스트 데이터 추출.
2. **특정 요소 선택**: `find_element`,`find_elements`를 사용하여 원하는 정보만 추출.
3. **실용성**: 실제 웹사이트에서 유용한 정보를 수집하는 방법 학습.

---
