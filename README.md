# ImpactJS GameJolt API

A simple plugin to comunicate your Impact game with GameJolt's API service. Currently supports trophies, highscores and user authentication.

## Installation and usage

Install the plugin by putting the `gamejolt.js` file into the `plugins` directory of your project.

Require the plugin in your main.js file.

	ig.module(
		'game.main'
	)
	.requires(
		'impact.game',
		'plugins.gamejolt'
	)
	...

Spawn the api class in your Game class init() function. Since it's a singleton, you can spawn it multiple times in different Game classes.

	Splash = ig.Game.extend({
		api: null,

		init: function() {
			this.api = new ig.GameJoltApi();
		}
	});

Configure the plugin by editing the gamejolt.js file.

	ig.GameJoltApi = ig.Class.extend({
    	/* fill in these - variable for every game */
    	_game_id: 0, // your game id from game management
    	_game_key: '', // you private key from game management
        _highscores: [
	        {name: 'Description', id: 0}, // description isn't used, put the leaderboard id as id
        ],
        _trophies: [
        	{name: 'Description', id: 0} // description isn't used, put the trophy id as id
        ],
    ...

Use it in your code (user authentication is automatic)

	ig.game.api.sendTrophy(0); // 0 is the index of the trophy in _trophies above
	ig.game.api.sendHighscore(0, 1234); // 0 is the index of the highscore in _highscores above, 1234 is points 

## Notes

* Don't forget to set up your trophies and leaderboards on the GameJolt's site in game management
* Leaderboards don't show up on the game's page until there's at least one score submitted to the primary highscore table

## Demo

You can check out the plugin in action at http://gamejolt.com/games/puzzle/duel-blockers/18844/