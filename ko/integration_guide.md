## 개요
### 연동서비스

Dooray! 메신저에서는 사람이 아닌 다양한 도구에게 명령하고 메시지를 받으면서 더 효율적으로 업무를 할 수 있습니다.
메신저에서 제공하지 않는 기능을 직접 구현하고 싶을 때 이 기능을 활용하여 여러분도 자신의 업무를 좀 더 효율적으로 자동화 할 수 있습니다.
Inline-image-2018-03-09 11.56.21.757.png

현재 소개할 기능은 커맨드를 직접 생성하는 것에 대한 내용이며, 앞으로 Bot, API 등 다양한 연동서비스를 제공할 예정입니다.

### 커맨드

커맨드는 ‘/’문자 뒤에 덧붙여서 특정한 기능을 수행하도록 하는 명령어입니다.
Dooray! 메신저에서는 기본적으로 ‘/mute’, ‘/status’, ‘/search’ 등의 System 커맨드를 제공합니다.
예컨대 메시지 내용을 찾거나, 자신의 상태를 바꾸는 등의 기능을 마우스의 클릭이나 다른 조작 없이 텍스트 입력으로 빠르게 실행할 수 있도록 도와줍니다.

Inline-image-2018-04-17 22.40.10.401.png

자신이 원하는 기능을 수행하는 커맨드를 직접 만들어 사용할 수 있습니다.
예를 들어 매일 아침 교통 정보와 날씨를 메시지로 받아볼 수 있고, 간단한 명령어를 입력하여 투표를 생성할 수도 있습니다.

아래 그림은 커맨드 서버와 메신저 서버 간의 통신 과정입니다.
Inline-image-2018-04-10 10.32.50.484.png

사용자는 '/문자'와 대화방에 등록된 커맨드를 입력합니다. 입력한 커맨드 정보는 메신저 서버를 통해 커맨드 서버로 전송이 됩니다. 커맨드 서버에서 처리한 결과를 메신저 서버로 전송합니다. 메신저 서버는 커맨드 서버로부터 받은 데이터를 기반으로 사용자에게 결과를 보여줍니다.

### 사용 환경

사용자는 PC와 모바일에서 커맨드를 입력하고 결과를 확인할 수 있습니다. 그렇기 때문에 커맨드 제작자는 모바일 환경에서의 레이아웃도 신경써야 합니다.
현재 대화방에 커맨드를 추가하는 기능은 PC에서만 제공합니다.

### 제작 가이드

커맨드의 제작 및 등록 방법에 대해서는 아래의 문서에서 설명합니다.

---

## 커맨드 추가하기

접 만든 커맨드를 사용하기 위해서 Dooray! 메신저에 추가해야 합니다.

### 추가 화면으로 이동

Dooray! 메신저 좌측 상단의 자신의 이름을 선택 > '연동 서비스’ 메뉴를 선택합니다.
스크린샷 2018-05-02 오전 9.23.39.png

지금은 아래와 같이 빈 화면이 표시됩니다.
Inline-image-2018-04-27 11.38.01.799.png

### 앱 추가

우선 앱을 만들어야 합니다. 앱은 연동서비스의 묶음 단위입니다.
하나의 앱에 여러 개의 커맨드를 추가할 수 있습니다. 아래의 정보를 입력하여 앱을 만들어 봅니다.
각 정보는 대화방에 공개된 커맨드를 등록할 때 목록에 노출됩니다.

Inline-image-2018-04-27 11.24.34.026.png

|구분|설명|
|---|---|
|Image|대화방에서 커맨드를 사용할 때 메시지의 전송자 아이콘으로 표시됩니다.|
|Name|대화방에서 커맨드를 사용할 때 메시지의 전송자 이름으로 표시됩니다.|
|Description|앱의 설명입니다.|

이제 앱이 만들어졌습니다. 생성되어 있는 Token과 비어 있는 커맨드 목록을 보실 수 있습니다.
Token 값은 커맨드 요청시 함께 전송되어 요청을 검증하는데에 사용합니다. Token 값이 외부에 유출되지 않도록 주의하시기 바랍니다. 만약 Token에 외부에 유출된 경우에는 Regenerate 버튼을 이용해 기존 Token을 파기하고 다시 발급해 사용하세요.
Inline-image-2018-04-27 11.30.33.092.png

### 커맨드 추가

