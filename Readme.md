# Sculk

## Setup

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
