# AI 코딩 도구 연동 (MCP)

<!-- synonyms: MCP, MCP 서버, AI 연동, AI 코딩, AI 도구, 코딩 어시스턴트, Claude, Claude Code, Cursor, 커서, Copilot, 코파일럿, Windsurf, Gemini, mcp 등록, mcp 설정, 매뉴얼 연동, ai assistant -->

> IBSheet8은 공식 **MCP 서버**를 제공합니다. Claude Code, Cursor, GitHub Copilot 같은 `MCP`를 지원하는 AI 코딩 도구에 한 번 등록해두면,
AI가 코드를 작성할 때 IBSheet8 **공식 매뉴얼을 직접 검색·조회**해서 실제 존재하는 API와 옵션만 사용합니다.<br/>
> AI가 그럴듯한 가짜 API를 만들어내는 문제가 사라지고, 항상 최신 매뉴얼 기준으로 답합니다.

## 서버 정보

| 항목 | 값 |
|---|---|
| 서버 주소 | `https://mcp.ibsheet.com/mcp` |
| 전송 방식 | Streamable HTTP |
| 인증 | 없음 (별도 키·로그인 불필요) |

등록 후에는 AI 도구를 **재시작(새 세션 시작)** 해야 연결됩니다.

## 등록 방법

### Claude Code

터미널에서 한 줄:

```bash
claude mcp add --transport http ibsheet8 https://mcp.ibsheet.com/mcp
```

또는 프로젝트 루트에 `.mcp.json` 파일을 만들면 저장소를 공유하는 팀원 전체에 적용됩니다:

```json
{
  "mcpServers": {
    "ibsheet8": {
      "type": "http",
      "url": "https://mcp.ibsheet.com/mcp"
    }
  }
}
```

확인: 새 세션에서 `/mcp` 입력 → `ibsheet8 ✔ connected`

### Cursor

프로젝트 루트에 `.cursor/mcp.json` (전역 적용은 `~/.cursor/mcp.json`):

```json
{
  "mcpServers": {
    "ibsheet8": {
      "url": "https://mcp.ibsheet.com/mcp"
    }
  }
}
```

### VS Code (GitHub Copilot)

터미널에서 한 줄:

```bash
code --add-mcp "{\"name\":\"ibsheet8\",\"type\":\"http\",\"url\":\"https://mcp.ibsheet.com/mcp\"}"
```

또는 프로젝트 루트에 `.vscode/mcp.json` 을 만들고, Copilot Chat을 **Agent 모드**로 사용합니다:

```json
{
  "servers": {
    "ibsheet8": {
      "type": "http",
      "url": "https://mcp.ibsheet.com/mcp"
    }
  }
}
```

### 그 외 도구

| 도구 | 설정 위치 | 설정 키 |
|---|---|---|
| Windsurf | `~/.codeium/windsurf/mcp_config.json` | `"serverUrl": "https://mcp.ibsheet.com/mcp"` |
| Gemini CLI | `~/.gemini/settings.json` | `"httpUrl": "https://mcp.ibsheet.com/mcp"` |
| Codex CLI | `~/.codex/config.toml` | `command = "npx"`, `args = ["-y", "mcp-remote", "https://mcp.ibsheet.com/mcp"]` |
| Claude Desktop | `claude_desktop_config.json` | `"command": "npx"`, `"args": ["-y", "mcp-remote", "https://mcp.ibsheet.com/mcp"]` |
| JetBrains IDE | Settings → Tools → AI Assistant → MCP | Command `npx` / Arguments `-y mcp-remote https://mcp.ibsheet.com/mcp` |

`mcp-remote`를 경유하는 도구는 Node.js 18 이상이 필요합니다.

Gemini CLI와 Codex CLI는 명령어 한 줄로도 등록됩니다:

```bash
gemini mcp add --transport http ibsheet8 https://mcp.ibsheet.com/mcp
codex mcp add ibsheet8 -- npx -y mcp-remote https://mcp.ibsheet.com/mcp
```

## 사용 방법

등록만 하면 AI가 IBSheet8 관련 질문에서 알아서 매뉴얼을 검색합니다.

```
IBSheet8로 조회 그리드 만들어줘. 컬럼은 이름/부서/입사일이고 입사일엔 달력 버튼.
```

AI가 매뉴얼에서 실제 속성을 찾아 정확한 코드를 작성합니다.
매뉴얼 참조를 강제하고 싶으면 "IBSheet8 매뉴얼을 검색해서"라고 덧붙이면 됩니다.

## 문제 해결

| 증상 | 확인할 것 |
|---|---|
| 도구 목록에 안 보임 | 도구 재시작(새 세션) 했는지, 설정 파일 위치·JSON 문법 |
| 연결 실패 | 서버 주소 오타, 인터넷/회사 프록시·방화벽 |
| mcp-remote 오류 | Node.js 18 이상 설치 여부 (`node -v`) |

<!-- 폐쇄망(인터넷 차단) 환경은 요청 시 사내 설치형 MCP 서버를 별도로 제공합니다. -->

## Read More
- [Quick Start](/docs/start/quick-start)
- [파일 구성](/docs/intro/files)
