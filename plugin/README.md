# On 문서 (on-document)

On 문서 원격 MCP 서버(`https://onmunseo.kr/mcp`)를 Claude 에 붙이는 플러그인입니다. 한글(HWP·HWPX)·PDF·워드·엑셀·파워포인트 문서에서 글과 표를 꺼내고, 자료를 보고서·계획서·보도자료 같은 공문서 꼴 한글(HWPX) 파일로 만들고, 결재 전에 맞춤법·날짜·금액·예산 셈을 점검하고, 개인정보를 찾아 가리고, 현행 법령 조문 원문을 확인합니다.

## 쓰는 법

플러그인을 더한 뒤 Claude 에게 평소처럼 말하면 됩니다.

- 「첨부한 ○○시 계획.hwpx 에서 표만 뽑아 보여 줘.」
- 「아래 메모로 ○○시 공문서 꼴 추진계획을 한글 파일로 만들어 줘.」
- 「이 보고서 초안을 결재 전에 점검해 줘 — 맞춤법, 날짜, 예산 합계.」
- 「이 글에서 주민등록번호·전화번호 같은 개인정보를 찾아 가려 줘.」
- 「이 글에 인용한 법 조항이 현행 법령과 맞는지 확인해 줘.」

Claude 앱(claude.ai·데스크톱)에서는 플러그인의 「커넥터」 칸에서 On 문서를 연결합니다. Claude Code 에서는 아래 한 줄로 더합니다.

```
/plugin install on-document --marketplace on-munseo/on-munseo.github.io
```

로그인 없이 하루 몫 안에서 씁니다. 글자 인식(스캔 문서)·PDF 만들기·쪽 그림 같은 무거운 일은 운영자가 메일 신청을 확인해 드리는 열쇠가 있어야 합니다. 도구 목록·한도·연결 방법은 [MCP 안내](https://github.com/on-munseo/on-munseo.github.io/blob/main/MCP.md)에 있습니다.

## 무엇을 보내고 어디에 남나

- 이 플러그인에는 프로그램 코드가 없습니다. 서버 주소 하나(`.mcp.json`)만 담겨 있습니다.
- On 문서 도구에 넘긴 문서와 글만 `onmunseo.kr`(국내 데이터센터)로 갑니다. 서버는 메모리에서만 처리하고 디스크에 쓰지 않으며, 처리가 끝나면 버립니다. 만든 파일은 15분 동안만 받을 수 있습니다.
- 서버는 문서를 AI 회사나 그 밖의 제3자에게 보내지 않습니다. 대화 기록·Claude 메모리·다른 파일은 받지 않습니다.
- 서버 기록에는 시각·요청 주소 꼴·결과 코드·걸린 시간·날짜별 이용 수 같은 운영 정보만 남고, 문서 내용·파일 이름은 남기지 않습니다. 자세한 것은 [개인정보 처리방침](https://onmunseo.kr/privacy)과 [이용약관](https://onmunseo.kr/terms)에 있습니다.
- 공개 문서와 본인 문서만 보내 주세요. 기관 내부 문서는 [웹 편집기](https://onmunseo.kr/app/)의 브라우저 안 기능이나 [내 PC 판](https://github.com/on-munseo/on-local)으로 다루세요.

## 문의

고장·질문은 [이슈](https://github.com/on-munseo/on-munseo.github.io/issues)에, 보안 문제는 [security.txt](https://onmunseo.kr/.well-known/security.txt)의 연락처로 알려 주세요.

---

## English

This plugin connects Claude to the hosted On Document (On 문서) MCP server at `https://onmunseo.kr/mcp`. It extracts text and tables from Korean HWP/HWPX, PDF, Word, Excel and PowerPoint files, turns notes into Korean government-style HWPX documents (reports, plans, press releases), checks drafts before approval (spelling, dates, amounts, budget arithmetic), finds and masks personal data, and looks up the current text of Korean statutes.

**Data.** The plugin contains no code, only the server address in `.mcp.json`. Only the documents and text you pass to On Document tools are sent to `onmunseo.kr` (a data center in South Korea). They are processed in memory, never written to disk, and discarded after processing; generated files can be downloaded for 15 minutes. Nothing is sent to AI companies or other third parties, and the server does not read conversation history, Claude's memory or other files. Server logs keep only operational data (time, request path pattern, status, duration, daily usage counts), never document content or file names. See the [privacy policy](https://onmunseo.kr/privacy) and [terms](https://onmunseo.kr/terms).

**Limits.** Lightweight tools work without sign-in within a daily quota. OCR, PDF output and page images need a key issued by the operator. Please send only public documents or your own documents.

**Support.** [GitHub issues](https://github.com/on-munseo/on-munseo.github.io/issues). Security reports: see [security.txt](https://onmunseo.kr/.well-known/security.txt).

**License.** The plugin configuration files are MIT-licensed. The On 문서 name and logo are not covered by the license.
