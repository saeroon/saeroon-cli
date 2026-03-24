# Changelog

## 0.2.0 (2026-03-24)

### New

- `template register` — 사이트를 마켓플레이스 템플릿으로 등록
- `template sync` — 소스 사이트 스키마를 템플릿에 동기화
- `template status` — 내 템플릿 목록 · 판매 · 수익 현황
- `template update` — 템플릿 메타데이터 수정
- `deploy --sync-template` — 배포 후 템플릿 자동 동기화
- `diff` — 스테이징 vs 프로덕션 스키마 비교
- `blocks <type>` — 개별 블록 상세 정보 (props, 예시)
- Smart asset handling — SHA-256 중복 검사 + 병렬 업로드
- AI context 자동 생성 — CLAUDE.md, .cursorrules, .vscode/settings.json

## 0.1.0 (2026-03-19)

### New

- `init` — 프로젝트 생성 (스타터 / 마켓플레이스 / 기존 사이트)
- `login` / `whoami` — API 키 인증
- `preview` — 실시간 미리보기 (REST / WebSocket)
- `validate` — 스키마 검증 + 품질 리포트
- `blocks` — 블록 카탈로그 조회
- `deploy` — 스테이징 / 프로덕션 배포
