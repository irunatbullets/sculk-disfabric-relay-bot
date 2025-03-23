# Sculk

Sculk is a discord bot that is designed to interact with my version of DisFabric. It currently supports three commands.

- `!uptime` will let you know how long sculk has been running.
- `!console ban <mc username> <reason>`
- `!console pardon <mc username>`
- `!channel add <mc_server_channel_id>`
- `!channel remove <mc_server_channel_id>`

Upon reading the `!console` commands from a staff channel, sculk will relay the commands to any defined Minecraft server channel and then report the result back to the staff channel.

## Setup

I removed `requirements.txt` because every system I've installed this on has had dependency issues, so the first step is to install `pip` and then:

```
pip install discord
pip install json5
```

Along with a `BOT_TOKEN` environment variable set, Sculk needs a `config.json5` file which contains the following (note the comments, which make this file a bit easier to maintain when you have lots of minecraft servers):

```
{
  "channels": {
    "mc_servers": [
      12345678, // Channel name
      91234567, // Channel name
      87654321  // Channel name
    ],
    "staff": 567345678,
    // How long to wait for a response from mc_servers
    "timeout": 2.0
  },
  "roles": [
    898760987, // OP
    358853689  // Moderator
  ]
}
```

I create a service in `/etc/systemd/system/sculk.service` like:

```
[Unit]
Description=Sculk
After=network.target

[Service]
Type=simple
User=murray
WorkingDirectory=/path/to/sculk-disfabric-relay-bot/
ExecStart=/usr/bin/python3 /path/to/sculk-disfabric-relay-bot/sculk.py
Restart=always
Environment="BOT_TOKEN=<paste your bot token here>"

[Install]
WantedBy=multi-user.target
```

Then I run the following to make sure it runs at startup.

```
sudo systemctl start sculk.service
sudo systemctl enable sculk.service
```
 
