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
sudo apt install gh  # GitHub CLI, the setup offers to install it if missing (see https://cli.github.com)

# Run it (asks for the authentication method on the first run)
./Navanoa-Setup

# Force a Personal Access Token (HTTPS) - recommended
./Navanoa-Setup --pat

# Or force an SSH key instead
./Navanoa-Setup --ssh

# Re-run and force update all config values (also replaces an expired token)
./Navanoa-Setup -u
```

The chosen method is remembered in `github.authmethod` in `~/.gitconfig`, so later runs
keep using it unless `--pat` / `--ssh` is given.

# GitHub authentication with a Personal Access Token

With `--pat` all GitHub repositories - `navona-scripts`, `NavonaSetup` and your project
repositories - are accessed over HTTPS with a Personal Access Token:

- the token is stored in `~/.git-credentials` (mode 600) and `credential.helper=store` is enabled
- git is configured to rewrite the SSH urls to HTTPS
  (`url.https://github.com/.insteadOf git@github-navona-tech:`), so existing clones and the
  nv* scripts that use the `github-navona-tech` host alias keep working unchanged
- the `gh` CLI is authenticated with the same token
- access to `navona-scripts` and `NavonaSetup` is verified before the setup continues

Create a fine-grained token at https://github.com/settings/tokens?type=beta with
"Resource owner" set to `Navona-Tech`, then grant:

| Repository | Access | Why |
| --- | --- | --- |
| `navona-scripts` | at least **read** (Contents: Read-only) | cloned/pulled by the setup and the nv* scripts |
| `NavonaSetup` | at least **read** (Contents: Read-only) | this setup script |
| any repository you work on | **read and write** (Contents: Read and write) | needed to push branches, commit and release |

The token can also be supplied in the `GITHUB_TOKEN` environment variable:

```bash
GITHUB_TOKEN=github_pat_xxx ./Navanoa-Setup --pat
```

When a token expires, re-run `./Navanoa-Setup -u` (or `--pat`) and paste a new one.
Note that git removes a rejected token from `~/.git-credentials`, so it has to be entered again.

# GitHub authentication with an SSH key

With `--ssh` the setup generates the `github-navona-tech` key, adds it to `~/.ssh/config`
and prints the public key to be registered as a deploy key with write permission. Any
HTTPS url rewrite left by a previous PAT setup is removed.
