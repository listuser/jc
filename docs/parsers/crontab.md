[Home](https://kellyjonbrazil.github.io/jc/)

# jc.parsers.crontab
jc - JSON CLI output utility `crontab -l` command output and crontab file parser

Supports `crontab -l` command output and crontab files.

Usage (cli):

    $ crontab -l | jc --crontab

    or

    $ jc crontab -l

Usage (module):

    import jc.parsers.crontab
    result = jc.parsers.crontab.parse(crontab_output)

Schema:

    {
      "variables": [
        {
          "name":             string,
          "value":            string
        }
      ],
      "schedule": [
        {
          "occurrence"        string,
          "minute": [
                              string
          ],
          "hour": [
                              string
          ],
          "day_of_month": [
                              string
          ],
          "month": [
                              string
          ],
          "day_of_week": [
                              string
          ],
          "occurrence":       string,
          "command":          string
        }
      ]
    }

Examples:

    $ crontab -l | jc --crontab -p
    {
      "variables": [
        {
          "name": "MAILTO",
          "value": "root"
        },
        {
          "name": "PATH",
          "value": "/sbin:/bin:/usr/sbin:/usr/bin"
        },
        {
          "name": "SHELL",
          "value": "/bin/bash"
        }
      ],
      "schedule": [
        {
          "minute": [
            "5"
          ],
          "hour": [
            "10-11",
            "22"
          ],
          "day_of_month": [
            "*"
          ],
          "month": [
            "*"
          ],
          "day_of_week": [
            "*"
          ],
          "command": "/var/www/devdaily.com/bin/mk-new-links.php"
        },
        {
          "minute": [
            "30"
          ],
          "hour": [
            "4/2"
          ],
          "day_of_month": [
            "*"
          ],
          "month": [
            "*"
          ],
          "day_of_week": [
            "*"
          ],
          "command": "/var/www/devdaily.com/bin/create-all-backups.sh"
        },
        {
          "occurrence": "yearly",
          "command": "/home/maverick/bin/annual-maintenance"
        },
        {
          "occurrence": "reboot",
          "command": "/home/cleanup"
        },
        {
          "occurrence": "monthly",
          "command": "/home/maverick/bin/tape-backup"
        }
      ]
    }

    $ cat /etc/crontab | jc --crontab -p -r
    {
      "variables": [
        {
          "name": "MAILTO",
          "value": "root"
        },
        {
          "name": "PATH",
          "value": "/sbin:/bin:/usr/sbin:/usr/bin"
        },
        {
          "name": "SHELL",
          "value": "/bin/bash"
        }
      ],
      "schedule": [
        {
          "minute": "5",
          "hour": "10-11,22",
          "day_of_month": "*",
          "month": "*",
          "day_of_week": "*",
          "command": "/var/www/devdaily.com/bin/mk-new-links.php"
        },
        {
          "minute": "30",
          "hour": "4/2",
          "day_of_month": "*",
          "month": "*",
          "day_of_week": "*",
          "command": "/var/www/devdaily.com/bin/create-all-backups.sh"
        },
        {
          "occurrence": "yearly",
          "command": "/home/maverick/bin/annual-maintenance"
        },
        {
          "occurrence": "reboot",
          "command": "/home/cleanup"
        },
        {
          "occurrence": "monthly",
          "command": "/home/maverick/bin/tape-backup"
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
Compatibility:  linux, darwin, aix, freebsd

Version 1.6 by Kelly Brazil (kellyjonbrazil@gmail.com)
