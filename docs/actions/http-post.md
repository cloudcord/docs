---
id: http-post
title: Action: HTTP Post
sidebar_label: HTTP Post
---

**Action ID:** `HTTP_POST`

The HTTP Post action allows you to forward a Discord event payload, like a message creation to a HTTP server via the HTTP POST method - it also allows you to reply with another CloudCord Action to execute.

## Action Parameters

| Parameter | Description                                | Example Data                                             | Required? |
|-----------|--------------------------------------------|----------------------------------------------------------|-----------|
| url       | The HTTP URL that CloudCord should POST to | https://api.my-cool-domain.party/cloudcord_hooks/command | true      |

## What gets sent to your HTTP server?
We'll send the Discord data payload within the body, with a few headers to help you identify the request.

### Body
The body of the request will be a Discord payload - it depends what triggers the action, but here's an example for the `MESSAGE_CREATE` event (e.g. when a command triggers the action). The Discord docs for this payload are located [here](https://discordapp.com/developers/docs/resources/channel#message-object)

```
{
   type: 0,
   tts: false,
   timestamp: '2019-06-10T19:27:35.568000+00:00',
   pinned: false,
   nonce: '587724563647823872',
   mentions: [],
   mention_roles: [],
   mention_everyone: false,
   member: {
      roles: ["ROLE_ID"],
      premium_since: '2019-06-04T20:07:49.737000+00:00',
      nick: null,
      mute: false,
      joined_at: '2019-01-16T14:08:09.578000+00:00',
      deaf: false
   },
   id: '587724564486946800',
   embeds: [],
   edited_timestamp: null,
   content: '>testhttp',
   channel_id: '535097935923380200',
   author: {
      username: 'Phineas',
      id: '94490510688792580',
      discriminator: '0001',
      avatar: 'a_ddd493dd817c50288868a0b8b5869ac8'
   },
   attachments: [],
   guild_id: '535097935923380200'
}
```

### Headers
| Header              	| Description                                                	| Example                                            	|
|---------------------	|------------------------------------------------------------	|----------------------------------------------------	|
| X-CloudCord-BotID   	| The Discord ID of the bot that sent the request            	| 581651542361374721                                 	|
| X-CloudCord-Emitter 	| The emitter ID of the command or module that sent the data 	| command:pinghttp                                   	|
| X-CloudCord-APIBase 	| The base URL of our API - this is for a future feature     	| https://api-dev.cloudcord.io                       	|
| X-CloudCord-Node    	| The CloudCord node identifier that executed the action     	| discord-gateway-gs-659576497-qw9bz                 	|
| User-Agent          	| The CloudCord user agent, see the example ->               	| cloudcord/1.1 (discord-gateway-gs-659576497-qw9bz) 	|
| Content-Type        	| Will always be application/json                            	| application/json                                   	|


## Replying to the Request
**Note: your server must respond within 5 seconds or we'll dismiss it**

You can reply to the request with a status code of `204 No Content` to do nothing, or you can respond with an action object for CloudCord to execute.

### Example: replying to the request with a SEND_MESSAGE_TO_CHANNEL action

Here's what we're responding to the request with:
```json
{
  "action": "SEND_MESSAGE_TO_CHANNEL",
  "parameters": {
    "channel_id": "579428153286590477",
    "message": "Pong!"
  }
}
```
This will then trigger CloudCord to execute the action, in this case it'll cause the bot to send a message to a channel with the ID of `579428153286590477` with the contents of "Pong!"