---
title: VScode에서 Minimal Mistakes 테마 블로그 컨트롤 하기
layout: single
classes: wide
permalink: /vscode-blog-connect/

---
Minimal Mistakes 테마를 사용하여 블로그를 운영시 VS Code와 연동해 편리하게 관리하려면 다음과 같은 설정 절차를 따라야 합니다. Windows 환경에 초점을 맞추어 설명하겠습니다.

---
### 1. Git 계정 생성 및 관련 소스 Fork하기
1. **Git 계정 생성하기**
    https://github.com 에서 SingUp하기 (개발자 전용 Gmail사용하기)

2. **관련 블로그 테마 Fork하기**
    - minimal mistakes 테마
    - 수정된 샘플 테마인 https://github.com/bigdataseek/bigdataseek.github.io로 이동
    - 우상단의 Fork 클릭
    - repostory명 입력란에 본인 git의 username 입력하기(username이 marbledata면 marbledata로 입력)

3. **Git 설치**
   - [Git for Windows](https://git-scm.com/download/win)를 설치합니다.
   - 설치 후 Git Bash를 사용해 기본 명령어를 실행할 수 있습니다.

4. **Git Bash 실행하여 본인 repository clone**
    - 시작 메뉴에서 "Git Bash"를 검색하여 실행합니다.
    - 본인 repository clone
    ```bash
     git clone https://github.com/본인username/본인username.github.io
     ```
    
---

### 2. **환경 설정 준비**
1. **Ruby 및 Bundler 설치**
   Minimal Mistakes는 Jekyll 기반으로 동작하므로 Ruby가 필요합니다.
   - [RubyInstaller](https://rubyinstaller.org/)를 통해 Windows용 Ruby를 설치합니다.
     - 설치 시 "Add Ruby executables to your PATH" 옵션을 체크하세요.
     - 설치 완료 후, `ridk install`을 실행해 필수 구성 요소를 설치합니다.
   - 설치 확인:
     ```bash
     ruby -v
     gem -v
     ```

2. **Jekyll 및 Bundler 설치**
   - RubyGems로 Jekyll과 Bundler를 설치합니다.
     ```bash
     gem install jekyll bundler
     ```

4. **VS Code 설치**
   - [VS Code](https://code.visualstudio.com/)를 설치하기

---

### 3. **VS Code와 연동**
1. **프로젝트 열기**
   - VS Code에서 `File > Open Folder`를 선택하고 블로그 프로젝트 폴더를 엽니다.

2. **Live Server 설정**

    - Gemfile 업데이트:
    ```bash
     bundle install
     ```

    - Jekyll 개발 서버를 실행합니다:
     ```bash
     bundle exec jekyll serve
     ```
   - 브라우저에서 `http://localhost:4000`로 블로그를 확인할 수 있습니다.

3. **VS Code 터미널 설정**
   - VS Code 내장 터미널에서 Jekyll 명령어를 실행하려면 `bash` 쉘을 사용하는 것이 좋습니다.
     - `Ctrl + Shift + P` > `Select Default Shell` > `Git Bash` 선택.

4. **자동화된 편집 경험**
   - VS Code에서 Ruby 관련 확장 프로그램과 Markdown 관련 플러그인을 설치해 개발 경험을 향상시킵니다.
   - 주요 확장 추천:
        - `Markdown All in One`, 
        - `Prettier - Code formatter`

---

### 4. **테마 커스터마이징**
Minimal Mistakes 테마는 `_config.yml`와 `_posts`, `_pages` 디렉토리를 수정하여 커스터마이징할 수 있습니다.

- **로고/이미지 추가**
  - `assets/images/`에 이미지를 추가한 뒤 `_config.yml`에서 참조합니다.


---


### 5. **수정사항 Commit**

--- 


### 요약
1. Ruby, Git, VS Code 설치.
2. Minimal Mistakes 테마 설치 및 Jekyll 설정.
3. VS Code와 연동해 개발.
4. GitHub Pages로 배포.

