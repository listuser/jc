[Home](https://kellyjonbrazil.github.io/jc/)

# jc.parsers.airport
jc - JSON CLI output utility `airport -I` command output parser

The `airport` program can be found at `/System/Library/PrivateFrameworks/Apple80211.framework/Versions/Current/Resources/airport`.

Usage (cli):

    $ airport -I | jc --airport

    or

    $ jc airport -I

Usage (module):

    import jc.parsers.airport
    result = jc.parsers.airport.parse(airport_command_output)

Schema:

    {
      "agrctlrssi":        integer,
      "agrextrssi":        integer,
      "agrctlnoise":       integer,
      "agrextnoise":       integer,
      "state":             string,
      "op_mode":           string,
      "lasttxrate":        integer,
      "maxrate":           integer,
      "lastassocstatus":   integer,
      "802_11_auth":       string,
      "link_auth":         string,
      "bssid":             string,
      "ssid":              string,
      "mcs":               integer,
      "channel":           string
    }

Examples:

    $ airport -I | jc --airport -p
    {
      "agrctlrssi": -66,
      "agrextrssi": 0,
      "agrctlnoise": -90,
      "agrextnoise": 0,
      "state": "running",
      "op_mode": "station",
      "lasttxrate": 195,
      "maxrate": 867,
      "lastassocstatus": 0,
      "802_11_auth": "open",
      "link_auth": "wpa2-psk",
      "bssid": "3c:37:86:15:ad:f9",
      "ssid": "SnazzleDazzle",
      "mcs": 0,
      "channel": "48,80"
    }

    $ airport -I | jc --airport -p -r
    {
      "agrctlrssi": "-66",
      "agrextrssi": "0",
      "agrctlnoise": "-90",
      "agrextnoise": "0",
      "state": "running",
      "op_mode": "station",
      "lasttxrate": "195",
      "maxrate": "867",
      "lastassocstatus": "0",
      "802_11_auth": "open",
      "link_auth": "wpa2-psk",
      "bssid": "3c:37:86:15:ad:f9",
      "ssid": "SnazzleDazzle",
      "mcs": "0",
      "channel": "48,80"
    }


## info
```python
info()
```
Provides parser metadata (version, author, etc.)

## parse
```python
parse(data, raw=False, quiet=False)
```

Main text parsing function

Parameters:

    data:        (string)  text data to parse
    raw:         (boolean) output preprocessed JSON if True
    quiet:       (boolean) suppress warning messages if True

Returns:

    Dictionary. Raw or processed structured data.

## Parser Information
Compatibility:  darwin

Version 1.4 by Kelly Brazil (kellyjonbrazil@gmail.com)
