# Signalgrid CLI Tool

A lightweight Bash CLI for interacting with the Signalgrid API.  
It allows you to test connectivity and send notifications to a channel.

---

## Requirements

- `bash`
- `curl`

---

## Installation

Save the script as:

```bash
signalgrid
```

Make it executable:

```bash
chmod +x signalgrid
```

(Optional) Move it into your PATH:

```bash
mv signalgrid /usr/local/bin/
```

---

## Configuration

Edit the script and set your client key:

```bash
CLIENT_KEY="[your-key-here]"
```

Default configuration inside the script:

- Endpoint: `api.signalgrid.co`
- API Version: `v1`

If no scheme is provided, `https://` is automatically prepended.  
A trailing slash is also automatically ensured.

---

## Usage

```bash
signalgrid [command] [options]
```

---

## Commands

### `ping`

Check connectivity to the configured endpoint.

```bash
signalgrid ping
```

The command returns:

- `OK` if reachable
- `FAIL` otherwise

---

### `help`

Display the help page.

```bash
signalgrid help
```

---

### `send`

Send a notification to a channel.

```bash
signalgrid send [options]
```

#### Required options

```bash
-c, --channel   [Hash]    Channel token
-b, --body      [String]  Notification body
```

#### Optional options

```bash
-s, --severity  [String]  crit | warn | info | success (default: info)
-C, --critical            Mark as critical
-t, --title     [String]  Notification title
-e, --endpoint  [FQDN]    Override endpoint
```

---

## Severity Mapping

Accepted values:

- `crit`
- `warn`
- `info`
- `success`

---

## Examples

Ping default server:

```bash
signalgrid ping
```

Send a notification:

```bash
signalgrid send \
  -c HASH123 \
  -s crit \
  -t "Backup Failed" \
  -b "Disk is full" \
```

Send a critical notification:

```bash
signalgrid send \
  -c HASH123 \
  -s crit \
  -t "Backup Failed" \
  -b "Disk is full" \
  -C
```

