# 작업 지침

## 변경 및 배포 경계

- 이 저장소는 `microsoft/rust-guidelines`의 fork가 아니다. upstream `src/`를 복사하거나 커밋하지 않는다.
- Git commit과 push는 각각 실행 전에 사용자의 명시적인 승인을 받는다. 작업 완료는 승인으로 간주하지 않는다.
- 자동 갱신은 `.github/workflows/track-upstream.yml`에서 PR로 제안한다. 검증 없이 생성물을 `main`에 직접 반영하거나 자동 병합하도록 바꾸지 않는다.

## 수정 위치

- `skills/pragmatic-rust-guidelines/`는 생성 결과다. 생성 파일만 직접 수정해 문제를 해결하지 않는다. 원인에 따라 `scripts/build_agent_skills.sh`, `scripts/SKILL.md.template` 또는 upstream 입력을 검토한다.
- 새 `M-*.md`가 매핑되지 않으면 실패를 우회하지 말고 분야 매핑과 출력 구조를 검토한다.
- 템플릿의 `<!-- ROUTING_TABLE_ENTRIES -->`, `<!-- UPSTREAM_SOURCE_REVISION -->` 표식을 유지한다. 규칙 삭제·이름 변경 시 정적 색인과 링크도 확인한다.

## 빌드 및 검증

- 빌더에는 별도로 준비한 깨끗한 upstream checkout의 루트를 전달한다: `bash scripts/build_agent_skills.sh "$UPSTREAM_CHECKOUT"`.
- 빌더 변경은 기존 스킬을 보존하도록 격리된 프로젝트 사본에서 검증한다. 파트 수, 규칙 ID·앵커·상대 링크, `SKILL.md`의 commit/date/tree SHA와 재실행 결과를 확인한다. 규칙 수를 고정값으로 가정하지 않는다.
- 문서·주석만 변경했다면 스킬을 재생성하지 말고 해당 범위의 구문·링크·diff를 확인한다.

## 참고 자료

- 원본 저장소: https://github.com/microsoft/rust-guidelines
- 추적 대상: https://github.com/microsoft/rust-guidelines/tree/main/src/guidelines
- 원본 가이드북: https://microsoft.github.io/rust-guidelines/
