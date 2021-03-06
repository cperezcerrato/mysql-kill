mysql-kill-query
================

This script let you find MySQL queries by patterns, execution time, or both  and kill them without restarting MySQL daemon.

**WARNING**: Use this script at your own risk. Kill some queries like UPDATES, INSERT, DELETE, etc can produce data/consistence loss.

Installation
============

Checkout the script:

```bash
$ wget --no-check-certificate -O /usr/local/bin/mysql-kill-query https://raw.github.com/cperezcerrato/mysql-kill-query/master/mysql-kill-query 
```

Set permissions:
```bash
$ chmod +x /usr/local/bin/mysql-kill-query
```
Set path (if necesary), and special MySQL options in the file /usr/local/bin/mysql-kill-query.

Variables:
```bash
MYSQL_BIN=""    # Path to MySQL binary command. If not set, fill with 'which mysql'
MYSQL_OPTS=""   # Optional params admited by MySQL binary, like -h (host), -s (socket), etc.
```
Feel free to put the script in the path you want.

Usage
=====

Kill MySQL queries that execution time is above the time (in seconds) specified by command line arguments.

```bash    
mysql-kill-query [ -p PATTERN ] [ -t TIME(in seconds) ] [-l /path/to/file.log ].

    -p  PATTERN (optional) Find PATTERN in MySQL queries.
    -t  TIME (optional) time in seconds, default 15.
    -i  ID (optional) Query ID to kill (specifying -p or -t is not needed using this).
    -l  logfile (optional) File to log killed queries.
    -s  Show running queries.
```
Examples:

Kill all queries that contains "exampledb"
```bash
$ mysql-kill-query -p exampledb
```

Kill all queries that contains "exampledb" and execution time is greater than 40 seconds and log in file /tmp/mysql-kill-queryed.log
```bash
$ mysql-kill-query -p exampledb -t 40 -l /tmp/mysql-kill-queryed.log
```

Kill all queries whose execution time highter 15 seconds (default)
```bash
$ mysql-kill-query
```
Kill all queries whose execution time is greater than 3 seconds:
```bash
$ mysql-kill-query -t 3
```

Kill query with id equal to XXXX:
```bash
$ mysql-kill-query -i XXXX
```

Show running queries in MySQL:
```bash
$ mysql-kill-query -s
```
