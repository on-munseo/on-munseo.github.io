# On 문서 설치 안내 — AI 도구용

이 파일은 AI 도구(Claude Code, Claude, ChatGPT, Cursor 등)가 읽고 그대로 따라 하라고 둔 설치 순서입니다. 사람이 읽는 안내는 [INSTALL.md](INSTALL.md)에 있습니다.

## 먼저 요약(세 줄)

1. **등록은 AI 가 한 번** — 사용자 범위로 등록하면 그 뒤 모든 새 대화에서 계속 씁니다.
2. **활성화는 사용자가 한 번** — 등록한 그 대화에는 도구가 아직 붙지 않습니다. Claude Code 터미널은 `/exit` 뒤 `claude` 다시, VS Code 는 새 대화 또는 창 다시 불러오기(명령 팔레트 「Developer: Reload Window」), Claude 데스크톱·웹·ChatGPT 는 커넥터 「연결」.
3. **열쇠가 없으면 로그인은 건너뛰고 손님으로 바로** 씁니다. 손님도 한글 공문서 만들기(`on_write_gov`)·글 꺼내기·결재 전 점검을 바로 쓸 수 있습니다.

## 서버

On 문서는 원격 MCP 서버 하나입니다. 설치할 프로그램은 없고, **주소 하나를 등록**하면 됩니다.

- MCP 주소: `https://onmunseo.duckdns.org/mcp` — 이 주소 하나를 권장합니다(도구 전부). 묶음 주소는 아래 「고급」에 있습니다.
- 전송 방식: Streamable HTTP(`http`)
- 인증: 열쇠가 있으면 OAuth. 처음 쓸 때 On 문서 로그인 창이 뜨고, 사용자가 받은 열쇠를 넣습니다. 열쇠를 대신 만들거나 추측하지 마세요.
- 열쇠를 주소 뒤나 설정 파일에 적지 마세요. 사용자가 「머리말로 넣어 달라」고 따로 말한 경우에만 `Authorization: Bearer <열쇠>` 머리말을 씁니다.

## 한글 문서 만들기 = On 공문서 쓰기(`on_write_gov`)

- 「한글 문서로 만들어 줘」처럼 보고서·계획서·결과보고서·보도자료 한글 문서를 만들 때 쓰는 도구는 `on_write_gov` 입니다. 휴먼명조·장 제목 막대·□ ○ - 단계의 공문서 꼴로 나옵니다.
- `on_write` 는 꾸밈 없는 일반 한글 문서를 만듭니다. style 없이 받은 원고가 공문서처럼 보이면 같은 공문서 꼴로 만들고 결과에 `auto_style` 을 적습니다(꾸밈 없는 꼴을 바라면 `plain: true`).

## 열쇠가 없으면(손님) — 등록 전에 먼저 읽기

- 사용자에게 열쇠가 없으면 **로그인(Authenticate) 단계는 건너뜁니다.** 등록만 하면 손님으로 바로 씁니다.
- 손님·열쇠 설명은 길게 하지 말고, 사용자가 바라는 일(한글 문서 만들기 등)을 바로 도구로 처리합니다.
- 손님 한도는 한 주소에서 하루 50번·1분에 6번, 요청 하나 6MB까지입니다. 열쇠 안내는 하루 몫이 찼다는 결과가 왔거나 열쇠가 필요한 도구를 바랄 때만 합니다. 열쇠 신청은 `onmunseo.key [at] gmail.com`(제목 「On 문서 열쇠 신청」)입니다.

## 도구별 순서

사용자가 쓰는 도구를 먼저 확인하고, 아래에서 그 도구의 순서만 따릅니다.

### A. Claude Code(터미널·VS Code 확장)

1. 이미 있는지 확인합니다(`claude` 명령이 있을 때).
   ```bash
   claude mcp list
   ```
   `on-document` 가 보이면 2단계를 건너뜁니다.
