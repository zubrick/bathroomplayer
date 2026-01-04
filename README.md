# bathroomplayer
![BathroomPlayer](./bathroomplayer.jpg)

M5Stack core S3 Home Assistant media player controller using esphome
for when I'm in my bathroom listening to music on my sonos speaker.
It works with any media_player entity in homeassistant, and it can
also be somewhere else than in you bathroom.

Inspired and with some code borrowed from the Bento device from SmartyVan: https://gist.github.com/SmartyVan/9583deff2d1281fb714d711ee8e83a78

To be a bit future-proof I went with the S3 version, but it should
work similiarly with the core2

I used the M5Stack Core S3 SE coupled with a battery backpack and the
charger base.

I also made a version compatible with the Espressif ESP32-S3-Box3 for
a desktop use.

## Configuration

Configuration for ESPHome is done with a yaml code that would resemble this:

```yaml
substitutions:
  devicename: bathroomplayer
  upper_devicename: Bathroom Player
  mediaplayer: media_player.bathroom
  hahost: "http://your-ha-ip-or-hostname:8123"

wifi:
  ssid: !secret wifi_ssid
  password: !secret wifi_password

  ap:
    ssid: ${upper_devicename} Fallback
    password: !secret wifi_password

ota:
  platform: esphome
  password: !secret ota_password

api:
  encryption:
    key: !secret api_key

packages:
  bathroomplayer:
    url: https://github.com/zubrick/bathroomplayer
    ref: main  # optional
    files: [ bathroomplayer-common.yaml, bathroomplayer-cores3-base.yaml ]
    refresh: 10s  # optional
```

replace `bathroomplayer-cores3-base.yaml` with
`bathroomplayer-box3-base.yaml` to use the Espressif ESP32-S3-Box3 instead
