[Home](https://kellyjonbrazil.github.io/jc/)

# jc.parsers.rpm_qi
jc - JSON CLI output utility `rpm -qi` command output parser

Works with `rpm -qi [package]` or `rpm -qia`.

The `..._epoch` calculated timestamp fields are naive (i.e. based on the local time of the system the parser is run on)

The `..._epoch_utc` calculated timestamp fields are timezone-aware and is only available if the timezone field is UTC.

Usage (cli):

    $ rpm -qia | jc --rpm-qi

    or

    $ jc rpm -qia

Usage (module):

    import jc.parsers.rpm_qi
    result = jc.parsers.rpm_qi.parse(rpm_qi_command_output)

Schema:

    [
      {
        "name":                     string,
        "epoch":                    integer,
        "version":                  string,
        "release":                  string,
        "architecture":             string,
        "install_date":             string,
        "install_date_epoch":       integer,          # naive timestamp
        "install_date_epoch_utc":   integer,          # Aware timestamp if timezone is UTC
        "group":                    string,
        "size":                     integer,
        "license":                  string,
        "signature":                string,
        "source_rpm":               string,
        "build_date":               string,
        "build_epoch":              integer,          # naive timestamp
        "build_epoch_utc":          integer,          # Aware timestamp if timezone is UTC
        "build_host":               string,
        "relocations":              string,
        "packager":                 string,
        "vendor":                   string,
        "url":                      string,
        "summary":                  string,
        "description":              string
      }
    ]

Examples:

    $ rpm -qia | jc --rpm-qi -p
    [
      {
        "name": "make",
        "epoch": 1,
        "version": "3.82",
        "release": "24.el7",
        "architecture": "x86_64",
        "install_date": "Wed 16 Oct 2019 09:21:42 AM PDT",
        "group": "Development/Tools",
        "size": 1160660,
        "license": "GPLv2+",
        "signature": "RSA/SHA256, Thu 22 Aug 2019 02:34:59 PM PDT, Key ID 24c6a8a7f4a80eb5",
        "source_rpm": "make-3.82-24.el7.src.rpm",
        "build_date": "Thu 08 Aug 2019 05:47:25 PM PDT",
        "build_host": "x86-01.bsys.centos.org",
        "relocations": "(not relocatable)",
        "packager": "CentOS BuildSystem <http://bugs.centos.org>",
        "vendor": "CentOS",
        "url": "http://www.gnu.org/software/make/",
        "summary": "A GNU tool which simplifies the build process for users",
        "description": "A GNU tool for controlling the generation of executables and other...",
        "build_epoch": 1565311645,
        "build_epoch_utc": null,
        "install_date_epoch": 1571242902,
        "install_date_epoch_utc": null
      },
      {
        "name": "kbd-legacy",
        "version": "1.15.5",
        "release": "15.el7",
        "architecture": "noarch",
        "install_date": "Thu 15 Aug 2019 10:53:08 AM PDT",
        "group": "System Environment/Base",
        "size": 503608,
        "license": "GPLv2+",
        "signature": "RSA/SHA256, Mon 12 Nov 2018 07:17:49 AM PST, Key ID 24c6a8a7f4a80eb5",
        "source_rpm": "kbd-1.15.5-15.el7.src.rpm",
        "build_date": "Tue 30 Oct 2018 03:40:00 PM PDT",
        "build_host": "x86-01.bsys.centos.org",
        "relocations": "(not relocatable)",
        "packager": "CentOS BuildSystem <http://bugs.centos.org>",
        "vendor": "CentOS",
        "url": "http://ftp.altlinux.org/pub/people/legion/kbd",
        "summary": "Legacy data for kbd package",
        "description": "The kbd-legacy package contains original keymaps for kbd package...",
        "build_epoch": 1540939200,
        "build_epoch_utc": null,
        "install_date_epoch": 1565891588,
        "install_date_epoch_utc": null
      },
      ...
    ]

    $ rpm -qia | jc --rpm-qi -p -r
    [
      {
        "name": "make",
        "epoch": "1",
        "version": "3.82",
        "release": "24.el7",
        "architecture": "x86_64",
        "install_date": "Wed 16 Oct 2019 09:21:42 AM PDT",
        "group": "Development/Tools",
        "size": "1160660",
        "license": "GPLv2+",
        "signature": "RSA/SHA256, Thu 22 Aug 2019 02:34:59 PM PDT, Key ID 24c6a8a7f4a80eb5",
        "source_rpm": "make-3.82-24.el7.src.rpm",
        "build_date": "Thu 08 Aug 2019 05:47:25 PM PDT",
        "build_host": "x86-01.bsys.centos.org",
        "relocations": "(not relocatable)",
        "packager": "CentOS BuildSystem <http://bugs.centos.org>",
        "vendor": "CentOS",
        "url": "http://www.gnu.org/software/make/",
        "summary": "A GNU tool which simplifies the build process for users",
        "description": "A GNU tool for controlling the generation of executables and other..."
      },
      {
        "name": "kbd-legacy",
        "version": "1.15.5",
        "release": "15.el7",
        "architecture": "noarch",
        "install_date": "Thu 15 Aug 2019 10:53:08 AM PDT",
        "group": "System Environment/Base",
        "size": "503608",
        "license": "GPLv2+",
        "signature": "RSA/SHA256, Mon 12 Nov 2018 07:17:49 AM PST, Key ID 24c6a8a7f4a80eb5",
        "source_rpm": "kbd-1.15.5-15.el7.src.rpm",
        "build_date": "Tue 30 Oct 2018 03:40:00 PM PDT",
        "build_host": "x86-01.bsys.centos.org",
        "relocations": "(not relocatable)",
        "packager": "CentOS BuildSystem <http://bugs.centos.org>",
        "vendor": "CentOS",
        "url": "http://ftp.altlinux.org/pub/people/legion/kbd",
        "summary": "Legacy data for kbd package",
        "description": "The kbd-legacy package contains original keymaps for kbd package..."
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
Compatibility:  linux

Version 1.4 by Kelly Brazil (kellyjonbrazil@gmail.com)
