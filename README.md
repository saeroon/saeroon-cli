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
  <a href="#install">Install</a>&nbsp;&nbsp;·&nbsp;&nbsp;
  <a href="#usage">Usage</a>&nbsp;&nbsp;·&nbsp;&nbsp;
  <a href="#commands">Commands</a>&nbsp;&nbsp;·&nbsp;&nbsp;
  <a href="#ai-first-development">AI-First</a>&nbsp;&nbsp;·&nbsp;&nbsp;
  <a href="https://developers.saeroon.com/docs">Documentation</a>
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

## Install

```bash
npx @saeroon/cli
```

Node.js 18+ 필요. 별도 설치 없이 `npx`로 바로 실행됩니다.

<br/>

## Usage

```bash
# 1. 인증
npx @saeroon/cli login

# 2. 프로젝트 생성
npx @saeroon/cli init

# 3. 실시간 미리보기
npx @saeroon/cli preview

# 4. 검증
npx @saeroon/cli validate

# 5. 배포
npx @saeroon/cli deploy --target production
```

<br/>

## Commands

### Auth

```
login                          API 키 등록
whoami                         현재 인증 상태 확인
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
blocks                         전체 블록 카탈로그
blocks <type>                  개별 블록 상세 정보
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

## Starters

`init` 시 빌트인 스타터를 선택할 수 있습니다:

| Template | Best for |
|----------|----------|
| `restaurant` | 음식점 · 카페 · 케이터링 |
| `portfolio` | 포트폴리오 · 이력서 |
| `business` | 비즈니스 · 기업 랜딩 |
| `saas` | SaaS · 서비스 소개 |

<br/>

## AI-First Development

프로젝트 생성 시 AI 에디터 컨텍스트가 자동으로 세팅됩니다:

| File | Editor |
|------|--------|
| `CLAUDE.md` | Claude Code |
| `.cursorrules` | Cursor |
| `.vscode/settings.json` | VS Code (JSON Schema 자동완성) |

AI에게 "히어로 섹션 추가해줘"라고 말하면, 스키마를 직접 수정해줍니다. 코딩 없이.

<br/>

## Preview

두 가지 미리보기 모드를 지원합니다:

| Mode | Latency | 특징 |
|------|---------|------|
| **REST** (기본) | ~500ms | 안정적, 브라우저 자동 오픈 |
| **WebSocket** | ~300ms | 실시간, 타이핑하면서 바로 확인 |

파일 저장 시 자동으로 반영됩니다.

<br/>

## Smart Asset Handling

`deploy` 시 로컬 이미지를 자동으로 처리합니다:

- **SHA-256 해시** 기반 중복 검사 — 같은 파일은 재업로드하지 않음
- **동시 업로드** — 최대 5개 병렬 처리
- `--dry-run`으로 업로드 전 리포트 확인

<br/>

## Configuration

| File | Location | Purpose |
|------|----------|---------|
| `config.json` | `~/.saeroon/` | API 키, 기본 설정 |
| `saeroon.config.json` | 프로젝트 루트 | siteId, templateId |
| `schema.json` | 프로젝트 루트 | 사이트 정의 |

<br/>

## Links

- [Developer Center](https://developers.saeroon.com) — API 키 발급, 문서
- [Block Catalog](https://developers.saeroon.com/blocks) — 85개 블록 탐색
- [Documentation](https://developers.saeroon.com/docs) — 전체 가이드

<br/>

## Feedback

버그 리포트, 기능 제안, 질문은 [Issues](https://github.com/saeroon/saeroon-cli/issues)에 남겨주세요.

<br/>

## License

[MIT](LICENSE)
