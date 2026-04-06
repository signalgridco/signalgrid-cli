# Signalgrid push CLI Tool

A lightweight Bash CLI for interacting with the Signalgrid API.  
It allows you to test connectivity and send notifications to a channel.

## Installation

Save the script as:

```bash
curl -fsSL https://signalgrid.co/install.sh | bash
```

---

## Configuration

Once you provide your client-key to the install script, everything is set up.

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

## Examples

Ping default server:

```bash
signalgrid ping
```

Send a notification:

```bash
signalgrid send \
  -c 098f6bcd4621d373cade4e832627b4f6 \
  -s crit \
  -t "Backup Failed" \
  -b "Disk is full" \
```

Send a critical notification:

```bash
signalgrid send \
  -c 098f6bcd4621d373cade4e832627b4f6 \
  -s crit \
  -t "Backup Failed" \
  -b "Disk is full" \
  -C
```