앱을 등록 한 후, Slash Command 영역의 '추가' 버튼을 누르면 커맨드를 추가할 수 있습니다.
되도록 하나의 앱에는 서로 밀접하게 관계가 있는 커맨드를 추가하는 것을 권장합니다.

미리 제작한 커맨드가 없다면, 다음 문서에서 예제로 설명할 /hi 커맨드를 입력하면 됩니다.
Command 추가.png

|구분|설명|
|---|---|
|Command|‘/’를 포함하여 대화방에서 입력할 명령어를 입력합니다.<br>명령어는 커맨드의 기능을 나타내는 직관적인 것이 좋습니다.|
|Request URL|커맨드를 실행 시 요청할 커맨드 서버 URL을 입력합니다.|
|Description|커맨드 사용할 때 표시될 설명입니다. 다른 사람이 커맨드의 기능을 쉽게 이해할 수 있도록 적어주세요.|
|Parameter Hint|커맨드와 함께 어떤 parameter를 적어야 하는지 설명해 주세요.<br>(지역,시간,사람,날짜, 텍스트, 숫자 등의 정보를 입력할 수 있습니다.)|
|Public|해당 커맨드를 다른 사람들도 대화방에 추가하여 사용할 수 있습니다.|

커맨드가 추가되었습니다.
Inline-image-2018-04-27 12.58.37.610.png

### Interactive Request URL 입력

버튼과 드롭 메뉴를 통해 사용자의 Action을 받으려면 Interactive Message 처리를 위한 별도의 URL이 필요합니다.

Command 만들기.png

|구분|설명|
|---|---|
|Interactive Message Request URL|버튼과 드롭 메뉴 등 메시지를 통해서 유저와 상호작용하는 경우, 유저의 요청을 전달할 URL을 입력합니다.|
|Interactive Message Optional URL|메시지에 dataSource를 external로 설정한 메뉴 목록 등을 제공하는 경우, 메뉴 목록을 요청할 URL을 입력합니다.|

---

## Hello World! 메시지 보내기
대화방에서 "/hi"라고 입력하면, "Hello world!"라고 대답하는 아주 간단한 커맨드를 만들어 보겠습니다.

### 커맨드 실행

사용자가 Dooray! 메신저를 통해 /hi 커맨드를 실행하면 커맨드 서버는 아래와 같은 JSON 데이터를 전달받습니다.

```json
{
    "tenantId": "1234567891234567891",
    "tenantDomain": "guide.dooray.com",
    "channelId": "1234567891234567891",
    "channelName": "커맨드 가이드 채널",
    "userId": "1234567891234567891",
    "userName": "홍길동",
    "command": "/hi",
    "text": "/hi"
    "responseUrl": "https://guide.dooray.com/messenger/api/commands/hook/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "appToken": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "triggerId": "1234567891234.xxxxxxxxxxxxxxxxxxxx"
}
```

|필드명|설명|
|---|---|
|tenantId|커맨드가 등록된 테넌트의 ID|
|tenantDomain|커맨드가 등록된 테넌트의 도메인|
|channelId|커맨드가 요청한 대화방의 ID|
|channelName|커맨드를 요청한 대화방의 이름|
|userId|커맨드를 요청한 사용자 ID|
|userName|커맨드를 요청한 사용자 이름|
|command|요청한 커맨드|
|text|커맨드와 함께 입력한 텍스트|
|responseUrl|커맨드 요청에 응답할 수 있는 웹 훅 URL|
|appToken|등록한 앱의 토큰. 정상 요청인지 검증할 때 사용|
|triggerId|다이얼로그에 사용하는 값|

### 응답

커맨드 서버는 전달받은 데이터를 이용해 사용자에게 응답할 데이터를 만듭니다. 그리고 이 데이터를 요청에 대한 응답으로 보내야 합니다. /hi 커맨드는 특별한 데이터 처리 없이 Hello World만 보내주면 됩니다.

```json
{
    "text": "Hello World!",
    "responseType": "ephemeral" // 생략 가능
}
```
위와 같이 응답하면 커맨드를 호출한 사용자에게만 보이는 메시지가 됩니다.

만약 대화방 내의 멤버들에게 모두 보여주고 싶은 경우 responseType을 "inChannel"로 응답에 추가하면 됩니다.

```json
{
    "text": "Hello World!",
    "responseType": "inChannel"
}
```
|필드명|설명|
|---|---|
|responseType|메시지 게시 타입을 설정합니다.<br>- inChannel: 전체 사용자에게 표시<br>- ephemeral: Command 호출한 사용자에게만 표시<br>(responseType이 없으면 ephemeral로 처리됩니다.)|
|text|메시지 내용|

