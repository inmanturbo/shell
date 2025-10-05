# shell

## Usage

Clone the repository

```bash
git clone https://github.com/inmanturbo/shell
```

Add to path

zsh

```zsh
grep -qxF 'export PATH="$PATH:$HOME/shell"' ~/.zshrc || echo 'export PATH="$PATH:$HOME/shell"' >> ~/.zshrc
```

bash
```bash
grep -qxF 'export PATH="$PATH:$HOME/shell"' ~/.bashrc || echo 'export PATH="$PATH:$HOME/shell"' >> ~/.bashrc
```

Make all scripts in the ~/shell folder executable

```bash
find ~/shell -type f ! -name "*.*" -exec chmod +x {} \;
```

Reload your shell

```bash
exec "$SHELL"
```

---

### Shell Programs (scripts)

- [i3-split-tabs](#i3-split-tabs)
- [valet-opcache](#valet-opcache)
- [vgrep](#vgrep)
- [vclassdef](#vclassdef)
- [vclassuse](#vclassuse)

---

### i3-split-tabs

Opens Nautilus file manager and Chrome browser side by side in tabbed containers.

#### Usage
```bash
i3-split-tabs
```

This will:
1. Open Nautilus file manager in your home directory
2. Split horizontally for side-by-side layout
3. Open Chrome with google.com in a new window
4. Convert both windows to tabbed containers (split v + layout tabbed)
5. Focus returns to the left container

---

### valet-opcache

A helper script to manage **PHP OPcache** settings for Laravel Valet (Linux).  
Lets you toggle between **development** and **production** OPcache configurations,  
and also create the config files automatically.

#### Features
- `install` command: Creates `10-opcache-dev.ini` and `10-opcache-prod.ini` for the current PHP version.
- **Preserves existing configs** — will not overwrite unless you pass `--force`.
- `dev` mode: Enables development-friendly OPcache settings that automatically detect file changes.
- `prod` mode: Enables production OPcache settings with maximum performance.
- `status` command: Shows current OPcache key settings.
- Automatically clears Laravel caches when in a Laravel project directory.
- Automatically reloads PHP-FPM after changes.

#### Usage
```bash
valet-opcache install         # Creates dev/prod configs (skips if already exist)
valet-opcache install --force # Overwrites dev/prod configs if they exist
valet-opcache dev             # Switch to development OPcache settings
valet-opcache prod            # Switch to production OPcache settings
valet-opcache status          # Show current OPcache settings
```

### First-time setup

```bash
valet-opcache install
```

This will:

1. Detect the current PHP version used by CLI/FPM.
2. Create the two config files in /etc/php/<version>/fpm/conf.d/ (unless they already exist).
3. Symlink 10-opcache.ini to the dev config by default.
4. Restart PHP-FPM.

#### Dev Mode

- `opcache.validate_timestamps=1`
- `opcache.revalidate_freq=2`

Ensures code changes are reflected without manually clearing OPcache.

Prod Mode

- `opcache.validate_timestamps=0`
- `opcache.revalidate_freq=0`

Maximizes performance by not checking file modification times.

### vgrep
Search only **Valet-linked** project paths for a pattern.

```bash
vgrep 'App\\Models\\User'          # search PHP/Blade in all Valet projects
vgrep -i 'class Team' jetstream    # case-insensitive; only projects with "jetstream" in path
vgrep -a 'window.Alpine'           # search all files (not just PHP/Blade)
```

### vclassdef
Find a class definition by name.

```bash
vclassdef Team
```

### vclassuse
Find usages of a fully-qualified class name (escape backslashes).

```bash
vclassuse 'App\\Models\\User'
```
