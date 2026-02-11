# obsidian-cli

Obsidian CLI integration plugin for Claude Code.

터미널에서 Obsidian vault를 조작할 수 있게 해주는 Claude Code 플러그인입니다.

[English](README.md)

## Features

- **노트 관리** — 생성, 읽기, 수정, 이동, 삭제
- **Daily Notes** — 오늘의 데일리 노트 읽기/쓰기
- **지식 검색** — 전문 검색, 태그, 백링크, 고아 노트 탐색
- **Properties** — YAML frontmatter 메타데이터 관리
- **작업 관리** — 태스크 목록 조회 및 필터링
- **고급 기능** — 플러그인, 테마, 워크스페이스, Publish, Sync 관리
- **개발자 도구** — JS eval, 콘솔, 스크린샷, CSS 검사

## About Obsidian CLI

이 플러그인은 Obsidian에서 공식 제공하는 [Obsidian CLI](https://help.obsidian.md/cli)를 기반으로 합니다. Obsidian CLI는 실행 중인 Obsidian 앱과 통신하여 노트 생성, vault 검색, 속성 관리 등의 작업을 터미널에서 수행할 수 있게 해주는 커맨드라인 인터페이스입니다.

> Obsidian CLI는 현재 **얼리 액세스** 기능입니다. [Catalyst 라이선스](https://obsidian.md/pricing)가 필요하며, `설정 → 일반 → 앱`에서 **"얼리 액세스 버전 받기"**를 활성화해야 합니다.

자세한 내용은 [Obsidian CLI 공식 문서](https://help.obsidian.md/cli)를 참고하세요.

## Prerequisites

- Obsidian 1.12+ (CLI 지원 버전)
- Obsidian 앱 실행 중 (CLI는 실행 중인 앱과 통신)
- `obsidian` 바이너리가 PATH에 등록
- [Catalyst 라이선스](https://obsidian.md/pricing) (얼리 액세스)

## Installation

```bash
# 마켓플레이스 등록 (최초 1회)
/plugin marketplace add https://github.com/yoonhoGo/claude-plugins

# 마켓플레이스에서 플러그인 설치
/plugin install obsidian-cli@yoonho-plugins

# 또는 GitHub에서 직접 추가 (마켓플레이스 없이)
/plugin add https://github.com/yoonhoGo/claude-plugins/tree/main/obsidian-cli
```

## Usage

### Skill (자동 활성화)

Obsidian 관련 요청을 하면 자동으로 skill이 활성화됩니다:

```
"Obsidian에서 meeting notes 검색해줘"
"오늘 데일리 노트에 작업 로그 추가해"
"backlinks 확인해줘"
"새 노트 만들어줘"
```

### Command

`/obsidian` 커맨드로 자연어 명령을 실행합니다:

```
/obsidian 오늘 데일리 노트 읽어줘
/obsidian "auth module" 관련 노트 검색
/obsidian project-plan 노트에 진행 상황 추가
/obsidian 태그 목록 보여줘
```

## Plugin Structure

```
obsidian-cli/
├── .claude-plugin/
│   └── plugin.json              # Plugin manifest
├── commands/
│   └── obsidian.md              # /obsidian command
├── skills/
│   └── obsidian-cli/
│       ├── SKILL.md             # Core skill (auto-activating)
│       └── references/
│           ├── file-management.md
│           ├── daily-notes.md
│           ├── search-navigation.md
│           ├── properties.md
│           ├── advanced.md
│           └── developer-tools.md
└── README.md
```

## Components

### Skill: obsidian-cli

Obsidian CLI 전체 명령어에 대한 지식을 제공합니다. 사용자가 Obsidian 관련 요청을 하면 자동으로 활성화되어 적절한 CLI 명령어를 실행합니다.

**트리거 예시:** "노트 생성", "vault 검색", "데일리 노트 추가", "백링크 확인" 등

### Command: /obsidian

자연어 입력을 받아 적절한 `obsidian` CLI 명령어로 변환하여 실행합니다.

## License

MIT
