동행복권 사이트에서 온라인으로 구매한 로또/연금복권이 최근 1주일내에 당첨된 것이 있는지 확인하는 github action입니다.

프로그램 리파지토리: <https://github.com/chaeyk/lottery-agent>

# inputs

| 이름 | 설명 |
| --- | --- |
| username | 동행복권 사이트의 계정  |
| password | 동행복권 사이트 계정의 비밀번호 |
| telegram-bot-token | 텔레그램 봇ID |
| telegram-chatid | 텔레그램 메시지 수신자 ID |
| lottery-code | 복권 종류 |

**lottery-code** 정의

| code | name|
| --- | --- |
| lo40 | 로또 6/45 |
| lp72 | 연금복권 720+ |


# 예제

**로또 확인**

[사용중인 코드](https://github.com/chaeyk/lottery-agent/blob/main/.github/workflows/lottery_check_lo40.yml)
  
```yaml
name: Lotto 6/45 result checker

on:
  schedule:
  - cron: 30 12 * * 6 # every Saturday on 09:30 PM (KST)
  workflow_dispatch: {}

jobs:
  check:
    runs-on: ubuntu-latest
    steps:
    - name: Check result
      uses: chaeyk/lottery-check-action@v1
      with:
        username: ${{ secrets.DHL_USERID }}
        password: ${{ secrets.DHL_PASSWORD }}
        telegram-bot-token: ${{ secrets.TLG_BOTTOKEN }}
        telegram-chatid: ${{ secrets.TLG_CHATID }}
        lottery-code: lo40
```

**연금복권 확인**

[사용중인 코드](https://github.com/chaeyk/lottery-agent/blob/main/.github/workflows/lottery_check_lp72.yml)
```yaml
name: Annuity Lottery 720+ result checker

on:
  schedule:
  - cron: 0 11 * * 4 # every Thursday on 08:00 PM (KST)
  workflow_dispatch: {}

jobs:
  check:
    runs-on: ubuntu-latest
    steps:
    - name: Check result
      uses: chaeyk/lottery-check-action@v1
      with:
        username: ${{ secrets.DHL_USERID }}
        password: ${{ secrets.DHL_PASSWORD }}
        telegram-bot-token: ${{ secrets.TLG_BOTTOKEN }}
        telegram-chatid: ${{ secrets.TLG_CHATID }}
        lottery-code: lp72
```
