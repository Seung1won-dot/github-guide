# 12. Git 설정

> Git의 기본 설정과 커스터마이징 방법을 학습합니다.

---

## 설정 Levels

Git 설정은 3단계로 나뉩니다.

```
System    (모든 사용자)    /etc/gitconfig
Global    (현재 사용자)    ~/.gitconfig
Local     (현재 저장소)    .git/config
```

| Level | 범위 | 우선순위 |
|-------|------|---------|
| `--system` | 시스템 전체 | lowest |
| `--global` | 사용자 전체 | middle |
| `--local` | 현재 저장소 | highest |

---

## 기본 설정

### 사용자 정보 (필수)

```bash
# Global 설정 (권장)
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"

# Local 설정 (특정 프로젝트만)
git config --local user.name "Project Name"
git config --local user.email "project@email.com"
```

### 에디터 설정

```bash
# VS Code (권장)
git config --global core.editor "code --wait"

# Vim
git config --global core.editor vim

# Nano
git config --global core.editor nano

# Windows
git config --global core.editor "code --wait"
```

---

## 출력 설정

### 컬러

```bash
# 컬러 활성화
git config --global color.ui auto

# 개별 설정
git config --global color.branch current "yellow reverse"
git config --global color.branch.remote "green"
git config --global color.diff.meta "yellow bold"
```

### 한글 파일명

```bash
# 한글 파일명 정상 표시 (Windows)
git config --global core.quotepath false
```

---

## 기본 동작 설정

### Pull 전략

```bash
# Rebase 모드 (히스토리 깔끔하게)
git config --global pull.rebase true

# Merge 모드 (기본)
git config --global pull.rebase false

# Rebase 시 자동 stash
git config --global rebase.autostash true
```

### Push 기본값

```bash
# 현재 브랜치만
git config --global push.default current

# 업스트림 설정된 브랜치만
git config --global push.default upstream

# 모든 브랜치
git config --global push.default matching
```

### 기본 브랜치명

```bash
# 새 저장소의 기본 브랜치명
git config --global init.defaultBranch main
```

---

## Credential 관리

### 캐시

```bash
# 시간 설정 (초)
git config --global credential.helper cache
git config --global credential.helper "cache --timeout=3600"
```

### Store

```bash
# 파일에 저장
git config --global credential.helper store

# ⚠️ 비밀번호가 평문으로 저장됨 (권장하지 않음)
```

### macOS

```bash
git config --global credential.helper osxkeychain
```

### Windows

```bash
# Manager
git config --global credential.helper manager

# Windows Credential Manager 사용
```

---

## Diff & Merge 설정

### Diff 도구

```bash
# VS Code
git config --global diff.tool vscode
git config --global difftool.vscode.cmd 'code --wait --diff $LOCAL $REMOTE'

# 사용
git difftool
```

### Merge 도구

```bash
# VS Code
git config --global merge.tool vscode
git config --global mergetool.vscode.cmd 'code --wait $MERGED'

# 사용
git mergetool
```

### Less 명령어

```bash
# 긴 출력에서 q로 종료
git config --global core.pager less

# 항상 pager 사용
git config --global core.pager less -FRX
```

---

## Alias 설정

### 단축 명령어

```bash
# 간단한 alias
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.unstage 'reset HEAD --'

# 복잡한 alias
git config --global alias.lg "log --graph --oneline --all"
git config --global alias.last "log -1 HEAD"
git config --global alias.visual "log --graph"
```

### Bash Alias

```bash
# ~/.bashrc 또는 ~/.zshrc에 추가
alias gs='git status'
alias ga='git add .'
alias gc='git commit'
alias gp='git push'
alias gl='git log --oneline'
alias gd='git diff'
alias gco='git checkout'
alias gb='git branch'
alias gpull='git pull'
alias gfetch='git fetch'
```

---

## 기본 Branch

```bash
# 현재 설정 확인
git config --global init.defaultBranch

# 변경
git config --global init.defaultBranch main
```

---

## Log 설정

```bash
# 기본 포맷
git config --global log.date relative
git config --global log.date short
git config --global log.date local
git config --global log.date iso

# 히스토리 제한
git config --global log.decorate short
```

---

## Ignore 설정

### Global .gitignore

```bash
# 전역으로 무시할 파일
git config --global core.excludesfile ~/.gitignore_global

# ~/.gitignore_global 파일 생성
# OS, IDE, 언어별 공통 파일 추가
```

예시:

```gitignore
# macOS
.DS_Store

# Windows
Thumbs.db

# IDE
.idea/
.vscode/

# Logs
*.log

# Node
node_modules/
```

---

## 자동纠错

```bash
# 오타 자동修正
git config --global help.autocorrect 10

# 설명:
# 0  = 비활성화
# 10 = 0.1초 후 자동 실행
# 20 = 0.2초 후 자동 실행
```

---

## 설정 확인

```bash
# 모든 설정
git config --list

# 특정 설정
git config user.name
git config core.editor

# 파일별 설정
git config --list --show-origin
```

---

## .gitconfig 파일

`~/.gitconfig` 파일을 직접 편집할 수 있습니다.

```ini
[user]
    name = Your Name
    email = your.email@example.com

[core]
    editor = code --wait
    autocrlf = input
    excludesfile = ~/.gitignore_global

[pull]
    rebase = true

[push]
    default = current

[alias]
    st = status
    co = checkout
    br = branch
    ci = commit
    lg = log --graph --oneline --all

[color]
    ui = auto

[help]
    autocorrect = 10
```

---

## 환경 변수

```bash
# GIT_AUTHOR, GIT_COMMITTER
# 설정하지 않으면 user.name, user.email 사용

# GIT_DIR (저장소 경로)
# GIT_WORK_TREE (작업 디렉토리 경로)

# GIT_SSH_COMMAND
GIT_SSH_COMMAND="ssh -i ~/.ssh/custom_key"

# GIT_EDITOR
GIT_EDITOR="vim"
```

---

## 권장 설정 복사

새 시스템에서 빠르게 설정:

```bash
# 1. 현재 설정 export
git config --global --list > gitconfig_backup.txt

# 2. 새 시스템에서 import
git config --global --list --file gitconfig_backup.txt | \
  while read line; do git config --global "$line"; done
```

---

## 명령어 요약표

| 명령어 | 설명 |
|--------|------|
| `git config --list` | 모든 설정 확인 |
| `git config --list --show-origin` | 설정 출처 포함 |
| `git config user.name` | 특정 설정 확인 |
| `git config --global <key> <value>` | Global 설정 |
| `git config --local <key> <value>` | Local 설정 |

---

[← 이전: SSH 설정](./11_SSH_설정.md) | [↑ 처음으로 →](../README.md)
