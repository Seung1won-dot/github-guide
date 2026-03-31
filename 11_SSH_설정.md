# 11. SSH 설정

> GitHub에서 SSH 키를 생성하고 연동하는 방법을 학습합니다.

---

## SSH란?

Secure Shell - 서버에 안전하게 연결하는 프로토콜입니다.

```
Without SSH:                    With SSH:
아이디/비밀번호 입력              키 기반으로 자동 인증
매번 입력해야 함                 한번 설정하면 자동

HTTPS: https://github.com/username/repo
SSH:   git@github.com:username/repo
```

---

## 왜 SSH인가?

| HTTPS | SSH |
|-------|-----|
| 매번 토큰 입력 필요 | 자동 인증 |
| 복잡한 비밀번호 | 간단한 설정 |
| 토큰 관리 필요 | 키 파일만 관리 |

---

## SSH 키 생성

### Ed25519 (권장)

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

### RSA (호환성)

```bash
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

### 진행 과정

```
Generating public/private ed25519 key pair.
Enter file in which to save the key (/c/Users/username/.ssh/id_ed25519):
# Enter를 눌러 기본 위치 사용

Created directory '/c/Users/username/.ssh'.

Enter passphrase (empty for no passphrase):
# 비밀번호 입력 (선택사항, 但し 권장)

Enter same passphrase again:
# 비밀번호 재입력
```

---

## 공개키 확인

```bash
# 공개키 출력
cat ~/.ssh/id_ed25519.pub
# 또는
type $HOME\.ssh\id_ed25519.pub   # Windows

# 출력 예시:
# ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAI...
# your_email@example.com
```

---

## GitHub에 SSH 키 추가

### 단계

1. GitHub에 로그인
2. **Settings** 클릭 (우측 상단 프로필 아이콘)
3. **SSH and GPG keys** 클릭
4. **New SSH key** 클릭
5. **Title**: 기기 이름 입력 (예: "My Laptop")
6. **Key**: 공개키 붙여넣기
7. **Add SSH key** 클릭

---

## 연결 테스트

```bash
# 테스트
ssh -T git@github.com

# 출력 예시 (성공):
# Hi username! You've successfully authenticated...

# 출력 예시 (실패):
# Permission denied (publickey)...
```

---

## Windows에서 SSH Agent 실행

```bash
# SSH Agent 서비스 시작
Start-Service ssh-agent

# 키 추가
ssh-add ~/.ssh/id_ed25519

# 키 목록 확인
ssh-add -l

# 시스템 시작 시 자동 실행 (관리자 권한)
Set-Service -Name ssh-agent -StartupType Automatic
```

---

## 다중 계정 설정

### 문제 상황

```
Personal: github.com/my-account
Work:     github.com/company-account
```

### 해결 방법

```bash
# 1. 작업용 키 생성
ssh-keygen -t ed25519 -C "work@email.com" -f ~/.ssh/id_ed25519_work

# 2. SSH Config 설정
# Windows: C:\Users\username\.ssh\config
# Linux/Mac: ~/.ssh/config
```

```ssh-config
# 기본 (Personal)
Host github.com
   HostName github.com
   User git
   IdentityFile ~/.ssh/id_ed25519
   IdentitiesOnly yes

# 작업용
Host github-work
   HostName github.com
   User git
   IdentityFile ~/.ssh/id_ed25519_work
   IdentitiesOnly yes
```

### 사용법

```bash
# Personal
git clone git@github.com:username/repo.git

# Work
git clone git@github-work:company/repo.git
```

---

## SSH Config 전체 예시

```ssh-config
# GitHub (Personal)
Host github.com
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_ed25519
    IdentitiesOnly yes

# GitHub Enterprise (Work)
Host github.company.com
    HostName github.company.com
    User git
    IdentityFile ~/.ssh/id_ed25519_work
    IdentitiesOnly yes

# GitLab
Host gitlab.com
    HostName gitlab.com
    User git
    IdentityFile ~/.ssh/id_ed25519_gitlab
    IdentitiesOnly yes
```

---

## 키 관리

```bash
# 키 목록 확인
ls -la ~/.ssh/

# 키 삭제
rm ~/.ssh/id_ed25519
rm ~/.ssh/id_ed25519.pub

# 비밀번호 변경
ssh-keygen -p -f ~/.ssh/id_ed25519

# 공개키フィンガープリント 확인
ssh-keygen -lf ~/.ssh/id_ed25519.pub
```

---

## 문제 해결

### 1. "Permission denied (publickey)"

```bash
# 키가 로드되었는지 확인
ssh-add -l

# 추가
ssh-add ~/.ssh/id_ed25519

# 디버그 출력으로 확인
ssh -vT git@github.com
```

### 2. "Could not open a connection to your authentication agent"

```bash
# Agent 시작
eval "$(ssh-agent -s)"

# 또는 Windows
Start-Service ssh-agent
```

### 3. 키가 인식되지 않음

```bash
# 퍼미션 확인 (Linux/Mac)
chmod 700 ~/.ssh
chmod 600 ~/.ssh/id_ed25519
chmod 644 ~/.ssh/id_ed25519.pub
```

### 4. Wrong key being used

```bash
# SSH Config에 IdentitiesOnly yes 추가
# 또는 명시적으로指定
ssh -i ~/.ssh/specific_key git@github.com
```

---

## GitHub Enterprise

```bash
# Enterprise URL로 clone
git clone git@github.company.com:org/repo.git
```

SSH Config:

```ssh-config
Host github.company.com
    HostName github.company.com
    User git
    IdentityFile ~/.ssh/company_key
```

---

## 명령어 요약표

| 명령어 | 설명 |
|--------|------|
| `ssh-keygen -t ed25519 -C "email"` | Ed25519 키 생성 |
| `cat ~/.ssh/id_ed25519.pub` | 공개키 확인 |
| `ssh -T git@github.com` | 연결 테스트 |
| `ssh-add ~/.ssh/key` | Agent에 키 추가 |
| `ssh-add -l` | 로드된 키 목록 |
| `ssh -vT git@github.com` | 디버그 |

---

[← 이전: GitHub CLI](./10_GitHub_CLI.md) | [다음: Git 설정 →](./12_Git_설정.md)
