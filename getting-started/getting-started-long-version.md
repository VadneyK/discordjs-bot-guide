# Getting Started - Long Version

So, you want to write a bot and you know some JavaScript, or maybe even node.js. You want to do cool things like a music bot, tag commands, random image searches, the whole shebang. Well you're at the right place!

{% hint style="info" %}
**This is the long version** with a whole lot of useless blabbering text, jokes and explanations.  
TL;DR \(short\) versions: [Windows](getting-started-windows-tl-dr.md), [Linux](getting-started-linux-tl-dr.md)
{% endhint %}

This tutorial will get you through the first steps of creating a bot, configuring it, making it run, and adding a couple of commands to it.

## Step 1: Creating your App and Bot account

The first step in creating a bot is to create your own Discord _application_. The bot will use the Discord API, which requires the creation of an account for authentication purposes. Don't worry though, it's super simple.

### Creating the App account

To create the application, head to the [Discord.com Application Page](https://discord.com/developers/applications/me). Assuming you're logged in \(if not, do so now\), you'll reach a page that looks like this:

![](../.gitbook/assets/image%20%281%29.png)

Click on \(you guessed it!\) **Create an application**. This brings you to the following page, in which you should simply enter a name for the _application_ \(this will be the inital bot username\). You don't really need a description or icon, but feel free to add one. Click **Save Changes** which will create the application itself.

![](../.gitbook/assets/image%20%283%29.png)

The **Client ID** on this page will be your bot's user ID. Nothing else on this page is relevant, it is not used in your bot \(however, you can enter a description

### Create the bot account

After creating the application, we need to create the **Bot User**. Go to the **Bot** section on the left, then click on **Add Bot**, then **Yes, Do it**.

![](../.gitbook/assets/image%20%282%29.png)

There's a few things you can change here.

* `Username` to change your bot's username on Discord \(this can also be done through code\).
* `Icon` to change the bot's avatar \(can also be done with discord.js\)
* `Token` This is your bot's token, which will be used when connecting to discord. See [the section below](getting-started-long-version.md#getting-your-bot-token) for details.
* `Public bot` This toggles the ability for other users to add your bot to their server. You can turn this on during development. 
* `Require Oauth2 Code Grant` Don't check this. Just, don't. It's not useful to you and will cause problems if you turn it on. 

### Add your bot to a server

Ok so, this might be a bit early to do this but it doesn't really matter - even if you haven't written a single line of code for your bot, you can already "invite" it to a server. In order to add a bot, you need _Manage Server_ permissions on that server. This is the **only** way to add a bot, it cannot use invite links or any other methods.

To generate the link, click on **Oauth2** in the app page, and scroll down to **Scopes**. Check the `BOT` scope to generate a link.

Usually, bots are invited with specific _permissions_ which are given to the bot's role on the server. This is optional, but you can set thos permissions in the **Bot** page, scrolling down to the **Bot Permissions** section. Check any permissions your bot requires. This modifies the invite link above, which you can then share.

Once you have the link, you can copy it to a browser window and visit it. When you do this, You get shown a window letting you choose the server where to add the bot, simply select the server and click **Authorize**.

![](../.gitbook/assets/gs4.png)

{% hint style="info" %}
You need to be logged in to Discord on the browser with your account to see a list of servers. You can only add a bot to servers where you have **Manage Server** permissions.
{% endhint %}

### Getting your Bot Token

{% hint style="danger" %}
Alright so, **big flashy warning**, **PAY ATTENTION**. This next part is really, really important: Your bot's **token** is meant to be **SECRET**. It is the way by which your bot authenticates with the Discord server in the same way that you login to Discord with a username and password. **Revealing your token is like putting your password on the internet**, and anyone that gets this token can use **your** bot connection to do things. Like delete all the messages on your server and ban everyone. If your token ever reaches the internet, **change it immediately**. This includes putting it on pastebin/hastebin, having it in a public github repository, displaying a screenshot of it, anything. **GOT IT? GOOD!**
{% endhint %}

With that warning out of the way, on to the next step. The Token, as I just mentioned, is the way in which the bot authenticates. To get it, go to the **Bot** section of the app page, then click **Copy** to copy it to the clipboard. You can also _view_ your token here if you wish:

![NEVER SHARE YOUR TOKEN! This cannot be overstated.](https://github.com/AnIdiotsGuide/discordjs-bot-guide/tree/cb3b11a9a73a0635199dc4de420c4e9ff49ab2f2/.gitbook/assets/image%20%284%29.png)

## Step 2: Getting your coding environment ready

This might go beyond saying but I'll say it anyway: You can't just start shoving bot code in notepad.exe and expect it to work. In order to use discord.js you will need a couple of things installed. At the very least:

* Get Node.js version 7.6 or higher \(earlier versions are not supported\). [Download for windows](https://nodejs.org/en/download/) or if you're on a linux distro, via [package manager](https://nodejs.org/en/download/package-manager/).
* Get an actual code editor. Don't use notepad or notepad++, they are not sufficient. [VS Code](https://www.visualstudio.com/en-us/products/code-vs.aspx) , [Sublime Text 3](https://www.sublimetext.com/3) and [Atom](https://atom.io/) are often recommended.

{% hint style="info" %}
An alternative: [c9.io](https://c9.io/). I personally appreciate c9.io as it's a full VPS with a great editor \(Ace\) and installing node, discord.js and all dependencies, then running the bot, is easy. You can't host it there, but you can certainly develop there. _This is not an endorsement_.
{% endhint %}

Once you have the required software, the next step is to prepare a _space_ for your code. Please don't just put your files on your desktop it's... unsanitary. If you have more than one hard drive or partition, you could create a special place for your development project. Mine, for example, is `D:\devel\` , and my bot is `d:\devel\omnicbot\` . Once you've created a folder, open your CLI \(command line interface\) in that folder. Linux users, you know how. Windows users, here's a trick: SHIFT+RightClick in the folder, then choose the "secret" command **Open command window here**. Magic!

And now ready for the next step!

## Installing Discord.js

So you have your CLI ready to go, in an empty folder, and you just wanna start coding. Alright, hold on one last second: let's install discord.js. But first we'll initialize this folder with NPM, which will ensure that any installed module will be here, and nowhere else. Simply run `npm init -y` and then hit Enter. A new file is created called `package.json`, [click here](https://docs.npmjs.com/files/package.json) for more info about it.

And now we install Discord.js through NPM, the Node Package Manager:

`npm install discord.js@11.6.4`

![](http://i.imgur.com/Gad8L2G.gif)

This will take a couple of heartbeats and display a lot of things on screen. Unless you have a big fat red message saying it didn't work, or package not found, or whatever, you're good to go. If you look at your folder, you'll notice that there's a new folder created here: `node_modules` . This contains all the installed packages for your project.

## Getting your first bot running

{% hint style="info" %}
I honestly consider that if you don't understand the code you're about to see, coding a bot might not be for you. If you do not understand the following sample, please go to [CodeAcademy](https://www.codecademy.com/learn/javascript) and learn Javascript first. I beg of you: stop, drop, and roll.
{% endhint %}

Okay finally, we're ready to start coding. \o/ Let's take a look at the most basic of examples, the ping-pong bot. Here's the code in its entirety:

```javascript
const Discord = require("discord.js");
const client = new Discord.Client();

client.on("ready", () => {
  console.log("I am ready!");
});

client.on("message", (message) => {
  if (message.content.startsWith("ping")) {
    message.channel.send("pong!");
  }
});

client.login("SuperSecretBotTokenHere");
```

{% hint style="info" %}
The variable `client` here is used an an example to represent the [&lt;Client&gt;](https://discord.js.org/#/docs/main/stable/class/Client) class. Some people call it `bot`, but you can technically call it whatever you want. I recommend sticking to `client` though!
{% endhint %}

Okay let's just... actually get this guy to work, because this is literally **a functional bot**. So let's make it run!

1. Copy that code and paste it in your editor.
2. Replace the string in the `client.login()` function with _your_ token
3. Save the file as `mybot.js`.
4. In the CLI \(which should still be in your project folder\) type the following command: `node mybot.js`

If all went well \(hopefully it did\) your bot is now connected to your server, it's in your userlist, and ready to answer all your commands... Well, at least, _one_ command: `ping`. In its current state, the bot will reply "pong!" to any message that starts with, _exactly_, `ping`. Let's demonstrate!

![](../.gitbook/assets/gs6.png)

Success! You now have a bot running! As you probably realize by now I could probably blabber on from here, showing you a bunch of stuff. But the scope of this tutorial is completed, so I'll shut up now! Ciao!

## The Next Step?

Now that you have a basic, functional bot, it's time to start adding new features! Head on over to [Your First Bot](../first-bot/your-first-bot.md) to continue on your journey with adding new commands and features!

## Addendum: Getting help and Support

Before you start getting support from Discord servers to help you with your bot, I strongly advise taking a look at the following, very useful, resources.

* [Discord.js v11 Documentation](https://discord.js.org/#/docs/main/v11/) : For the love of all that is \(un\)holy, **read the documentation**. Yes, it will be alien at first if you are not used to "developer documentation" but it contains a whole lot of information about each and every feature of the API. Combine this with the examples above to see the API in context.
* [An Idiot's Guide](https://www.youtube.com/c/AnIdiotsGuide) is another great channel with more material. York's guides are great, and he continues to update them.
* [Evie.Codes on Youtube](https://www.youtube.com/channel/UCvQubaJPD0D-PSokbd5DAiw): If you prefer video to words, Evie's youtube series \(which is good, though no longer maintained with new videos!\) gets you started with bots.
* [An Idiot's Guide Official Server](https://discord.gg/vXVxsAjSMF): The official server for An Idiot's Guide. Full of friendly helpful users!
* [Discord.js Official Server](https://discord.gg/bRCvFy9): The official server has a number of competent people to help you, and the development team is there too!

