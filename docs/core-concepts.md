---
id: core-concepts
title: Core Concepts
sidebar_label: Core Concepts
---

This page explains the building-blocks and components of CloudCord.

## Bots
A bot is represented by a Discord user ID, and are deployed by using the console

## Modules
A module is a pluggable component you can add to a bot. They can do things like register and listen to commands, listen to specific gateway events or listen to events outside Discord.

## Commands
Commands have specific names, or IDs - globally prefixed by a "command prefix" which are tied to an Action or a list of Actions.

### Execution
A Command is executed when a user types the command prefix, followed by the command name in a Discord channel where the bot has read permissions, and all inhibitors return true.

### Inhibitors
An inhibitor is a function which gets checked and needs to return true before a command is executed. A command can hold multiple inhibitors, our current inhibitors are listed below.

#### Permission Checking
The permission checking inhibitor checks the command's required permissions, set by the user or by a module, before executing. If the permission doesn't match, then this inhibitor will return `false` with a message about the permission required to use the command.

#### NSFW Channel Checking
If a command is marked as NSFW, this inhibitor will check the channel the command's being executed in, and, if not NSFW, will return `false` with a message explaining that the command needs to be run in a non-NSFW channel.


## Actions
An action is a function which runs an arbitrary function, usually being a Discord action like sending a message to a channel. Actions can be called by Commands or Modules.