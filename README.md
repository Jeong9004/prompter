# prompter

> 원래 프롬프트를 아래 지침대로 전문가 수준으로 다시 써 주는 Claude 스킬

## 지침

### 핵심 전제

단순히 더 길거나 거대한 작업(bigger)이 아닌, 본질을 파고드는 더 깊이 있는 작업(deeper)을 원함

### 프롬프트 재작성 전 4가지 요구 조건

1. **전문가의 관점 파악**: 해당 분야 최고 전문가라면 하겠지만, 현재 질문자가 놓치거나 요구하지 않은 작업이 무엇인지 제시
2. **1차 가공되지 않은 원자료 정의**: 이미 요약·가공된 2차 정보 대신, 전문가가 처음부터 참고할 가장 기초적인 '원천 데이터(Raw material)' 명시
3. **구체적 방법론 및 도구 지정**: 실제로 그들이 활용할 특정한 방법론(Methodology)과 툴(Tools) 제시
4. **객관적 검증 기준 마련**: 사용자와 AI의 주관적 판단 외에, 결과물이 옳고 유효함을 증명할 수 있는 객관적 검증 방법 제시

### 최종 지시

위 4가지를 반영하여 원래 질문자의 프롬프트를 전문가 수준으로 다시 작성(Rewrite)할 것

다시 작성한 프롬프트에는 아래 3가지 지시를 담을 것

1. 최종목표를 생각하라고 할 것
2. 최종목표를 토대로 작업순서를 역설계해서 계획을 짜라고 할 것
3. 최종목표 달성을 위한 루프를 짜 달라고 할 것

## 사용법

```
/prompter <원래 프롬프트>
```

1. 질문 없이 바로 다시 쓴 프롬프트가 코드블록 하나로 나옵니다.
2. 코드블록을 복사해서 **새 대화**에 붙여넣습니다.
3. AI가 먼저 인터뷰(grill-with-docs)를 하면 답합니다.
4. 인터뷰가 끝나면 AI가 작업을 시작합니다.

## 출력 형태

```
# [작업명]

## 원래 요청
## 최종목표
## 작업순서 (최종목표에서 역설계)
## 루프
## 전문가의 관점: 놓치거나 요구하지 않은 작업
## 1차 원자료 (Raw material)
## 방법론(Methodology)·도구(Tools)
## 객관적 검증 기준

## 시작 전
grill-with-docs 인터뷰 지시
```

- 원래 요청은 원문 그대로 들어갑니다.
- 분량은 A4 1~2쪽 이내입니다.

## 설치

### Claude Code

```bash
npx skills add Jeong9004/prompter -g -a claude-code --skill prompter --skill grilling --skill domain-modeling
```

설치 후 새 세션을 열면 `/prompter` 를 쓸 수 있습니다.

### Claude Desktop · claude.ai

1. [Releases](https://github.com/Jeong9004/prompter/releases/latest) 에서 zip 3개를 내려받습니다.
   - [`prompter.zip`](https://github.com/Jeong9004/prompter/releases/latest/download/prompter.zip)
   - [`grilling.zip`](https://github.com/Jeong9004/prompter/releases/latest/download/grilling.zip)
   - [`domain-modeling.zip`](https://github.com/Jeong9004/prompter/releases/latest/download/domain-modeling.zip)
2. **Customize > Skills > + > Upload a skill** 에서 하나씩 올립니다.
   - 메뉴 이름은 버전에 따라 "설정 > 기능"일 수 있습니다.
   - 코드 실행 기능이 켜진 유료 플랜이 필요합니다.

### 스킬을 못 쓰는 환경

[`skills/prompter/SKILL.md`](skills/prompter/SKILL.md) 내용(맨 위 `---` 사이 부분 제외)을 Project 지침에 붙여넣습니다.

## 포함된 스킬

| 스킬 | 구분 | 하는 일 |
|---|---|---|
| [`prompter`](skills/prompter/SKILL.md) | 필수 | 원래 프롬프트를 지침대로 다시 씀 |
| [`grilling`](skills/grilling/SKILL.md) | 필수 | 번호와 추천 답을 붙여 라운드별로 인터뷰 |
| [`domain-modeling`](skills/domain-modeling/SKILL.md) | 필수 | 인터뷰 중 정해진 용어·결정을 문서로 남김 |
| [`grill-with-docs`](skills/grill-with-docs/SKILL.md) | 선택 | 위 두 스킬을 한 번에 부르는 단축 명령 (`/grill-with-docs`) |
| [`wayfinder`](skills/wayfinder/SKILL.md) | 선택 | 한 대화로 안 끝나는 큰 작업을 나눠 진행 |
| [`prototype`](skills/prototype/SKILL.md), [`research`](skills/research/SKILL.md), [`setup-matt-pocock-skills`](skills/setup-matt-pocock-skills/SKILL.md) | 선택 | wayfinder가 내부에서 사용 |

- grill-with-docs 는 사람이 입력할 때만 실행되는 단축 명령이라, 다시 쓴 프롬프트는 `grilling` 과 `domain-modeling` 을 직접 부르도록 되어 있습니다.
- 스킬이 없어도 같은 방식으로 직접 인터뷰하라는 지시가 들어 있어 동작합니다.

## 라이선스

- `prompter`: [MIT](LICENSE)
- 나머지 스킬: [Matt Pocock](https://github.com/mattpocock/skills) 의 MIT 스킬을 수정 없이 함께 배포, [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md)
