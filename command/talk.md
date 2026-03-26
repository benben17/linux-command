talk
===

Talk to another user

## Description

The **talk command** is a client tool for the talk server, allowing users to chat with other users. It is easy to use: as long as you know the address of the person you wish to talk to, you can invite them to a conversation.

### Syntax

```shell
talk (parameters)
```

### Parameters

*   User: Specify the user to chat with.
*   Terminal: Specify the user's terminal.

### Examples

For example, if user `jdx` logged into host `rs6000.cic.test.com` wants to talk to user `wangxz` logged into host `tirc.cs.test.com`, they can enter:

```shell
talk wangxz@tirc.cs.test.com
```

The Talk Daemon on the internet will send a message inviting `wangxz` to chat. The following message will appear on `wangxz`'s screen along with a notification bell:

```shell
Message from Talk_Daemon@tirc.cs.test.com at 21:44 …
talk: connection requested by jdx@rs6000.cic.test.com
talk: respond with:  talk jdx@rs6000.cic.test.com
```

User `wangxz` should then follow the prompt and enter:

```shell
talk jdx@rs6000.cic.test.com
```

Once the connection is established, the two users can begin chatting. Both terminals will display **[Connection established]** and ring. The screen will be split into two halves by a horizontal line: the top half displays your own input, and the bottom half displays the other person's input. Both users can type simultaneously, and their input will be displayed in real-time.

While typing, you can press **BACKSPACE** to correct the previous character, **CTRL+w** to delete a whole word, or **CTRL+U** to delete an entire line. Additionally, **CTRL+L** refreshes the screen. To end the conversation, either party can press **CTRL+C**. It is polite to say "goodbye" before closing. When the program ends, the following message is displayed:

```shell
[Connection closing. Exiting]
```

A talk request might not always succeed. If the other person is not logged in, the program will display:

```shell
[Your party is not logged on]
```

If the user is logged in but does not respond, `talk` will send an invitation every 10 seconds and display:

```shell
[Ringing your party again]
```

You can press **CTRL+C** to terminate the request. Sometimes you might see:

```shell
[Checking for invitation on caller’s machine]
```

This indicates that the `talk` programs on the two machines are incompatible. In this case, you can try the `ntalk` or `ytalk` commands.

If you are doing urgent work (like editing an email) and do not want to be interrupted by talk invitations, use:

```shell
mesg n
```

To temporarily refuse messages. Anyone trying to talk to you will see:

```shell
[Your party is refusing messages]
```

Remember to turn message reception back on with `mesg y` once you finish your work.
