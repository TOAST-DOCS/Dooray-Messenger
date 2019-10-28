## Dooray! > Messenger > Incoming Hook Guide

### Incoming Hook

Dooray! provides the incoming hook function that allows sending messages to a specific chatroom.

### Sending a message to a chatroom

In the terminal, create the following script. This is for Linux and macOS with `curl` installed.

```bash
hook_url=
curl -H "Content-Type: application/json" -X POST -d '{"botName": "MyBot", "botIconImage": "https://static.dooray.com/static_images/dooray-bot.png", "text":"Dooray!"}' $hook_url
```

In the script above, type a URL that points to a specific chatroom. 

From the 'Settings' menu, choose 'Service Link' and click the 'Add Link' button of 'incoming' in the 'Add Service' tab. On the screen, select a chatroom to link and then click the 'Save' button to copy the address to the Clipboard.

Add the copied address after `hook_url` in the above script.

```bash
hook_url=https://hook.dooray.com/services/...
curl -H "Content-Type: application/json" -X POST -d '{"botName": "MyBot", "botIconImage": "https://static.dooray.com/static_images/dooray-bot.png", "text":"Dooray!"}' $hook_url
```

Save this as `simple.sh` and execute it to see your message being sent to the chatroom.


![hook1](http://static.toastoven.net/prod_dooray_messenger/hook1.png)


### Data Format

The following script shows the JSON part from the program executed above:

```json
{
    "botName": "MyBot", 
    "botIconImage": "https://static.dooray.com/static_images/dooray-bot.png", 
    "text":"Dooray!"
}
```

Besides the `text` area, use the `attachments` area to add a title to the body and also add a colored rectangle to the text. 

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

Sending this script shows the following result: When moving the script to `simple.sh`, you must remove the wrap.

![hook2](http://static.toastoven.net/prod_dooray_messenger/hook2.png)


If necessary, you can repeat the `attachments` area as many times as you want.

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
