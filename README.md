#roomba

Control your Roomba robot using it's onboard serial interface

##Usage:

You must have a serial connection to Roomba's serial interface (exposed via 
the mini-din connector at 5v TTL signal levels).  The Roomba speaks a protocol 
called ROI described 
[here](http://www.irobot.com/images/consumer/hacker/Roomba_SCI_Spec_Manual.pdf).


##Example:

	var Roomba = require('../roomba.js').Roomba

	var bot = new Roomba({
	    sp: { path: '/dev/ttyAMA0', options: { baudrate: 57600 }},
	    update_freq: 200
	});

	bot.once('ready', function () {
		console.log('spinning up');
		bot.send({ cmd: 'DRIVE', data: [500, -1] });
	});

	bot.on('sense', function (sensors) {
		if (sensors.bump.right || sensors.bump.left) {
			console.log('bump detected');
			// stop spinning
			bot.send({ cmd: 'DRIVE', data: [0, -1] });
		}
	});

##TODO:

see issues.

##License:

MIT.
