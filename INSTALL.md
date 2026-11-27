# On 문서 설치

길은 셋입니다 — ① 내 PC 판(npm 꾸러미 `on-munseo-local` — 문서가 이 컴퓨터 밖으로 안 감) · ② 법령 짝 주소(도구에 넣은 낱말·글만 서버로) · ③ 서버 판(설치할 프로그램 없이 주소 하나 — 공개 문서용). 길마다 한 줄은 [README 맨 위](README.md#ai-에게--이-저장소를-설치하려면)에 있습니다.

**가장 쉬운 길:** 쓰는 AI 도구(Claude Code 등)에 이렇게 말하세요.

> https://github.com/on-munseo/on-munseo.github.io 의 On 문서를 설치해 줘

AI 는 이 저장소의 [llms-install.md](llms-install.md)를 읽고 순서대로 붙입니다.

1. **등록은 AI 가 한 번** — 사용자 범위로 등록해 두면 그 뒤 모든 새 대화에서 계속 씁니다.
2. **활성화는 내가 한 번** — 등록한 그 대화에는 도구가 아직 붙지 않습니다. Claude Code 터미널은 `/exit` 뒤 `claude` 를 다시, VS Code 는 새 대화를 열거나 창을 다시 불러오고(명령 팔레트 「Developer: Reload Window」), Claude 데스크톱·웹·챗GPT 는 커넥터에서 「연결」을 누릅니다.
3. **열쇠가 없으면 로그인은 건너뛰고 손님으로 바로** 씁니다. 손님도 한글 공문서 만들기·글 꺼내기·결재 전 점검을 바로 씁니다.

한글 보고서·계획서·결과보고서·보도자료는 **공문서 쓰기(`on_write_gov`)** 가 만듭니다. `on_write` 는 꾸밈 없는 일반 한글 문서를 만들고, 원고가 공문서처럼 보이면 같은 공문서 꼴로 만듭니다(꾸밈 없는 꼴은 `plain: true`).

서버 판 주소(`/mcp`)에는 법령 원문 도구 **On 근거**(`law_article`·`med_article`·`law_check_citations` 등)도 들어 있어, 문서에 쓴 법령 조문과 인용을 법제처 원문으로 확인합니다.

## 손으로 붙이기

<!-- ai-install -->
**먼저 — 내 PC 판(문서를 이 컴퓨터 밖으로 보내지 않음, 인터넷 안 씀):** Claude Code 는 `claude mcp add -s user on-local -- npx -y on-munseo-local@0.2.1`, Codex 는 `codex mcp add on-local -- npx -y on-munseo-local@0.2.1`(사람이 이 PC 의 여러 AI 도구에 한 번에: `npx -y on-munseo-local@0.2.1 setup --pair` — 법령 짝 주소까지) · 판 고정 — 자동으로 새 판을 받지 않음, 새 판으로 올리기: 등록한 줄의 판 번호만 새 판으로 바꿔 다시 붙입니다(Claude Code 는 `claude mcp remove -s user on-local` 뒤 새 판 번호로 위 한 줄). Node.js 20 이상(띄울 때 npx 가 npm 저장소에 새 판을 묻는 것까지 없애려면 `npm install -g on-munseo-local` 뒤 명령을 `on-munseo-local` 로). 공문서 쓰기·법령은 짝 주소 `https://onmunseo.kr/mcp/law`(도구에 넣은 원고·질문·채울 서식만 서버로). 아래 표는 ③ 서버 판(Node 없이 바로 — 공개 문서용) 붙이는 법입니다. 확인할 거리(꾸러미·지문·만든 이·이용 조건)는 [README](README.md#ai-에게--이-저장소를-설치하려면)에 있습니다.
<!-- ai-install -->

주소: `https://onmunseo.kr/mcp`

| 도구 | 하는 법 |
|---|---|
| Claude Code | 터미널에서 `claude mcp add --transport http -s user on-document https://onmunseo.kr/mcp` 한 줄. `claude` 명령이 없는 곳(VS Code 확장 등)은 `~/.claude.json` 의 `mcpServers` 에 `"on-document": { "type": "http", "url": "https://onmunseo.kr/mcp" }` 를 더함. 그다음 Claude Code 를 다시 켬(`/exit` 뒤 `claude`, VS Code 는 새 대화). 열쇠가 있으면 `/mcp` → `on-document` → 로그인 |
| Claude Code 플러그인 | `/plugin marketplace add on-munseo/on-munseo.github.io` → `/plugin install on-document@on-munseo` → `/mcp` 에서 로그인 |
| Claude 데스크톱·claude.ai | 설정 → 커넥터 → 맞춤 커넥터 추가 → 이름 `On 문서`, 주소 붙여 넣기 → 「연결」 |
| 챗GPT | 설정 → 앱·커넥터 → 고급 설정에서 개발자 모드 켜기 → 만들기 → 주소, 인증 「OAuth」 |
| Cursor 등 | `mcp.json` 의 `mcpServers` 에 `"on-document": { "url": "https://onmunseo.kr/mcp" }` |
| Codex | 설정 파일 `~/.codex/config.toml` 에 두 줄 `[mcp_servers.on-document]`·`url = "https://onmunseo.kr/mcp"` 를 더하고 새 세션을 엶(`codex mcp add --url` 은 곧바로 로그인 창을 띄움). 열쇠가 있으면 그 뒤 `codex mcp login on-document` |
| VS Code | 터미널에서 `code --add-mcp '{"name":"on-document","type":"http","url":"https://onmunseo.kr/mcp"}'` 한 줄 |

- **열쇠가 있으면:** 연결할 때 뜨는 On 문서 로그인 창에 넣습니다. 주소 뒤나 설정 파일에 적지 마세요.
- **열쇠가 없으면(손님):** 로그인 없이 손님 도구 38개(문서 도구 22개 + 법령 원문 On 근거 16개)를 씁니다. 한 주소에서 하루 50번·1분에 6번(법령 도구는 따로 하루 100번·1분에 20번), 요청 하나 6MB까지입니다. 많이 쓰거나 글자 인식·PDF 정밀 읽기, 한글로 바꾸기·PDF·쪽 그림·도장 도구가 필요하면 열쇠를 받습니다. 열쇠 신청: `onmunseo.key [at] gmail.com`(제목에 「On 문서 열쇠 신청」).
- 설치 없이 웹에서 바로 쓰려면 [onmunseo.kr/app/](https://onmunseo.kr/app/) 을 엽니다.

주소는 `/mcp` 하나를 권장합니다. 고급용 묶음별 주소·도구 목록·Claude 데스크톱 설정 파일·curl 예시는 [MCP.md](MCP.md)에 있습니다.
