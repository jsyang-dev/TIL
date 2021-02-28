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

# git lg 명령어 설정
git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit --"

# 직접 수정 가능
vi ~/.gitconfig

# 정상 설정 확인
git config --list
```

### Git 기본

```bash
git add <파일명>
git commit <파일명>
```

### Branch 관련

```bash
# Show available local branch
git branch

# Show available remote branch
git branch -r

# Show available All branch
git branch -a

# Create branch
git branch <브랜치명>

# Checkout branch
git checkout <브랜치명>

# Create & Checkout branch
git checkout -b <브랜치명>

# Merge branch
git merge <브랜치명>

# Delete branch
git branch -D <브랜치명>

# Push with specified remote branch
$ git push origin <브랜치명>

# See the difference between two branches
$ git diff <브랜치명1> <브랜치명2>
```

### File rename

```bash
# Worst
mv <원본파일명> <변경파일명>  # deleted, new file

# Best
git mv <원본파일명> <변경파일명>  #renamed
```

### Unstaging

```bash
# Unstaging
git reset HEAD <파일명>

# Unstaging and remove
git rm -f <파일명>
```

### Edit commit log

```bash
# Edit latest commit
git commit --amend

# Edit prior commit
git rebase -i <commit>

# Abort rebase
git rebase --abort

# Complete rebase
$ git rebase --continue
```

### Reset commit log

```bash
# Worst: reset -> 이력이 사라짐
git reset --hard HEAD~3
git push -f origin <브랜치명>

# Best: revert -> 이력 commit 생성
git revert --no-commit HEAD~3
git commit
git push origin <브랜치명>
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

## Branching models

- Git Flow
  - (hotfix) - master - (release) - develop - feature
  - 장점: 가장 많이 적용, 각 단계가 명확히 구분
  - 단점: 복잡하다

- GitHub Flow
  - master - feature
  - 장점: 브랜치 모델 단순화, master의 모든 커밋은 deployable
  - 단점: CI 의존성 높음. 의도치 않은 배포가 이루어질 수 있음(Pull Request로 방지)

- GitLab Flow
  - production - pre-production - master - feature
  - 장점: deploy, issue에 대한 대응이 가능하도록 보완
  - 단점: Git Flow와 반대 (master<->develop, production<->master)

## 유용한 사이트

- .gitignore 생성: [https://gitignore.io](https://gitignore.io)
- git-flow cheatsheet: [https://danielkummer.github.io/git-flow-cheatsheet/index.ko_KR.html](https://danielkummer.github.io/git-flow-cheatsheet/index.ko_KR.html)