2. 사용자 범위로 등록합니다. 아래 세 길 가운데 되는 것 하나를 차례로 씁니다.
   - **길 1 — `claude` 명령이 있으면:**
     ```bash
     claude mcp add --transport http -s user on-document https://onmunseo.duckdns.org/mcp
     ```
   - **길 2 — `claude` 명령이 없으면(VS Code 확장 등 PATH 에 없는 환경):** 사용자 설정 파일 `~/.claude.json` 의 맨 위 `"mcpServers"` 에 아래 항목을 더합니다. 이미 있는 다른 설정과 서버는 지우지 마세요(JSON 으로 읽어 이 키만 더하고 다시 씀). `"mcpServers"` 가 없으면 맨 위에 새로 둡니다. 이 꼴은 길 1 이 만드는 것과 같습니다.
     ```json
     {
       "mcpServers": {
         "on-document": { "type": "http", "url": "https://onmunseo.duckdns.org/mcp" }
       }
     }
     ```
   - **길 3 — 파일을 고칠 수 없으면:** 사용자에게 Claude Code 대화창에 두 줄을 차례로 넣으라고 안내합니다.
     ```
     /plugin marketplace add on-munseo/on-munseo.github.io
     /plugin install on-document@on-munseo
     ```
3. 열쇠가 있는 사용자만: Claude Code 안에서 `/mcp` 를 열고 `on-document` 를 골라 「Authenticate」를 누르면 브라우저에 On 문서 로그인 창이 뜹니다. 열쇠가 없으면 이 단계는 건너뜁니다.
4. **설치가 끝나면 사용자에게 반드시 알립니다:** 「등록했어요. 이 도구를 다시 켜거나 새 대화를 열어야 On 문서 도구가 보입니다(Claude Code 터미널은 `/exit` 뒤 `claude`, VS Code 는 새 대화 또는 창 다시 불러오기). 그다음부터는 모든 대화에서 계속 씁니다.」

### B. Claude 데스크톱 앱 · claude.ai(웹)

설정 파일을 고치지 말고, 사용자에게 다음 순서를 안내합니다.

1. 설정 → 커넥터 → 「맞춤 커넥터 추가」(사용자 지정 커넥터 추가).
2. 이름 `On 문서`, 원격 MCP 서버 주소 `https://onmunseo.duckdns.org/mcp`.
3. 「연결」을 누릅니다. 열쇠가 있으면 뜨는 On 문서 로그인 창에 넣고, 없으면 손님으로 씁니다.
4. **끝나면 사용자에게 알립니다:** 「새 대화를 열면 On 문서 도구가 보입니다.」

요금제·판에 따라 메뉴 이름이 조금 다르거나 이 메뉴가 없을 수 있습니다.

### C. ChatGPT(웹·앱)

1. 설정 → 앱·커넥터 → 고급 설정에서 「개발자 모드」를 켭니다.
2. 「만들기」(사용자 MCP 서버 추가)에서 이름 `On 문서`, 주소 `https://onmunseo.duckdns.org/mcp`, 인증 「OAuth」.
3. 연결할 때 뜨는 On 문서 로그인 창에 열쇠를 넣습니다. 대화 창의 도구(+) 메뉴에서 On 문서를 켭니다.
4. **끝나면 사용자에게 알립니다:** 「새 대화에서 도구(+) 메뉴의 On 문서를 켜면 씁니다.」

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

**끝나면 사용자에게 알립니다:** 「설정의 MCP 화면에서 On 문서를 켜거나 도구를 다시 켜면 보입니다.」

## 지금 대화에서 바로 쓰기(활성화 전 임시)

등록한 그 대화에서 사용자가 곧바로 「한글 문서 만들어 줘」라고 했는데 On 문서 도구가 아직 안 보이면, 사용자를 기다리게 하지 말고 같은 주소를 HTTP 로 직접 불러 손님으로 처리할 수 있습니다. 서버는 상태를 두지 않는 방식이라 `tools/call` 하나로 됩니다(`initialize` 는 안 해도 됨).

