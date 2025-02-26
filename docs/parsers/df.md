[Home](https://kellyjonbrazil.github.io/jc/)

# jc.parsers.df
jc - JSON CLI output utility `df` command output parser

Usage (cli):

    $ df | jc --df

    or

    $ jc df

Usage (module):

    import jc.parsers.df
    result = jc.parsers.df.parse(df_command_output)

Schema:

    [
      {
        "filesystem":        string,
        "size":              string,
        "1k_blocks":         integer,
        "512_blocks":        integer,
        "used":              integer,
        "available":         integer,
        "capacity_percent":  integer,
        "ifree":             integer,
        "iused":             integer,
        "use_percent":       integer,
        "iused_percent":     integer,
        "mounted_on":        string
      }
    ]

Examples:

    $ df | jc --df -p
    [
      {
        "filesystem": "devtmpfs",
        "1k_blocks": 1918820,
        "used": 0,
        "available": 1918820,
        "use_percent": 0,
        "mounted_on": "/dev"
      },
      {
        "filesystem": "tmpfs",
        "1k_blocks": 1930668,
        "used": 0,
        "available": 1930668,
        "use_percent": 0,
        "mounted_on": "/dev/shm"
      },
      {
        "filesystem": "tmpfs",
        "1k_blocks": 1930668,
        "used": 11800,
        "available": 1918868,
        "use_percent": 1,
        "mounted_on": "/run"
      },
      ...
    ]

    $ df | jc --df -p -r
    [
      {
        "filesystem": "devtmpfs",
        "1k_blocks": "1918820",
        "used": "0",
        "available": "1918820",
        "use_percent": "0%",
        "mounted_on": "/dev"
      },
      {
        "filesystem": "tmpfs",
        "1k_blocks": "1930668",
        "used": "0",
        "available": "1930668",
        "use_percent": "0%",
        "mounted_on": "/dev/shm"
      },
      {
        "filesystem": "tmpfs",
        "1k_blocks": "1930668",
        "used": "11800",
        "available": "1918868",
        "use_percent": "1%",
        "mounted_on": "/run"
      },
      ...
    ]


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

    List of Dictionaries. Raw or processed structured data.

## Parser Information
Compatibility:  linux, darwin, freebsd

Version 1.9 by Kelly Brazil (kellyjonbrazil@gmail.com)
