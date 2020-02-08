## Dooray! > Messenger > スラッシュコマンドガイド
### 連動サービス

Doorayメッセンジャーでは、人とのコミュニケーション以外にも、さまざまなツールへ向けてコマンドを作成し、メッセージを受信しながら、より効率的に業務を行うことができます。メッセンジャーで提供していない機能を直接実装したいときは、この機能を使って自分の仕事をさらに効率的に自動化することができます。ここで紹介する機能は、直接作成できるコマンドとその説明です。今後、ボット(BOT)はAPIなど、さまざまな連動サービスを提供する予定です。

### スラッシュコマンド

スラッシュコマンド(以降コマンド)は、メッセージ入力欄に/(スラッシュ)をつけて特定の機能を実行させるコマンドです。Doorayメッセンジャーでは、基本的に/mute、/status、/searchなどのコマンドを提供しています。例えば、メッセージの内容を検索したり、自分のステータスを変更したりするなどの機能を、マウスのクリックや他の操作をすることなく、キーボード入力だけで実行できるようにサポートします。

![2](http://static.toastoven.net/prod_dooray_messenger/integration/2.png)

自分が望む機能を実行するコマンドを直接入力して使用することができます。例えば、毎朝の交通情報や天気予報をメッセージとして受け取ったり、簡単なコマンドを入力して投票を作成したりすることもできます。
下図は、コマンドサーバーとメッセンジャーサーバー間の通信プロセスです。

![3](http://static.toastoven.net/prod_dooray_messenger/integration/3.png)

ユーザーは/(スラッシュ)とチャットルームに登録されているコマンドを入力します。入力したコマンド情報は、メッセンジャーサーバーを通じてコマンドサーバーに送信され、コマンドサーバーで処理した結果をメッセンジャーサーバーに送信します。メッセンジャーサーバーは、コマンドサーバーから受信したデータに基づいて、ユーザーに結果を表示します。

### 使用環境

ユーザーは、PCとモバイルでコマンドを入力して結果を確認することができます。そのため、コマンドの作成者は、モバイル環境でのレイアウトにも気を配る必要があります。現在、チャットルームにコマンドを追加する機能は、PC上でのみ提供しています。

### 作成ガイド

コマンドの作成と登録方法について、ご案内します。

---

## コマンドの追加

自作コマンドを使用するにはDoorayメッセンジャーに追加する必要があります。

### 追加画面に移動

Doorayメッセンジャー左上の自分の名前を選択し「スラッシュコマンド連動」メニューを選択します。

![4](http://static.toastoven.net/prod_dooray_messenger/integration/4_2.png)

下記のように空白の画面が表示されます。

![5](http://static.toastoven.net/prod_dooray_messenger/integration/5.png)

### アプリ追加

まずアプリを作成します。アプリは連動サービスをひとまとめにしたユニットです。1つのアプリに複数のコマンドを追加することができます。下記の情報を入力してアプリを作成します。各情報は、チャットルームに公開されたコマンドを登録する際、リストに表示されます。

![6](http://static.toastoven.net/prod_dooray_messenger/integration/6.png)

|区分|説明|
|---|---|
|Image|チャットルームでコマンドを使用すると、メッセージ送信者のアイコンに表示されます。|
|Name|チャットルームでコマンドを使用すると、メッセージ送信者の名前に表示されます。|
|Description|アプリの説明|

アプリが作成されると、作成されたトークンと空のコマンドリストが確認できます。トークンは、コマンド発行時に送信され、リクエストを検証するために使用します。トークンが外部に流出しないように注意しましょう。トークンが外部に流出してしまった場合は、「Regenerate」ボタンから既存のトークンを破棄し、再発行してご使用ください。

![7](http://static.toastoven.net/prod_dooray_messenger/integration/7.png)

### コマンド追加

アプリ登録後、スラッシュコマンド領域の「追加」ボタンを押すと、コマンドを追加することができます。なるべく1つのアプリには、相互に密接に関係するコマンドを追加することをお勧めします。事前に作成したコマンドがない場合は、下のサンプルのように  /hiコマンドを追加してみましょう。

![8](http://static.toastoven.net/prod_dooray_messenger/integration/8.png)

|区分|説明|
|---|---|
|Command|`/`を含むチャットルームで入力するコマンドを入力します。コマンドは、コマンドの機能を表す直感的なものがよいでしょう。|
|Request URL|コマンド実行時にリクエストするコマンドサーバーのURLを入力します。|
|Description|コマンドを使用するときに表示される説明です。<br> 他のユーザーがコマンドの機能を簡単に理解できるように記入しましょう。|
|Parameter Hint|コマンドとともに、どのようなパラメータを記載する必要があるか説明してください。<br>(地域、時間、人物、日付、テキスト、数字などの情報を入力できます。)|
|Public|このコマンドを他のユーザーもチャットルームに追加して使用することができます。|

コマンドが追加されました。

![9](http://static.toastoven.net/prod_dooray_messenger/integration/9.png)

### Interactive Request URLを入力

ボタンとドロップダウンメニューを通じてユーザーのアクションを受け取るには対話的メッセージ(Interactive Message)処理のため、別途URLが必要です。

![10](http://static.toastoven.net/prod_dooray_messenger/integration/10.png)

|区分|説明|
|---|---|
|Interactive Message Request URL|ボタンとドロップダウンメニューなどのメッセージを通じてユーザーと対話する場合、ユーザーのリクエストを伝えるURLを入力します。|
|Interactive Message Optional URL|メッセージにdataSourceをexternalで設定したメニューリストなどを提供する場合、メニューリストをリクエストするURLを入力します。|

---

## 「Hello World!」メッセージを送る

チャットルームで `/hi`と入力すると、「Hello World!」と答える、ごく簡単なコマンドを作成してみましょう。

### コマンド実行

ユーザーがDoorayメッセンジャーから/hiコマンドを実行すると、コマンドサーバーは、下記のようなJSONデータを受け取ります。

```javascript
{
    "tenantId": "1234567891234567891",
    "tenantDomain": "guide.dooray.com",
    "channelId": "1234567891234567891",
    "channelName": "커맨드 가이드 채널",
    "userId": "1234567891234567891",
    "command": "/hi",
    "text": ""
    "responseUrl": "https://guide.dooray.com/messenger/api/commands/hook/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "appToken": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "triggerId": "1234567891234.xxxxxxxxxxxxxxxxxxxx"
}
```

|フィールド名|説明|
|---|---|
|tenantId|コマンドが登録されているテナントID|
|tenantDomain|コマンドが登録されているテナントのドメイン|
|channelId|コマンドを発行したチャットルームID|
|channelName|コマンドを発行したチャットルーム名|
|userId|コマンドを発行したユーザーID|
|command|発行したコマンド|
|text|コマンドとともに入力したテキスト|
|responseUrl|コマンドリクエストに応答するWebフックURL|
|appToken|登録したアプリのトークン、正常なリクエストか検証する際に使用|
|cmdToken|API呼び出し時に使用するトークン|
|triggerId|ダイアログに使用する値|

### 応答

コマンドサーバーは、配信されたデータを利用してユーザーに応答するデータを作成します。そして、このデータをリクエストに対する応答として送信します。 `/hi` コマンドは、特別なデータ処理はなく `Hello World!`のみ送信します。

```javascript
{
    "text": "Hello World!",
    "responseType": "ephemeral"
}
```

上記のように応答すると、コマンドを呼び出したユーザーにのみメッセージが表示されます。チャットルーム内のメンバーにすべて表示させたい場合は、
 `responseType`を `inChannel`で応答に追加します。

```javascript
{
    "text": "Hello World!",
    "responseType": "inChannel"
}
```

|フィールド名|デフォルト|説明|
|---|---|---|
|responseType|ephemeral|メッセージの投稿タイプを設定します。<br>- inChannel: 全ユーザーに表示 <br>- ephemeral:  呼び出したユーザーにのみ表示|
|text||メッセージの内容|

---

## メッセージを送信する4つの方法

コマンド実行時、メッセンジャーサーバーは、4種類の方法でメッセージを送信することができます。

- 最初のメッセージを送信
- メッセージ送信後に追加送信
- 既存の送信メッセージを更新
- 既存の送信メッセージを削除し、新規メッセージを送信

### 最初のメッセージを送信

メッセージを新規に送信する方法は簡単です。

```javascript
{
    "responseType": "inChannel",
    "text": "Hello World!"
}
```

### メッセージの追加送信

`replaceOriginal`を `false`にすると、メッセージを新規に送信します。

```javascript
{
    "replaceOriginal": false,
    "responseType": "inChannel",
    "text": "Hello World!"
}
```

### 既存の送信メッセージを更新

`replaceOriginal`を `true`にすると、既存の送信メッセージの位置で内容だけを変更し、通知も行いません。また、既存のメッセージの `responseType`を切り替えて更新することはできません。`responseType`を切り替えるには、メッセージを新規に送信する必要があります。

```javascript
{
    "responseType": "inChannel",
    "replaceOriginal": true,
    "text": "Hello World!(Updated)"
}
```

### 既存の送信メッセージを削除し、新規メッセージを送信

この場合は、チャットルームの参加者に通知が届くので、参加者に内容が変更されたことを伝えるのに効果的です。
`deleteOriginal`を `true`にすると、既存のメッセージが削除され、再送信されます。

```javascript
{
    "responseType": "inChannel",
    "deleteOriginal": true,
    "text": "Hello World!(Updated)"
}
```

必要に応じてメッセージの送信方法を選択し、コマンドを作成しましょう。

---

## メッセージにボタン挿入

応答メッセージは、 `attachments` フィールドを利用してボタンを表示することができます。メッセージを受信したユーザーは、ボタンを押して双方向コミュニケーションができます。ボタンの挿入方法と、ボタンの選択結果を受信して処理する方法を説明します。
下記は、入力したメッセージをチャットルームに送信するかどうかを確認するattachmentsを含むメッセージです。

```javascript
{
    "text": "Message",
    "attachments": [
        {
            "callbackId": "send-a1b2c3", //ユーザーの双方向コミュニケーション時に送信されます。 双方向コミュニケーションが起きたattachmentを識別するときに使用できます。
            "actions": [
                {
                    "name": "send",
                    "type": "button",
                    "text": "Send", // ユーザーに出力されるボタンテキスト
                    "value": "posting", // アクション動作に使用する(ユーザーに見えない)値
                    "style": "primary" // ボタンのスタイルを変更できます。primary, danger, default
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

そのメッセージを受け取ると、次のような「Send」と「Cancel」ボタンがあるメッセージが作成されます。

![11](http://static.toastoven.net/prod_dooray_messenger/integration/11.png)

「Send」ボタンを押してみましょう。下記のようなデータがコマンドサーバーのInteractive Request URLに転送されます。

```javascript
{
    // テナント、チャンネル、メンバー情報が提供されます。
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
    },
    "commandName": "/post",
    "command": "/post",
    "text": "",
    "callbackId": "send-a1b2c3", // ユーザーが選択したアクションが属するattachmentのコールバックID
    "actionText": "Send", // aactionName - ユーザーが選択したアクション名
    "actionValue": "posting", // actionValue - ユーザーが選択したアクションの値
    "appToken": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "cmdToken": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "triggerId": "",
    "commandRequestUrl": "https://command.example.com/req",
    "channelLogId": "-7386965175150134411",
    "originalMessage": { /* アクションが発生したメッセージが含まれます。*/ }
    }
}
```

ユーザーがボタンを押したときの処理は、コマンドサーバーで実装する必要があります。

---

## メッセージにドロップダウンメニュー挿入

aattachmentsメッセージの中にはドロップダウンメニューを置くことができます。ドロップダウンメニューでチャンネルリスト、テナントのメンバーリスト、または任意のリストから1つを選択することができます。

次のサンプルでは、チームのメンバーが最も好きなボードゲームを選んで一緒にプレイしようとしています。下記メッセージのようなボードゲームのリストを、ドロップダウンメニューを使って投票してみましょう。

### 静的ドロップダウンメニュー

`options` フィールドを利用してリストを構成できます。

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

上記のattachmentsを用いて下図のようなドロップダウンメニューを表示することができます。

![12](http://static.toastoven.net/prod_dooray_messenger/integration/12.png)

### 動的ドロップダウンメニュー

動的ドロップダウンメニューは、`options` の代わりに `dataSource`を使用します。`dataSource`は、値に基づいて、メンバー、チャットルーム、外部データを表示することができます。

|dataSource|リスト|
|---|---|
|users|メンバー|
|channels|チャットルーム|
|external|外部データ|

#### メンバーリスト
`dataSource`に `users`でメッセージを構成して送信すると、現在のチャットルームのメンバーリストを表示することができます。ユーザーがドロップダウンメニューに検索語を入力すると、テナント全体のメンバーを検索できます。

```javascript
"attachments": [
    {
        "type": "select",
        "name": "sel_users",
        "text": "ユーザー出力",
        "dataSource": "users"
    }
]
```

![13](http://static.toastoven.net/prod_dooray_messenger/integration/13.png)

#### チャットルームのリスト
`dataSource`に `channels`でメッセージを構成して送信すると、ユーザーが属しているチャットルームのリストを表示することができます。

```javascript
"attachments": [
    {
        "type": "select",
        "name": "sel_channels",
        "text": "대화방 출력",
        "dataSource": "channels"
    }
]
```

![14](http://static.toastoven.net/prod_dooray_messenger/integration/14.png)

#### 外部データのリスト
`dataSource`に `external`でメッセージを構成して送信すると、外部データのリストを表示することができます。外部データのリストは、アプリ設定時に登録したInteractive Optional URLにデータをリクエストして受信します。

``` javascript
"attachments": [
    {
        "type": "select",
        "name": "sel_external",
        "text": "チャットルーム出力",
        "dataSource": "external"
    }
]
```

クライアントは、Interactive Optional URLで次のメッセージとともに、外部データのリストをリクエストします。

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

コマンドサーバーでは、上記のメッセージを利用して、ドロップダウンメニューのリストを返します。

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

![15](http://static.toastoven.net/prod_dooray_messenger/integration/15.png)

---

## attachmentsメッセージの送信

コマンドは、attachmentsという特別な形式のメッセージを送信することができます。attachmentsのコンポーネントには、先述したボタンとドロップダウンメニューの他にもさまざまなものがあります。attachmentsメッセージをうまく使用すると、ユーザーの目に留まるだけでなく、追加情報をリクエストしたり、返信したりするなどの行動を巧み誘導することができます。

### attachmentsメッセージ

下記メッセージの各ブロックが、タイトル、説明、画像、リンク、ボタン、ドロップダウンメニューなどを持つことができるattachmentです。最大20個のattachmentブロックが集まってattachmentsメッセージを構成します。

![16](http://static.toastoven.net/prod_dooray_messenger/integration/16.png)

|番号|名前|説明|
|---|---|---|
|1|text|メッセージの内容|
|2|attachment|メッセージに添付したもの。複数のattachmentをまとめてattachmentsと呼びます。|
|3|authorName|作成者の名前。authorLinkへのリンクをかけることができます。|
|4|title|attachmentのタイトル|
|5|text|attachmentの内容|
|6|thumbUrl|attachmentに入れるサムネイル画像|
|7|imageUrl|attachmentに入れる画像のURL|
|8|field|shortの値によって1行に1または2つずつ表示されるフィールド|
|10|Interactive Menu|ドロップダウンメニュー|
|11|Interactive Button|ボタン

### データ

データのフォーマットは下記のとおりです。

```javascript
{
    "text": "NHN IT News!",
    "attachments": [
        {
            "callbackId": "guide-a1b2c3",
            "text": "Appleは本日午前2時、WWDCを通じてiPhoneXの発売を公示した。",
            "title": "iPhoneX 発売",
            "titleLink": "https://dooray.com/",
            "authorName": "NHN News",
            "authorLink": "https://dooray.com/",
            "imageUrl": "http://it.chosun.com/data/photos/cdn/20180423/2850453_09555838720000.jpg",
            "thumbUrl": "http://www.kinews.net/news/photo/201804/119143_167793_5622.png",
        },
        {
            "fields": [
                {
                    "title": "発売予定日",
                    "value": "2018年冬",
                    "short": true
                },
                {
                    "title": "予想価格",
                    "value": "125,000円",
                    "short": true
                }
            ]
        },
        {
            "fields": [
                {
                    "title": "説明",
                    "value": "日本未発売",
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
                    "text": "チャンネル選択",
                    "name": "guide-sel",
                    "dataSource": "channels"
                }
            ]
        },
        {
            "actions": [
                {
                    "type": "button",
                    "text": "共有",
                    "name": "guide-btn",
                    "value": "btnValue"
                },
                {
                    "type": "button",
                    "text": "次へ",
                    "name": "guide-btn",
                    "value": "btnValue"
                },
            ]
        }
    ]
}
```

### コンポーネント分析

データのコンポーネントを詳しく見てみましょう。

#### Message Object

|フィールド名|デフォルト|説明|
|---|---|---|
|text||メッセージテキスト|
|attachments||attachmentの配列|
|responseType|"ephemeral"|メッセージ表示対象<br>- "ephemeral": コマンドを実行したユーザーにのみ表示 <br>- "inChannel": チャンネル内の全ユーザーに表示
|replaceOriginal|true|対話的メッセージ(Interactive Message)応答時において、既存メッセージの修正するか否か|
|deleteOriginal|false|対話的メッセージ(Interactive Message)応答時において、既存メッセージの削除するか否か|

#### Attachment Object

|フィールド名|デフォルト|説明|
|---|---|---|
|text||attachmentのテキスト|
|title||attachmentのタイトル|
|titleLink||attachmentのタイトルをクリックすると移動するリンク|
|authorName||attachmentの作成者|
|authorLink||attachmentの作成者をクリックすると移動するリンク|
|fields||フィールドの配列|
|actions||アクションの配列|
|callbackId||アクションエレメントの作動時に一緒に伝達される値(セッション維持などの用途に使用)|
|imageUrl||画像アドレス|
|thumbUrl||サムネイルアドレス|
|color|#4757C4|attachmentの縦線の色(HTML色コード)|

#### Field Object

|フィールド名|デフォルト|説明|
|---|---|---|
|title||フィールドのタイトル|
|value||フィールドのテキスト|
|short|false|フィールド幅の設定(trueで設定時、半分の幅)|

#### Action Object

|フィールド名|デフォルト|説明|
|---|---|---|
|type||アクションタイプ<br>- "button": ボタン<br>- "select": ドロップダウンメニュー|
|text||ボタン、ドロップダウンメニューに表示されるテキスト|
|name||コマンドサーバーに配信されるフィールド名|
|value||コマンドサーバーに配信されるフィールド値|
|style|"default"|ボタンの色<br>- "primary": ハイライトカラー<br>- "default": 基本色|
|options||オプションの配列|
|dataSource||「options」の代わりに指定できるオプション値<br>- "users": ユーザーリスト<br>- "channels": チャンネルリスト<br>- "external": Interactive Message Optional URLからもってくる

#### Option Object

|フィールド名|デフォルト|説明|
|---|---|---|
|text||オプションのテキスト|
|value||コマンドサーバーに送信されるフィールドの値|

---

## Incoming Webhook(responseUrl)
슬래시 커맨드의 특성에 따라 임의의 시간에 메시지를 보내야 하는 경우가 있습니다.(예시: 매일 특정 시간에 오늘의 일정을 알려주는 슬래시 커맨드) 이 경우에는 responseUrl을 활용해 메시지를 전송합니다.

### 요청 방법
#### POST https://{tenantDomain}/messenger/api/commands/hook/{cmdToken}

##### request body
attachments 메시지 보내기의 Message Object를 참조
```javascript
{
    "responseType": "ephemeral", 
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
### 결과 반환
* 성공 여부: $.header.isSuccessful에 true, false 값을 반환합니다.
* 실패 원인: $.header.resultCode에 코드 값을 $.header.resultMessage에 상세 실패 정보를 반환합니다.

## 대화 상자 사용하기
별도의 영역에서 정보를 입력받을 수 있는 대화 상자를 띄웁니다.

### 요청 방법
#### POST https://{tenantDomain}/messenger/api/channels/{channelId}/dialogs

##### request header
* token: cmdToken

##### request body
```javascript
{
    token: "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    triggerId: "1111111111111.xxxxxxxxxxxxxxxxxxxx.3333333333333",
    callbackId: "guide-a1b2c3",
    dialog: {
        callbackId: 'guide-a1b2c3',
        title: 'Guide Dialog',
        submitLabel: 'Send',
        elements: [
            {
                type: 'text',
                subtype: 'number',
                label: 'Page Number',
                name: 'page',
                value: 0,
                minLength: 1,
                maxLength: 2,
                placeholder: '0 ~ 50',
                hint: 'Must in 0 ~ 50'
            },
            {
                type: 'textarea',
                label: 'Note',
                name: 'note',
                optional: true
            },
            {
                type: 'select',
                label: 'Is this important?',
                name: 'important',
                value: 'false',
                options: [
                    {
                        label: 'Yes',
                        value: 'true'
                    },
                    {
                        label: 'No',
                        value: 'false'
                    }
                ]
            }
        ]
    }
}
```

| 필드명 | 기본값 | 설명 |
| --- | --- | --- |
| triggerId | | 어떤 커맨드 요청에서 유발된 Dialog인지 구분해주는 값 |
| callbackId |  | 전송할 때 함께 전달될 값(세션 유지 등의 용도로 사용) |
| title |  | Dialog 제목 |
| submitLabel | "Submit" | 전송 버튼 텍스트 지정 |
| elements |  | **Element**의 배열 |

### 결과 반환

* 성공 여부: $.header.isSuccessful에 true, false 값을 반환합니다.
* 실패 원인: $.header.resultCode에 코드 값을 $.header.resultMessage에 상세 실패 정보를 반환합니다.



#### Element Object
| 필드명 | 기본값 | 설명 |
| --- | --- | --- |
| type |  | 필드 타입<br>"text": 텍스트 필드<br>"textarea": 장문 텍스트 필드<br>"select": 드롭 메뉴 |
| subtype |  | type이 text일 때 모바일에서 출력할 키보드 타입<br>"number", "email", "tel", "url" |
| label |  | 사용자에게 출력되는 필드명 |
| name |  | 커맨드 서버에 전달되는 필드명 |
| value |  | 필드에 기본으로 입력된 값(type이 select일 때 Option value로 지정해두면 자동 선택) |
| options |  | type이 select일 때 출력되는 **Option**의 배열 |
| dataSource |  | type이 select일 때 options 대신 출력할 데이터 |
| minLength |  | 최소 입력 글자수 |
| maxLength |  | 최대 입력 글자수 |
| placeholder |  | 필드에 출력되는 힌트(입력 시 사라짐) |
| hint |  | 필드 아래에 출력되는 힌트 |
| optional | false | 해당 필드의 필수 입력 여부 설정(false로 하면 필수 입력) |

#### Option Object

|필드명|기본값|설명|
|---|---|---|
|label||Option 텍스트|
|value||커맨드 서버에 전달되는 필드값|

### 대화 상자 전송 처리
위의 API를 활용해 사용자에게 대화 상자를 띄웠습니다. 이후 사용자가 해당 대화 상자를 작성해서 전송하면 이를 처리해야 합니다.

#### 메신저 서버에서 커맨드 서버로의 요청
``` javascript
{
    "type": "dialog_submission",
    "tenant": {
        "id": "1234567891234567891",
        "domain": "guide.dooray.com"
    },
    "channel": {
        "id": "1234567891234567891",
        "name": "커맨드 가이드 채널"
    },
    "user": {
        "id": "1234567891234567891"
    },
    "responseUrl": "https://guide.dooray.com/messenger/api/commands/hook/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "cmdToken": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "updateCmdToken": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "prevCmdToken": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "callbackId": "guide-a1b2c3",
    "submission": {
        "page": "100",
        "note": "자주 봐야하는 부분",
        "important": "true"
    }
}

```

|필드명|설명|
|---|---|
|type|발생한 이벤트의 타입(dialog_submission)|
|tenant|커맨드를 호출한 사용자가 속한 테넌트의 정보|
|channel|커맨드를 호출한 채널의 정보|
|user|커맨드를 호출한 사용자의 정보|
|responseUrl|커맨드를 호출에 응답하기 위한 인커밍 웹훅 URL|
|cmdToken|API 호출 시에 사용하는 Token|
|callbackId|Dialog에 지정된 Callback ID|
|submission|Dialog에 지정된 element의 name과 사용자가 작성한 값을 Key와 Value로 한 Object|

#### 커맨드 서버에서 메신저 서버로의 응답
두 가지 경우가 존재합니다.

* 사용자 입력값에 오류가 없을 경우, 응답을 비우고 HTTP 200 응답을 합니다.

* 오류가 있을 경우, HTTP 200 응답과 함께 errors로 응답합니다.

``` javascript
{
    errors: [
        {
            name: 'page',
            error: 'Page number는 50을 넘을 수 없습니다.'
        }
    ]
}
```

|필드명|기본값|설명|
|---|---|---|
|name||오류를 찾은 element의 name|
|error||출력할 오류 메시지|

---

## 대화방에 커맨드 등록하기

### 대화방에 커맨드를 등록

커맨드는 자신이 참여하고 있는 1:1 대화, 그룹 대화 등에 등록하여 활용할 수 있습니다. 커맨드 추가 화면을 여는 방법은 두 가지가 있습니다.

첫째, 메신저 우측 상단의 설정 메뉴를 통해 추가할 수 있습니다.

![17](http://static.toastoven.net/prod_dooray_messenger/integration/17.png)

둘째, 대화방의 입력창에 `/`를 입력 후 나타나는 화면에서 '연동 서비스' 버튼을 통해 추가할 수 있습니다.

![18](http://static.toastoven.net/prod_dooray_messenger/integration/18.png)

커맨드 추가 화면에는 공개된 커맨드나 자신이 생성한 커맨드가 표시됩니다. 원하는 커맨드 우측의 '추가' 버튼을 눌러 대화방에 커맨드를 추가하세요. 만약 커맨드가 없다면 본 문서의 처음으로 돌아가 커맨드를 만들어 보세요.

![19](http://static.toastoven.net/prod_dooray_messenger/integration/19.png)

![20](http://static.toastoven.net/prod_dooray_messenger/integration/20.png)

### 커맨드 공개

만약 자신이 만든 커맨드의 멋진 기능을 조직 내의 다른 사람들과 공유하고 싶다면 공개로 설정해 주세요. 조직 내의 다른 사람들도 자유롭게 대화방에 추가하여 사용할 수 있습니다. 비공개로 변경해도 이미 추가한 커맨드는 다른 사람이 계속 사용할 수 있으니, 다른 사람들이 더 이상 커맨드를 사용하지 못하게 하려면 등록한 커맨드를 삭제해 주세요.

---

## 예제: 투표 커맨드 

### 커맨드 서버 요구사항

커맨드 서버는 등록한 커맨드대로 동작하는 REST API를 제공해야 합니다.

|API 종류|설명|필수 |메소드|
|------|---|---|---|
|커맨드 Request URL|사용자의 커맨드 실행 요청을 처리할 URL|O|POST|
|Interactive Message의 Request URL|사용자의 액션(버튼 클릭, 드롭다운 메뉴 선택)을 처리할 URL|X|POST|
|Interactive Message의Optional URL|드롭다운 메뉴에서 외부 데이터 제공할 URL|X|POST|

### 투표 커맨드

예제로 대화방에 투표를 만들고 참여할 수 있는 투표 커맨드를 만들겠습니다.
예제 코드는 [Github](https://github.com/nhnent/dooray.vote)에서 확인할 수 있습니다. 

![21](http://static.toastoven.net/prod_dooray_messenger/integration/21.png)

#### API

커맨드 Request URL과 Interactive Message의 Request URL만 사용합니다.

#### 커맨드 실행 포맷

사용자가 투표 커맨드를 실행할 입력 포맷은 아래처럼 입력하도록 합니다.

```javascript
/vote {제목} {항목1} "{공백을 포함한 항목}" ... {항목n}
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

![22](http://static.toastoven.net/prod_dooray_messenger/integration/22_1.png)

커맨드 서버는 커맨드 Request URL로 사용자가 입력한 값을 포함한 JSON 데이터를 받게 됩니다.

``` javascript
{
    "tenantId": "1234567891234567891",
    "tenantDomain": "guide.dooray.com",
    "channelId": "1234567891234567891",
    "channelName": "Command 가이드",
    "userId": "1234567891234567891",
    "command": "/vote",
    "text": "점심식사 짜장면 짬뽕 \"사천 탕수육\"",
    "responseUrl": "https://guide.dooray.com/messenger/api/commands/hook/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "appToken": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "cmdToken": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "triggerId": "1234567891234.xxxxxxxxxxxxxxxxxxxx"
}
```

|필드명|설명|
|----|---|
|tenantId|커맨드가 등록된 테넌트의 ID|
|tenantDomain|커맨드가 등록된 테넌트 도메인|
|channelId|커맨드를 요청한 대화방의 ID|
|channelName|커맨드를 요청한 대화방 제목|
|userId|커맨드를 요청한 사용자 ID|
|command|커맨드 이름|
|text|사용자가 입력한 전체 텍스트|
|responseUrl|커맨드를 요청한 대화방의 Webhook URL|
|appToken|커맨드를 등록한 앱의 토큰(요청 검증으로 활용)|
|cmdToken|API 호출 시에 사용하는 Token|
|triggerId|다이얼로그 실행 ID|

### 커맨드 실행 요청에 대한 응답

![23](http://static.toastoven.net/prod_dooray_messenger/integration/23_1.png)

커맨드 실행 요청에 대한 응답으로 실행 사용자에게만 보이는 확인 메시지를 보냅니다. 투표를 생성하거나 취소할 수 있는 버튼을 사용자에게 제공하기 위해 아래와 같이 메시지를 전송합니다.

``` javascript
{
    "responseType": "ephemeral",
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
                    "value": "사천 탕수육",
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
                    "value": "점심식사 짜장면 짬뽕 \"사천 탕수육\"",
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

사용자가 전송 버튼을 누르면 아래와 같은 데이터가 Interactive Message의 Request URL로 전송됩니다.

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
    "text": "점심식사 짜장면 짬뽕 \"사천 탕수육\"",
    "callbackId": "vote",
    "actionText": "Submit",
    "actionValue": "점심식사 짜장면 짬뽕 \"사천 탕수육\"",
    "appToken": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "cmdToken": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "triggerId": "1234567891234.xxxxxxxxxxxxxxxxxxxx",
    "commandRequestUrl": "https://command.guide.doc/req",
    "channelLogId": "-7386965175150134411",
    "originalMessage": { /* Message Object */ }
}
```

|필드명|설명|
|----|---|
|callbackId|사용자가 선택한 액션이 속해있는 Attachment의 ID|
|actionText|사용자가 선택한 액션 텍스트|
|actionValue|사용자가 선택한 액션 값|
|commandRequestUrl|커맨드 Request URL|
|channelLogId|메시지 ID|
|originalMessage|이전 응답으로 받은 메시지|

### 액션 실행에 대한 응답

![24](http://static.toastoven.net/prod_dooray_messenger/integration/24_1.png)

'Submit' 버튼에 대한 응답으로 투표 생성 메시지를 전송합니다. 생성 확인 메시지는 더 이상 필요가 없기 때문에 삭제하고 메시지를 새로 생성합니다.

``` javascript
{
    "responseType": "inChannel", 
    "deleteOriginal": true, 
    "text": "(dooray://1234567891234567891/members/1234567891234567891 \"member\") created the vote!",
    "attachments": [
        {
            "callbackId": "1525223162093-(dooray://1234567891234567891/members/1234567891234567891 \"member\")",
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
                    "text": "사천 탕수육",
                    "value": 2
                }
            ],
            "color": "#4286f4"
        },
        {
            "callbackId": "1525223162093-(dooray://1234567891234567891/members/1234567891234567891 \"member\")",
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

|필드명|기본값|설명|
|----|---|---|
|deleteOriginal|false|새 메시지를 생성하기 전 기존 메시지 삭제 여부|
|replaceOriginal|true|기존 메시지 업데이트 여부|

이 후 사용자가 누르는 버튼은 액션 실행 요청과 그에 따른 응답의 반복입니다.
