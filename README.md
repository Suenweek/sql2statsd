# sql2statsd

`sql2statsd` is a CLI utility that queries SQL database and posts
results to
[StatsD](https://github.com/etsy/statsd)
based on a provided YAML config files.


## Installation

`virtualenv` recommended.

- From Github:
    ```
    pip install -e git+https://github.com/Suenweek/sql2statsd#egg=sql2statsd
    ```


## Usage

`sql2statsd` is intended to be run as a scheduled task (e.g. a `cron`
job).

1. Create YAML config files based on a schemas provided below.
2. Place them in OS-specific default locations (run `sql2statsd --help`
    to find them out) or use custom locations.
3. Run:
    ```
    sql2statsd <JOB_CONFIG>
    ```

Passing custom db servers and statsd servers config files as
parameters each time is tedious, so you may want to specify
`SQL2STATSD_DB_SERVERS` and `SQL2STATSD_STATSD_SERVERS` env vars
instead.


## Config schema

### Db servers

```yaml
<str>:  # Db server name
    host: <str>
    port: <int>
    user: <str>
    password: <str>
```

### Statsd servers

```yaml
<str>:  # Stats server name
    host: <str>
    port: <int>
```

### Job

```yaml
db_server: <str>  # Database server name
db_name: <str>
statsd_server: <str>  # Statsd server name
stat: <str>
query: <str>
```