```bash
cat > call.json <<'EOF'
{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"on_write_gov","arguments":{
 "style":"결과보고서",
 "markdown":"# ○○ 회의 결과보고\n\n## Ⅰ. 회의 개요\n\n○ 일시: 2026. 11. 20.(금) 14:00\n○ 장소: ○○ 회의실\n\n## Ⅱ. 주요 내용\n\n○ 교육 과정 8회 운영, 수료 214명\n"}}}
EOF
curl -s https://onmunseo.duckdns.org/mcp \
  -H "Content-Type: application/json" -H "Accept: application/json, text/event-stream" \
  --data-binary @call.json
```

- 결과 `result.content[0].text` 는 JSON 글입니다. 그 안의 `file.url` 이 만든 한글 파일 주소이고 **15분**만 열리니 바로 사용자에게 알립니다. `check.same` 이 `true` 면 원고의 글·숫자를 하나도 잃지 않은 것입니다. `tell_user` 는 사용자에게 그대로 전할 말입니다.
- 원고에 따옴표·줄바꿈이 많으면 위처럼 파일(`--data-binary @call.json`)로 보내면 깨지지 않습니다.
- 결과를 건넬 때 사용자에게 한 줄 덧붙입니다: 「다음부터는 다시 켠 뒤 On 문서 도구로 바로 됩니다.」

## 확인

- Claude Code: `claude mcp list` 에서 `on-document` 가 보이고, 다시 켠 뒤 `/mcp` 에서 연결됨으로 나오면 끝입니다.
- 첫 시험: 「○○ 회의 결과를 한글 결과보고로 만들어 줘」라고 하면 `on_write_gov` 가 불립니다. 공개 문서나 본인 문서로 「이 파일 글 꺼내 줘」라고 하면 `on_read` 가 불립니다.
- 설치 없이 웹에서 바로 쓰려면 https://onmunseo.duckdns.org/app/ 을 엽니다. 질문·고장 신고는 https://github.com/on-munseo/on-munseo.github.io/issues 입니다.

## 고급 — 기능만 골라 붙이기

보통은 `/mcp` 하나면 됩니다. 묶음 하나만 붙여야 할 까닭이 있을 때만 주소 끝을 바꾸고, 서버 이름도 묶음에 맞게 바꿉니다. 한글 공문서 만들기(`on_write_gov`)는 `/mcp` 와 `/mcp/gov` 에 있습니다.

| 서버 이름 | 주소 | 하는 일 |
|---|---|---|
| `on-text` | `https://onmunseo.duckdns.org/mcp/text` | 한글·PDF·오피스에서 글과 표 꺼내기 |
| `on-check` | `https://onmunseo.duckdns.org/mcp/check` | 결재 전 점검 |
| `on-mask` | `https://onmunseo.duckdns.org/mcp/mask` | 개인정보 찾기·가리기 |
| `on-hwpx` | `https://onmunseo.duckdns.org/mcp/hwpx` | 한글 파일 만들기(`on_write`)·바꾸기·쪽 그림 |
| `on-gov` | `https://onmunseo.duckdns.org/mcp/gov` | 공문서 꼴 한글 쓰기(`on_write_gov`)·표·그래프·체계도 |
| `on-tidy` | `https://onmunseo.duckdns.org/mcp/tidy` | 개조식·맞춤법·쉬운 말 |

## 지켜 주세요

- 공개 문서와 본인 문서만 보내게 안내합니다. 대외비 등 보안 표시가 있는 문서는 서버가 처리하지 않습니다.
- 문서는 서버 메모리에서만 다루고 처리 뒤 버립니다. 결과 파일 주소는 15분만 열립니다.
- 자세한 도구 목록과 다른 연결 방법은 [MCP.md](MCP.md)에 있습니다.
