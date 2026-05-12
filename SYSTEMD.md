# HBlink4 Systemd Service Installation

This directory contains systemd service files for running HBlink4 and its dashboard as system services.

## Service File

- `hblink4.service` - Main HBlink4 DMR server

## Installation

### 1. Install the service files

Copy the service file to systemd's system directory:

```bash
sudo cp hblink4.service /etc/systemd/system/
```

### 2. Reload systemd

Tell systemd to reload its configuration:

```bash
sudo systemctl daemon-reload
```

### 3. Enable services (optional)

To start the service automatically at boot:

```bash
sudo systemctl enable hblink4
```

### 4. Start the service

```bash
sudo systemctl start hblink4
```

## Service Management

### Check service status

```bash
sudo systemctl status hblink4
```

### View logs

```bash
# View logs for HBlink4
sudo journalctl -u hblink4 -f

# View logs for dashboard
sudo journalctl -u hblink4-dash -f

# View last 100 lines
sudo journalctl -u hblink4 -n 100
```

### Stop service

```bash
sudo systemctl stop hblink4
```

### Restart service

```bash
sudo systemctl restart hblink4
```

### Disable autostart

```bash
sudo systemctl disable hblink4
```

## Security Features

Both services include security hardening:
- `NoNewPrivileges=true` - Prevents privilege escalation
- `PrivateTmp=true` - Isolates /tmp directory

## Troubleshooting

### Service won't start

Check the status and logs:
```bash
sudo systemctl status hblink4
sudo journalctl -u hblink4 -n 50
```

Common issues:
- Virtual environment not found: Check path in `ExecStart=`
- Permission errors: Ensure user/group are correct
- Config file errors: Check HBlink4 configuration files
- Port conflicts: Another service using the same ports

### Dashboard can't connect to HBlink4

1. Ensure HBlink4 is running: `sudo systemctl status hblink4`
2. Check dashboard config points to correct socket/host
3. Check logs: `sudo journalctl -u hblink4-dash -n 50`

