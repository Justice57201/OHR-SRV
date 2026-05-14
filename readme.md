# Enable Root User Login on Debian

## 1. Set a Root Password

To enable the root account:

```bash
sudo passwd root
```

You will be prompted:

```text
Enter new password:
Retype new password:
```

Example output:

```text
passwd: password updated successfully
```

This unlocks the root account.

---

## 2. Switch to Root

Test the account:

```bash
su -
```

Enter the root password.

Prompt changes from:

```bash
user@debian:~$
```

to:

```bash
root@debian:~#
```

---

## 3. Enable SSH Root Login

Edit the SSH server configuration:

```bash
sudo nano /etc/ssh/sshd_config
```

Find:

```text
PermitRootLogin prohibit-password
```

Change to:

```text
PermitRootLogin yes
```

Save and restart SSH:

```bash
sudo systemctl restart ssh
```

## Done


# Installation

1. Clone this repository:
```bash
cd /opt
git clone https://github.com/Justice57201/HBlink4.git
cd /opt/HBlink4
```

2. Create a virtual environment and activate it:
```bash
python3 -m venv venv
source venv/bin/activate
```

3. Install requirements:
```bash
pip install -r requirements.txt
```

## Configuration

Copy the sample configuration file and modify it for your needs:
```bash
cp config/config_sample.json config/config.json
cp dashboard/config_sample.json dashboard/config.json
```

See the [Configuration Guide](docs/configuration.md) for complete documentation of all settings.

## Running

### Production (systemd services)
For production deployments with automatic startup, see [SYSTEMD.md](SYSTEMD.md).

### Development
```bash
# Start all services together
./run_all.sh

# Or start services separately:
python3 run.py              # HBlink4 server
python3 run_dashboard.py    # Web dashboard (in another terminal)
```

Access the dashboard at http://localhost:8080. See [Dashboard Documentation](dashboard/README.md) for features and configuration.

## Documentation

Comprehensive documentation is available in the `docs/` directory:

- **[Configuration Guide](docs/configuration.md)** - Complete configuration reference with all settings explained
- **[Dashboard README](dashboard/README.md)** - Dashboard features and usage
- **[Systemd Service Installation](SYSTEMD.md)** - Production deployment with automatic startup
- **[Connecting Repeaters](docs/connecting_to_hblink4.md)** - How to connect repeaters to HBlink4
- **[Call Routing](docs/routing.md)** - Inbound/outbound filtering, contention, and assumed slot state
- **[DMRD Translation](docs/dmrd_translation.md)** - Per-repeater slot/TGID remap and rf_src override (RPTO extended syntax)
- **[Stream Tracking](docs/stream_tracking.md)** - How DMR transmission streams are managed
- **[Stream Tracking Diagrams](docs/stream_tracking_diagrams.md)** - Visual walkthrough of stream lifecycle and contention
- **[Hang Time](docs/hang_time.md)** - Preventing conversation interruption
- **[Protocol Specification](docs/protocol.md)** - HomeBrew DMR protocol details
- **[Integration Guide](docs/integration.md)** - Using HBlink4 as a module
- **[Logging](docs/logging.md)** - Log management and rotation
- **[Roadmap / TODO](docs/TODO.md)** - Planned work (performance monitoring, multi-hop outbound, config UI)
- **[OpenBridge Analysis](docs/OPENBRIDGE_ANALYSIS.md)** - Reference analysis for future OpenBridge support
- **[Release Notes v4.8.0](docs/RELEASE_NOTES_v4.8.0.md)** - Current release — unit (private) call routing, DMR data-call classification, RPTO empty-slot fix
- **[Release Notes v4.7.0](docs/RELEASE_NOTES_v4.7.0.md)** - asyncio, DMRA, outbound connections, DMRD translation

## License

Copyright (C) 2016-2025 Cortney T. Buffington, N0MJS n0mjs@me.com
This project is licensed under the GNU GPLv3 License - see the LICENSE file for details.

## Acknowledgments

- Original HBlink3 by Cort Buffington, N0MJS
- The MMDVM and DMR community
