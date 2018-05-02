## 개요
### 연동서비스

Dooray! 메신저에서는 사람이 아닌 다양한 도구에게 명령하고 메시지를 받으면서 더 효율적으로 업무를 할 수 있습니다.
메신저에서 제공하지 않는 기능을 직접 구현하고 싶을 때 이 기능을 활용하여 여러분도 자신의 업무를 좀 더 효율적으로 자동화 할 수 있습니다.
![1](http://static.toastoven.net/prod_dooray_messenger/integration/1.png)

현재 소개할 기능은 커맨드를 직접 생성하는 것에 대한 내용이며, 앞으로 Bot, API 등 다양한 연동서비스를 제공할 예정입니다.

### 커맨드

커맨드는 ‘/’문자 뒤에 덧붙여서 특정한 기능을 수행하도록 하는 명령어입니다.
Dooray! 메신저에서는 기본적으로 ‘/mute’, ‘/status’, ‘/search’ 등의 System 커맨드를 제공합니다.
예컨대 메시지 내용을 찾거나, 자신의 상태를 바꾸는 등의 기능을 마우스의 클릭이나 다른 조작 없이 텍스트 입력으로 빠르게 실행할 수 있도록 도와줍니다.

![2](http://static.toastoven.net/prod_dooray_messenger/integration/2.png)

자신이 원하는 기능을 수행하는 커맨드를 직접 만들어 사용할 수 있습니다.
예를 들어 매일 아침 교통 정보와 날씨를 메시지로 받아볼 수 있고, 간단한 명령어를 입력하여 투표를 생성할 수도 있습니다.

아래 그림은 커맨드 서버와 메신저 서버 간의 통신 과정입니다.

![3](http://static.toastoven.net/prod_dooray_messenger/integration/3.png)

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

![4](http://static.toastoven.net/prod_dooray_messenger/integration/4.png)

지금은 아래와 같이 빈 화면이 표시됩니다.

![5](http://static.toastoven.net/prod_dooray_messenger/integration/5.png)

### 앱 추가

우선 앱을 만들어야 합니다. 앱은 연동서비스의 묶음 단위입니다.
하나의 앱에 여러 개의 커맨드를 추가할 수 있습니다. 아래의 정보를 입력하여 앱을 만들어 봅니다.
각 정보는 대화방에 공개된 커맨드를 등록할 때 목록에 노출됩니다.
![6](http://static.toastoven.net/prod_dooray_messenger/integration/6.png)

|구분|설명|
|---|---|
|Image|대화방에서 커맨드를 사용할 때 메시지의 전송자 아이콘으로 표시됩니다.|
|Name|대화방에서 커맨드를 사용할 때 메시지의 전송자 이름으로 표시됩니다.|
|Description|앱의 설명입니다.|

이제 앱이 만들어졌습니다. 생성되어 있는 Token과 비어 있는 커맨드 목록을 보실 수 있습니다.
Token 값은 커맨드 요청시 함께 전송되어 요청을 검증하는데에 사용합니다. Token 값이 외부에 유출되지 않도록 주의하시기 바랍니다. 만약 Token에 외부에 유출된 경우에는 Regenerate 버튼을 이용해 기존 Token을 파기하고 다시 발급해 사용하세요.

![7](http://static.toastoven.net/prod_dooray_messenger/integration/7.png)

### 커맨드 추가

앱을 등록 한 후, Slash Command 영역의 '추가' 버튼을 누르면 커맨드를 추가할 수 있습니다.
되도록 하나의 앱에는 서로 밀접하게 관계가 있는 커맨드를 추가하는 것을 권장합니다.

미리 제작한 커맨드가 없다면, 다음 문서에서 예제로 설명할 /hi 커맨드를 입력하면 됩니다.

![8](http://static.toastoven.net/prod_dooray_messenger/integration/8.png)

|구분|설명|
|---|---|
|Command|‘/’를 포함하여 대화방에서 입력할 명령어를 입력합니다.<br>명령어는 커맨드의 기능을 나타내는 직관적인 것이 좋습니다.|
|Request URL|커맨드를 실행 시 요청할 커맨드 서버 URL을 입력합니다.|
|Description|커맨드 사용할 때 표시될 설명입니다. 다른 사람이 커맨드의 기능을 쉽게 이해할 수 있도록 적어주세요.|
|Parameter Hint|커맨드와 함께 어떤 parameter를 적어야 하는지 설명해 주세요.<br>(지역,시간,사람,날짜, 텍스트, 숫자 등의 정보를 입력할 수 있습니다.)|
|Public|해당 커맨드를 다른 사람들도 대화방에 추가하여 사용할 수 있습니다.|

커맨드가 추가되었습니다.

![9](http://static.toastoven.net/prod_dooray_messenger/integration/9.png)

### Interactive Request URL 입력

버튼과 드롭 메뉴를 통해 사용자의 Action을 받으려면 Interactive Message 처리를 위한 별도의 URL이 필요합니다.

![10](http://static.toastoven.net/prod_dooray_messenger/integration/10.png)

|구분|설명|
|---|---|
|Interactive Message Request URL|버튼과 드롭 메뉴 등 메시지를 통해서 유저와 상호작용하는 경우, 유저의 요청을 전달할 URL을 입력합니다.|
|Interactive Message Optional URL|메시지에 dataSource를 external로 설정한 메뉴 목록 등을 제공하는 경우, 메뉴 목록을 요청할 URL을 입력합니다.|

---

## Hello World! 메시지 보내기
대화방에서 "/hi"라고 입력하면, "Hello world!"라고 대답하는 아주 간단한 커맨드를 만들어 보겠습니다.

### 커맨드 실행

사용자가 Dooray! 메신저를 통해 /hi 커맨드를 실행하면 커맨드 서버는 아래와 같은 JSON 데이터를 전달받습니다.

```javascript
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

```javascript
{
    "text": "Hello World!",
    "responseType": "ephemeral" // 생략 가능
}
```
위와 같이 응답하면 커맨드를 호출한 사용자에게만 보이는 메시지가 됩니다.

만약 대화방 내의 멤버들에게 모두 보여주고 싶은 경우 responseType을 "inChannel"로 응답에 추가하면 됩니다.

```javascript
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

```javascript
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

```javascript
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

![11](http://static.toastoven.net/prod_dooray_messenger/integration/11.png)

Send버튼을 눌러봅시다. 아래와 같은 데이터가 커맨드 서버의 Interactive Request URL로 전송됩니다.

```javascript
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

```javascript
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

![12](http://static.toastoven.net/prod_dooray_messenger/integration/12.png)

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

```javascript
"attachments": [
    {
        "type": "select",
        "name": "sel_users",
        "text": "사용자 출력",
        "dataSource": "users"
    }
]
```

![13](http://static.toastoven.net/prod_dooray_messenger/integration/13.png)

#### 대화방 목록
dataSource에 'channels'로 메시지를 구성해 전송하면 사용자가 속한 대화방 목록을 보여줄 수 있습니다.

```javascript
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

```javascript
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

```javascript
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

![14](http://static.toastoven.net/prod_dooray_messenger/integration/14.png)

---

## attachments 메시지 보내기

커맨드는 attachments라는 특별한 형태의 메시지를 전송할 수 있습니다. attachments의 구성 요소에는 다른 문서에서 설명하였던 버튼과 드롭다운메뉴 외에도 다양한 것이 있습니다. attachments 메시지를 잘 사용하면 사용자의 눈에 잘 띌뿐 아니라 추가 정보를 요청하거나 회신하는 등의 행동을 능숙하게 유도할 수 있습니다.

Dooray! Messenger는 Slack과 유사한 형태의 데이터 타입과 Attachments UI를 제공합니다.
기존에 Slack integration을 제작한 경험이 있다면 익숙하게 작업할 수 있습니다.

### attachments 메시지

아래의 보시는 메시지의 블록 하나 하나가 타이틀, 설명, 이미지, 링크, 버튼, 드롭 메뉴 등을 가질 수 있는 attachment입니다. 최대 20개의 attachment 블록이 모여 attachments 메시지를 구성합니다.

![15](http://static.toastoven.net/prod_dooray_messenger/integration/15.png)

|번호|이름|설명|
|---|---|---|
|1|text|메시지의 내용입니다.|
|2|attachment|메시지에 첨부한 내용입니다. 여러 개의 attachment를 합쳐서 attachments라고 부릅니다.|
|3|authorName|작성자 이름입니다. authorLink로 링크를 걸 수 있습니다.|
|4|title|attachment의 제목입니다.|
|5|text|attachment의 내용입니다.|
|6|thumbUrl|attachment에 넣을 섬네일 이미지입니다.|
|7|imageUrl|attachment에 넣을 이미지 URL입니다.|
|8|field|short의 값에 따라 한 줄에 하나 또는 두 개씩 표시되는 필드입니다.|
|10|Interactive Menu|드롭다운 메뉴입니다.|
|11|Interactive Button|버튼입니다.

### 데이터

데이터의 포맷은 아래와 같습니다.

```javascript
{
    "text": "NHN IT News!",
    "attachments": [
        {
            "callbackId": "guide-a1b2c3",
            "text": "애플은 오늘 오전 2시에 WWDC를 통해 아이폰X 출시를 알렸다.",
            "title": "아이폰 X 출시",
            "titleLink": "https://dooray.com/",
            "authorName": "NHN News",
            "authorLink": "https://dooray.com/",
            "imageUrl": "http://it.chosun.com/data/photos/cdn/20180423/2850453_09555838720000.jpg",
            "thumbUrl": "http://www.kinews.net/news/photo/201804/119143_167793_5622.png",
        },
        {
            "fields": [
                {
                    "title": "출시 예정일",
                    "value": "2018년 겨울",
                    "short": true
                },
                {
                    "title": "예상 가격",
                    "value": "125만원",
                    "short": true
                }
            ]
        },
        {
            "fields": [
                {
                    "title": "설명",
                    "value": "한국 미출시",
                }
            ]
        },
        {
            "fields": [
                {
                    "title": "IOS",
                    "value": "High Sierra OS",
                }
            ]
        },
        {
            "actions": [
                {
                    "type": "select",
                    "text": "채널선택",
                    "name": "guide-sel",
                    "dataSource": "channels"
                }
            ]
        },
        {
            "actions": [
                {
                    "type": "button",
                    "text": "공유하기",
                    "name": "guide-btn",
                    "value": "btnValue"
                },
                {
                    "type": "button",
                    "text": "다음 뉴스",
                    "name": "guide-btn",
                    "value": "btnValue"
                },
            ]
        }
    ]
}
```

### 구성 요소 분석

데이터의 구성 요소를 좀 더 자세히 살펴 보겠습니다.

#### Message Object
|필드명|기본값|설명|
|---|---|---|
|text||메시지 텍스트|
|attachments||Attachment의 배열|
|responseType|"ephemeral"|메시지 표시 대상<br>"ephemeral": Command를 실행한 사용자에게만 표시<br>"inChannel": 채널 내 전체 사용자에게 표시
|replaceOriginal|true|Interactive Message에 대한 응답 시 기존 메시지 수정 여부|
|deleteOriginal|false|Interactive Message에 대한 응답 시 기존 메시지 삭제 여부|

#### Attachment Object
|필드명|기본값|설명|
|---|---|---|
|text||Attachment 텍스트|
|title||Attachment 제목|
|titleLink||Attachment 제목 클릭 시 이동할 링크|
|authorName||Attachment 작성자|
|authorLink||Attachment 작성자 클릭 시 이동할 링크|
|fields||Field의 배열|
|actions||Action의 배열|
|callbackId||Action 요소 작동 시 함께 전달될 값(세션 유지 등의 용도로 사용)|
|imageUrl||이미지 주소|
|thumbUrl||섬네일 주소|
|color|"#4757C4"|Attachment 세로줄 색상(HTML 색상코드)|

#### Field Object
|필드명|기본값|설명|
|---|---|---|
|title||Field 제목|
|value||Field 텍스트|
|short|false|Field 너비 설정(true로 설정 시 절반 너비)|

#### Action Object
|필드명|기본값|설명|
|---|---|---|
|type||Actiontype<br>"button": 버튼<br>"select": 드롭 메뉴|
|text||버튼, 드롭 메뉴에 표시될 텍스트|
|name||커맨드 서버에 전달되는 필드명|
|value||커맨드 서버에 전달되는 필드값|
|style|"default"|버튼 색상<br>"primary": 강조 색상<br>"default": 기본 색상|
|options||Option의 배열|
|dataSource||options 대신 지정할 수 있는 option 값<br>"users": 사용자 목록<br>"channels": 채널 목록<br>"external": Interactive Message Optional URL에서 가져오기

#### Option Object
|필드명|기본값|설명|
|---|---|---|
|text||Option 텍스트|
|value||커맨드 서버에 전달되는 필드값|

---

## 대화방에 커맨드 등록하기

### 대화방에 커맨드를 등록

커맨드는 자신이 참여하고 있는 1:1대화, 그룹 대화 등에 등록하여 활용할 수 있습니다.
커맨드 추가 화면을 여는 방법은 두 가지가 있습니다.

첫째, 메신저 우측 상단의 설정 메뉴를 통해 추가할 수 있습니다.

![16](http://static.toastoven.net/prod_dooray_messenger/integration/16.png)

둘째, 대화방의 입력창에 '/'를 입력 후 나타나는 화면에서 '연동서비스' 버튼을 통해 추가할 수 있습니다.

![17](http://static.toastoven.net/prod_dooray_messenger/integration/17.png)

커맨드 추가 화면에는 공개된 커맨드나 자신이 생성한 커맨드가 표시됩니다. 원하는 커맨드의 추가 버튼을 눌러 대화방에 커맨드를 추가하세요. 만약 커맨드가 없다면 본 문서의 처음으로 돌아가 커맨드를 만들어 보세요.

![18](http://static.toastoven.net/prod_dooray_messenger/integration/18.png)

![19](http://static.toastoven.net/prod_dooray_messenger/integration/19.png)

### 커맨드 공개

만약 자신이 만든 커맨드의 멋진 기능을 조직 내의 다른 사람들과 공유하고 싶다면 공개로 설정해 주세요.
조직 내의 다른 사람들도 자유롭게 대화방에 추가하여 사용할 수 있습니다.

비공개로 변경해도 이미 추가한 커맨드는 다른 사람이 계속 사용할 수 있으니, 다른 사람들이 더 이상 커맨드를 사용하지 못하게 하려면 등록한 커맨드를 삭제해 주세요.

---

## 투표 커맨드 

### 커맨드 서버 요구사항

커맨드 서버는 등록한 커맨드대로 동작하는 REST API를 제공해야 합니다.

| API 종류 | 설명 | 필수 | 메소드 |
| ------ | --- | :---: | :---: |
| 커맨드 Request URL | 사용자의 커맨드 실행 요청을 처리할 URL | O | POST |
| Interactive Message의 Request URL | 사용자의 액션(버튼 클릭, 드롭 메뉴 선택)을 처리할 URL | X | POST |
| Interactive Message의Optional URL | 드롭 메뉴에서 외부 데이터 제공할 URL | X | POST |

### 투표 커맨드

예제로 대화방에 투표를 만들고 참여할 수 있는 투표 커맨드를 만들겠습니다.

![20](http://static.toastoven.net/prod_dooray_messenger/integration/20.png)

#### API

커맨드 Request URL과 Interactive Message의 Request URL만 사용합니다.

#### 커맨드 실행 포맷

사용자가 투표 커맨드를 실행 할 입력 포맷은 아래처럼 입력하도록 합니다.

```
/vote "{제목}" "{항목1}" "{항목2}" [... "{항목n}"]

```

#### 시나리오

1. 사용자가 커맨드 실행
2. 커맨드를 실행한 사용자에게만 보이는 투표 생성 확인 메시지 출력
3. 생성 버튼을 눌러서 대화방 멤버에게 모두 보이는 투표 메시지 출력
4. 대화방 멤버들이 투표 버튼으로 투표 참여
5. 투표를 생성한 사용자가 투표 종료
6. 투표 결과 출력

### 투표 커맨드 실행 요청

사용자가 투표 커맨드를 아래와 같이 실행합니다.

![21](http://static.toastoven.net/prod_dooray_messenger/integration/21.png)

커맨드 서버는 커맨드 Request URL로 사용자가 입력한 값을 포함한 JSON 데이터를 받게 됩니다.

``` javascript
{
    "tenantId": "1234567891234567891",
    "tenantDomain": "guide.dooray.com",
    "channelId": "1234567891234567891",
    "channelName": "Command 가이드",
    "userId": "1234567891234567891",
    "userName": "홍길동",
    "command": "/vote",
    "text": "\"점심식사\" \"짜장면\" \"짬뽕\" \"탕수육\"",
    "responseUrl": "https://guide.dooray.com/messenger/api/commands/hook/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "appToken": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "triggerId": "1234567891234.xxxxxxxxxxxxxxxxxxxx"
}

```

| 필드 명 | 설명 |
| ---- | --- |
| tenantId | 커맨드가 등록된 테넌트의 ID |
| tenantDomain | 커맨드가 등록된 테넌트 도메인 |
| channelId | 커맨드를 요청한 대화방의 ID |
| channelName | 커맨드를 요청한 대화방 제목 |
| userId | 커맨드를 요청한 사용자 ID |
| userName | 커맨드를 요청한 사용자 이름 |
| command | 커맨드 이름 |
| text | 사용자가 입력한 전체 텍스트 |
| responseUrl | 커맨드를 요청한 대화방의 Webhook URL |
| appToken | 커맨드를 등록한 앱의 토큰(요청 검증으로 활용) |
| triggerId | 다이얼로그 실행 ID |

### 커맨드 실행 요청에 대한 응답

![22](http://static.toastoven.net/prod_dooray_messenger/integration/22.png)

커맨드 실행 요청에 대한 응답으로 실행 사용자에게만 보이는 확인 메시지를 보냅니다.
투표를 생성하거나 취소할 수 있는 버튼을 사용자에게 제공하기 위해 아래와 같이 메시지를 전송합니다.

``` javascript
{
    "responseType": "ephemeral", // 생략 가능
    "text": "Click 'Submit' button to start the vote.",
    "attachments": [
        {
            "title": "점심식사",
            "fields": [
                {
                    "title": "Item 1",
                    "value": "짜장면",
                    "short": true
                },
                {
                    "title": "Item 2",
                    "value": "짬뽕",
                    "short": true
                },
                {
                    "title": "Item 3",
                    "value": "탕수육",
                    "short": true
                }
            ]
        },
        {
            "callbackId": "vote",
            "actions": [
                {
                    "name": "vote",
                    "type": "button",
                    "text": "Submit",
                    "value": "\"점심식사\" \"짜장면\" \"짬뽕\" \"탕수육\"",
                    "style": "primary"
                },
                {
                    "name": "vote",
                    "type": "button",
                    "text": "Cancel",
                    "value": "cancel"
                }
            ]
        }
    ]
}

```

### 액션 실행 요청

사용자가 Submit 버튼을 누르면 아래와 같은 데이터가 Interactive Message의 Request URL로 전송됩니다.

``` javascript
{
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
    "commandName": "/vote",
    "command": "/vote",
    "text": "\"점심식사\" \"짜장면\" \"짬뽕\" \"탕수육\"",
    "callbackId": "vote",
    "actionText": "Submit",
    "actionValue": "\"점심식사\" \"짜장면\" \"짬뽕\" \"탕수육\"",
    "appToken": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "cmdToken": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "triggerId": "1234567891234.xxxxxxxxxxxxxxxxxxxx",
    "commandRequestUrl": "https://command.guide.doc/req",
    "channelLogId": "-7386965175150134411",
    "originalMessage": { /* Message Object */ }
}
```

| 필드 명 | 설명 |
| ---- | --- |
| callbackId | 사용자가 선택한 액션이 속해있는 Attachment의 ID |
| actionText | 사용자가 선택한 액션 텍스트 |
| actionValue | 사용자가 선택한 액션 값 |
| commandRequestUrl | 커맨드 Request URL |
| channelLogId | 메시지 ID |
| originalMessage | 이전 응답으로 받은 메시지 |

### 액션 실행에 대한 응답

![23](http://static.toastoven.net/prod_dooray_messenger/integration/23.png)

Submit 버튼에 대한 응답으로 투표 생성 메시지를 전송합니다.
생성 확인 메시지는 더 이상 필요가 없기 때문에 삭제하고 메시지를 새로 생성합니다.

``` javascript
{
    "responseType": "inChannel", // 대화방 멤버 모두에게 표시
    "deleteOriginal": true, // true로 설정 시 기존 메시지를 삭제합니다. (기본값: false)
    // "inChannel", "ephemeral" 메시지 간의 전환은 "deleteOriginal"이 true일 때만 가능합니다.
    // replaceOriginal - true로 설정 시 기존 메시지를 업데이트 하고, false로 설정 시 새로운 메시지를 생성합니다. (기본값: true)
    // 새로운 메시지를 생성한 경우에만 푸시/노티가 발생합니다.
    "text": "[@홍길동](dooray://1234567891234567891/members/1234567891234567891 \"member\") created the vote!",
    "attachments": [
        {
            "callbackId": "1525223162093-[@홍길동](dooray://1234567891234567891/members/1234567891234567891 \"member\")",
            "title": "점심식사",
            "actions": [
                {
                    "name": "vote",
                    "type": "button",
                    "text": "짜장면",
                    "value": 0
                },
                {
                    "name": "vote",
                    "type": "button",
                    "text": "짬뽕",
                    "value": 1
                },
                {
                    "name": "vote",
                    "type": "button",
                    "text": "탕수육",
                    "value": 2
                }
            ],
            "color": "#4286f4"
        },
        {
            "callbackId": "1525223162093-[@홍길동](dooray://1234567891234567891/members/1234567891234567891 \"member\")",
            "text": "",
            "actions": [
                {
                    "name": "vote",
                    "type": "button",
                    "text": "Close the vote (Show result)",
                    "value": "end"
                }
            ]
        }
    ]
}
```

| 필드 명 | 설명 | 기본값 |
| ---- | --- | --- |
| deleteOriginal | 새  메시지를 생성하기 전 기존 메시지 삭제 여부 | false |
| replaceOriginal | 기존 메시지 업데이트 여부 | true |

사용자에게 보여지는 텍스트에 멘션 뱃지를 표현할 수 있습니다. 멘션 뱃지는 아래와 같이 사용하면 됩니다.

```javascript
[@{사용자이름}](dooray://{테넌트ID}/members/{사용자ID} "member")
```

이 후 사용자가 누르는 버튼은 액션 실행 요청과 그에 따른 응답의 반복입니다.
