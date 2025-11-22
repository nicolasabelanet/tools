# 🧰 Tools

Manage your development tools using a clean, reproducible,
**symlink-based tools system** powered by **GNU Stow**.\
This repository provides a convention-driven layout where each directory
maps directly to its destination in your `$HOME`, allowing safe
installation, removal, and updates without polluting your filesystem.

## 🧠 Overview

This tools setup is built around a few core principles:

- **Declarative filesystem layout:** The directory structure inside
  the repo mirrors its final placement in `$HOME`.
- **Symlink-based installation:** GNU Stow manages all tools by
  creating symlinks instead of copying files.
- **Zero interference:** Stow ensures no accidental overwrites and
  keeps your environment portable and maintainable.

When installed via Stow, this layout cleanly symlinks into `$HOME`,
e.g.:

    ~/.local/bin/tmux-switch-session -> ~/tools/.local/bin/tmux-switch-session

## 📦 Installation

### 1. Clone the repository

```bash
cd ~
git clone https://github.com/nicolasabelanet/tools.git
```

### 2. Install the `.local` package (scripts, utilities)

```bash
cd ~/tools
stow .local
```

This creates symlinks for every script in:

    tools/.local/bin/

so they appear in:

    ~/.local/bin/

## 🧪 Verifying the Installation

Ensure `~/.local/bin` is on your `$PATH`:

```bash
echo $PATH | grep -q "$HOME/.local/bin" && echo "OK" || echo "MISSING"
```

If missing, add this to your shell:

```bash
export PATH="$HOME/.local/bin:$PATH"
```

Then reload:

```bash
source ~/.zshrc
```

Validate that your scripts resolve correctly:

```bash
which tmux-switch-session
```

## ⚙️ Development Workflow

To add a new script:

1.  Place it into:

        tools/.local/bin/

2.  Make it executable:

    ```bash
    chmod +x .local/bin/my-script
    ```

3.  Re-stow the package:

    ```bash
    stow .local
    ```

Stow will update the symlinks automatically.
