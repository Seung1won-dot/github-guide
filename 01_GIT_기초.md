# 1. Git 기초

> Git의 핵심 개념과 원리를 이해합니다.

---

## Git이란?

Git은 **분산 버전 관리 시스템(DVCS)**입니다.

여러 개발자가 동시에 같은 프로젝트에서 작업할 수 있도록 도와주는 도구입니다.

---

## 핵심 개념: 3가지 공간

```
┌─────────────────────────────────────────────────────────┐
│                    Git의 3가지 공간                       │
├─────────────────────────────────────────────────────────┤
│                                                         │
│   Working Directory          Staging Area          Git Directory │
│   (작업 디렉토리)              (스테이징 영역)          (Git 저장소)      │
│   ┌───────────┐            ┌───────────┐          ┌───────────┐  │
│   │ 파일 수정 │ ────────▶ │  git add  │ ───────▶ │  git      │  │
│   │   중      │            │           │          │  commit   │  │
│   └───────────┘            └───────────┘          └───────────┘  │
│                                                         │
│   수정된 파일들                커밋 대기 파일           저장된 버전      │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

### 1. Working Directory (작업 디렉토리)

프로젝트의 파일이 실제로 저장되어 있는 폴더입니다.

- 파일을 수정하면 → Working Directory에서 변경 발생
- 아직 Git의 관리 하에 있지 않은 상태

### 2. Staging Area (스테이징 영역)

커밋할 파일을 준비하는 공간입니다.

- `git add`로 파일을 추가
- 커밋 전에 최종 확인 가능
- 선택적으로 파일 포함 가능

### 3. Git Directory (저장소)

프로젝트의 모든 버전과 히스토리가 저장되는 공간입니다.

- `.git` 폴더 안에 모든 정보 저장
- 커밋하면 → 여기서 영구적으로 저장

---

## 왜 Git인가?

| 특징 | 설명 |
|------|------|
| **분산 관리** | 모든 개발자가 전체 저장소 사본을 가짐 |
| **비선형 개발** | 브랜치로 자유로운 병렬 개발 가능 |
| **속도** | 대부분의 操作이 로컬에서 수행되어 매우 빠름 |
| **무결성** | 모든 데이터에 SHA-1 해시로 무결성 보장 |
| **오프라인 가능** | 인터넷 없이도 대부분의 操作 가능 |

---

## 용어 정리

| 용어 | 설명 |
|------|------|
| **Repository** | Git이 관리하는 프로젝트 폴더 |
| **Commit** | 변경사항의 스냅샷을 저장하는 행위/결과 |
| **Branch** | 독립적인 개발 라인을 만드는 기능 |
| **Merge** | 여러 브랜치의 변경사항을 합치는 행위 |
| **Clone** | 원격 저장소를 내 컴퓨터로 복사 |
| **Push** | 로컬 변경사항을 원격에 올리기 |
| **Pull** | 원격 변경사항을 로컬에 가져오기 |

---

## Git 설치 확인

```bash
# 설치 여부 확인
git --version

# 예시 출력
# git version 2.40.0
```

### 설치 방법

| OS | 방법 |
|----|------|
| **Windows** | [git-scm.com](https://git-scm.com/download/win) 다운로드 |
| **macOS** | `brew install git` |
| **Linux** | `sudo apt install git` (Ubuntu/Debian) |

---

## Git 설정

```bash
# 사용자 정보 설정 (필수 - 커밋할 때 필요)
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"

# 기본 브랜치명 설정
git config --global init.defaultBranch main

# 컬러 활성화
git config --global color.ui auto

# 설정 확인
git config --list
```

---

## 저장소 초기화

```bash
# 새 프로젝트 시작
git init

# 기존 프로젝트 복제
git clone https://github.com/username/repository.git

# 특정 폴더에 복제
git clone https://github.com/username/repository.git my-folder
```

---

## Git의 상태

```
┌─────────────────────────────────────────────────────────────┐
│                      파일의 생명주기                          │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│   Untracked ──▶ Staged ──▶ Committed                       │
│       │            │            │                          │
│       │            │            └── Repository에 저장        │
│       │            │                                     │
│       │            └── git add 후 (커밋 대기)              │
│       │                                                │
│       └── Git이 관리하지 않는 새 파일                      │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

| 상태 | 설명 |
|------|------|
| **Untracked** | Git이 관리하지 않는 새 파일 |
| **Modified** | 수정되었지만 Staging Area에 없음 |
| **Staged** | 커밋 대기 상태 |
| **Committed** | Git 저장소에 저장됨 |

---

[← 이전: README](../README.md) | [다음: GitHub 기초 →](./02_GITHUB_기초.md)
