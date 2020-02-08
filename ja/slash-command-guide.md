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
    "channelName": "Command Guide",
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
        "name" "Command Guide"
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
        "text": "チャットルーム出力",
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
        "name": "Command Guide"
    },
    "user": {
        "id": "1234567891234567891",
        "name": "山田太郎"
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
スラッシュコマンドの特性によって任意の時間にメッセージを送信しなければならない場合があります。(例：毎日特定の時間に、今日のスケジュールを知らせるスラッシュコマンド）このような場合には、responseUrlを活用してメッセージを送信します。

### リクエスト方法
#### POST https://{tenantDomain}/messenger/api/commands/hook/{cmdToken}

##### request body
「attachmentsメッセージの送信」のMessage Objectを参照
```javascript
{
    "responseType": "ephemeral", 
    "text": "Click 'Submit' button to start the vote.",
    "attachments": [
        {
            "title": "ランチ",
            "fields": [
                {
                    "title": "Item 1",
                    "value": "和食",
                    "short": true
                },
                {
                    "title": "Item 2",
                    "value": "中華",
                    "short": true
                },
                {
                    "title": "Item 3",
                    "value": "タイ 料理",
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
                    "value": "\"ランチ\" \"和食\" \"짬뽕\" \"タイ 料理\"",
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
### 結果を返す
* 成否の結果: $.header.isSuccessfulに true, false を返します。
* エラーの原因: $.header.resultCodeにコード値を、$.header.resultMessageに詳しいエラー情報を返します。

## ダイアログボックスの使用
別途領域に情報を入力することができるダイアログボックスを表示させます。

### リクエスト方法
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

| フィールド名 | デフォルト | 説明 |
| --- | --- | --- |
| triggerId | | どのコマンドリクエストがきっかけとなったダイアログかを区分する値 |
| callbackId |  | 送信時に一緒に渡される値(セッション維持などの用途に使用) |
| title |  | ダイアログのタイトル |
| submitLabel | "Submit" | 送信ボタンのテキストを指定 |
| elements |  | **エレメント**の配列 |

### 結果を返す

* 成否の結果: $.header.isSuccessfulにtrue、falseを返します。
* ·	エラーの原因: $.header.resultCodeにコード値を、$.header.resultMessageに詳しいエラー情報を返します。

#### Element Object

| フィールド名 | デフォルト | 説明 |
| --- | --- | --- |
| type |  | フィールドタイプ<br>"text": テキストフィールド<br>"textarea": 長文テキストフィールド<br>"select": ドロップダウンメニュー |
| subtype |  | typeがtextのときにモバイルから出力するキーボードタイプ<br>"number", "email", "tel", "url" |
| label |  | ユーザーに出力されるフィールド名 |
| name |  | コマンドサーバーに送信されるフィールド名 |
| value |  | フィールドにデフォルト入力された値(typeがselectのときにOption valueに指定しておくと自動的に選択)|
| options |  | typeがselectのときに出力されるオプションの配列 |
| dataSource |  | typeがselectのときにoptionsの代わりに出力するデータ |
| minLength |  | 最小入力文字数 |
| maxLength |  | 最大入力文字数 |
| placeholder |  | フィールドに出力されるヒント(入力時に消える)|
| hint |  | フィールドの下に出力されるヒント|
| optional | false | 当該フィールドの必須入力かどうかを設定(falseにすると必須入力)|

#### Option Object

|フィールド名|デフォルト|説明|
|---|---|---|
|label||オプションのテキスト|
|value||コマンドサーバーに送信されるフィールドの値|

### ダイアログボックスの転送処理
上記のAPIを活用してユーザーにダイアログボックスを表示しました。以後、ユーザーがそのダイアログボックスを作成して送信すると、これを処理する必要があります。

#### メッセンジャーサーバーからコマンドサーバーへのリクエスト
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

|フィールド名|説明|
|---|---|
|type|発生したイベントのタイプ(dialog_submission)|
|tenant|コマンドを呼び出したユーザーが属するテナント情報|
|channel|コマンドを呼び出したチャンネル情報|
|user|コマンドを呼び出したユーザー情報|
|responseUrl|コマンド呼び出しに応答するための着信WebフックURL|
|cmdToken|API呼び出し時に使用するトークン|
|callbackId|ダイアログに指定されたコールバックID|
|submission|ダイアログで指定されたエレメント名とユーザーが作成した値をkeyとvalueにしたオブジェクト|

#### コマンドサーバーからメッセンジャーサーバーへの応答
2つの場合があります。

* ユーザー入力値にエラーがない場合は、応答を空けてHTTP 200応答をします。

* エラーがある場合は、HTTP 200応答とともにerrorsと応答します。

``` javascript
{
    errors: [
        {
            name: 'page',
            error: 'Page numberは最大50です。'
        }
    ]
}
```

|フィールド名|デフォルト|説明|
|---|---|---|
|name||エラーを発見したエレメント名|
|error||出力するエラーメッセージ|

---

## チャットルームにコマンドを登録

### コマンド登録

コマンドは、自分が参加している1:1会話、グループチャットなどに登録して活用できます。コマンドの追加画面を開く方法は2種類あります。
まず、メッセンジャー右上の設定メニューから追加できます。

![17](http://static.toastoven.net/prod_dooray_messenger/integration/17.png)

または、チャットルームの入力ウィンドウに/を入力した後に表示される画面で、「スラッシュコマンド連動」ボタンから追加できます。

![18](http://static.toastoven.net/prod_dooray_messenger/integration/18.png)

コマンド追加画面には、公開されたコマンドや自分が作成したコマンドが表示されます。希望するコマンドの右側にある「追加」ボタンを押して、チャットルームにコマンドを追加します。もしコマンドがない場合は、このドキュメントの最初に戻ってコマンドを作成してください。

![19](http://static.toastoven.net/prod_dooray_messenger/integration/19.png)

![20](http://static.toastoven.net/prod_dooray_messenger/integration/20.png)

### コマンド公開

自分が作ったコマンドの便利な機能を組織内のユーザーと共有したい場合は公開で設定してください。組織内のユーザーも自由にチャットルームに追加して使用することができます。非公開に変更しても、すでに追加されたコマンドは他のユーザーも継続して使用できるため、他人がコマンドを使用できないようにするには、登録したコマンドを削除してください。

---

## 例：投票コマンド 

### コマンドサーバーの要件

コマンドサーバーは登録されたコマンドに従って動作するREST APIを提供する必要があります。

|APIの種類|説明|必須|メソッド|
|------|---|---|---|
|Command Request URL|ユーザーのコマンド実行リクエストを処理するURL|O|POST|
|Interactive Message Request URL|ユーザーのアクション(ボタンのクリック、ドロップダウンメニューを選択)を処理するURL|X|POST|
|Interactive Message Optional URL|ドロップダウンメニューから外部データを提供するURL|X|POST|

### 投票コマンド

例として、チャットルームに投票を作成し、参加できる投票コマンドを作りましょう。サンプルコードは、[Github](https://github.com/nhnent/dooray.vote)で確認できます。 

![21](http://static.toastoven.net/prod_dooray_messenger/integration/21.png)

#### API

Command Request URLとInteractive Message Request URLのみ使用します。

#### コマンドの実行フォーマット

ユーザーが投票コマンドを実行する入力フォーマットは、下記のように入力します。

```javascript
/vote {タイトル} {項目1} "{空白を含めた項目}" ... {項目n}
```

#### シナリオ

1. ユーザーがコマンドを実行
2. コマンドを実行したユーザーだけに表示される投票作成用のメッセージを出力
3. 作成ボタンを押してチャットルームのすべてのメンバーに表示される投票メッセージを出力
4. チャットルームのメンバーが投票ボタンで投票に参加
5. 投票を作成したユーザーが投票終了
6. 投票結果の出力

### 投票コマンドの実行リクエスト

ユーザーが投票コマンドを下記のように実行します。

![22](http://static.toastoven.net/prod_dooray_messenger/integration/22_1.png)

コマンドサーバーは、Command Request URLにユーザーが入力した値を含むJSONデータを取得します。

``` javascript
{
    "tenantId": "1234567891234567891",
    "tenantDomain": "guide.dooray.com",
    "channelId": "1234567891234567891",
    "channelName": "Command Guide",
    "userId": "1234567891234567891",
    "command": "/vote",
    "text": "ランチ 和食 中華 \"タイ 料理\"",
    "responseUrl": "https://guide.dooray.com/messenger/api/commands/hook/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "appToken": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "cmdToken": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "triggerId": "1234567891234.xxxxxxxxxxxxxxxxxxxx"
}
```

|フィールド名|説明|
|----|---|
|tenantId|コマンドが登録されたテナントID|
|tenantDomain|コマンドが登録されたテナントのドメイン|
|channelId|コマンドをリクエストしたチャットルームID|
|channelName|コマンドをリクエストしたチャットルームのタイトル|
|userId|コマンドをリクエストしたユーザーID|
|command|コマンド名|
|text|ユーザーが入力したテキスト|
|responseUrl|コマンドをリクエストしたチャットルームのWebフックURL|
|appToken|コマンドを登録したアプリのトークン（リクエストの検証に活用)|
|cmdToken|API呼び出し時に使用するトークン|
|triggerId|ダイアログの実行ID|

### コマンドの実行リクエストに対する応答

![23](http://static.toastoven.net/prod_dooray_messenger/integration/23_1.png)

コマンド実行リクエストに応答して実行ユーザーにのみ表示される確認メッセージを送信します。投票を作成したり、キャンセルしたりできるボタンをユーザーに提供するため、下記のようにメッセージを送信します。

``` javascript
{
    "responseType": "ephemeral",
    "text": "Click 'Submit' button to start the vote.",
    "attachments": [
        {
            "title": "ランチ",
            "fields": [
                {
                    "title": "Item 1",
                    "value": "和食",
                    "short": true
                },
                {
                    "title": "Item 2",
                    "value": "中華",
                    "short": true
                },
                {
                    "title": "Item 3",
                    "value": "タイ 料理",
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
                    "value": "ランチ 和食 中華 \"タイ 料理\"",
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

### アクションの実行リクエスト

ユーザーが送信ボタンを押すと、下記のようなデータがInteractive Message Request URLに転送されます。

``` javascript
{
    "tenant": {
        "id": "1234567891234567891",
        "domain": "guide.dooray.com"
    },
    "channel": {
        "id": "1234567891234567891",
        "name": "Command Guide"
    },
    "user": {
        "id": "1234567891234567891",
        "name": "山田太郎"
    },
    "commandName": "/vote",
    "command": "/vote",
    "text": "ランチ 和食 中華  \"タイ 料理\"",
    "callbackId": "vote",
    "actionText": "Submit",
    "actionValue": "ランチ 和食 中華 \"タイ 料理\"",
    "appToken": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "cmdToken": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "triggerId": "1234567891234.xxxxxxxxxxxxxxxxxxxx",
    "commandRequestUrl": "https://command.guide.doc/req",
    "channelLogId": "-7386965175150134411",
    "originalMessage": { /* Message Object */ }
}
```

|フィールド名|説明|
|----|---|
|callbackId|ユーザーが選択したアクションが属するattachmentのID|
|actionText|ユーザーが選択したアクションのテキスト|
|actionValue|ユーザーが選択したアクション値|
|commandRequestUrl|Command Request URL|
|channelLogId|メッセージID|
|originalMessage|以前の応答からのメッセージ|

### アクションの実行に応答

![24](http://static.toastoven.net/prod_dooray_messenger/integration/24_1.png)

「Submit」ボタンに応答して投票作成メッセージを送信します。作成確認メッセージは、これ以上必要ないので、削除してメッセージを新規に作成します。

``` javascript
{
    "responseType": "inChannel", 
    "deleteOriginal": true, 
    "text": "(dooray://1234567891234567891/members/1234567891234567891 \"member\") created the vote!",
    "attachments": [
        {
            "callbackId": "1525223162093-(dooray://1234567891234567891/members/1234567891234567891 \"member\")",
            "title": "ランチ",
            "actions": [
                {
                    "name": "vote",
                    "type": "button",
                    "text": "和食",
                    "value": 0
                },
                {
                    "name": "vote",
                    "type": "button",
                    "text": "中華",
                    "value": 1
                },
                {
                    "name": "vote",
                    "type": "button",
                    "text": "タイ 料理",
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

|フィールド名|デフォルト|説明|
|----|---|---|
|deleteOriginal|false|新規メッセージ作成前に既存メッセージを削除するか否か|
|replaceOriginal|true|既存メッセージを更新するか否か|

この後、ユーザーが押すボタンは、アクションの実行リクエストとそれに伴うレスポンスの繰り返しです。
