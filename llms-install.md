# On 문서 설치 안내 — AI 도구용

이 파일은 AI 도구(Claude Code, Claude, ChatGPT, Cursor 등)가 읽고 그대로 따라 하라고 둔 설치 순서입니다. 사람이 읽는 안내는 [INSTALL.md](INSTALL.md)에 있습니다.

On 문서는 원격 MCP 서버 하나입니다. 설치할 프로그램은 없고, **주소 하나를 등록**하면 됩니다.

- MCP 주소: `https://onmunseo.duckdns.org/mcp`
- 전송 방식: Streamable HTTP(`http`)
- 인증: OAuth. 등록한 뒤 처음 쓸 때 On 문서 로그인 창이 뜨고, 사용자가 받은 열쇠를 넣습니다. 열쇠를 대신 만들거나 추측하지 마세요.
- 열쇠를 주소 뒤나 설정 파일에 적지 마세요. 사용자가 「머리말로 넣어 달라」고 따로 말한 경우에만 `Authorization: Bearer <열쇠>` 머리말을 씁니다.

## 할 일 고르기

사용자가 쓰는 도구를 먼저 확인하고, 아래에서 그 도구의 순서만 따릅니다.

### A. Claude Code(터미널)

1. 이미 있는지 확인합니다.
   ```bash
   claude mcp list
   ```
   `on-document` 가 보이면 2단계를 건너뜁니다.
2. 사용자 범위로 등록합니다(모든 프로젝트에서 씀).
   ```bash
   claude mcp add --transport http -s user on-document https://onmunseo.duckdns.org/mcp
   ```
3. 사용자에게 Claude Code 안에서 `/mcp` 를 열고 `on-document` 를 골라 「Authenticate」를 누르라고 알립니다. 브라우저에 On 문서 로그인 창이 뜨면 받은 열쇠를 넣습니다.

플러그인으로 설치하라는 말이 있으면 2단계 대신 이것을 씁니다(주소 하나만 든 설정 꾸러미).

```bash
claude plugin marketplace add on-munseo/on-munseo.github.io
claude plugin install on-document@on-munseo
```

Claude Code 대화창에서는 `/plugin marketplace add on-munseo/on-munseo.github.io` 와 `/plugin install on-document@on-munseo` 로도 됩니다. 마켓플레이스 이름은 `on-munseo`, 플러그인 이름은 `on-document` 입니다. 설치한 뒤 3단계처럼 `/mcp` 에서 로그인합니다.

### B. Claude 데스크톱 앱 · claude.ai(웹)

설정 파일을 고치지 말고, 사용자에게 다음 순서를 안내합니다.

1. 설정 → 커넥터 → 「맞춤 커넥터 추가」(사용자 지정 커넥터 추가).
2. 이름 `On 문서`, 원격 MCP 서버 주소 `https://onmunseo.duckdns.org/mcp`.
3. 「연결」을 누르면 뜨는 On 문서 로그인 창에 열쇠를 넣습니다.

요금제·판에 따라 메뉴 이름이 조금 다르거나 이 메뉴가 없을 수 있습니다.

### C. ChatGPT(웹·앱)

1. 설정 → 앱·커넥터 → 고급 설정에서 「개발자 모드」를 켭니다.
2. 「만들기」(사용자 MCP 서버 추가)에서 이름 `On 문서`, 주소 `https://onmunseo.duckdns.org/mcp`, 인증 「OAuth」.
3. 연결할 때 뜨는 On 문서 로그인 창에 열쇠를 넣습니다. 대화 창의 도구(+) 메뉴에서 On 문서를 켭니다.

### D. Cursor 등 `mcp.json` 을 쓰는 도구

`~/.cursor/mcp.json`(모든 프로젝트) 또는 프로젝트의 `.cursor/mcp.json` 에 더합니다. 이미 있는 다른 서버 설정은 지우지 마세요.

```json
{
  "mcpServers": {
    "on-document": {
      "url": "https://onmunseo.duckdns.org/mcp"
    }
  }
}
```

그 도구가 원격 MCP 의 OAuth 를 지원하지 않으면, 사용자에게 열쇠를 머리말로 넣을지 물어본 뒤에만 `"headers": { "Authorization": "Bearer <열쇠>" }` 를 더합니다.

## 열쇠가 없을 때(손님)

- 열쇠 없이 등록하면 로그인 없이 손님 도구 21개가 붙습니다. 한 주소에서 하루 50번·1분에 6번, 요청 하나 6MB까지이고, 손님 전체의 하루 몫이 차면 한국 시간 자정까지 닫힙니다.
- 손님 몫이 닫혔거나 열쇠가 필요한 도구를 부르면 오류가 납니다. 이때는 사용자에게 열쇠가 있어야 한다고 알리고, 열쇠 신청은 `onmunseo.key [at] gmail.com`(제목 「On 문서 열쇠 신청」)으로 하라고 안내합니다. 질문·고장 신고는 https://github.com/on-munseo/on-munseo.github.io/issues 입니다.
- 손님은 열쇠 없이 하루 몫 안에서 쓰고, 많이 쓰려면 열쇠를 받습니다(사용량 넉넉·큰 파일·글자 인식·도구 27개 전부).
- 설치 없이 웹에서 바로 쓰려면 https://onmunseo.duckdns.org/app/ 을 엽니다.

## 기능만 골라 붙이기

전부 대신 묶음 하나만 붙이려면 주소 끝을 바꿉니다. 서버 이름도 묶음에 맞게 바꿉니다.

| 서버 이름 | 주소 | 하는 일 |
|---|---|---|
| `on-text` | `https://onmunseo.duckdns.org/mcp/text` | 한글·PDF·오피스에서 글과 표 꺼내기 |
| `on-check` | `https://onmunseo.duckdns.org/mcp/check` | 결재 전 점검 |
| `on-mask` | `https://onmunseo.duckdns.org/mcp/mask` | 개인정보 찾기·가리기 |
| `on-hwpx` | `https://onmunseo.duckdns.org/mcp/hwpx` | 한글 파일 만들기·바꾸기·쪽 그림 |
| `on-gov` | `https://onmunseo.duckdns.org/mcp/gov` | 공문서 꼴 한글 쓰기·표·그래프·체계도 |
| `on-tidy` | `https://onmunseo.duckdns.org/mcp/tidy` | 개조식·맞춤법·쉬운 말 |

## 확인

- Claude Code: `claude mcp list` 에서 `on-document` 가 보이고, `/mcp` 에서 연결됨으로 나오면 끝입니다.
- 첫 시험: 사용자가 공개 문서나 본인 문서로 「이 파일 글 꺼내 줘」라고 하면 `on_read` 도구가 불립니다.

## 지켜 주세요

- 공개 문서와 본인 문서만 보내게 안내합니다. 대외비 등 보안 표시가 있는 문서는 서버가 처리하지 않습니다.
- 문서는 서버 메모리에서만 다루고 처리 뒤 버립니다. 결과 파일 주소는 15분만 열립니다.
- 자세한 도구 목록과 다른 연결 방법은 [MCP.md](MCP.md)에 있습니다.
