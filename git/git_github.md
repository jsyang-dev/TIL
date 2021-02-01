# Git 강의

## 개요

리누스 토발즈가 2주만에 만든 버전관리 시스템이라고 한다(대단..)

## 특징

- 빠른 속도, 단순한 구조
- 분산형 저장소 지원
- 비선형적 개발 가능(브랜치)

## 대표 서비스

- GitHub: 비영리였던, Microsoft에 인수된 가장 유명한 서비스
- Bitbucket: Atlassian이 서비스. Jira, Confluence, Trello 등의 부가도구와 유기적
- GitLab: GitLab이 서비스. 사설 서버 구성이 가능

## 명령어

### Git 설치 확인

```bash
git -v
```

### Git 환경설정

```bash
# 환경설정
git config --global user.name "your username"
git config --global user.email "your email"
git config --global core.editor "vim"
git config --global core.pager "cat"

# 직접 수정 가능
vi ~/.gitconfig

# 정상 설정 확인
git config --list
```

### Git 기본 명령어

```bash
git add [파일명]
git commit [파일명]
git push origin master
```

## Conventional Commits

- commit의 제목은 commit을 설명하는 하나의 구나 절로 완성
- prefix 다음 첫 문자는 대문자로
- prefix 꼭 달기
  - feat: 기능 개발 관련
  - fix: 오류 개선 혹은 버그 패치
  - docs: 문서화 작업
  - test: test 관련
  - conf: 환경설정 관련
  - build: 빌드 관련
  - ci: Continuous Integration 관련
- 참고: [https://www.conventionalcommits.org/ko/v1.0.0/](https://www.conventionalcommits.org/ko/v1.0.0/)
