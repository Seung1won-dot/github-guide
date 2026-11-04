# Git & GitHub 가이드

Git 기초 개념부터 브랜치, 원격 저장소, 협업 워크플로우, GitHub CLI·SSH 설정까지 공부하며 정리한 한국어 학습 문서 모음입니다. 위에서부터 차례로 읽으면 개념에서 실전까지 자연스럽게 이어집니다.

| 항목 | 내용 |
|------|------|
| 학습 목표 | Git의 동작 원리를 이해하고, 브랜치 · 원격 저장소 · PR 기반 협업을 혼자서도 막힘없이 하기 |
| 학습 범위 | 12개 문서 — 시작하기(2) · 핵심 기능(4) · 협업 & 실전(3) · 보충 자료(3) |
| 형태 | 개인 학습 정리 |
| 형식 | Markdown 문서 (각 문서 끝에 이전/다음 문서 링크) |
| 기간 | 2026-03 (커밋 기준) |
| 상태 | 1~12장 완료 |

## 목차

### 시작하기

| 문서 | 내용 |
|------|------|
| [01. Git 기초](./01_GIT_기초.md) | Git이란? 핵심 개념과 원리 |
| [02. GitHub 기초](./02_GITHUB_기초.md) | GitHub란? 주요 기능과 역할 |

### 핵심 기능

| 문서 | 내용 |
|------|------|
| [03. 기초 명령어](./03_기초_명령어.md) | init, add, commit, status 등 기본 명령어 |
| [04. 브랜치 관리](./04_브랜치_관리.md) | 브랜치 생성 · 전환 · 병합, 충돌 해결 |
| [05. 원격 저장소](./05_원격_저장소.md) | 원격 연결, push, pull, fetch |
| [06. 커밋 메시지](./06_커밋_메시지.md) | Conventional Commits 규칙과 좋은 예시 |

### 협업 & 실전

| 문서 | 내용 |
|------|------|
| [07. 협업 워크플로우](./07_협업_워크플로우.md) | Git Flow, GitHub Flow, Fork & PR |
| [08. 실전 팁](./08_실전_팁.md) | 되돌리기, stash, 태그, 자주 하는 실수 |
| [09. 명령어 레퍼런스](./09_명령어_레퍼런스.md) | 빠른 명령어 조회표 |

### 보충 자료

| 문서 | 내용 |
|------|------|
| [10. GitHub CLI](./10_GitHub_CLI.md) | GitHub CLI(`gh`) 설치와 활용 |
| [11. SSH 설정](./11_SSH_설정.md) | SSH 키 생성과 GitHub 연동 |
| [12. Git 설정](./12_Git_설정.md) | 기본 설정과 커스터마이징 |

## 빠른 시작

가장 자주 쓰는 흐름입니다. 자세한 설명은 [03. 기초 명령어](./03_기초_명령어.md)와 [07. 협업 워크플로우](./07_협업_워크플로우.md)에 있습니다.

1. 저장소 복제

```bash
git clone https://github.com/username/repository.git
```

2. 새 브랜치를 만들고 전환 (`git checkout -b`와 같음)

```bash
git switch -c feature/your-feature
```

3. 작업 후 커밋

```bash
git add .
git commit -m "feat: 설명"
```

4. 푸시한 뒤 GitHub에서 Pull Request 만들기

```bash
git push -u origin feature/your-feature
```

## 커밋 타입 한눈에

전체 규칙과 예시는 [06. 커밋 메시지](./06_커밋_메시지.md)에 있습니다.

| 타입 | 용도 | 예시 |
|------|------|------|
| `feat` | 새 기능 | `feat(auth): add OAuth login` |
| `fix` | 버그 수정 | `fix(cart): resolve quantity bug` |
| `docs` | 문서 | `docs: update README` |
| `refactor` | 리팩토링 | `refactor(api): simplify validation` |
| `test` | 테스트 | `test: add unit tests` |
| `chore` | 기타 | `chore: update dependencies` |

## 프로젝트 구조

```text
github-guide/
├── README.md                 목차 (이 문서)
├── 01_GIT_기초.md ~ 02_GITHUB_기초.md       시작하기
├── 03_기초_명령어.md ~ 06_커밋_메시지.md    핵심 기능
├── 07_협업_워크플로우.md ~ 09_명령어_레퍼런스.md  협업 & 실전
└── 10_GitHub_CLI.md ~ 12_Git_설정.md        보충 자료
```

## 더 읽을거리

- [Pro Git (한국어)](https://git-scm.com/book/ko/v2) — 무료 온라인 책
- [GitHub Skills](https://skills.github.com/) — GitHub 공식 실습 과정
- [Oh My Git!](https://ohmygit.org/) — 게임으로 배우는 Git

## 라이선스

[MIT](LICENSE)
