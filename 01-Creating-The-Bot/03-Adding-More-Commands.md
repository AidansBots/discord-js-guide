**Adding More Commands**

A bot with nothing but a single command would be boring, and you probably have a bunch of command ideas floating around in your head already, right? Let's begin, then.

Here's what your message event should currently look like:

```java
client.on('message', message => {
	if (message.content === '!ping') {
		message.channel.send('Pong.');
	}
});
```

Before doing anything else, make a property to store the prefix you've configured. Instead of `const config = ...`, you can destructure the config file to extract the prefix and token variables.

```java
const { prefix, token } = require('./config.json');
// ...
client.login(token);
```

From now on, if you change the prefix or token in your config.json file, it'll change in your bot file as well. You'll be using the prefix variable a lot soon.

**Simple command structure**

You already have an if statement that checks messages for a ping/pong command. Adding other command checks is just as easy; chain an else if to your existing condition.

```java
client.on('message', message => {
	if (message.content === `${prefix}ping`) {
		message.channel.send('Pong.');
	} else if (message.content === `${prefix}beep`) {
		message.channel.send('Boop.');
	}
});
```

There are a few potential issues with this. For example, the ping command won't work if you send !ping test. It will only match !ping and nothing else. The same goes for the other command. If you want your commands to be more flexible, you can do the following:

```java
client.on('message', message => {
	if (message.content.startsWith(`${prefix}ping`)) {
		message.channel.send('Pong.');
	} else if (message.content.startsWith(`${prefix}beep`)) {
		message.channel.send('Boop.');
	}
});
```

Now the ping command will trigger whenever the message starts with !ping! Sometimes this is what you want, but other times, you may want to match only exactly !ping - it varies from case to case, so be mindful of what you need when creating commands.

**Displaying real data**

Let's start displaying some real data. For now, we'll be displaying basic member/server info.

**Server info command**

Make another if statement to check for commands using `server` as the command name. You've already interacted with the Message object via `message.channel.send()`. You get the message object, access the channel it's from, and send a message to it. Just like how `message.channel` gives you the message's channel, `message.guild` gives you the message's server.

```java
client.on('message', message => {
	if (message.content === `${prefix}ping`) {
		message.channel.send('Pong.');
	} else if (message.content === `${prefix}beep`) {
		message.channel.send('Boop.');
	} else if (message.content === `${prefix}server`) {
		message.channel.send(`This server's name is: ${message.guild.name}`);
	}
});
```

If you want to expand upon that command and add some more info, here's an example of what you can do:

```java
client.on('message', message => {
	if (message.content === `${prefix}ping`) {
		message.channel.send('Pong.');
	} else if (message.content === `${prefix}beep`) {
		message.channel.send('Boop.');
	} else if (message.content === `${prefix}server`) {
		message.channel.send(`Server name: ${message.guild.name}\nTotal members: ${message.guild.memberCount}`);
	}
});
```

That would display both the server name and the amount of members in it.

Of course, you can modify this to your liking. You may also want to display the date the server was created or the server's region. You would do those in the same manner–use `message.guild.createdAt` or `message.guild.region`, respectively.

**User info command**

Set up another if statement and use the command name user-info.

```java
client.on('message', message => {
	if (message.content === `${prefix}ping`) {
		message.channel.send('Pong.');
	} else if (message.content === `${prefix}beep`) {
		message.channel.send('Boop.');
	} else if (message.content === `${prefix}server`) {
		message.channel.send(`This server's name is: ${message.guild.name}`);
	} else if (message.content === `${prefix}user-info`) {
		message.channel.send(`Your username: ${message.author.username}\nYour ID: ${message.author.id}`);
	}
});
```

This will display the message author's username (not nickname, if they have one set), as well as their user ID.

And there you have it! As you can see, it's quite simple to add additional commands.

**The problem with `if`/`else if`**

If you don't plan to make more than seven or eight commands for your bot, then using an if/else if chain is sufficient; it's presumably a small project at that point, so you shouldn't need to spend too much time on it. However, this isn't the case for most of us.

You probably want your bot to be feature-rich and easy to configure and develop, right? Using a giant if/else if chain won't let you achieve that; it will only hinder your development process. After you read up on creating arguments, we'll be diving right into something called a "command handler" - code that makes handling commands easier and much more efficient.

Before continuing, here's a small list of reasons why you shouldn't use if/else if chains for anything that's not a small project:

- Takes longer to find a piece of code you want.
- Easier to fall victim to spaghetti code.
- Difficult to maintain as it grows.
- Difficult to debug.
- Difficult to organize.
- General bad practice.

In short, it's just not a good idea. But that's why this guide exists! Go ahead and read the next few pages to prevent these issues before they happen, learning new things along the way.
