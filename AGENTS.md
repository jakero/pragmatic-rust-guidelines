# 작업 지침

## 변경 및 배포 경계

- 이 저장소는 `microsoft/rust-guidelines`의 fork가 아니다. upstream `src/`를 복사하거나 커밋하지 않는다.
- 자동 갱신은 `.github/workflows/sync-upstream-skill.yml`에서 PR로 제안한다. 검증 없이 생성물을 `main`에 직접 반영하거나 자동 병합하도록 바꾸지 않는다.
- 프로젝트에 변경 사항(스크립트 동작, 워크플로 설정, 디렉터리 구조 등)이 발생하면 `README.md`에 함께 반영할 내용을 검토한 뒤 사용자에게 알린다.
- 검토, 계획 작성 등 조사만 지시받은 경우 분석 결과만 보고하고 파일 수정은 진행하지 않는다. 구현은 지시문에 수정·반영이 함께 명시되어 있거나 사용자의 명시적인 승인이 있을 때만 진행한다.

## Git 작업

- Git commit과 push는 각각 실행 전에 사용자의 명시적인 승인을 받는다. 작업 완료는 승인으로 간주하지 않는다.
- sparse-checkout 범위 밖 파일을 스테이징할 때는 대상 경로를 명시해 `git add --sparse -- <경로>`를 사용한다. 스테이징·커밋 오류를 우회하려고 sparse-checkout 설정을 변경하지 않는다. 체크아웃 범위 변경이 작업 목적일 때는 변경 전후 패턴과 `git status`를 확인한다.
- 커밋 전 `git diff --cached --stat`와 `git diff --cached`로 스테이징된 파일 범위와 내용을 확인한다.
- Git 커밋 메시지 제목은 저장소 관례인 `type(scope): subject` 또는 `type: subject` 형식을 따른다. 도구명이나 모델명(예: `[Gemini]`)을 접두어로 사용하지 않는다.

## 수정 위치

- `skills/pragmatic-rust-guidelines/`는 생성 결과다. 생성 파일만 직접 수정해 문제를 해결하지 않는다. 문제가 출력 형식·구조에 있으면 `scripts/build_agent_skills.sh`나 `scripts/SKILL.md.template`을, 원본 규칙 내용에 있으면 upstream 입력을 검토한다.
- 새 `M-*.md`가 매핑되지 않으면 실패를 우회하지 말고 분야 매핑과 출력 구조를 검토한다.
- 빌드 스크립트의 `RULE_ID_ALIASES`와 `UNRESOLVED_RULE_REFS`는 upstream 가이드라인의 교차 참조 차이(이전 식별자, 대응 규칙 부재)를 보정한다.
  - 새 참조 차이를 발견하면 upstream의 대상 파일·규칙 ID를 확인한다.
  - 이전 ID가 현행 규칙을 가리키는 경우에만 `RULE_ID_ALIASES`를 갱신한다.
  - 현재 대응 규칙이 없는 참조는 내용을 추측하거나 다른 규칙으로 대체하지 않는다.
  - `UNRESOLVED_RULE_REFS`에 임의로 추가해 검증을 우회하지 않는다.
  - 별칭 대상이 사라지거나 예외 ID가 실제 규칙으로 등장하면 해당 매핑을 재검토·제거하고 빌드를 다시 검증한다.
- 템플릿의 `<!-- ROUTING_TABLE_ENTRIES -->`, `<!-- UPSTREAM_SOURCE_REVISION -->` 표식을 유지한다. 규칙 삭제·이름 변경 시 정적 색인과 링크도 확인한다.
- 생성 스킬을 변경·배포할 때 `skills/pragmatic-rust-guidelines/LICENSE.md`의 MIT 저작권·허가문 전문을 보존한다. 다른 프로젝트에 배포할 때는 상대 링크와 라이선스가 유지되도록 `SKILL.md`, `parts/`, `LICENSE.md`를 함께 복사한다.

## 빌드 및 검증

- 빌더 검증은 `README.md`의 수동 빌드 절차에 따라 별도로 준비한 깨끗한 upstream checkout을 사용하며, 실제 작업 트리가 아닌 격리된 프로젝트 사본 안에서 먼저 실행한다: `bash scripts/build_agent_skills.sh "$UPSTREAM_CHECKOUT"`.
- 빌더 변경 검증 시 기존 스킬을 보존하면서 사본의 출력을 점검한다.
  - 파트 수, 규칙 ID·앵커·상대 링크, `SKILL.md`의 commit/date/tree SHA와 재실행 결과를 확인한다.
  - 자동 갱신이 읽는 `Guidelines tree:` 항목의 형식과 단일성을 유지한다. 규칙 수를 고정값으로 가정하지 않는다.
- 생성 스킬의 실제 저장소 반영이 요청된 경우에만, 격리 검증에 사용한 것과 동일한 upstream checkout 및 tree SHA로 작업 트리에서 빌더를 실행하여 산출물 diff를 확인한다. 생성 파일을 수동 편집하여 반영하지 않는다.
- 생성 입력과 무관한 문서·주석만 변경했다면 스킬을 재생성하지 말고 해당 범위의 구문·링크·diff를 확인한다.
- `scripts/SKILL.md.template`을 변경한 경우 깨끗한 upstream에서 재생성하여 파트 및 앵커 링크와 함께 `Guidelines tree:` 항목의 형식·단일성을 검증한다.
- 워크플로(`.github/workflows/`)나 스크립트(`scripts/`)를 수정한 경우, `git diff --check`로 공백·개행 오류를 확인한다.
- 워크플로(`.github/workflows/`)를 수정한 경우, 실제 YAML 파서나 `actionlint` 등으로 구문을 검증하며, 검증 도구를 실행할 수 없는 환경이면 해당 사실을 명시한다.
- 셸 스크립트(`scripts/`)를 수정한 경우, 지원 환경(Bash 4+ 및 GNU coreutils)에서 `bash -n` 구문 점검과 해당 변경의 동작을 검증하고 비표준 경로를 하드코딩하지 않는다. CI 에러 보고(`report_build_error`) 등 Actions 어노테이션 경로를 수정한 경우 `::error::` 출력 형식을 확인한다.

## 작업 인계 (Handoff)

- 에이전트 간 작업 인계를 위해 `handoff.md`를 작성할 때는 기존 내용에 덧붙이지 말고 항상 새로 작성(전체 덮어쓰기)한다.

## 참고 자료

- `README.md`: 빌드 과정, 갱신 워크플로, 규칙 교차 참조 보정의 상세 설명
- 원본 저장소: [https://github.com/microsoft/rust-guidelines](https://github.com/microsoft/rust-guidelines)
- 추적 대상: [https://github.com/microsoft/rust-guidelines/tree/main/src/guidelines](https://github.com/microsoft/rust-guidelines/tree/main/src/guidelines)
- 원본 가이드북: [https://microsoft.github.io/rust-guidelines/](https://microsoft.github.io/rust-guidelines/)

