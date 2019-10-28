## Dooray! > Messenger > Slash (/) Command Guide
### Link Service

Dooray! Messenger allows you to command various tools (not humans) and get messages from them for more efficient work. If you want to implement functions not provided by Messenger, you can use this function to automate your work more efficiently. The function to be introduced here is how to create a command yourself. Various link services, such as Bots and APIs, will be provided later.

### Slash (/) Command

Slash(/) Command (hereafter, command) is a command coming after `/` to perform a specific function. Dooray! Messenger provides commands including `/mute`, `/status`, and `/search` by default. For example, these commands help you execute the functions quickly, such as searching the message contents or changing your status using the keyboard without a mouse or any other controls.

![2](http://static.toastoven.net/prod_dooray_messenger/integration/2.png)

You can create and use a command to perform a desired function by yourself. For example, you can get traffic information and weather every morning or create a vote by entering simple commands.

The following figure shows the communication process between the command and Messenger servers.

![3](http://static.toastoven.net/prod_dooray_messenger/integration/3.png)

Enter `/` followed by a command registered to the chatroom. The command entered is sent to the command server via Messenger server. The command server sends the processed result to the Messenger server. The Messenger server displays the result based on the data from the command server.

### Environment for Use

Users can enter the command and view the result on PC or mobile. Therefore, the command creator must consider the layout in the mobile environment.
Now, the function to add commands to a chatroom is supported for PC only.

### Guide to Create a Command

Please see the following documentation for how to create and register a command.

---

## Add a Command

To use your own command, you must add it to Dooray! Messenger.

### Move to Add Screen

Dooray! Click your name at the top left of the Dooray! Messenger and select the 'Link Service' menu.

![4](http://static.toastoven.net/prod_dooray_messenger/integration/4_2.png)

An empty screen is displayed as shown below.

![5](http://static.toastoven.net/prod_dooray_messenger/integration/5.png)

### Add App

First, you must create an app. App is a bundle unit of linked services. You can add several new commands to one app. Create an app by entering the following information. Each piece of information is exposed when an open command is registered to the chatroom.
![6](http://static.toastoven.net/prod_dooray_messenger/integration/6.png)

|Classification|Description|
|---|---|
|Image|Displayed as a submitter icon of a message when a command is used in a chatroom.|
|Name|Displayed as a submitter name of a message when a command is used in a chatroom.|
|Description|Description of the app.|

Now, an app has been created. You can see the create token and an empty command list. The token is sent together when a command is requested and used to verify the request. Please be careful not to expose the token to the external. If the token has been exposed externally, use the 'Regenerate' button to remove the existing token and regenerate one.

![7](http://static.toastoven.net/prod_dooray_messenger/integration/7.png)

### Add a Command

After registering an app, click the 'Add' button on the slash command area to add a command. It is recommended to add commands which are closely related to each other to one app. If you have no commands created in advance, add `/hi` command as shown in the following example.

![8](http://static.toastoven.net/prod_dooray_messenger/integration/8.png)

|Classification|Description|
|---|---|
|Command|Enter the command including `/` to be entered in the chatroom.<br>It is recommended to use intuitive command which shows the function of command.|
|Request URL|Enter the command server URL to be requested when the command is executed.|
|Description|Description to be displayed when the command is used. Enter the description to let others understand the function of a command easily.|
|Parameter Hint|Describe the parameters which must be entered along with the command.<br>(You can enter the information such as location, time, person, date, text, and number.)|
|Public|Other members can also be added to the chatroom and use the command.|

The command has been added.

![9](http://static.toastoven.net/prod_dooray_messenger/integration/9.png)

### Enter Interactive Request URL

To get the user's action using buttons and drop-down menu, you need a separate URL to process the interactive message.

![10](http://static.toastoven.net/prod_dooray_messenger/integration/10.png)

|Classification|Description|
|---|---|
|Interactive Message Request URL|When you interact with a user via messages such as buttons and drop-down menu, enter the URL to send the user's request.|
|Interactive Message Optional URL|If you provide menu list of which dataSource is set to external, enter the URL to request the menu list.|

---

## "Hello World!" Send a message
Let's make a very simple command. When entering `/hi` in a chatroom, this command will return "Hello world!".

### Execute a command

When a user executes the `/hi` command via Dooray! Messenger, the command server receives JSON data as follows.

```javascript
{
    "tenantId": "1234567891234567891",
    "tenantDomain": "guide.dooray.com",
    "channelId": "1234567891234567891",
    "channelName": "Command Guide Channel",
    "userId": "1234567891234567891",
    "command": "/hi",
    "text": ""
    "responseUrl": "https://guide.dooray.com/messenger/api/commands/hook/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "appToken": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "triggerId": "1234567891234.xxxxxxxxxxxxxxxxxxxx"
}
```

|Field Name|Description|
|---|---|
|tenantId|The ID of tenant where the command has been registered|
|tenantDomain|The domain of tenant where the command has been registered|
|channelId|The ID of the chatroom that the command has requested|
|channelName|The ID of the chatroom which has requested the command|
|userId|The ID of the user who has requested the command|
|command|Requested command|
|text|Text entered with the command|
|responseUrl|Web hook URL which can respond to the command request|
|appToken|Token of the registered app. It is used to verify if the request is normal.|
|triggerId|The value use for dialog|

### Response

The command server creates response data by using the received data. And the data should be sent as the response to the request. `/hi` command should send only `Hello World!` without any special processing of data.

```javascript
{
    "text": "Hello World!",
    "responseType": "ephemeral"
}
```
When the above response is sent, it becomes a message which can be seen only by the user who has called for the command. If you want to show the message to all members in the chatroom, add `responseType` as `inChannel` to the response.

```javascript
{
    "text": "Hello World!",
    "responseType": "inChannel"
}
```
|Field Name|Default|Description|
|---|---|---|
|responseType|ephemeral|Set the message post type.<br>- inChannel: Shows to all users<br>- ephemeral:  Shows only to users who called for it|
|text||Message contents|

---

## Four ways to send a message

When a command is executed, Messenger server can send a message in four ways.

- Send a message for the first time
- Send another message after sending one
- Update a sent message
- Delete a sent message and then send a new message

### Send a message for the first time

This is the simplest way to send a new message.

```javascript
{
    "responseType": "inChannel",
    "text": "Hello World!"
}
```

### Send another message

Set `replaceOriginal` to `false` to send a new message.

```javascript
{
    "replaceOriginal": false,
    "responseType": "inChannel",
    "text": "Hello World!"
}
```

### Update a sent message

Set `replaceOriginal` to change only the contents while keeping the message location, and no notification is received. You cannot update `responseType` of the existing message. To change `responseType`, you must send a new message.

```javascript
{
    "responseType": "inChannel",
    "replaceOriginal": true,
    "text": "Hello World!(Updated)"
}
```

### Delete a sent message and then send a new message

In this case, a notification is sent to the participants of the chatroom, so it is useful to notify them of the changes. Set `deleteOriginal' to `true` to delete the existing message and send a new message.

```javascript
{
    "responseType": "inChannel",
    "deleteOriginal": true,
    "text": "Hello World!(Updated)"
}
```

Create a command by selecting an appropriate way to send a message for your needs.

---

## Include a button in a message

A button can be displayed in a response message by using the `attachments` field. The person who received the message can interact by clicking the button. The following description shows how to include a button and how to receive and handle the result of clicking the button.

The following message includes attachments and asks for confirmation whether to send the message typed below to the chatroom or not.

```javascript
{
    "text": "Message",
    "attachments": [
        {
            "callbackId": "send-a1b2c3", // This is sent together when the user interaction occurs. This can be used to identify the attachment with the interaction.
            "actions": [
                {
                    "name": "send",
                    "type": "button",
                    "text": "Send", // The button text displayed to the user
                    "value": "posting", // A value used for action (not visible to the user)
                    "style": "primary" // You can change the button style. primary, danger, default
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

When the message is received, you can see that a message with 'Send' and 'Cancel' buttons has been created as shown below.

![11](http://static.toastoven.net/prod_dooray_messenger/integration/11.png)

Click the 'Send' button. The following data is sent to the Interactive Request URL of the command server.

```javascript
{
    // It provides tenant, channel, and member information.
    "tenant": {
        "id": "1234567891234567891",
        "domain": "guide.dooray.com"
    },
    "channel": {
        "id": "1234567891234567891",
        "name" "Command Guide Channel"
    },
    "user": {
        "id": "1234567891234567891",
    },
    "commandName": "/post",
    "command": "/post",
    "text": "",
    "callbackId": "send-a1b2c3", // The callbackId of the attachment where the user-selected action belongs.
    "actionText": "Send", // actionText - The text of user-selected action.
    "actionValue": "posting", // actionValue - The value of user-selected action.
    "appToken": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "cmdToken": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "triggerId": "",
    "commandRequestUrl": "https://command.example.com/req",
    "channelLogId": "-7386965175150134411",
    "originalMessage": { /* Includes the message where the action occurred. */ }
    }
}
```

Processing when the user has clicked the button should be implemented in the command server.

---

## Include a drop-down menu in the message

You can include a drop-down menu in the attachments message. You can select either channel list, tenant member list, or random list from the drop-down menu.

In the following example, you will try to choose the board game most liked by your team members and play it with them. As shown in the following message, create a vote with the drop-down menu which has a list of board games.

### Static drop-down menu

Configure a list by using the `options` field.

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

You can show the drop-down menu through the above attachments as shown on the following screen.

![12](http://static.toastoven.net/prod_dooray_messenger/integration/12.png)

### Dynamic drop-down menu

Dynamic drop-down menu uses `dataSource` instead of `options`. Depending on the value, `dataSource` can show members, chatroom, or external data.

|Classification|Description|
|---|---|
|dataSource|List|
|users|Member|
|channels|Chatroom|
|external|External data|

#### Member List
If configuring a message with `dataSource` of `users`, you can show the member list of the current chatroom. The user can enter the keyword in the drop-down menu to search all tenant members.

```javascript
"attachments": [
    {
        "type": "select",
        "name": "sel_users",
        "text": "User output",
        "dataSource": "users"
    }
]
```

![13](http://static.toastoven.net/prod_dooray_messenger/integration/13.png)

#### Chatroom List
By configuring and sending a message with `channels` of `dataSource`, you can show the chatroom list where the user belongs.

```javascript
"attachments": [
    {
        "type": "select",
        "name": "sel_channels",
        "text": "Chatroom output",
        "dataSource": "channels"
    }
]
```

![14](http://static.toastoven.net/prod_dooray_messenger/integration/14.png)

#### External Data List
If configuring the message with `dataSource` of `external`, you can show the external data list. The external data list is requested via the Interactive Optional URL registered while setting the app.

``` javascript
"attachments": [
    {
        "type": "select",
        "name": "sel_external",
        "text": "External data",
        "dataSource": "external"
    }
]
```

The client requests the external data list along with the following message using the Interactive Optional URL.

```javascript
{
    "type": "interactive_message",
    "tenant": {
        "id": "1234567891234567891",
        "domain": "guide.dooray.com"
    },
    "channel": {
        "id": "1234567891234567891",
        "name": "Command Guide Channel"
    },
    "user": {
        "id": "1234567891234567891",
        "name": "Hong Gil Dong"
    },
    "callbackId": "sample",
    "actionName": "sel_externel",
    "actionTs": 1524734546105
}
```

The command server sends the drop down list as a response by using the above message.

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

## Send an attachments message

A command can send a specific message type called attachments. The component of attachments are various including buttons and drop-down menu described in other documents. With this attachments message, you can make the message attract user's attentions and guide behaviors such as requests or replies easily.

### Attachments message

Each message block shown below is an attachment which can have a title, a description, an image, a link, a button, a drop-down menu, etc. Up to 20 attachment blocks can configure an attachments message.

![16](http://static.toastoven.net/prod_dooray_messenger/integration/16.png)

|No.|Name|Description|
|---|---|---|
|1|text|The message contents.|
|2|attachment|The contents attached to the message. Attachments refers to several attachments.|
|3|authorName|The author's name. You can link with authorLink.|
|4|title|The title of attachment.|
|5|text|The text of attachment.|
|6|thumbUrl|The thumbnail image to insert in the attachment.|
|7|imageUrl|An image URL to be attached to the attachment.|
|8|field|One or two fields are displayed according to the value of short.|
|10|Interactive Menu|A drop-down menu.|
|11|Interactive Button|A button.

### Data

The data format is as follows.

```javascript
{
    "text": "NHN IT News!",
    "attachments": [
        {
            "callbackId": "guide-a1b2c3",
            "text": "On 2 a.m. today, Apple has announced release of iPhone X at the WWDC.",
            "title": "Release of iPhone X",
            "titleLink": "https://dooray.com/",
            "authorName": "NHN News",
            "authorLink": "https://dooray.com/",
            "imageUrl": "http://it.chosun.com/data/photos/cdn/20180423/2850453_09555838720000.jpg",
            "thumbUrl": "http://www.kinews.net/news/photo/201804/119143_167793_5622.png",
        },
        {
            "fields": [
                {
                    "title": "Release date",
                    "value": "Winter in 2018",
                    "short": true
                },
                {
                    "title": "Expected price",
                    "value": "KRW 1.25 million won",
                    "short": true
                }
            ]
        },
        {
            "fields": [
                {
                    "title": "Description",
                    "value": "Not released in Korea",
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
                    "text": "Select the Channel",
                    "name": "guide-sel",
                    "dataSource": "channels"
                }
            ]
        },
        {
            "actions": [
                {
                    "type": "button",
                    "text": "Share",
                    "name": "guide-btn",
                    "value": "btnValue"
                },
                {
                    "type": "button",
                    "text": "Next news",
                    "name": "guide-btn",
                    "value": "btnValue"
                },
            ]
        }
    ]
}
```

### Components Analysis

Now, we will look into the components of the data.

#### Message Object
|Field Name|Default|Description|
|---|---|---|
|text||Message text|
|attachments||Array of the Attachment|
|responseType|"ephemeral"|The target to whom a message will be displayed <br>- "ephemeral": Displays a message only to the user who has executed the command<br>- "inChannel": Displays a message to all users in the channel
|replaceOriginal|true|Whether to modify the existing message when responding to the Interactive Message|
|deleteOriginal|false|Whether to delete the existing message when responding to the Interactive Message|

#### Attachment Object
|Field Name|Default|Description|
|---|---|---|
|text||Attachment text|
|title||Attachment title|
|titleLink||Link to jump to by clicking the Attachment title|
|authorName||Attachment author|
|authorLink||Link to jump to by clicking the Attachment author|
|fields||Array of the Field|
|actions||Array of the Action|
|callbackId||The value to be sent when the Action element is executed(Used for keeping the session)|
|imageUrl||Image address|
|thumbUrl||Thumbnail address|
|color|#4757C4|Attachment vertical line color (HTML color code)|

#### Field Object
|Field Name|Default|Description|
|---|---|---|
|title||Field title|
|value||Field text|
|short|false|Sets the field width (half of the width if true)|

#### Action Object
|Field Name|Default|Description|
|---|---|---|
|type||Actiontype<br>- "button": button<br>- "select": Drop-down menu|
|text||Button, text to be displayed on the drop-down menu|
|name||The field name to be sent to the command server|
|value||The field value to be sent to the command server|
|style|"default"|Button color<br>- "primary": Highlight color<br>- "default": Default color|
|options||Array of the Option|
|dataSource||The option value which can be allocated instead of 'options'<br>- "users": User list<br>- "channels": Channel list<br>- "external": Gets the Interactive Message from the optional URL

#### Option Object
|Field Name|Default|Description|
|---|---|---|
|text||Option text|
|value||The field value to be sent to the command server|

---

## Use a dialog box
A dialog box is displayed, which allows you to input information on a separated area.

### How to request
|Classification 1|Classification 2|Description|
|---|---|---|
|URL||https://{domain}.dooray.com/messenger/api/channels/{channelId}/dialogs|
|Method||POST|
|Header|token|{cmdToken}|
|Body|triggerId|{triggerId}|
||dialog|{Dialog Object}|    

### Returns the result

* Success or Fail: Returns true or false with $.header.isSuccessful.
* Cause of failure: Returns the code value with $.header.resultCode and the detailed failure information with $.header.resultMessage.

#### Dialog Object
``` javascript
{
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
```

| Field Name | Default | Description |
| --- | --- | --- |
| callbackId |  | The value to be sent along with submission(Used for keeping the session) |
| title |  | Dialog title |
| submitLabel | "Submit" | Assign the text for the Submit button |
| elements |  | Array of the **Element** |

#### Element Object
| Field Name | Default | Description |
| --- | --- | --- |
| type |  | The field type<br>"text": Text field<br>"textarea": Long text<br>"select": Drop-down menu |
| subtype |  | The keyboard type to be displayed when the type is text<br>"number", "email", "tel", "url" |
| label |  | The field name displayed to the user |
| name |  | The field name to be sent to the command server |
| value |  | Default value in the field (automatically selected when it is set to an option value if the type is select) |
| options |  | The array of **Option** output when the type is select |
| dataSource |  | The data to be output instead of options when the type is select |
| minLength |  | The minimum number of input characters |
| maxLength |  | The maximum number of input characters |
| placeholder |  | A hint shown in the field (disappears when text is typed in the field) |
| hint |  | A hint shown under the field |
| optional | false | Set whether the field is mandatory or not (if false, the field is mandatory) |

#### Option Object

|Field Name|Default|Description|
|---|---|---|
|text||Option text|
|value||The field value to be sent to the command server|

### Submit processing
With the above API, a dialog has been displayed to the user. Then the user fills the dialog and the dialog must be processed.

#### Request from Messenger server to the command server
``` javascript
{
    "type": "dialog_submission",
    "tenant": {
        "id": "1234567891234567891",
        "domain": "guide.dooray.com"
    },
    "channel": {
        "id": "1234567891234567891",
        "name": "Command Guide Channel"
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
        "note": "Part to be noted frequently",
        "important": "true"
    }
}

```

|Field Name|Description|
|---|---|
|type|The type of event which has occurred (dialog_submission)|
|tenant|Information of the tenant where the command-calling user belongs|
|channel|Information of the channel where the command has been called|
|user|Information of the user who has called the command|
|responseUrl|The incoming web hook URL to respond to the command call|
|cmdToken|The token used to call API|
|callbackId|The callback ID assigned to the dialog|
|submission|The object of which key and value are the element name assigned to the dialog and the user-written value, respectively|

#### Response from the command server to Messenger server
There are two cases:

* When there is no error in the user input value, clears the response and then responds with HTTP 200.

* When there is any error, responds with errors including HTTP 200.

``` javascript
{
    errors: [
        {
            name: 'page',
            error: 'The page number cannot exceed 50.'
        }
    ]
}
```

|Field Name|Default|Description|
|---|---|---|
|name||The name of element where errors have been found|
|error||The error message to be output|

---

## Register a command to a chatroom

### Register a command to a chatroom

You can register a command to the 1:1 chat or the group chat where you are participating. There are two ways to open the Add Command window:

First, add a command through the Setting menu on the right top of the Messenger.

![17](http://static.toastoven.net/prod_dooray_messenger/integration/17.png)

Second, input `/` in the input line of the chatroom and click the 'Link Service' button to add a command.

![18](http://static.toastoven.net/prod_dooray_messenger/integration/18.png)

The Add Command window shows the open command or the command you have created. Click 'Add' button on the right side of the desired command to add the command to the chatroom. If there is no command, return to the start page of this document and create a command.

![19](http://static.toastoven.net/prod_dooray_messenger/integration/19.png)

![20](http://static.toastoven.net/prod_dooray_messenger/integration/20.png)

### Open a command

If you want to share cool functions of your commands, set the command to Open. Other members in your organization can add and use the command in the chatroom freely. Even if you change the setting to Private, the command which has already been added can be used by others. If you don't want others to use the command any more, delete the registered command.

---

## Example: Vote command 

### Requirements of the command server

The command server must provide REST API which is operated by command as registered.

|API types|Description|Required |Method|
|------|---|---|---|
|Command Request URL|The URL which will process the command execution request from the user|O|POST|
|Request URL of the Interactive Message|The URL which processes the user's action (button click, drop-down menu selection)|X|POST|
|Optional URL of the Interactive Message|The URL which provides external data through the drop-down menu|X|POST|

### Vote command

As an example, create a vote command which can create a vote in a chatroom and allow users to participate in the vote.
For the example code, see [Github](https://github.com/nhnent/dooray.vote). 

![21](http://static.toastoven.net/prod_dooray_messenger/integration/21.png)

#### API

Use the command request URL and the request URL of the interactive message only.

#### Command execution format

Enter the input format for the user to execute the vote command as follows.

```javascript
/vote {Title} {Item 1} "{Item including blank}" ... {Item n}
```

#### Scenario

1. The user executes a command
2. Displays a confirmation message that a vote has been created is displayed; this message is visible only to the user who has executed the command
3. Click the Create button to display the vote message which can be seen by all members in the chatroom
4. The members in the chatroom will vote by clicking the Vote button
5. The user who has created vote will close the vote
6. Display the vote result

### Request to execute the vote command

The user executes the vote command as follows.

![22](http://static.toastoven.net/prod_dooray_messenger/integration/22_1.png)

The command server receives the JSON data, which include the user-input value, via the command request URL.

``` javascript
{
    "tenantId": "1234567891234567891",
    "tenantDomain": "guide.dooray.com",
    "channelId": "1234567891234567891",
    "channelName": "Command Guide",
    "userId": "1234567891234567891",
    "command": "/vote",
    "text": "Lunch Jajangmyeon Jjamppong\"Sichuan-style sweet and sour pork\"",
    "responseUrl": "https://guide.dooray.com/messenger/api/commands/hook/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "appToken": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "triggerId": "1234567891234.xxxxxxxxxxxxxxxxxxxx"
}
```

|Field Name|Description|
|----|---|
|tenantId|The ID of tenant where the command has been registered|
|tenantDomain|The domain of tenant where the command has been registered|
|channelId|The ID of the chatroom which requests the command|
|channelName|The title of the chatroom which requests the command|
|userId|The ID of the user who has requested the command|
|command|The command name|
|text|The entire text typed by the user|
|responseUrl|The Webhook URL of the chatroom which requests the command|
|appToken|The token of app which registered the command(Used for verifying the request)|
|triggerId|Dialog execution ID|

### Response to the command execution request

![23](http://static.toastoven.net/prod_dooray_messenger/integration/23_1.png)

As a response to the command execution request, a confirmation message is sent and this is only visible to the user who has executed the command. The message is sent the following message to the user in order to provide a button that creates or cancels voting.

``` javascript
{
    "responseType": "ephemeral",
    "text": "Click 'Submit' button to start the vote.",
    "attachments": [
        {
            "title": "Lunch",
            "fields": [
                {
                    "title": "Item 1",
                    "value": "Jajangmyeon",
                    "short": true
                },
                {
                    "title": "Item 2",
                    "value": "Jjamppong",
                    "short": true
                },
                {
                    "title": "Item 3",
                    "value": "Sichuan-style sweet and sour pork",
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
                    "value": "Lunch Jajangmyeon Jjamppong\"Sichuan-style sweet and sour pork\"",
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

### Request the execution of the action

When the user click the Submit button, the following data is sent to the Request URL of the interactive message.

``` javascript
{
    "tenant": {
        "id": "1234567891234567891",
        "domain": "guide.dooray.com"
    },
    "channel": {
        "id": "1234567891234567891",
        "name": "Command Guide Channel"
    },
    "user": {
        "id": "1234567891234567891",
        "name": "Hong Gil Dong"
    },
    "commandName": "/vote",
    "command": "/vote",
    "text": "Lunch Jajangmyeon Jjamppong\"Sichuan-style sweet and sour pork\"",
    "callbackId": "vote",
    "actionText": "Submit",
    "actionValue": "Lunch Jajangmyeon Jjamppong\"Sichuan-style sweet and sour pork\"",
    "appToken": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "cmdToken": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "triggerId": "1234567891234.xxxxxxxxxxxxxxxxxxxx",
    "commandRequestUrl": "https://command.guide.doc/req",
    "channelLogId": "-7386965175150134411",
    "originalMessage": { /* Message Object */ }
}
```

|Field Name|Description|
|----|---|
|callbackId|The ID of the attachment where the user-selected action belongs|
|actionText|The action text selected by the user|
|actionValue|The action value selected by the user|
|commandRequestUrl|Command Request URL|
|channelLogId|Message ID|
|originalMessage|Message received as a previous response|

### Response to action execution

![24](http://static.toastoven.net/prod_dooray_messenger/integration/24_1.png)

As a response to the 'Submit' button, the vote creation message is sent. Since the creation confirmation message is not necessary any more, it will be deleted and a new message will be created.

``` javascript
{
    "responseType": "inChannel", 
    "deleteOriginal": true, 
    "text": "(dooray://1234567891234567891/members/1234567891234567891 \"member\") created the vote!",
    "attachments": [
        {
            "callbackId": "1525223162093-(dooray://1234567891234567891/members/1234567891234567891 \"member\")",
            "title": "Lunch",
            "actions": [
                {
                    "name": "vote",
                    "type": "button",
                    "text": "Jajangmyeon",
                    "value": 0
                },
                {
                    "name": "vote",
                    "type": "button",
                    "text": "Jjamppong",
                    "value": 1
                },
                {
                    "name": "vote",
                    "type": "button",
                    "text": "Sichuan-style sweet and sour pork",
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

|Field Name|Default|Description|
|----|---|---|
|deleteOriginal|false|Whether to delete a previous message or not before creating a new message|
|replaceOriginal|true|Whether to update a previous message or not|

After that, the buttons which the user will click are repetition of the action execution request and the response to that request.
