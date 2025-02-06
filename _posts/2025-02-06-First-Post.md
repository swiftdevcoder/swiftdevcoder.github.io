- 에러발생-
  * Ignoring ffi-1.15.5 because its extensions are not built. Try: gem pristine ffi --version 1.15.5


Ruby 2.6.10 버전은 꽤 오래된 버전이며, minimal-mistakes와 최신 gem들과 호환성 문제가 있을 수 있습니다. 최신 버전의 Ruby로 업그레이드하는 것을 추천드립니다.

MacOS에서 Ruby 업그레이드 방법:

1. 먼저 rbenv 설치 (Ruby 버전 관리자):
```bash
brew install rbenv ruby-build
```

2. rbenv 초기화:
```bash
echo 'eval "$(rbenv init - zsh)"' >> ~/.zshrc  # zsh 사용시
# 또는
echo 'eval "$(rbenv init - bash)"' >> ~/.bashrc  # bash 사용시
```

3. 터미널 재시작 후, 최신 안정 버전의 Ruby 설치:
```bash
rbenv install 3.2.3  # 현재 안정 버전
rbenv global 3.2.3   # 시스템 전체 기본 버전으로 설정
```

4. Ruby 버전 확인:
```bash
ruby -v
```

5. gem 환경 초기화:
```bash
gem update --system
gem install bundler jekyll
```

6. 프로젝트 폴더로 이동하여 다시 시도:
```bash
bundle install
bundle exec jekyll serve
```

이렇게 하면 ffi 관련 오류를 포함한 대부분의 호환성 문제가 해결될 것입니다. Ruby 3.x 버전은 더 나은 성능과 최신 보안 업데이트를 제공합니다.
