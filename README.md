# Home Assistant ntfy-send

## Background

In order to be able to send notifications from Home Assistant with Actions,
I wanted to write a script to handle this since the integration does not

## Features

- Ability to use a custom server using "-s SERVERURL"
- Ability to send actions with "-A view,Button Label 1,URL1;view,Button Label 2,URL2;"
- Ability to use /config/.netrc to authentication with custom SERVERURL
- Replace strings in command like %ha% and %token% with secrets:
  home_assistant_base_url and ntfy_send_long_lived_token, respectively

## Installation

1. Copy ntfy-send to /config/bin/ntfy-send on your Home Assistant Server
1. Create a new shell-command in /config/configuration.yaml

```
shell_command:
  ntfy_send: >
    /config/bin/ntfy-send -t '{{ topic | default("testing-mike-phone") }}'
      -m '{{ message }}'
      {{ "-T '" + title | default("") | string + "'" if title else "" }}
      {{ "-g '" + tags | default("") | string + "'" if tags else "" }}
      {{ "-p '" + priority | default("") | string + "'" if priority else "" }}
      {{ "-A '" + actions | default("") | string + "'" if actions else "" }}
      {{ "-a '" + attach | default("") | string + "'" if attach else "" }}
      {{ "-c '" + click | default("") | string + "'" if click else "" }}
      {{ "-i '" + icon | default("") | string + "'" if icon else "" }}
```
