---
id: what-is-cloudcord
title: What is CloudCord?
sidebar_label: What is CloudCord?
---

CloudCord is a service that allows anyone to create their own Discord bots with no programming knowledge required. It deploys your bot onto the cloud, Google Cloud specifically - in the same region and zone as Discord's servers which enables you to have insanely fast interaction with your bot. We've also designed our infrastructure and systems to be highly available, recovering from any errors that may occur within Discord or CloudCord.

It splits bot creation into logical [core concepts](core-concepts) which make it easy to understand the flow of data between your bot, Discord and outside services.

CloudCord also has advanced and realtime monitoring which gives you insight on how your bot's performing, who's using it and when they're using it.

We've also had developers in mind while developing CloudCord - we know the current standards for Discord bot development and hosting are annoying and require maintenance - e.g. keeping your bot online when Discord goes down or has hiccups, having to run a VM, having to keep that VM up all the time, and often paying for resources you don't need. With CloudCord, you can use our custom scripting (coming soon) or [HTTP Post action](actions/http-post) to create stateless Discord bots, not having to worry about the gateway connection or errors. We do all that for you.

## The Console
The console is the gateway to CloudCord - it allows you to do everything from deploying and configuring to monitoring your bots. It's located at https://console.cloudcord.io.

### Home (/)
The home page allows you to see all of your bots deployed on CloudCord and perform simple actions on them. There's also a button in the top right to deploy new bots.

### Deploy (/new)
The deploy page allows you to deploy Discord bots onto CloudCord by providing the authentication token.

### Billing (/billing)
The billing page allows you to see your current account balance, past payments, and allows you to top up your account using either PayPal or a debit/credit card. For debit/credit card processing we use [Stripe](https://stripe.com) to process all payments.

### Bot: Overview (/bots/:botId)
The bot overview page allows you to see various statistics about your bot as well as streamed realtime events.

### Bot: Guilds (/bots/:botId/guilds)
The guilds page allows you to see what Discord servers your bot is in and allows you to perform certain actions on them, like leaving a guild.

### Bot: Commands (/bots/:botId/commands)
The commands page shows the custom commands you've added to your bot, and allows you to toggle or edit the command.

### Bot: Command Editor (/bots/:botId/commands/:command)
The command editor page allows you to create, edit and delete custom commands for your bot.

#### Command Name
The command name is always followed by your bot's prefix by default and is what triggers your command when mentioned at the start of a message in a Discord text channel. For example, if there was a bot had `!` as it's prefix and had a command named `test`, the command would be triggered by sending `!test` within a Discord text channel.

#### Actions
You can add multiple actions you want the command to run when executed. See [here](core-concepts/#actions) for more details.

### Bot: Modules (/bots/:botId/modules)
The modules page shows you your currently enabled modules, allowing you to configure them and also shows you other modules you can add to your bot that you don't currently have enabled. Please note that some of these modules may be Pro-plan only (you'll see a star next to the name if so).

### Bot: Module Config Editor (/bots/:botId/modules/:moduleId)
The module editor allows you to edit specific details about a module and it's commands. You can usually set what permissions are required for a module's command to be executed, customize what messages the command sends when executed and toggle the command on & off.

### Bot: Plans (/bots/:botId/plans)
The plans page allows you to upgrade to a higher premium plan, as long as you have balance in your CloudCord account.

### Bot: Settings (/bots/:botId/settings)
The settings page allows you to configure and tune miscellaneous things about your bot that don't fit in the other pages.

#### Bot Prefix
The bot prefix is what is used globally within your custom commands and modules to prefix commands. For example, if I had a prefix of `!` and a command named `test`, I'd trigger that command by sending `!test` into a Discord text channel. Bots on the Pro plan can set their prefix to whatever they like.

#### Presence Message
The presence message is what's displayed under your bot's name on the Discord member list (e.g. `Playing cloudcord.io`). If your bot is on the Pro plan, you can set this to whatever you like.