---

## 메시지를 전송하는 4가지 방법(최초 전송/추가 전송/업데이트/기존 메시지 삭제 후 전송)

커맨드 실행 시, 메신저 서버는 4가지의 방식으로 메시지를 전송할 수 있습니다.

최초로 메시지를 전송
메시지를 보낸 후 추가로 전송
기존에 보낸 메시지를 업데이트
기존에 보낸 메시지를 삭제하고 메시지를 새로 전송

1. 메시지를 최초 전송

메시지를 새로 보내는 방법은 간단합니다.

```json
{
    "responseType": "inChannel",
    "text": "Hello World!"
}
```

2. 메시지를 추가로 전송

replaceOriginal 을 false 로 하면 메시지를 새로 전송합니다.

```json
{
    "replaceOriginal": false,
    "responseType": "inChannel",
    "text": "Hello World!"
}
```

3. 기존에 보낸 메시지를 업데이트

replaceOriginal을 true로 하면 기존에 보낸 메시지의 위치에 그대로 내용만 변경되며, 알림도 오지 않습니다.
기존 메시지의 responseType과 다르게 업데이트 할 수 없습니다. responseType을 바꾸기 위해선 메시지를 새로 전송해야 합니다.

```json
{
    "responseType": "inChannel",
    "replaceOriginal": true,
    "text": "Hello World!(Updated)"
}
```

4. 기존에 보낸 메시지를 삭제하고 메시지를 새로 전송

이 경우에는 대화방의 참여자에게 알림이 가기 때문에 대화방의 사람들이 변경되는 내용을 알게 하고 싶을 때 효과적입니다.

deleteOriginal을 true로 하면 기존 메시지가 삭제되고 다시 전송됩니다.

{
    "responseType": "inChannel",
    "deleteOriginal": true,
    "text": "Hello World!(Updated)"
}

필요한 기능에 맞는 메시지 전송 방법을 선택하여 커맨드를 제작하시기 바랍니다.

---

## 메시지에 버튼 넣기

응답 메시지는 attachments 필드를 이용해 버튼을 표시할 수 있습니다. 메시지를 받은 사람은 버튼을 눌러 상호작용을 할 수 있습니다. 버튼을 넣는 방법과 버튼을 선택한 결과를 받아 처리하는 방법을 알아보겠습니다.

아래는 입력한 메시지를 대화방에 전송할지 확인하는 attachments가 포함된 메시지입니다.

```json
{
    "text": "Message",
    "attachments": [
        {
            "callbackId": "send-a1b2c3", // 사용자 interaction시 함께 전송됩니다. interaction이 일어난 Attachment를 식별할 때 쓸 수 있습니다.
            "actions": [
                {
                    "name": "send",
                    "type": "button",
                    "text": "Send", // 사용자에게 출력되는 버튼 텍스트
                    "value": "posting", // Action 동작에 사용하는 (사용자에게 보이지 않는) 값
                    "style": "primary" // 버튼의 스타일을 바꿀 수 있습니다. primary, danger, default
                },
                {
                    "name": "send",
                    "type": "button",
                    "text": "Cancel",
                    "value": "cancel"
                }
            ]
        }
    ]
}
```

해당 메시지를 받으면, 아래와 같이 Send와 Cancel 버튼이 있는 메시지가 생성된 것을 확인할 수 있습니다.
attachment 메시지에 버튼 넣기.png

Send버튼을 눌러봅시다. 아래와 같은 데이터가 커맨드 서버의 Interactive Request URL로 전송됩니다.

```json
{
    // 테넌트, 채널, 멤버 정보가 제공됩니다.
    "tenant": {
        "id": "1234567891234567891",
        "domain": "guide.dooray.com"
    },
    "channel": {
        "id": "1234567891234567891",
        "name" "커맨드 가이드 채널"
    },
    "user": {
        "id": "1234567891234567891",
        "name": "홍길동"
    },
    "commandName": "/post",
    "command": "/post",
    "text": "",
    "callbackId": "send-a1b2c3", // 사용자가 선택한 Action이 속해있는 Attachment의 callbackId입니다.
    "actionText": "Send", // actionText - 사용자가 선택한 Action의 Text입니다.
    "actionValue": "posting", // actionValue - 사용자가 선택한 Action의 Value입니다.
    "appToken": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "cmdToken": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "triggerId": "",
    "commandRequestUrl": "https://command.example.com/req",
    "channelLogId": "-7386965175150134411",
    "originalMessage": { /* action이 발생한 메시지가 포함됩니다. */ }
    }
}
```

