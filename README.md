<p align="center">
  <img src="https://saeroon.diskn.com/e82ODzSxYY" alt="Saeroon" width="56" height="56" />
</p>

<h1 align="center">Saeroon CLI</h1>

<p align="center">
  <strong>JSON 스키마 하나로 웹사이트를 만들고, 미리보고, 배포하세요.</strong><br/>
  Build, preview, and ship websites — all from your terminal.
</p>

<p align="center">
  <a href="https://www.npmjs.com/package/@saeroon/cli"><img src="https://img.shields.io/npm/v/@saeroon/cli?style=flat-square&color=black" alt="npm" /></a>
  <a href="https://www.npmjs.com/package/@saeroon/cli"><img src="https://img.shields.io/npm/dm/@saeroon/cli?style=flat-square&color=black" alt="downloads" /></a>
  <a href="#license"><img src="https://img.shields.io/badge/license-MIT-black?style=flat-square" alt="license" /></a>
</p>

<br/>

<p align="center">
  <a href="#quick-start">Quick Start</a>&nbsp;&nbsp;·&nbsp;&nbsp;
  <a href="#commands">Commands</a>&nbsp;&nbsp;·&nbsp;&nbsp;
  <a href="#workflows">Workflows</a>&nbsp;&nbsp;·&nbsp;&nbsp;
  <a href="#ai-first-development">AI-First</a>&nbsp;&nbsp;·&nbsp;&nbsp;
  <a href="https://hosting.saeroon.com/developer/docs">Documentation</a>
</p>

<br/>

---

<br/>

## Why Saeroon CLI?

코드 실행 없이, **JSON 스키마 하나**로 완전한 웹사이트를 정의합니다. 85가지 블록을 조합하고, 터미널에서 실시간으로 미리보고, 한 줄로 배포하세요.

```
schema.json  →  preview  →  validate  →  deploy  →  live 🚀
```

<br/>

## Quick Start

```bash
# 1. 인증
npx @saeroon/cli login

# 2. 프로젝트 생성
npx @saeroon/cli init

# 3. 실시간 미리보기
npx @saeroon/cli preview

# 4. 검증 & 배포
npx @saeroon/cli validate
npx @saeroon/cli deploy --target production
```

Node.js 18+ 필요. 별도 설치 없이 `npx`로 바로 실행됩니다.

<br/>

## Commands

### Auth

```
login                          API 키 등록 및 연결 확인
whoami                         현재 인증 상태 및 프로젝트 설정 확인
```

### Development

```
init                           새 프로젝트 생성
init --template restaurant     스타터 템플릿으로 시작
init --from-template <id>      마켓플레이스 템플릿으로 시작
init --from-site <siteId>      기존 사이트에서 시작

preview                        실시간 미리보기 (REST)
preview --mode ws              저지연 WebSocket 미리보기
preview --device mobile        디바이스별 미리보기

validate                       스키마 검증 + 품질 리포트
validate --local               오프라인 구조 검증
blocks                         전체 블록 카탈로그
blocks <type>                  개별 블록 상세 정보
add <block-type>               schema.json에 블록 추가 (기본 props + 부모 children 자동 연결)
upload <path>                  이미지를 Saeroon CDN에 업로드
generate                       AI로 사이트 스키마 생성
compare                        레퍼런스 ↔ 프리뷰 시각 비교
```

### Deployment

```
deploy                         스테이징 배포 (기본)
deploy --target production     프로덕션 배포
deploy --dry-run               에셋 리포트만 확인
deploy --sync-template         배포 후 템플릿 자동 동기화

diff                           스테이징 vs 프로덕션 비교
```

### Templates

```
template register              내 사이트를 마켓플레이스 템플릿으로 등록
template sync                  소스 사이트 → 템플릿 동기화
template status                내 템플릿 현황 · 판매 · 수익
template update                템플릿 메타데이터 수정
```

<br/>

## Workflows

### Create → Preview → Deploy

```
init ──→ preview ──→ validate ──→ deploy --target staging
                                        │
                                        ▼
                                  diff (staging vs production)
                                        │
                                        ▼
                                  deploy --target production
```

### AI-Assisted Creation

```
generate --ref <url> ──→ validate --local ──→ add <블록> ──→ preview
        or                                                      │
generate --prompt <text>                              upload ./assets/
                                                      --replace-in schema.json
                                                                │
                                                          compare --ref ──→ deploy
```

### Template Marketplace

```
deploy --target production
        │
        ▼
template register ──→ template sync ──→ template status
```

`--sync-template` 플래그로 배포와 동시에 템플릿 동기화도 가능합니다:

```bash
npx @saeroon/cli deploy --target production --sync-template
```

<br/>

## AI-First Development

프로젝트 생성 시 AI 에디터 컨텍스트가 자동으로 세팅됩니다:

| File | Editor |
|------|--------|
| `CLAUDE.md` | Claude Code |
| `.cursorrules` | Cursor |
| `.vscode/settings.json` | VS Code (JSON Schema 자동완성) |
| `.claude/settings.json` | MCP 서버 설정 (Claude Code) |

AI에게 "히어로 섹션 추가해줘"라고 말하면, 스키마를 직접 수정해줍니다. 코딩 없이.

### JSON Schema 자동완성

`schema.json`에 `$schema` 필드가 포함되어 VS Code/Cursor에서 **속성 자동완성 + 타입 검증 + 인라인 설명**이 즉시 작동합니다:

```json
{
  "$schema": "https://hosting.saeroon.com/schema/v1.20.0/site-schema.json",
  "schemaVersion": "1.20.0"
}
```

