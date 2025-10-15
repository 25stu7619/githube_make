# GitHub 사용 방법 가이드

GitHub를 처음 시작하는 분들을 위한 완벽 가이드입니다.

## 목차
- [1. GitHub 시작하기](#1-github-시작하기)
- [2. 저장소(Repository) 관리](#2-저장소repository-관리)
- [3. Git 기본 명령어](#3-git-기본-명령어)
- [4. 브랜치(Branch) 관리](#4-브랜치branch-관리)
- [5. 협업하기](#5-협업하기)
- [6. 이슈(Issues) 관리](#6-이슈issues-관리)
- [7. Pull Request](#7-pull-request)
- [8. GitHub Actions](#8-github-actions)
- [9. 유용한 팁](#9-유용한-팁)

---

## 1. GitHub 시작하기

### 1.1 계정 만들기
1. [GitHub](https://github.com) 웹사이트 방문
2. "Sign up" 버튼 클릭
3. 이메일, 비밀번호, 사용자명 입력
4. 이메일 인증 완료

### 1.2 Git 설치
```bash
# Windows: git-scm.com에서 다운로드

# Mac
brew install git

# Linux (Ubuntu/Debian)
sudo apt-get install git

# 설치 확인
git --version
```

### 1.3 Git 초기 설정
```bash
# 사용자 이름 설정
git config --global user.name "Your Name"

# 이메일 설정
git config --global user.email "your.email@example.com"

# 설정 확인
git config --list
```

---

## 2. 저장소(Repository) 관리

### 2.1 새 저장소 만들기

**웹에서 만들기:**
1. GitHub 로그인
2. 우측 상단 "+" 버튼 클릭
3. "New repository" 선택
4. 저장소 이름, 설명 입력
5. Public/Private 선택
6. README 파일 추가 (선택)
7. "Create repository" 클릭

**로컬에서 만들기:**
```bash
# 새 디렉토리 생성
mkdir my-project
cd my-project

# Git 저장소 초기화
git init

# README 파일 생성
echo "# My Project" >> README.md

# 파일 추가
git add README.md

# 첫 커밋
git commit -m "Initial commit"

# GitHub 저장소와 연결
git remote add origin https://github.com/username/repository.git

# 푸시
git push -u origin main
```

### 2.2 기존 저장소 복제하기
```bash
# HTTPS로 복제
git clone https://github.com/username/repository.git

# SSH로 복제
git clone git@github.com:username/repository.git

# 특정 브랜치 복제
git clone -b branch-name https://github.com/username/repository.git
```

---

## 3. Git 기본 명령어

### 3.1 파일 추가 및 커밋
```bash
# 작업 디렉토리 상태 확인
git status

# 특정 파일 추가
git add filename.txt

# 모든 변경사항 추가
git add .

# 커밋하기
git commit -m "커밋 메시지"

# 추가와 커밋 동시에
git commit -am "커밋 메시지"
```

### 3.2 변경사항 확인
```bash
# 변경사항 보기
git diff

# 스테이징된 변경사항 보기
git diff --staged

# 커밋 히스토리 보기
git log

# 간단한 로그 보기
git log --oneline

# 그래프로 보기
git log --graph --oneline --all
```

### 3.3 원격 저장소와 동기화
```bash
# 원격 저장소에서 가져오기 (fetch + merge)
git pull

# 원격 저장소에 올리기
git push

# 원격 저장소 확인
git remote -v

# 원격 저장소 추가
git remote add origin https://github.com/username/repository.git
```

### 3.4 변경사항 되돌리기
```bash
# 작업 디렉토리 변경사항 취소
git checkout -- filename.txt

# 스테이징 취소
git reset HEAD filename.txt

# 마지막 커밋 취소 (변경사항 유지)
git reset --soft HEAD~1

# 마지막 커밋 취소 (변경사항 삭제)
git reset --hard HEAD~1

# 특정 커밋으로 되돌리기
git revert commit-hash
```

---

## 4. 브랜치(Branch) 관리

### 4.1 브랜치 기본
```bash
# 브랜치 목록 보기
git branch

# 원격 브랜치 포함 목록
git branch -a

# 새 브랜치 만들기
git branch feature-branch

# 브랜치 전환
git checkout feature-branch

# 브랜치 만들고 전환 (한 번에)
git checkout -b feature-branch

# 최신 Git (2.23+)
git switch feature-branch
git switch -c feature-branch
```

### 4.2 브랜치 병합
```bash
# main 브랜치로 전환
git checkout main

# feature 브랜치 병합
git merge feature-branch

# 병합 충돌 해결 후
git add .
git commit -m "Merge conflict resolved"
```

### 4.3 브랜치 삭제
```bash
# 로컬 브랜치 삭제
git branch -d feature-branch

# 강제 삭제
git branch -D feature-branch

# 원격 브랜치 삭제
git push origin --delete feature-branch
```

---

## 5. 협업하기

### 5.1 Fork와 Clone
1. GitHub에서 원하는 저장소 페이지 방문
2. 우측 상단 "Fork" 버튼 클릭
3. 내 계정으로 복사된 저장소 확인
4. 로컬로 clone:
```bash
git clone https://github.com/your-username/forked-repo.git
cd forked-repo
```

### 5.2 Upstream 설정
```bash
# 원본 저장소를 upstream으로 추가
git remote add upstream https://github.com/original-owner/original-repo.git

# 확인
git remote -v

# upstream에서 최신 변경사항 가져오기
git fetch upstream

# main 브랜치 업데이트
git checkout main
git merge upstream/main
```

### 5.3 협업자 추가
1. 저장소 페이지에서 "Settings" 클릭
2. 좌측 메뉴에서 "Collaborators" 선택
3. "Add people" 버튼 클릭
4. 사용자명 또는 이메일로 검색
5. 초대 전송

---

## 6. 이슈(Issues) 관리

### 6.1 이슈 생성
1. 저장소의 "Issues" 탭 클릭
2. "New issue" 버튼 클릭
3. 제목과 설명 작성
4. 라벨(Label), 담당자(Assignee) 지정
5. "Submit new issue" 클릭

### 6.2 이슈 템플릿
`.github/ISSUE_TEMPLATE/bug_report.md` 파일 생성:
```markdown
---
name: Bug Report
about: 버그 리포트 작성
title: '[BUG] '
labels: bug
assignees: ''
---

## 버그 설명
버그에 대한 명확한 설명

## 재현 방법
1. 
2. 
3. 

## 예상 동작


## 실제 동작


## 스크린샷


## 환경
- OS: 
- 브라우저: 
- 버전: 
```

### 6.3 이슈 연결
```bash
# 커밋 메시지에서 이슈 참조
git commit -m "Fix login bug #123"

# 이슈 자동 닫기
git commit -m "Fixes #123"
git commit -m "Closes #123"
git commit -m "Resolves #123"
```

---

## 7. Pull Request

### 7.1 PR 생성하기
1. 새 브랜치에서 작업 완료
```bash
git checkout -b feature/new-feature
# 작업 수행
git add .
git commit -m "Add new feature"
git push origin feature/new-feature
```

2. GitHub 웹사이트에서:
   - 저장소 페이지 방문
   - "Pull requests" 탭 클릭
   - "New pull request" 버튼 클릭
   - base와 compare 브랜치 선택
   - 제목과 설명 작성
   - "Create pull request" 클릭

### 7.2 PR 템플릿
`.github/PULL_REQUEST_TEMPLATE.md` 파일 생성:
```markdown
## 변경사항 설명


## 관련 이슈
Closes #

## 변경 유형
- [ ] 버그 수정
- [ ] 새 기능
- [ ] 문서 업데이트
- [ ] 리팩토링

## 체크리스트
- [ ] 코드가 정상적으로 동작함
- [ ] 테스트 추가/업데이트 완료
- [ ] 문서 업데이트 완료
- [ ] 코드 리뷰 완료

## 스크린샷 (해당되는 경우)

```

### 7.3 코드 리뷰
- "Files changed" 탭에서 변경사항 확인
- 특정 라인에 코멘트 추가
- "Review changes" 버튼으로 승인/변경요청
- 대화를 통해 개선사항 논의

### 7.4 PR 병합
1. 리뷰 승인 후 "Merge pull request" 클릭
2. 병합 방식 선택:
   - **Merge commit**: 모든 커밋 이력 유지
   - **Squash and merge**: 하나의 커밋으로 합치기
   - **Rebase and merge**: 선형 이력 유지
3. "Confirm merge" 클릭
4. 브랜치 삭제 옵션 선택

---

## 8. GitHub Actions

### 8.1 기본 워크플로우
`.github/workflows/ci.yml` 파일 생성:
```yaml
name: CI

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest
    
    steps:
    - uses: actions/checkout@v3
    
    - name: Set up Node.js
      uses: actions/setup-node@v3
      with:
        node-version: '18'
    
    - name: Install dependencies
      run: npm install
    
    - name: Run tests
      run: npm test
    
    - name: Build
      run: npm run build
```

### 8.2 자동 배포 예제
```yaml
name: Deploy

on:
  push:
    branches: [ main ]

jobs:
  deploy:
    runs-on: ubuntu-latest
    
    steps:
    - uses: actions/checkout@v3
    
    - name: Deploy to GitHub Pages
      uses: peaceiris/actions-gh-pages@v3
      with:
        github_token: ${{ secrets.GITHUB_TOKEN }}
        publish_dir: ./dist
```

---

## 9. 유용한 팁

### 9.1 .gitignore 파일
프로젝트 루트에 `.gitignore` 파일 생성:
```
# 의존성
node_modules/
vendor/

# 환경 변수
.env
.env.local

# 빌드 결과물
dist/
build/
*.log

# IDE 설정
.vscode/
.idea/
*.swp

# OS 파일
.DS_Store
Thumbs.db
```

### 9.2 SSH 키 설정
```bash
# SSH 키 생성
ssh-keygen -t ed25519 -C "your.email@example.com"

# SSH 에이전트에 키 추가
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519

# 공개 키 복사
cat ~/.ssh/id_ed25519.pub
```

GitHub 설정:
1. Settings → SSH and GPG keys
2. "New SSH key" 클릭
3. 공개 키 붙여넣기

### 9.3 유용한 명령어 모음
```bash
# 스태시 (임시 저장)
git stash
git stash list
git stash apply
git stash pop

# 태그
git tag v1.0.0
git push origin v1.0.0

# 특정 파일만 체크아웃
git checkout branch-name -- path/to/file

# 커밋 작성자 변경
git commit --amend --author="Name <email@example.com>"

# 원격 브랜치 추적
git branch --set-upstream-to=origin/main main
```

### 9.4 GitHub CLI 사용
```bash
# GitHub CLI 설치
brew install gh  # Mac
winget install GitHub.cli  # Windows

# 로그인
gh auth login

# 저장소 복제
gh repo clone owner/repo

# PR 생성
gh pr create

# 이슈 생성
gh issue create
```

### 9.5 좋은 커밋 메시지 작성법
```
feat: 새로운 기능 추가
fix: 버그 수정
docs: 문서 수정
style: 코드 포맷팅, 세미콜론 누락 등
refactor: 코드 리팩토링
test: 테스트 코드 추가
chore: 빌드 업무, 패키지 매니저 설정 등

예시:
feat: 사용자 로그인 기능 추가
fix: 로그아웃 시 세션 오류 수정
docs: README에 설치 방법 추가
```

---

## 참고 자료

- [GitHub 공식 문서](https://docs.github.com)
- [Git 공식 문서](https://git-scm.com/doc)
- [GitHub Learning Lab](https://lab.github.com)
- [Pro Git Book](https://git-scm.com/book/ko/v2)

---

**Happy Coding! 🚀**
