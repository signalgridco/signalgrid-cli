# Signalgrid CLI Tool

A lightweight Bash CLI for interacting with the Signalgrid API.  
It allows you to test connectivity and send notifications to a channel using simple command-line arguments.

## Requirements

- Bash
- curl

## Installation

1. Save the script as `signalgrid`
2. Make it executable:

   chmod +x signalgrid

3. (Optional) Move it to your PATH:

   mv signalgrid /usr/local/bin/

## Configuration

Edit the script and set your client key:

CLIENT_KEY="[your-key-here]"

Default configuration:

- Endpoint: api.signalgrid.co
- API Version: v1

The script automatically prepends `https://` if no scheme is provided and ensures proper URL formatting.

## Usage

signalgrid [command] [options]

### Commands

ping  
Check connectivity to the configured endpoint.

help  
Show the help page.

send  
Send a notification to a channel.

## Global Options

-e, --endpoint [FQDN]  
Override the API endpoint (default: api.signalgrid.co)

## Send Command Options

-c, --channel [Hash]  
Channel token (required)

-b, --body [String]  
Notification body text (required)

-s, --severity [String]  
crit, warn, info, success (default: info)

-C, --critical  
Mark notification as critical (optional)

-t, --title [String]  
Notification title (optional)

## Examples

Ping the default server:

signalgrid ping

Send a critical notification:

signalgrid send -c HASH123 -s crit -t "Backup Failed" -b "Disk is full" -C

Send to a custom endpoint:

signalgrid send -c HASH123 -b "Hello" -e dev.signalgrid.co

## Severity Mapping

The CLI accepts:

- crit
- warn
- info
- success

The value is normalized to uppercase and sent to the API as:

type=CRIT | WARN | INFO | SUCCESS

Invalid severity values default to `info`.

## Exit Codes

- 0 on success
- 1 on validation or command error

## Notes

- The script uses `curl --form-string` to send multipart form data.
- The API endpoint used for notifications is:

  {endpoint}/v1/push
