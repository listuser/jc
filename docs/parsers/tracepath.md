[Home](https://kellyjonbrazil.github.io/jc/)

# jc.parsers.tracepath
jc - JSON CLI output utility `tracepath` command output parser

Supports `tracepath` and `tracepath6` output.

Usage (cli):

    $ tracepath 1.2.3.4 | jc --tracepath

    or

    $ jc tracepath 1.2.3.4

Usage (module):

    import jc.parsers.tracepath
    result = jc.parsers.tracepath.parse(tracepath_command_output)

Schema:

    {
      "pmtu":                       integer,
      "forward_hops":               integer,
      "return_hops":                integer,
      "hops": [
        {
          "ttl":                    integer,
          "guess":                  boolean,
          "host":                   string,
          "reply_ms":               float,
          "pmtu":                   integer,
          "asymmetric_difference":  integer,
          "reached":                boolean
        }
      ]
    }

Examples:

    $ tracepath6 3ffe:2400:0:109::2 | jc --tracepath -p
    {
      "pmtu": 1480,
      "forward_hops": 2,
      "return_hops": 2,
      "hops": [
        {
          "ttl": 1,
          "guess": true,
          "host": "[LOCALHOST]",
          "reply_ms": null,
          "pmtu": 1500,
          "asymmetric_difference": null,
          "reached": false
        },
        {
          "ttl": 1,
          "guess": false,
          "host": "dust.inr.ac.ru",
          "reply_ms": 0.411,
          "pmtu": null,
          "asymmetric_difference": null,
          "reached": false
        },
        {
          "ttl": 2,
          "guess": false,
          "host": "dust.inr.ac.ru",
          "reply_ms": 0.39,
          "pmtu": 1480,
          "asymmetric_difference": 1,
          "reached": false
        },
        {
          "ttl": 2,
          "guess": false,
          "host": "3ffe:2400:0:109::2",
          "reply_ms": 463.514,
          "pmtu": null,
          "asymmetric_difference": null,
          "reached": true
        }
      ]
    }

    $ tracepath6 3ffe:2400:0:109::2 | jc --tracepath -p -r
    {
      "pmtu": "1480",
      "forward_hops": "2",
      "return_hops": "2",
      "hops": [
        {
          "ttl": "1",
          "guess": true,
          "host": "[LOCALHOST]",
          "reply_ms": null,
          "pmtu": "1500",
          "asymmetric_difference": null,
          "reached": false
        },
        {
          "ttl": "1",
          "guess": false,
          "host": "dust.inr.ac.ru",
          "reply_ms": "0.411",
          "pmtu": null,
          "asymmetric_difference": null,
          "reached": false
        },
        {
          "ttl": "2",
          "guess": false,
          "host": "dust.inr.ac.ru",
          "reply_ms": "0.390",
          "pmtu": "1480",
          "asymmetric_difference": "1",
          "reached": false
        },
        {
          "ttl": "2",
          "guess": false,
          "host": "3ffe:2400:0:109::2",
          "reply_ms": "463.514",
          "pmtu": null,
          "asymmetric_difference": null,
          "reached": true
        }
      ]
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
Compatibility:  linux

Version 1.3 by Kelly Brazil (kellyjonbrazil@gmail.com)
