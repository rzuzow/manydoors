# Manydoors Doorbot

ManyLabs has a collaborative DoorBot!  No one owns it; we all manage it together, from this page.

Purpose: Record and share tap-in, tap-out actions of members (with a ISO 14443A keyfob/card) and document workspace usage.

## Getting Started
1. Get a keyfob or keycard (if you have one already, you can use it)
2. Add your rfid number and name/alias to https://github.com/jhpoelen/manydoors/blob/master/ids.csv (ask for help if this is hard for you)
3. Tap-in and Tap-out when entering and leaving ManyLabs by placing your keyfob on the inside/outside facing coils on the door.
4. See your enter/exit actions on the Slack Channel

## features

1. use rfid to record entry/exit at the manylabs door.
2. automatically updates ids from this github repo when new ones are available
3. keeps a local event log on the pi
4. posts a enter/exit events on the [#door channel of manylabs slack](https://manylabs.slack.com/archives/door/)

# Code setup/ service maintenance

* Login to pi using ```ssh pi@door.local``` (ask for location and access credentials on Slack)
* (if new setup) clone github repo using ```git clone https://github.com/jhpoelen/manydoors.git access_control```
* (if new setup) create a file ```access_control.ini``` with content like:
* (if existing) cd access_control
* (if existing) do whenever you need to do, probably ```git pull --rebase``` to get latest changes
``` 
[slack.com]
Token=yourtoken
```
* create symlink to start service ```sudo ln -s /home/pi/rfid/access_control/access_control.conf /etc/init/access_control.conf```
* restart service using ```sudo service access_control restart```
* edit crontab for synching github repo ```crontab -e```
* add ```* * * * * cd /home/pi/rfid/access_control && git pull --rebase```