### AI Generation

```bash
# 레퍼런스 URL → Playwright 스크린샷 → Claude 분석 → schema.json
npx @saeroon/cli generate --ref https://example.com

# 프롬프트 기반 생성
npx @saeroon/cli generate --prompt "카페 홈페이지, 모던 스타일, 주황 강조색"

# 출력 파일 지정
npx @saeroon/cli generate --ref https://example.com --output my-site.json
```

<br/>

## Validate

| 모드 | 사용 | 특성 |
|------|------|------|
| 기본 (서버) | `validate` | API 호출, Editor Parity 검증 + SEO·GEO·성능·접근성 품질 점수 |
| `--local` | `validate --local` | 오프라인, 구조 검증 3단계 (Schema Structure → Block Properties → Reference Integrity) |

<br/>

## Preview

두 가지 미리보기 모드를 지원합니다:

| Mode | Latency | 특징 |
|------|---------|------|
| **REST** (기본) | ~500ms | 안정적, 브라우저 자동 오픈 |
| **WebSocket** | ~300ms | 실시간, 타이핑하면서 바로 확인 |

```bash
npx @saeroon/cli preview              # REST (기본)
npx @saeroon/cli preview --mode ws    # WebSocket (저지연)
npx @saeroon/cli preview --device mobile  # 디바이스 지정
```

파일 저장 시 자동으로 반영됩니다.

<br/>

## Asset Handling

### `upload` — 독립 에셋 업로드

개발 중 이미지를 CDN에 업로드하고 schema.json 내 경로를 자동 교체합니다.

```bash
# 단일 파일 → CDN URL 반환
npx @saeroon/cli upload ./assets/hero.jpg

# 디렉토리 전체 → URL 매핑 테이블 출력
npx @saeroon/cli upload ./assets/

# schema.json 내 로컬 경로를 CDN URL로 자동 교체
npx @saeroon/cli upload ./assets/ --replace-in schema.json
```

### `deploy` — 배포 시 자동 에셋 처리

`deploy` 시 로컬 이미지 파일을 자동으로 감지·해시·업로드합니다.

- **SHA-256 해시** 기반 중복 검사 — 같은 파일은 재업로드하지 않음
- **동시 업로드** — 최대 5개 병렬 처리
- `--dry-run`으로 업로드 전 리포트 확인

```bash
npx @saeroon/cli deploy --dry-run
```

<br/>

## Block Scaffolding

`add` 명령으로 블록을 빠르게 추가합니다. Block Catalog API에서 기본 props를 가져와 부모 children에 자동 연결합니다.

```bash
# 기본 — 인터랙티브 부모 선택
npx @saeroon/cli add heading-block

# 부모 + 위치 지정
npx @saeroon/cli add image-block --parent root --after hero-1

# ID + 페이지 지정
npx @saeroon/cli add content-showcase --id insights --parent main --page about
```

<br/>

## Visual Diff

레퍼런스 사이트와 프리뷰 결과를 시각적으로 비교합니다.

```bash
npx @saeroon/cli compare \
  --ref https://example.com \
  --preview https://preview.hosting.saeroon.com/abc \
  --width 1280 --height 800
```

<br/>

## Starters

`init` 시 빌트인 스타터를 선택할 수 있습니다:

| Template | Best for |
|----------|----------|
| `restaurant` | 음식점 · 카페 · 케이터링 |
| `portfolio` | 포트폴리오 · 이력서 |
| `business` | 비즈니스 · 기업 랜딩 |
| `saas` | SaaS · 서비스 소개 |

```bash
npx @saeroon/cli init --template restaurant
```

마켓플레이스 템플릿에서도 시작할 수 있습니다:

```bash
npx @saeroon/cli init --from-template <template-id>
```

<br/>

## Configuration

| File | Location | Purpose |
|------|----------|---------|
| `config.json` | `~/.saeroon/` | API 키, 기본 설정 |
| `saeroon.config.json` | 프로젝트 루트 | siteId, templateId |
| `schema.json` | 프로젝트 루트 | 사이트 정의 |

<br/>

## Security

CLI는 다음 보안 조치를 적용합니다:

- **API 통신**: HTTPS 전용, SSRF 방어 (Private IP 차단), 30초 타임아웃
- **JSON 파싱**: Prototype Pollution 방어 (`secure-json-parse`)
- **파일 접근**: Path Traversal 방어 (CWD 외부 접근 차단)
- **API Key**: 입력 시 마스킹, 설정 파일 저장 (`~/.saeroon/config.json`)
- **Rate Limit**: 429 응답 시 `Retry-After` 기반 자동 재시도 (최대 3회)

<br/>

## Requirements

- Node.js 18+
- Saeroon API Key ([Developer Center](https://hosting.saeroon.com/developer/keys)에서 발급)
- (선택) Playwright — `compare`, `generate --ref` 명령용 (`npx playwright install chromium`)
- (선택) ImageMagick — `compare` 오버레이 diff용

<br/>

## Links

- [Developer Center](https://hosting.saeroon.com/developer) — API 키 발급, 문서
- [Block Catalog](https://hosting.saeroon.com/developer/blocks) — 85개 블록 탐색
- [Documentation](https://hosting.saeroon.com/developer/docs) — 전체 가이드

<br/>

## Feedback

버그 리포트, 기능 제안, 질문은 [Issues](https://github.com/saeroon/saeroon-cli/issues)에 남겨주세요.

<br/>

## License

[MIT](LICENSE)
