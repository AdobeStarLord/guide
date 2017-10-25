# Common questions

## Legend

* `<client>` is a placeholder for the Client object, such as `const client = new Discord.Client();`.
* `<message>` is a placeholder for the Message object, such as `client.on('message', message => { ... });`.
* `<guild>` is a placeholder for the Guild object, such as `<message>.guild` or `<client>.guilds.get('<id>')`.

## Administrative

### How do I ban a user?

```js
const user = <message>.mentions.users.first();
<guild>.ban(user);
```

### How do I kick a user?

```js
const user = <message>.mentions.users.first();
<guild>.kick(user);
```

### How do I add a role to a guild member?

```js
const role = <guild>.roles.find('name', '<role name>');
const member = <message>.mentions.members.first();
member.addRole(role);
```

## Miscellaneous

### How do I set my playing status?

```js
<client>.user.setGame('<game>');
```

**Notes:**

* If you would like to set your playing status upon startup, you must place the `<client>.user.setGame()` method in a `ready` event listener (`client.on('ready', () => {});`).

* If you're using a selfbot to change your playing status, you won't be able to view the status change, but other users will.

### How do I prompt the user for additional input?

```js
<message>.channel.send('Please enter more input.').then(() => {
	const filter = m => <message>.author.id === m.author.id;

	<message>.channel.awaitMessages(filter, { time: 60000, maxMatches: 1, errors: ['time'] })
		.then(messages => {
			<message>.channel.send(`You've entered: ${messages.first().content}`);
		})
		.catch(() => {
			<message>.channel.send('You did not enter any input!');
		});
});
```

<p class="tip">If you want to learn more about this syntax or want to learn about reaction collectors as well, check out [this dedicated guide page for collectors](/creating-your-bot/collectors)!</p>