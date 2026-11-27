# On 문서 설치 안내 — AI 도구용

이 파일은 AI 도구(Claude Code, Claude, ChatGPT, Cursor 등)가 읽고 그대로 따라 하라고 둔 설치 순서입니다. 사람이 읽는 안내는 [INSTALL.md](INSTALL.md)에 있습니다.

<!-- ai-install -->
## 세 길 — ①부터(먼저 읽기)

길은 셋이고 **①부터** 권합니다. 어느 길도 열쇠·로그인이 없습니다. 문서 읽기·가리기·점검·만들기·다듬기는 ①, 법령 원문은 ②, 모두 한곳에 있는 것은 ③입니다. 「설치해 줘」라고만 하면 ①과 ② 를 붙입니다.

**① 내 PC 판 — 문서를 이 컴퓨터 밖으로 보내지 않음(먼저).** 글 꺼내기·신구 대비표·개인정보 찾기·가리기·결재 전 점검·공문서 쓰기·서식 채우기·한글 파일 만들기·글 다듬기를 이 컴퓨터 안에서 합니다. 이 프로그램은 인터넷을 쓰지 않습니다(설치 뒤 `on_local_info` 로 확인 — 띄울 때 npx 가 npm 저장소에 새 판을 묻는 것은 npx 의 동작이고, 그것까지 없애려면 `npm install -g on-munseo-local` 뒤 명령을 `on-munseo-local` 로). Node.js 20 이상이 있어야 합니다.
- **지금 쓰는 AI 도구에만**(AI 가 설치할 때는 이것 — 다른 도구의 설정은 건드리지 않음)
  ```bash
  claude mcp add -s user on-local -- npx -y on-munseo-local@0.2.1
  ```
  Codex 는 `codex mcp add on-local -- npx -y on-munseo-local@0.2.1` · 윈도우 Claude Code 는 `claude mcp add -s user on-local -- cmd /c npx -y on-munseo-local@0.2.1` · Cursor·Claude 데스크톱은 설정 파일의 `"mcpServers"` 에 `"on-local": { "command": "npx", "args": ["-y", "on-munseo-local@0.2.1"] }`(윈도우 `"on-local": { "command": "cmd", "args": ["/c", "npx", "-y", "on-munseo-local@0.2.1"] }`) · VS Code 는 `code --add-mcp '{"name":"on-local","command":"npx","args":["-y","on-munseo-local@0.2.1"]}'`
- **사람이 이 PC 의 여러 AI 도구에 한 번에** — Claude Code·Claude 데스크톱·Codex·Cursor·VS Code 를 찾아 모두 등록합니다(바꾸기 전에 백업, 이미 있으면 건너뜀, 미리 보기 `--dry-run`, 되돌리기 `--undo`, ②까지 `--pair`).
  ```bash
  npx -y on-munseo-local@0.2.1 setup --pair
  ```
