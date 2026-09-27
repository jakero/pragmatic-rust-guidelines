# 작업 지침

- 이 저장소는 `microsoft/rust-guidelines`의 fork가 아니다. upstream `src/`를 이 저장소에 복사하거나 커밋하지 않는다.
- `skills/pragmatic-rust-guidelines/`는 생성 결과다. 규칙 본문·파트 구성 문제는 원인에 따라 `scripts/build_agent_skills.sh`, `scripts/SKILL.md.template` 또는 upstream 입력을 검토하고, 생성 파일만 직접 고쳐 해결하지 않는다.
- 빌더에는 별도로 준비한, 변경 사항이 없는 upstream checkout의 루트 경로를 전달한다: `bash scripts/build_agent_skills.sh "$UPSTREAM_CHECKOUT"`.
- 빌더를 검증할 때는 기존 스킬을 보존하도록 격리된 프로젝트 사본에서 실행한다. 13개 파트, 규칙 ID·앵커·상대 링크, `SKILL.md`의 commit/date/tree SHA, 재실행 결과를 확인한다. 규칙 수는 upstream에 따라 변하므로 고정값으로 가정하지 않는다.
- 새 `M-*.md` 규칙이 기존 분야에 매핑되지 않으면 빌드 실패를 우회하지 않는다. 분야 매핑과 출력 구조를 검토한다.
- `<!-- ROUTING_TABLE_ENTRIES -->` 및 `<!-- UPSTREAM_SOURCE_REVISION -->` 표식을 유지한다. 원본 규칙의 삭제·이름 변경 시 템플릿의 정적 색인과 링크도 확인한다.
- 자동 갱신은 `.github/workflows/track-upstream.yml`이 PR로 제안한다. 검증 없이 생성물을 `main`에 직접 반영하거나 자동 병합하도록 바꾸지 않는다.
- 문서·주석만 바꾸는 작업에는 스킬 재생성을 요구하지 않는다. 변경 범위에 맞는 구문·링크 검사와 diff 검토를 수행한다.
