# 10. GitHub CLI

> GitHub CLI 설치와 활용법을 학습합니다.

---

## GitHub CLI란?

命令行에서 GitHub를 사용할 수 있게 해주는 도구입니다.

```
Without CLI:              With CLI:
브라우저 열기 ──▶ GitHub    터미널에서 바로 사용
     │                        │
     │                        ├── gh pr create
     │                        ├── gh issue list
     ▼                        └── gh repo clone
```

---

## 설치

### macOS

```bash
# Homebrew
brew install gh

# MacPorts
sudo port install gh
```

### Windows

```bash
# Winget (권장)
winget install GitHub.cli

# Chocolatey
choco install gh
```

### Linux

```bash
# Debian/Ubuntu
sudo apt install gh

# Fedora
sudo dnf install gh

# Snap
sudo snap install gh
```

### Binaries

直接 [github.com/cli/cli](https://github.com/cli/cli/releases)에서 다운로드

---

## 인증

```bash
# 로그인
gh auth login

# 상태 확인
gh auth status

# 로그아웃
gh auth logout

# 토큰으로 로그인 (CI/CD용)
gh auth login --with-token < TOKEN
```

### 인증 옵션

```bash
gh auth login
# ? What account do you want to log into? GitHub.com
# ? What is your preferred protocol for Git operations? SSH
# ? Generate a new SSH key to add to your GitHub account? Yes
# ? Enter a passphrase for your new SSH key: (비밀번호)
# ? Title for your SSH key: GitHub CLI
# ? Upload your SSH public key to your GitHub account? Yes
```

---

## Repository

```bash
# 새 저장소 생성 (현재 디렉토리)
gh repo create

# 새 저장소 생성 (원격)
gh repo create my-repo

# Public 저장소
gh repo create my-repo --public

# Private 저장소
gh repo create my-repo --private

# Clone
gh repo clone owner/repo
gh repo clone owner/repo -- --branch develop

# Fork
gh repo fork owner/repo

# View
gh repo view
gh repo view owner/repo --web
```

---

## Pull Request

### 생성

```bash
# 대화형
gh pr create

# 직접 지정
gh pr create --title "Add feature" --body "Description"

# 파일에서 본문 읽기
gh pr create --title "Add feature" --body-file body.md

# 자동으로 제목/본문 채우기 (커밋 메시지 기반)
gh pr create --fill

# 브랜치 지정
gh pr create --base main --head feature-branch

# 리뷰어 지정
gh pr create --reviewer username1,username2
```

### 조회

```bash
# 목록
gh pr list
gh pr list --state open
gh pr list --state closed
gh pr list --author @me

# 필터
gh pr list --label bug
gh pr list --assignee @me
gh pr list --search "feat:"

# 상세
gh pr view 123
gh pr view 123 --web
gh pr view 123 --comments
```

### 리뷰

```bash
# 승인
gh pr review 123 --approve

# 변경 요청
gh pr review 123 --request-changes -b "의견"

# 코멘트만
gh pr review 123 --comment -b "의견"
```

### 병합 & 닫기

```bash
# 병합
gh pr merge 123
gh pr merge 123 --squash  # 스쿼시
gh pr merge 123 --rebase # 리베이스
gh pr merge 123 --admin  # 관리자만

# 병합 후 자동 삭제
gh pr merge 123 --delete-branch

# 닫기
gh pr close 123
```

---

## Issue

### 생성

```bash
# 대화형
gh issue create

# 직접 지정
gh issue create --title "Bug: login fails" --body "Steps to reproduce"

# 파일에서 본문
gh issue create --title "Bug" --body-file bug.md

# 라벨
gh issue create --label bug,priority-high

# 담당자
gh issue create --assignee username
```

### 조회

```bash
# 목록
gh issue list
gh issue list --state open
gh issue list --label bug

# 필터
gh issue list --assignee @me
gh issue list --search "keyword"

# 상세
gh issue view 123
gh issue view 123 --web
```

### 관리

```bash
# 닫기
gh issue close 123

# 코멘트
gh issue comment 123 --body "의견"
```

---

## Release

```bash
# 생성
gh release create v1.0.0
gh release create v1.0.0 --title "Version 1.0" --notes "Release notes"

# 파일 첨부
gh release create v1.0.0 --attach asset.zip

# 목록
gh release list

# 상세
gh release view v1.0.0

# 삭제
gh release delete v1.0.0
```

---

## Gist

```bash
# 생성
echo "content" | gh gist create
gh gist create file.txt
gh gist create --public file.txt

# 목록
gh gist list

# View
gh gist view abc123
```

---

## Workflow

```bash
# 목록
gh run list

# 상세
gh run view 12345

# 대기 중인 workflow 실행
gh workflow run

# 특정 workflow 실행
gh workflow run build.yml

# 다운로드 (artifact)
gh run download 12345 --dir ./artifacts
```

---

## 검색

```bash
# Repository 검색
gh search repos --qualifiers language=javascript stars=>1000

# Issue 검색
gh search issues "login bug" --label bug

# PR 검색
gh search prs "feat:" --state open

# 코드 검색
gh search code "function login" --owner my-org
```

---

## Alias

```bash
# Alias 등록
gh alias set co 'pr checkout'
gh alias set ls 'repo list'

# Alias 목록
gh alias list

# 사용
gh co 123      # gh pr checkout 123
gh ls          # gh repo list
```

---

## 환경 변수

CI/CD에서 유용합니다.

```bash
# 토큰 지정
GH_TOKEN=ghp_xxx gh pr create

# 기본 출력 형식
GH_FORMAT=json
GH_FORMAT=csv

# 호스트 지정
GH_HOST=github.example.com
```

---

## 팁 & 트릭

```bash
# 항상 --web 플래그로 브라우저 열기
gh repo view --web
gh issue create --web

# jq와 함께 사용
gh pr list --json number,title,state | jq '.[] | select(.state == "OPEN")'

# 타이틀 자동 생성
gh pr create --title "$(git log -1 --format=%s)"

# 대화형 선택
gh pr create --reviewer $(gh api repos/:owner/:repo/contributors --jq '.[0].login')
```

---

## 명령어 요약표

| 카테고리 | 명령어 |
|---------|--------|
| **인증** | `gh auth login`, `gh auth status` |
| **Repo** | `gh repo create`, `gh repo clone`, `gh repo fork` |
| **PR** | `gh pr create`, `gh pr list`, `gh pr merge` |
| **Issue** | `gh issue create`, `gh issue list`, `gh issue close` |
| **Release** | `gh release create`, `gh release list` |
| **Run** | `gh run list`, `gh workflow run` |
| **검색** | `gh search repos`, `gh search issues` |

---

[← 이전: 명령어 레퍼런스](./09_명령어_레퍼런스.md) | [다음: SSH 설정 →](./11_SSH_설정.md)
