# Pragmatic Rust Guidelines 에이전트 스킬

Microsoft [Pragmatic Rust Guidelines](https://microsoft.github.io/rust-guidelines/)를 AI 에이전트가 분야와 규칙별로 찾아볼 수 있도록 재구성한 스킬입니다. 원본 저장소는 [microsoft/rust-guidelines](https://github.com/microsoft/rust-guidelines)입니다.

이 문서는 스킬을 설치·관리하는 사람을 위한 안내입니다. 에이전트가 Rust 코드를 작성하거나 검토할 때 참고할 진입점은 [`SKILL.md`](skills/pragmatic-rust-guidelines/SKILL.md)입니다.

## 다른 프로젝트에서 사용

1. 대상 프로젝트에서 에이전트의 스킬 검색 디렉터리를 확인합니다.
2. 이 저장소의 루트에서 스킬 폴더 전체를 복사합니다. 상대 경로 링크가 유지되려면 `SKILL.md`와 `parts/`가 함께 있어야 합니다.

   ```bash
   # TARGET_SKILLS_DIR: 대상 프로젝트의 스킬 검색 디렉터리
   cp -R skills/pragmatic-rust-guidelines "$TARGET_SKILLS_DIR/"
   ```

3. 대상 에이전트 도구에 스킬 검색 경로를 설정하고 `pragmatic-rust-guidelines`를 참고해 Rust 코드를 작성하거나 검토해 달라고 요청합니다. 검색 경로 설정과 호출 방법은 도구마다 다릅니다.

## 포함된 파일

- [`SKILL.md`](skills/pragmatic-rust-guidelines/SKILL.md): 적용 지침, 작업별 빠른 색인, 분야별 색인, 반영된 원본 저장소(upstream)의 리비전 정보. 에이전트의 시작점입니다. 상단에 원본 스타일의 저작권 및 라이선스 출처 식별 주석이 포함되어 있습니다.
- [`parts/`](skills/pragmatic-rust-guidelines/parts/): 분야별 목차와 각 규칙의 근거·본문. 아래 표에서 직접 열 수 있습니다.
- [`LICENSE.md`](skills/pragmatic-rust-guidelines/LICENSE.md): 원본 Microsoft Pragmatic Rust Guidelines의 MIT 라이선스 저작권 고지(Copyright notice) 및 허가문 전문(Permission notice). MIT 라이선스 요건을 온전히 충족하려면 단순 주석만이 아닌 본 전문 파일이 함께 배포되어야 합니다.
- [`scripts/`](scripts/): 생성 스크립트와 진입점 템플릿. 다른 프로젝트에서 스킬을 **사용**할 때는 복사할 필요가 없습니다.

### 분야별 지침

| 분야 | 다루는 내용 |
| :--- | :--- |
| [공통](skills/pragmatic-rust-guidelines/parts/01-universal.md) | Rust 전반의 관행, 정적 검증, 명명, 로깅 |
| [라이브러리 · 상호운용](skills/pragmatic-rust-guidelines/parts/02-1-libs-interop.md) | Rust·외부 타입과 trait, I/O |
| [라이브러리 · API UX](skills/pragmatic-rust-guidelines/parts/02-2-libs-ux.md) | 추상화, 오류, 생성 패턴, 메서드 설계 |
| [라이브러리 · 견고성](skills/pragmatic-rust-guidelines/parts/02-3-libs-resilience.md) | 테스트 가능성, 강한 타입, 전역 상태, 로깅 |
| [라이브러리 · 빌드](skills/pragmatic-rust-guidelines/parts/02-4-libs-building.md) | 시작 경험, 시스템 의존 크레이트, Cargo 기능 |
| [매크로](skills/pragmatic-rust-guidelines/parts/03-macros.md) | 선언형·프로시저 매크로 설계 |
| [애플리케이션](skills/pragmatic-rust-guidelines/parts/04-apps.md) | 바이너리 오류 처리, 할당자, 대상 CPU |
| [FFI](skills/pragmatic-rust-guidelines/parts/05-ffi.md) | 상태 격리, 값 변환, 이름 지정 |
| [정확성](skills/pragmatic-rust-guidelines/parts/06-correctness.md) | `unsafe`, soundness, panic |
| [성능](skills/pragmatic-rust-guidelines/parts/07-performance.md) | 처리량, 메모리·할당, 해싱, 비동기 스택 |
| [프로젝트](skills/pragmatic-rust-guidelines/parts/08-project.md) | Cargo workspace, 크레이트 구조, MSRV |
| [문서](skills/pragmatic-rust-guidelines/parts/09-docs.md) | 첫 문장, 모듈 문서, 정본 링크, 인라인 문서 |
| [AI 지원](skills/pragmatic-rust-guidelines/parts/10-ai.md) | 항목별 탐색, 테스트, Rust다운 설계 |

## 원본과 생성 스킬의 차이

원본 저장소는 에이전트용으로 지침을 모은 단일 파일 `src/agents/all.txt`를 제공합니다. 이 프로젝트는 같은 원본 가이드라인을 `SKILL.md` 진입점과 분야별 `parts/`로 나누어, 에이전트가 현재 작업에 필요한 지침을 선택적으로 찾아 읽도록 구성합니다.

`SKILL.md`의 작업별·분야별 색인에서 관련 규칙으로 이동하고, 해당 규칙의 근거·예외·코드 예시를 확인하는 흐름입니다. 단순히 문서를 분할하는 데 그치지 않고, 규칙별 앵커와 내부 링크, 적용 지침을 함께 제공해 탐색과 적용을 돕습니다.

분야별 규칙의 텍스트 본문·근거·코드 예시는 포함하되, 링크와 표시 형식은 스킬에 맞게 정리합니다.

| 구분 | 처리 방식 |
| :--- | :--- |
| 개요·체크리스트 | `src/guidelines/README.md`의 가이드북 소개·기고 절차와 `src/guidelines/checklist/README.md`의 전체 점검표는 포함하지 않습니다. 핵심 적용 원칙(`must/should`의 유연성, `Spirit Over Letter`)은 `SKILL.md`에 담습니다. |
| 이미지 | `src/guidelines/docs/`의 rustdoc 화면 캡처 4개와 `src/guidelines/libs/interop/M-TYPES-SEND.png`의 성능 그래프를 포함하지 않습니다. |
| 표시 형식 | PNG 이미지 태그와 단독 `<div>` 래퍼를 생략하고, 원본의 보충 설명·주의 표식(`<tip></tip>`, `<alert></alert>`)을 `Tip: `·`Caution: `으로 바꿉니다. |
| 규칙 참조 | 과거 ID `M-ABSTRACTIONS-DONT-NEST`와 `M-DOC-FIRST-SENTENCE`는 현재 규칙의 앵커로 연결합니다. 원본에 대응 규칙이 없는 `M-RUNTIME-ABSTRACTED`는 링크 없이 보존하고, 관련 규칙에 `Unavailable source reference` 안내를 넣습니다. |

**이미지의 시각 정보는 스킬에 없습니다.** 화면 배치나 성능 그래프의 비교가 필요하면 원본 문서를 확인하세요. `#[doc(inline)]` 사용 조건, 첫 문장 길이, `Send` 호환성과 성능상 주의점은 텍스트 본문에 남아 있습니다. 미해결 규칙 참조의 내용은 추측하거나 다른 규칙으로 대체하지 않습니다.

각 규칙에는 고유 ID 기반 앵커(`<a id="M-..."></a>`)가 있습니다. `SKILL.md`의 색인은 이 앵커를 가리키며, 앵커 이동을 지원하지 않는 도구에서는 해당 ID를 검색해 규칙을 찾을 수 있습니다.

## 갱신 및 재생성

이 저장소는 독립된 프로젝트로 운영되며, [microsoft/rust-guidelines](https://github.com/microsoft/rust-guidelines)의 `main` 브랜치 내 `src/guidelines` 트리를 추적합니다. 저장소 내에는 upstream의 원본 `src/` 전체를 복사·커밋하지 않고 `.github/`와 `scripts/`, 그리고 생성된 스킬(`skills/pragmatic-rust-guidelines/`)만을 관리합니다.

### 자동 갱신 (GitHub Actions)

GitHub Actions 워크플로(`.github/workflows/track-upstream.yml`)를 통해 정기적으로 upstream 변경을 감지하고 갱신 PR을 제안합니다.

- **실행 주기**: 매주 월요일 03:17 UTC 정기 실행 (`schedule`) 및 수동 실행 (`workflow_dispatch`).
- **변경 감지 기준**: upstream `microsoft/rust-guidelines`의 `HEAD:src/guidelines` Git tree SHA와 현재 `skills/pragmatic-rust-guidelines/SKILL.md`에 기록된 `Guidelines tree:` SHA를 비교합니다.
- **Tree SHA와 Commit SHA의 차이**: Commit SHA는 upstream 저장소 전체의 변경(루트 문서, 타 디렉터리, CI 등)을 모두 반영하지만, Guidelines Tree SHA는 `src/guidelines` 내부 파일 내용이 실제로 변경되었을 때만 바뀝니다. 따라서 가이드라인 본문과 무관한 커밋으로 인한 불필요한 스킬 재생성을 원천 차단합니다.
- **단일 PR 제안**: 변경이 감지되거나 수동 실행에서 `force=true`인 경우 스킬을 재생성하고, `automation/upstream-guidelines` 브랜치를 대상으로 단일 PR을 생성하거나 기존 PR을 갱신합니다. 변경분은 사람이 직접 리뷰한 뒤 `main`에 병합합니다 (`main` 브랜치에 직접 push하지 않습니다).
- **실패 시 안전성**: upstream clone, 검증, 빌드 단계에서 오류가 발생하면 workflow가 실패로 종료되며 PR을 생성하지 않고 기존 정상 스킬을 유지합니다.
- **부트스트랩 기준본 안내**: 저장소 초기 `main`에는 복사된 구버전 스킬이 부트스트랩 기준본으로 포함되어 있으며, `Guidelines tree` 항목이 없습니다. 최초 GitHub Actions 실행 시 이를 감지하여 최신 upstream 가이드라인으로 재생성하는 첫 번째 PR을 자동으로 제안합니다. 해당 PR을 검토 후 병합하기 전까지는 초기 부트스트랩 스킬이 제공됩니다.

### 수동 빌드 방법

로컬에서 직접 스킬을 재생성하려면 별도의 임시 upstream sparse checkout을 준비한 뒤 빌더 스크립트를 실행합니다.

```bash
# 1. 별도 임시 디렉터리에 upstream 저장소의 src/guidelines만 sparse checkout
UPSTREAM_TMP="$(mktemp -d)"
git clone --depth=1 --filter=blob:none --sparse --branch main https://github.com/microsoft/rust-guidelines.git "$UPSTREAM_TMP/rust-guidelines"
git -C "$UPSTREAM_TMP/rust-guidelines" sparse-checkout set src/guidelines

# 2. 저장소 루트에서 빌더 실행 (upstream 작업 트리의 절대 경로 전달)
bash scripts/build_agent_skills.sh "$UPSTREAM_TMP/rust-guidelines"

# 3. 임시 upstream 디렉터리 정리
rm -rf "$UPSTREAM_TMP"
```

빌드 결과는 `skills/pragmatic-rust-guidelines/`의 `SKILL.md`와 13개 분야별 파트입니다. `SKILL.md`의 **Source Revision** 섹션에서 반영된 upstream 커밋 SHA, 커밋 날짜, Guidelines Git tree SHA를 확인할 수 있습니다.

### 스킬이 생성되는 과정

`scripts/build_agent_skills.sh`는 다음 10단계를 거쳐 스킬을 안전하게 만듭니다.

1. **upstream 소스 리비전 및 입력 무결성 검증**: 전달된 경로가 Git 저장소 최상위 루트인지, `HEAD:src/guidelines` 트리가 존재하는지, 작업 트리 내 `src/guidelines`의 tracked/staged/untracked 변경 사항이 없는 깨끗한 상태인지 검증합니다. 통과 시 commit SHA, commit date, guidelines tree SHA를 획득합니다.
2. **원본 규칙 목록 구성 및 누락 검증**: 13개 분야 디렉터리와 README.md include 구문을 분석하여 규칙 ID 매핑을 구축하고, `src/guidelines` 아래 모든 `M-*.md` 파일이 빠짐없이 카테고리에 매핑되었는지 전수 검증합니다. 비매핑 규칙 파일이 발견되면 파일 경로를 출력하고 즉시 실패 처리합니다.
3. **템플릿 조기 검증**: 출력 디렉터리를 변경하기 전에 `scripts/SKILL.md.template` 파일의 존재 및 필수 치환 표식(`<!-- ROUTING_TABLE_ENTRIES -->`, `<!-- UPSTREAM_SOURCE_REVISION -->`)의 포함 여부를 미리 확인합니다.
4. **임시 스테이징 디렉터리 준비**: 기존 스킬 파일을 즉시 삭제하지 않고 격리된 임시 작업 디렉터리(`skills/.build_stage.*`)를 생성하여 파트 파일들과 라이선스(`LICENSE.md`)를 먼저 안전하게 생성할 수 있도록 준비합니다.
5. **분야별 파트 작성**: 공식 공개 순서대로 13개 파트 파일을 스테이징 공간에 작성합니다. 각 파일에는 분야 소개, 목차(TOC)와 규칙별 Rationale 요약, 정제된 규칙 본문이 들어갑니다. 코드 블록(fence)을 정밀 추적하여 내부 내용을 온전히 보존하며, 고유 앵커 삽입, `<why>`의 `Rationale` 변환, 버전 태그 및 이미지 생략, `Tip: `·`Caution: ` 라벨 정규화, 파트 간 링크 재작성을 적용합니다.
6. **파트와 규칙 앵커 확인**: 실제 생성된 총 규칙 수가 2단계에서 파악한 원본 규칙 수와 정확히 일치하는지, 각 파트 파일에 해당 규칙의 고유 앵커(`<a id="M-..."></a>`)가 빠짐없이 들어갔는지 스테이징 공간에서 검사합니다.
7. **`SKILL.md` 작성**: `scripts/SKILL.md.template`을 읽어 분야별 색인 표와 출처 리비전 정보(저장소 URL, 커밋 SHA, 커밋 날짜, Guidelines tree SHA)를 치환한 `SKILL.md`를 스테이징 공간에 작성합니다.
8. **생성 문서의 연결 전수 검사**: 스테이징 공간에 생성된 모든 Markdown 파일 내의 상대 링크와 규칙 앵커 대상이 실제로 존재하는지 전수 검사합니다. 아울러 `SKILL.md`에 언급된 모든 규칙 ID가 유효한 ID인지 검증합니다.
9. **백업 및 복원 트랜잭션을 통한 최종 반영**: 모든 검증을 통과한 경우, 기존 배포 디렉터리를 임시 백업(`skills/.build_backup.*`)으로 이동한 뒤 검증된 스테이징 디렉터리를 배포 위치로 승격합니다(`mv`). 승격 도중 예기치 않은 오류가 발생하더라도 트랩이 백업을 원래 위치로 자동 복원합니다.
10. **완료 결과 출력**: 생성된 파트 수(13개), 정제된 규칙 수(89개), 스킬 디렉터리 및 진입점 파일 경로를 콘솔에 출력하고 종료합니다.

### 라이선스

원본 Microsoft Pragmatic Rust Guidelines는 MIT License로 배포되며, 본 프로젝트의 [`LICENSE.md`](LICENSE.md) 및 스킬 디렉터리 [`skills/pragmatic-rust-guidelines/LICENSE.md`](skills/pragmatic-rust-guidelines/LICENSE.md)에 저작권 및 허가문 전문이 보존되어 배포됩니다.
