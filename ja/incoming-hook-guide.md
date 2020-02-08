## Dooray! > Messenger > 着信フックガイド

### 着信フック

Doorayは、特定のチャットルームにメッセージを送信できる着信フック(incoming hook)を提供しています。

### チャットルームにメッセージ送信

端末環境で次のようなスクリプトを作成します。Linux、macOS基準で、`curl`がインストールされていると仮定します。

```bash
hook_url=
curl -H "Content-Type: application/json" -X POST -d '{"botName": "MyBot", "botIconImage": "https://static.dooray.com/static_images/dooray-bot.png", "text":"Dooray!"}' $hook_url
```

上記のスクリプトで `hook_url`に特定のチャットルームを指すURLを記載する必要があります。 

「設定」メニューから「サービス連動」または「着信Webフック連動」を選択し、「サービス追加」タブから「Incoming」の「連動追加」ボタンを押します。画面で連動したいチャットルームをチェックして、「保存」ボタンを押すと、そのアドレスがクリップボードにコピーされます。

そのアドレスを上記のスクリプトで `hook_url` の次に貼り付けます。

```bash
hook_url=https://hook.dooray.com/services/...
curl -H "Content-Type: application/json" -X POST -d '{"botName": "MyBot", "botIconImage": "https://static.dooray.com/static_images/dooray-bot.png", "text":"Dooray!"}' $hook_url
```

この内容を `simple.sh`で保存してコマンドラインから実行すると、チャットルームにメッセージが送信されることを確認できます。


![hook1](http://static.toastoven.net/prod_dooray_messenger/hook1.png)


### データフォーマット

先に実行したプログラムでJSON部分だけを見ると、次のようになります。

```json
{
    "botName": "MyBot", 
    "botIconImage": "https://static.dooray.com/static_images/dooray-bot.png", 
    "text":"Dooray!"
}
```

`text` 領域以外に `attachments` の領域を使用すると、本文のほかにタイトルを追加することができ、色が付いた四角形で包むこともできます。

```json
{
    "botName": "MyBot", 
    "botIconImage": "https://static.dooray.com/static_images/dooray-bot.png", 
    "text":"Dooray!",
    "attachments" : [
        {
            "title" : "title",
            "titleLink" : "http://dooray.com/",
            "text" : "message",
            "color" : "red"
        }
    ]
}
```

この内容を送信すると、次のように表示されます。上記の内容を `simple.sh`に移すとき、改行を取り除く必要があります。

![hook2](http://static.toastoven.net/prod_dooray_messenger/hook2.png)


`attachments` 領域は、複数回繰り返すことができます。.

```json
{
    "botName": "MyBot", 
    "botIconImage": "https://static.dooray.com/static_images/dooray-bot.png", 
    "text":"Dooray!",
    "attachments" : [
        {
            "title" : "title",
            "titleLink" : "http://dooray.com/",
            "text" : "message",
            "color" : "red"
        },
        {
            "title" : "title2",
            "titleLink" : "http://dooray.com/",
            "text" : "message2",
            "color" : "green"
        }
    ]
}
```

![hook3](http://static.toastoven.net/prod_dooray_messenger/hook3.png)
