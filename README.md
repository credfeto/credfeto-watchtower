# credfeto-watchtower

Docker Compose configuration for running [Watchtower](https://github.com/nicholas-fedor/watchtower) to keep the host's containers up to date.

## Configuration

Settings are read from environment variables, which can be set in a `.env` file on the host alongside `docker-compose.yml`.

| Variable                            | Default        | Description                                                         |
|-------------------------------------|----------------|---------------------------------------------------------------------|
| `WATCHTOWER_SCHEDULE`               | `0 54 * * * *` | Cron expression controlling when Watchtower checks for new images.  |
| `WATCHTOWER_NOTIFICATIONS_HOSTNAME` | _(none)_       | Hostname reported in Watchtower notifications.                      |

### Schedule

`WATCHTOWER_SCHEDULE` uses a 6-field cron expression with seconds as the first field:

```text
second minute hour day-of-month month day-of-week
```

The default `0 54 * * * *` runs once an hour at 54 minutes past the hour. To override it, add a line to the host's `.env` file, for example:

```text
WATCHTOWER_SCHEDULE=0 0 3 * * *
```

### Image cleanup

`WATCHTOWER_CLEANUP` is always enabled, so Watchtower removes the old image after updating a container to a new one. It is not configurable.
