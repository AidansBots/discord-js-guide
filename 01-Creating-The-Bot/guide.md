**Creating the bot file**

Open up your preferred code editor (whether it be Visual Studio Code (opens new window), Atom (opens new window), Sublime Text (opens new window), or any other editor of your choice) and create a new file. If you're brand new and aren't sure what to use, go with Visual Studio Code.

We suggest that you save the file as index.js, but you may name it whatever you wish, as long as it ends with .js.

**Logging in to Discord**

Once you've created a new file, do a quick check to see if you have everything setup correctly. Copy & paste the following code into your file and save it. Don't worry if you don't understand it right away—we explain more in-depth after this.

```java
const Discord = require('discord.js');
const client = new Discord.Client();

client.once('ready', () => {
	console.log('Ready!');
});

client.login('your-token-goes-here');
```

Head back to your console window, type in node your-file-name.js, and press enter. If you see the Ready! message after a few seconds, you're good to go! If not, try going back a few steps and make sure you followed everything correctly.

**Start-up code explained**

Here's the same code with comments, so it's easier to understand what's going on.

```java
// require the discord.js module
const Discord = require('discord.js');

// create a new Discord client
const client = new Discord.Client();

// when the client is ready, run this code
// this event will only trigger one time after logging in
client.once('ready', () => {
	console.log('Ready!');
});

// login to Discord with your app's token
client.login('your-token-goes-here');
Although it's not a lot, it's good to know what each bit of your code does. But, as it currently is, this won't do anything. You probably want to add some commands that run whenever someone sends a specific message, right? Let's get started on that, then!
```

**Listening for messages**

First, make sure to close the process in your console. You can do so by pressing Ctrl + C inside the console. Go back to your code editor and add the following piece of code above the client.login() line.

```java
client.on('message', message => {
	console.log(message.content);
});
```
Notice how the code uses .on rather than .once like in the ready event. This means that it can trigger multiple times. Save the file, go back to your console, and start the process up again. Whenever a message is sent inside a channel your bot can access, the console will log the message's content. Go ahead and test it out!

**Replying to messages**

Logging to the console is great and all, but it doesn't provide any feedback for the end-user. Let's create a basic ping/pong command before you move on to making real commands. Remove the console.log(message.content) line from your code and replace it with the following:

```java
client.on('message', message => {
	if (message.content === '!ping') {
		// send back "Pong." to the channel the message was sent in
		message.channel.send('Pong.');
	}
});
```
Restart your bot and then send !ping to a channel your bot has access to. If all goes well, you should see something like this:

You've successfully created your first Discord bot command! Exciting stuff, isn't it? This is only the beginning, so let's move on to making some more commands.
