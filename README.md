# pywit

`pywit` is the Python SDK for [Wit.ai](http://wit.ai).

## Install

Using `pip`:
```bash
pip install wit
```

From source:
```bash
git clone https://github.com/wit-ai/pywit
pip install .
```

## Usage

See the `examples` folder for examples.

## API

### Versioning

The default API version is `20220622`.
You can target a specific version by setting the env variable `WIT_API_VERSION`.

### Overview

`pywit` provides a Wit class with the following methods:
* `message` - the Wit [message API](https://wit.ai/docs/http/20220622#get-intent-via-text-link)
* `speech` - the Wit [speech API](https://wit.ai/docs/http/20220622#post--speech-link)
* `dictation` - the Wit [dictation API](https://wit.ai/docs/http/20220622#post--dictation-link)
* `interactive` - starts an interactive conversation with your bot

### Wit class

The Wit constructor takes the following parameters:
* `access_token` - the access token of your Wit instance

A minimal example looks like this:

```python
from wit import Wit

client = Wit(access_token)
client.message('set an alarm tomorrow at 7am')
```

### .message()

The Wit [message API](https://wit.ai/docs/http/20220622#get-intent-via-text-link).

Takes the following parameters:
* `msg` - the text you want Wit.ai to extract the information from

Example:
```python
resp = client.message('what is the weather in London?')
print('Yay, got Wit.ai response: ' + str(resp))
```

### .speech()

The Wit [speech API](https://wit.ai/docs/http/20220622#post--speech-link).

Takes the following parameters:
* `audio_file` - a file handler opened in binary mode
* `headers` - (optional) the dict of headers (e.g. "Content-Type")

Example:
```python
resp = None
with open('test.wav', 'rb') as f:
  resp = client.speech(f, {'Content-Type': 'audio/wav'})
print('Yay, got Wit.ai response: ' + str(resp))
```

### .dictation()

The Wit [dictation API](https://wit.ai/docs/http/20220622#post--dictation-link).

Takes the following parameters:
* `audio_file` - a file handler opened in binary mode
* `headers` - (optional) the dict of headers (e.g. "Content-Type")

Example:
```python
resp = None
with open('test.wav', 'rb') as f:
  resp = client.dictation(f, {'Content-Type': 'audio/wav'})
print('Yay, got Wit.ai response: ' + str(resp))
```

### .interactive()

Starts an interactive conversation with your bot.

Example:
```python
client.interactive()
```

See the [docs](https://wit.ai/docs) for more information.


### Logging

Default logging is to `STDOUT` with `INFO` level.

You can set your logging level as follows:
``` python
from wit import Wit
import logging
client = Wit(token)
client.logger.setLevel(logging.WARNING)
```

You can also specify a custom logger object in the Wit constructor:
``` python
from wit import Wit
client = Wit(access_token=access_token, logger=custom_logger)
```

See the [logging module](https://docs.python.org/2/library/logging.html) and
[logging.config](https://docs.python.org/2/library/logging.config.html#module-logging.config) docs for more information.


## License

The license for pywit can be found in LICENSE file in the root directory of this source tree.


## Terms of Use

Our terms of use can be found at https://opensource.facebook.com/legal/terms.


## Privacy Policy

Our privacy policy can be found at https://opensource.facebook.com/legal/privacy.