사용자가 버튼을 눌렀을 때의 처리는 커맨드 서버에서 구현해야 합니다.

---

## 메시지에 드롭다운 메뉴 넣기

attachments 메시지 안에는 드롭다운 메뉴를 넣을 수 있습니다.
드롭다운 메뉴로 채널 목록, 테넌트의 멤버 목록, 또는 임의의 목록에서 하나를 선택할 수 있습니다.

아래 예시에서는 팀원들이 가장 좋아하는 보드 게임을 뽑아서 함께 플레이하려고 합니다.
아래의 메시지처럼 보드 게임 목록이 있는 드롭다운 메뉴를 활용하여 투표를 받아봅시다.

### 정적 드롭다운 메뉴

options 필드를 이용해 목록을 구성할 수 있습니다.

```json
"attachments": [
   {
       "name": "games_list",
       "text": "Pick a game...",
       "type": "select",
       "options": [
           {
               "text": "rock-scissors-paper",
               "value": "rcp"
           },
           {
               "text": "monopoly",
               "value": "monopoly"
           },
           {
               "text": "Checkers",
               "value": "checkers"
           },
           {
               "text": "Chess",
               "value": "chess"
           },
           {
               "text": "Poker",
               "value": "poker"
           },
           {
               "text": "scrabble",
               "value": "scrabble"
           }
       ]
   }
]
```

위 Attachments를 통해 아래 화면과 같은 드롭다운 메뉴를 보여줄 수 있습니다.

Inline-image-2018-04-26 17.54.06.114.png

### 동적 드롭다운 메뉴

동적 드롭다운 메뉴는 options 대신 dataSource를 이용합니다. dataSource 값에 따라 멤버, 대화방, 외부 데이터를 보여줄 수 있습니다.

|구분|설명|
|---|---|
|dataSource|목록|
|users|멤버|
|channels|대화방|
|external|외부 데이터|

#### 멤버 목록
dataSource에 'users'로 메시지를 구성해 전송하면 현재 대화방의 멤버 목록을 보여줄 수 있습니다. 사용자가 드롭다운 메뉴에 검색어를 입력해 테넌트 전체 멤버를 검색 할 수 있습니다.

```
"attachments": [
    {
        "type": "select",
        "name": "sel_users",
        "text": "사용자 출력",
        "dataSource": "users"
    }
]
```

Inline-image-2018-04-26 18.11.07.988.png

#### 대화방 목록
dataSource에 'channels'로 메시지를 구성해 전송하면 사용자가 속한 대화방 목록을 보여줄 수 있습니다.

```json
"attachments": [
    {
        "type": "select",
        "name": "sel_channels",
        "text": "대화방 출력",
        "dataSource": "channels"
    }
]

Inline-image-2018-04-26 18.17.43.842.png

외부 데이터 목록
dataSource에 'external'로 메시지를 구성해 전송하면 외부 데이터 목록을 보여줄 수 있습니다. 외부 데이터 목록은 앱 설정시 등록한 Interactive Optional URL로 데이터를 요청해 받아옵니다.

"attachments": [
    {
        "type": "select",
        "name": "sel_external",
        "text": "외부 데이터",
        "dataSource": "external"
    }
]
```

클라이언트는 Interactive Optional URL로 아래 메시지와 함께 외부 데이터 목록을 요청합니다.

```json
{
    "type": "interactive_message",
    "tenant": {
        "id": "1234567891234567891",
        "domain": "guide.dooray.com"
    },
    "channel": {
        "id": "1234567891234567891",
        "name": "Command 가이드 채널"
    },
    "user": {
        "id": "1234567891234567891",
        "name": "홍길동"
    },
    "callbackId": "sample",
    "actionName": "sel_externel",
    "actionTs": 1524734546105
}
```

커맨드 서버에서 위 메시지를 이용해 드롭다운 메뉴의 목록을 응답해 줍니다.

```json
{
    "options": [
        {
            "text": "external",
            "value": "value1"
        },
        {
            "text": "load",
            "value": "value2"
        },
        {
            "text": "success",
            "value": "value3"
        }
    ]
}
```

Inline-image-2018-04-26 18.33.43.080.png