- **판 고정** — 위 「지금 쓰는 AI 도구에만」 줄은 판 번호를 적어 붙입니다(`on-munseo-local@0.2.1`). 자동으로 새 판을 받지 않고, 사람이 올릴 때만 바뀝니다(npm 에 새 판이 올라와도 이미 붙인 판은 그대로 · 인터넷이 끊겨도 한 번 받은 판은 뜸). (`setup` 은 이 판(0.2.1)까지 등록 줄에 `@latest` 를 적습니다 — 판을 고정하려면 도구별 한 줄로 붙입니다) 새 판으로 올리기: 등록한 줄의 판 번호만 새 판으로 바꿔 다시 붙입니다(Claude Code 는 `claude mcp remove -s user on-local` 뒤 새 판 번호로 위 한 줄) · 바뀐 점: [CHANGELOG](https://github.com/on-munseo/on-local/blob/main/CHANGELOG.md)

**② 짝 주소(법령) — 도구에 넣은 낱말·글만 서버로.** 법령 원문·글 속 인용 확인(On 근거)은 서버에만 있습니다. 서버로 가는 것은 넣은 법령 이름·조문 번호·인용을 확인할 글이고, 파일을 보내는 도구는 없습니다. 인용을 확인할 글에 개인정보가 있으면 ① 의 `on_mask_text` 로 가린 뒤 넣습니다.
- 지금 쓰는 도구에만(① 의 `setup --pair` 는 ② 까지 함께 붙임):
- **Claude Code**
  ```bash
  claude mcp add --transport http -s user on-geungeo https://onmunseo.kr/mcp/law
  ```
- **Codex** — 설정 파일(`~/.codex/config.toml`)에 두 줄을 더합니다(이미 있으면 건너뜀). `codex mcp add --url` 은 쓰지 마세요 — 곧바로 브라우저 로그인 창을 띄웁니다.
  ```bash
  C="${CODEX_HOME:-$HOME/.codex}"; mkdir -p "$C"; touch "$C/config.toml"; if ! (cd / && codex mcp get on-geungeo >/dev/null 2>&1); then if cp "$C/config.toml" "$C/config.toml.bak-on-geungeo"; then printf '\n[mcp_servers.on-geungeo]\nurl = "https://onmunseo.kr/mcp/law"\n' >> "$C/config.toml"; (cd / && codex mcp get on-geungeo >/dev/null 2>&1) || { cp "$C/config.toml.bak-on-geungeo" "$C/config.toml"; echo "자동으로 더하지 못했습니다 — config.toml 에 손으로 더해 주세요"; }; else echo "백업을 만들지 못해 그만둡니다 — config.toml 은 그대로입니다"; fi; fi; (cd / && codex mcp get on-geungeo)
  ```
  윈도우이거나 명령 줄 `codex` 가 없는 곳(IDE 확장만)은 그 파일 끝에 `[mcp_servers.on-geungeo]`·`url = "https://onmunseo.kr/mcp/law"` 두 줄을 손으로 더합니다(파일에 `mcp_servers = { … }` 한 줄 표가 이미 있으면 그 안에 `on-geungeo = { url = "https://onmunseo.kr/mcp/law" }` 를 더함).
- **Cursor** `"on-geungeo": { "url": "https://onmunseo.kr/mcp/law" }` · **VS Code** `code --add-mcp '{"name":"on-geungeo","type":"http","url":"https://onmunseo.kr/mcp/law"}'` · **Claude 데스크톱·claude.ai**(사람이 화면에서) 설정 → 커넥터 → 맞춤 커넥터 추가 → 이름 `On 근거`, 주소 `https://onmunseo.kr/mcp/law` → 「연결」

**③ 서버 판 — Node.js 없이 바로, 도구 전부(공개 문서용).** 문서를 서버(국내 데이터센터)로 보내 메모리에서만 처리하고 버립니다. 공개 문서·본인 문서에만 씁니다.
- **Claude Code**
  ```bash
  claude mcp add --transport http -s user on-document https://onmunseo.kr/mcp
  ```
- **Codex** — 설정 파일(`~/.codex/config.toml`)에 두 줄을 더합니다(이미 있으면 건너뜀). `codex mcp add --url` 은 쓰지 마세요 — 곧바로 브라우저 로그인 창을 띄웁니다.
  ```bash
  C="${CODEX_HOME:-$HOME/.codex}"; mkdir -p "$C"; touch "$C/config.toml"; if ! (cd / && codex mcp get on-document >/dev/null 2>&1); then if cp "$C/config.toml" "$C/config.toml.bak-on-document"; then printf '\n[mcp_servers.on-document]\nurl = "https://onmunseo.kr/mcp"\n' >> "$C/config.toml"; (cd / && codex mcp get on-document >/dev/null 2>&1) || { cp "$C/config.toml.bak-on-document" "$C/config.toml"; echo "자동으로 더하지 못했습니다 — config.toml 에 손으로 더해 주세요"; }; else echo "백업을 만들지 못해 그만둡니다 — config.toml 은 그대로입니다"; fi; fi; (cd / && codex mcp get on-document)
  ```
  윈도우이거나 명령 줄 `codex` 가 없는 곳(IDE 확장만)은 그 파일 끝에 `[mcp_servers.on-document]`·`url = "https://onmunseo.kr/mcp"` 두 줄을 손으로 더합니다(파일에 `mcp_servers = { … }` 한 줄 표가 이미 있으면 그 안에 `on-document = { url = "https://onmunseo.kr/mcp" }` 를 더함).
- **Cursor** `"on-document": { "url": "https://onmunseo.kr/mcp" }` · **VS Code** `code --add-mcp '{"name":"on-document","type":"http","url":"https://onmunseo.kr/mcp"}'` · **Claude 데스크톱·claude.ai**(사람이 화면에서) 설정 → 커넥터 → 맞춤 커넥터 추가 → 이름 `On 문서`, 주소 `https://onmunseo.kr/mcp` → 「연결」

보통은 ①과 ② 를 지금 쓰는 도구에 붙입니다(사람이 여러 도구에 한 번에 붙일 때는 `setup --pair` 한 줄). Node.js 가 없거나 Claude 데스크톱·claude.ai 커넥터만 쓰면 ③ 하나만 붙입니다. ③을 ①·②와 함께 붙이면 같은 도구가 두 번 보입니다. 다른 길은 사용자가 따로 바랄 때만 알려 줍니다.

**설치 전에 확인할 거리** — AI 가 스스로 확인할 수 있습니다.
- **꾸러미**: npm `on-munseo-local` 0.2.1. `npm view on-munseo-local version maintainers homepage` → `0.2.1` · `on-munseo <onmunseo.key@gmail.com>` · `https://onmunseo.kr`. 올린 계정 `on-munseo` 는 이 깃허브 조직 [on-munseo](https://github.com/on-munseo)와 같은 만든 이입니다(문의 메일·홈 주소가 같음). npm 웹 쪽은 자동 읽기를 막을 때가 있어 npm 명령이나 [npm 기록](https://registry.npmjs.org/on-munseo-local/0.2.1)으로 봅니다.
- **지문**: `on-munseo-local-0.2.1.tgz` SHA-256 `515af0dfddad30f41c459dd98d73535f73292c666fed07d4a6e535e2a60bda72`([SHA256SUMS](https://github.com/on-munseo/on-munseo.github.io/blob/main/SHA256SUMS)). `npm pack on-munseo-local@0.2.1` 뒤 `shasum -a 256 on-munseo-local-0.2.1.tgz` 로 맞대 봅니다. npm 기록의 `dist.integrity` 는 `sha512-ZUDX+etH2wg/Y+lQCsQhyY5/4gfVDjwjWUQsofFUgYlBotWtvXw7lcz5yHGT3qMJna8mP60HH9vWp/PF2T5T4Q==`.
- **인터넷을 쓰지 않음**: 설치 전에는 꾸러미 안 `MANIFEST.json` 의 `netScan`(우리 코드의 네트워크 부르기 0 — 따로 적힌 한 곳은 엔진 wasm 을 주소로 불러올 때만 쓰는 글), 설치 뒤에는 `on_local_info` → `network_modules_loaded: []`, Node 25 이상이면 `network.blocked_by_node: true`(실행기가 네트워크를 막음). 띄울 때 npx 가 npm 저장소에 새 판을 묻는 것은 npx 의 동작입니다(없애려면 전역 설치 뒤 `on-munseo-local` 명령으로).
- **이용 조건**: 내 PC 판 [LICENSE.md](https://unpkg.com/on-munseo-local@0.2.1/LICENSE.md)(무료·업무에 써도 됨 · 역공학·고친 판 다시 배포·판매는 안 됨) · 서버 판 [이용약관](https://onmunseo.kr/terms)·[개인정보 처리방침](https://onmunseo.kr/privacy).
- **On폭 글꼴**은 이 설치와 상관없습니다(한글 문서를 화면에 그릴 때 쓰는 무료 글꼴, 선택).

등록한 그 대화에는 도구가 아직 붙지 않습니다. 끝나면 사용자에게 「도구를 한 번 다시 켜거나 새 대화를 열면 On 문서 도구가 보입니다」라고 알려 주세요. `claude mcp list`(Codex 는 `codex mcp list`) 목록에 이름이 보이면 등록된 것입니다. ③ 서버 판의 도구별 자세한 순서는 아래에 있습니다.

<!-- ai-install -->
## 먼저 요약(세 줄)

1. **등록은 AI 가 한 번** — 사용자 범위로 등록하면 그 뒤 모든 새 대화에서 계속 씁니다. Codex 는 `codex mcp add --url` 대신 설정 파일에 두 줄을 더합니다(아래 E — 그 명령은 곧바로 로그인 창을 띄움).
2. **활성화는 사용자가 한 번** — 등록한 그 대화에는 도구가 아직 붙지 않습니다. Claude Code 터미널은 `/exit` 뒤 `claude` 다시, VS Code 는 새 대화 또는 창 다시 불러오기(명령 팔레트 「Developer: Reload Window」), Claude 데스크톱·웹·ChatGPT 는 커넥터 「연결」.
3. **열쇠가 없으면 로그인은 건너뛰고 손님으로 바로** 씁니다. 손님도 한글 공문서 만들기(`on_write_gov`)·글 꺼내기·결재 전 점검을 바로 쓸 수 있습니다.

## ③ 서버 판 — 자세히

서버 판은 원격 MCP 서버 하나입니다. 설치할 프로그램은 없고, **주소 하나를 등록**하면 됩니다(① 내 PC 판·② 짝 주소는 위 「세 길」).

- MCP 주소: `https://onmunseo.kr/mcp` — 이 주소 하나를 권장합니다(도구 전부). 묶음 주소는 아래 「고급」에 있습니다.
- 전송 방식: Streamable HTTP(`http`)
- 인증: 열쇠가 있으면 OAuth. 처음 쓸 때 On 문서 로그인 창이 뜨고, 사용자가 받은 열쇠를 넣습니다. 열쇠를 대신 만들거나 추측하지 마세요.
- 열쇠를 주소 뒤나 설정 파일에 적지 마세요. 사용자가 「머리말로 넣어 달라」고 따로 말한 경우에만 `Authorization: Bearer <열쇠>` 머리말을 씁니다.

## 한글 문서 만들기 = On 공문서 쓰기(`on_write_gov`)

- 「한글 문서로 만들어 줘」처럼 보고서·계획서·결과보고서·보도자료 한글 문서를 만들 때 쓰는 도구는 `on_write_gov` 입니다. 휴먼명조·장 제목 막대·□ ○ - 단계의 공문서 꼴로 나옵니다.
- `on_write` 는 꾸밈 없는 일반 한글 문서를 만듭니다. style 없이 받은 원고가 공문서처럼 보이면 같은 공문서 꼴로 만들고 결과에 `auto_style` 을 적습니다(꾸밈 없는 꼴을 바라면 `plain: true`).

## 법령 원문 = On 근거(`law_…`·`med_…`)

- 같은 주소(`/mcp`)에 법령 원문 도구 16개가 들어 있고, 열쇠가 없어도 씁니다. 법제처 현행 원문을 미리 받아 둔 사본이며 결과 끝에 받은 날이 적힙니다.
- 법령 조문을 말하거나 문서에 법령을 인용할 때는 기억에 기대지 말고 `law_article`(현행 법령 전체)·`med_article`(의료·응급 법률 55개 — 위임·개정·벌칙·판례까지)로 원문을 확인하고, 다 쓴 글은 `law_check_citations` 로 인용을 맞대어 봅니다.

## 열쇠가 없으면(손님) — 등록 전에 먼저 읽기

- 사용자에게 열쇠가 없으면 **로그인(Authenticate) 단계는 건너뜁니다.** 등록만 하면 손님으로 바로 씁니다.
- 손님·열쇠 설명은 길게 하지 말고, 사용자가 바라는 일(한글 문서 만들기 등)을 바로 도구로 처리합니다.
- 손님 한도는 한 주소에서 하루 50번·1분에 6번(법령 도구 `law_`·`med_` 는 따로 하루 100번·1분에 20번), 요청 하나 6MB까지입니다. 로컬 파일은 명령을 쓸 수 있으면 `curl -s --data-binary @파일 -H "x-file-name: 파일이름" https://onmunseo.kr/api/drop` 로 올려 받은 `url` 을 `file_url` 로 넘깁니다(base64 보다 빠름). 열쇠 안내는 하루 몫이 찼다는 결과가 왔거나 열쇠가 필요한 도구를 바랄 때만 합니다. 열쇠 신청은 `onmunseo.key [at] gmail.com`(제목 「On 문서 열쇠 신청」)입니다.

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
     claude mcp add --transport http -s user on-document https://onmunseo.kr/mcp
     ```
   - **길 2 — `claude` 명령이 없으면(VS Code 확장 등 PATH 에 없는 환경):** 사용자 설정 파일 `~/.claude.json` 의 맨 위 `"mcpServers"` 에 아래 항목을 더합니다. 이미 있는 다른 설정과 서버는 지우지 마세요(JSON 으로 읽어 이 키만 더하고 다시 씀). `"mcpServers"` 가 없으면 맨 위에 새로 둡니다. 이 꼴은 길 1 이 만드는 것과 같습니다.
     ```json
     {
       "mcpServers": {
         "on-document": { "type": "http", "url": "https://onmunseo.kr/mcp" }
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
2. 이름 `On 문서`, 원격 MCP 서버 주소 `https://onmunseo.kr/mcp`.
3. 「연결」을 누릅니다. 열쇠가 있으면 뜨는 On 문서 로그인 창에 넣고, 없으면 손님으로 씁니다.
4. **끝나면 사용자에게 알립니다:** 「새 대화를 열면 On 문서 도구가 보입니다.」

요금제·판에 따라 메뉴 이름이 조금 다르거나 이 메뉴가 없을 수 있습니다.

### C. ChatGPT(웹·앱)

1. 설정 → 앱·커넥터 → 고급 설정에서 「개발자 모드」를 켭니다.
2. 「만들기」(사용자 MCP 서버 추가)에서 이름 `On 문서`, 주소 `https://onmunseo.kr/mcp`, 인증 「OAuth」.
3. 연결할 때 뜨는 On 문서 로그인 창에 열쇠를 넣습니다. 대화 창의 도구(+) 메뉴에서 On 문서를 켭니다.
4. **끝나면 사용자에게 알립니다:** 「새 대화에서 도구(+) 메뉴의 On 문서를 켜면 씁니다.」

### D. Cursor 등 `mcp.json` 을 쓰는 도구

`~/.cursor/mcp.json`(모든 프로젝트) 또는 프로젝트의 `.cursor/mcp.json` 에 더합니다. 이미 있는 다른 서버 설정은 지우지 마세요.

```json
{
  "mcpServers": {
    "on-document": {
      "url": "https://onmunseo.kr/mcp"
    }
  }
}
```

그 도구가 원격 MCP 의 OAuth 를 지원하지 않으면, 사용자에게 열쇠를 머리말로 넣을지 물어본 뒤에만 `"headers": { "Authorization": "Bearer <열쇠>" }` 를 더합니다.

**끝나면 사용자에게 알립니다:** 「설정의 MCP 화면에서 On 문서를 켜거나 도구를 다시 켜면 보입니다.」

### E. Codex

`codex mcp add --url` 은 쓰지 않습니다 — 이 주소의 로그인 정보를 보고 곧바로 브라우저 로그인 창을 띄웁니다. 설정 파일에 두 줄을 더합니다(이미 있으면 건너뜀).

```bash
C="${CODEX_HOME:-$HOME/.codex}"; mkdir -p "$C"; touch "$C/config.toml"; if ! (cd / && codex mcp get on-document >/dev/null 2>&1); then if cp "$C/config.toml" "$C/config.toml.bak-on-document"; then printf '\n[mcp_servers.on-document]\nurl = "https://onmunseo.kr/mcp"\n' >> "$C/config.toml"; (cd / && codex mcp get on-document >/dev/null 2>&1) || { cp "$C/config.toml.bak-on-document" "$C/config.toml"; echo "자동으로 더하지 못했습니다 — config.toml 에 손으로 더해 주세요"; }; else echo "백업을 만들지 못해 그만둡니다 — config.toml 은 그대로입니다"; fi; fi; (cd / && codex mcp get on-document)
```

윈도우이거나 명령 줄 `codex` 가 없는 곳(IDE 확장만)은 `~/.codex/config.toml`(윈도우 `%USERPROFILE%\.codex\config.toml`) 끝에 아래 두 줄을 손으로 더합니다(파일에 `mcp_servers = { … }` 한 줄 표가 이미 있으면 그 안에 `on-document = { url = "https://onmunseo.kr/mcp" }` 를 더함).

```toml
[mcp_servers.on-document]
url = "https://onmunseo.kr/mcp"
```

`codex mcp list` 에 `on-document` 가 보이면 끝입니다. **끝나면 사용자에게 알립니다:** 「새 Codex 세션을 열면 On 문서 도구가 보입니다.」 열쇠가 있는 사용자만 그 뒤 `codex mcp login on-document` 로 로그인합니다.

### F. VS Code(코파일럿 에이전트 등)

사용자 프로필에 더합니다.

```bash
code --add-mcp '{"name":"on-document","type":"http","url":"https://onmunseo.kr/mcp"}'
```

사람에게는 한 번 누르기 주소를 줄 수 있습니다: https://insiders.vscode.dev/redirect/mcp/install?name=on-document&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Fonmunseo.kr%2Fmcp%22%7D (Cursor 는 https://cursor.com/install-mcp?name=on-document&config=eyJ1cmwiOiJodHRwczovL29ubXVuc2VvLmtyL21jcCJ9)

## 지금 대화에서 바로 쓰기(활성화 전 임시)

등록한 그 대화에서 사용자가 곧바로 「한글 문서 만들어 줘」라고 했는데 On 문서 도구가 아직 안 보이면, 사용자를 기다리게 하지 말고 같은 주소를 HTTP 로 직접 불러 손님으로 처리할 수 있습니다. 서버는 상태를 두지 않는 방식이라 `tools/call` 하나로 됩니다(`initialize` 는 안 해도 됨).

```bash
cat > call.json <<'EOF'
{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"on_write_gov","arguments":{
 "style":"결과보고서",
 "markdown":"# ○○ 회의 결과보고\n\n## Ⅰ. 회의 개요\n\n○ 일시: 2026. 11. 20.(금) 14:00\n○ 장소: ○○ 회의실\n\n## Ⅱ. 주요 내용\n\n○ 교육 과정 8회 운영, 수료 214명\n"}}}
EOF
curl -s https://onmunseo.kr/mcp \
  -H "Content-Type: application/json" -H "Accept: application/json, text/event-stream" \
  --data-binary @call.json
```

- 결과 `result.content[0].text` 는 JSON 글입니다. 그 안의 `file.url` 이 만든 한글 파일 주소이고 **15분**만 열리니 바로 사용자에게 알립니다. `check.same` 이 `true` 면 원고의 글·숫자를 하나도 잃지 않은 것입니다. `tell_user` 는 사용자에게 그대로 전할 말입니다.
- 원고에 따옴표·줄바꿈이 많으면 위처럼 파일(`--data-binary @call.json`)로 보내면 깨지지 않습니다.
- 결과를 건넬 때 사용자에게 한 줄 덧붙입니다: 「다음부터는 다시 켠 뒤 On 문서 도구로 바로 됩니다.」

## 확인

- Claude Code: `claude mcp list` 에서 `on-document` 가 보이고, 다시 켠 뒤 `/mcp` 에서 연결됨으로 나오면 끝입니다. Codex 는 `codex mcp list` 에서 `on-document` 가 보이면 끝입니다.
- 첫 시험: 「○○ 회의 결과를 한글 결과보고로 만들어 줘」라고 하면 `on_write_gov` 가 불립니다. 공개 문서나 본인 문서로 「이 파일 글 꺼내 줘」라고 하면 `on_read` 가 불립니다. 「응급의료법 제2조 원문 보여 줘」라고 하면 `med_article` 이나 `law_article` 이 불립니다.
- 설치 없이 웹에서 바로 쓰려면 https://onmunseo.kr/app/ 을 엽니다. 질문·고장 신고는 https://github.com/on-munseo/on-munseo.github.io/issues 입니다.

## 고급 — 기능만 골라 붙이기

보통은 `/mcp` 하나면 됩니다. 묶음 하나만 붙여야 할 까닭이 있을 때만 주소 끝을 바꾸고, 서버 이름도 묶음에 맞게 바꿉니다. 한글 공문서 만들기(`on_write_gov`)는 `/mcp` 와 `/mcp/gov` 에 있습니다.

| 서버 이름 | 주소 | 하는 일 |
|---|---|---|
| `on-text` | `https://onmunseo.kr/mcp/text` | 한글·PDF·오피스에서 글과 표 꺼내기 |
| `on-check` | `https://onmunseo.kr/mcp/check` | 결재 전 점검 |
| `on-mask` | `https://onmunseo.kr/mcp/mask` | 개인정보 찾기·가리기 |
| `on-hwpx` | `https://onmunseo.kr/mcp/hwpx` | 한글 파일 만들기(`on_write`)·바꾸기·쪽 그림 |
| `on-gov` | `https://onmunseo.kr/mcp/gov` | 공문서 꼴 한글 쓰기(`on_write_gov`)·표·그래프·체계도 |
| `on-tidy` | `https://onmunseo.kr/mcp/tidy` | 개조식·맞춤법·쉬운 말 |
| `on-write` | `https://onmunseo.kr/mcp/write` | 공문서 쓰기·한글 만들기·서식 채우기·글 다듬기·법령 — 문서를 읽어 가는 도구 없이 |
| `on-geungeo` | `https://onmunseo.kr/mcp/law` | 법령 원문(On 근거) — 현행 법령 조문·문구 찾기·인용 확인, 의료·응급 법률의 위임·개정·벌칙·판례 |

## 지켜 주세요

- 서버를 거치는 MCP 에는 공개 문서와 본인 문서만 보내게 안내하고, 기관 내부 문서는 웹 편집기(onmunseo.kr/app)에서 브라우저 안에서 처리하는 기능(한글 열기·고치기·저장, 결재 전 점검, 개인정보 가리기)으로 다루게 안내합니다. 대외비 등 보안 표시가 있는 문서는 서버가 처리하지 않습니다.
- 문서는 서버 메모리에서만 다루고 처리 뒤 버립니다. 결과 파일 주소는 15분만 열립니다.
- 자세한 도구 목록과 다른 연결 방법은 [MCP.md](MCP.md)에 있습니다.
