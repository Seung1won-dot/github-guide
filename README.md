# 📚 Git & GitHub 완벽 가이드

> 이 저장소는 Git과 GitHub를 효과적으로 사용하는 모든 것을 담고 있습니다.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

---

## 📖 목차

### 시작하기
| 문서 | 설명 |
|------|------|
| [01_GIT_기초.md](./01_GIT_기초.md) | Git이란? 핵심 개념과 원리 |
| [02_GITHUB_기초.md](./02_GITHUB_기초.md) | GitHub란? 주요 기능과 역할 |

### 핵심 기능
| 문서 | 설명 |
|------|------|
| [03_기초_명령어.md](./03_기초_명령어.md) | init, add, commit, status 등 기본 명령어 |
| [04_브랜치_관리.md](./04_브랜치_관리.md) | 브랜치 생성, 전환, 병합, 충돌 해결 |
| [05_원격_저장소.md](./05_원격_저장소.md) | 원격 연결, push, pull, fetch |
| [06_커밋_메시지.md](./06_커밋_메시지.md) | Conventional Commits 규칙과 좋은 예시 |

### 협업 & 실전
| 문서 | 설명 |
|------|------|
| [07_협업_워크플로우.md](./07_협업_워크플로우.md) | Git Flow, GitHub Flow, Fork & PR |
| [08_실전_팁.md](./08_실전_팁.md) | 되돌리기, stash, 태그, 자주 하는 실수 |
| [09_명령어_레퍼런스.md](./09_명령어_레퍼런스.md) | 빠른 명령어 조회 |

### 보충 자료
| 문서 | 설명 |
|------|------|
| [10_GitHub_CLI.md](./10_GitHub_CLI.md) | GitHub CLI 설치와 활용 |
| [11_SSH_설정.md](./11_SSH_설정.md) | SSH 키 생성 및 연동 |
| [12_Git_설정.md](./12_Git_설정.md) | 기본 설정과 커스터마이징 |

---

## 🚀 빠른 시작

```bash
# 1. 저장소 복제
git clone https://github.com/username/repository.git

# 2. 새 브랜치 생성 후 시작
git checkout -b feature/your-feature

# 3. 작업 후 커밋
git add .
git commit -m "feat: 설명"

# 4. 푸시 후 Pull Request 생성
git push -u origin feature/your-feature
```

---

## 📝 커밋 타입 가이드

| Type | 용도 | 예시 |
|------|------|------|
| `feat` | 새 기능 | `feat(auth): add OAuth login` |
| `fix` | 버그 수정 | `fix(cart): resolve quantity bug` |
| `docs` | 문서 | `docs: update README` |
| `refactor` | 리팩토링 | `refactor(api): simplify validation` |
| `test` | 테스트 | `test: add unit tests` |
| `chore` | 기타 | `chore: update dependencies` |

---

## 🔗 유용한 링크

- [Pro Git Book](https://git-scm.com/book/ko/v2) - 무료 온라인 북
- [GitHub Skills](https://skills.github.com/) - 공식 튜토리얼
- [Oh My Git](https://ohmygit.org/) - 인터랙티브 학습

---

## 📄 라이선스

MIT License - 자유롭게 사용, 수정, 배포 가능

---

*⭐ 이 저장소가 도움이 되셨다면 Star를 눌러주세요!*
