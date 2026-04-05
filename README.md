# NavonaSetup
Public setup scripts to start configuration

# Quick Guide

Download the initial setup script

```bash
wget https://raw.githubusercontent.com/Navona-Tech/NavonaSetup/refs/heads/main/Navanoa-Setup

```

or 

```bash
curl https://raw.githubusercontent.com/Navona-Tech/NavonaSetup/refs/heads/main/Navanoa-Setup

```
or use the browser to download it

https://raw.githubusercontent.com/Navona-Tech/NavonaSetup/refs/heads/main/Navanoa-Setup

# Run it

```bash
# If you used the browser to download, the file is your downloads directory
cd <download location>
chmod +x Navanoa-Setup

# Required tools
sudo apt install git python3-git
sudo apt install gh  # required only for --pat mode (or see https://cli.github.com)

# Run with SSH key authentication (default)
./Navanoa-Setup

# Or run with Personal Access Token authentication
./Navanoa-Setup --pat

# Re-run and force update all config values
./Navanoa-Setup -u
```
