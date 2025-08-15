# shell

## Usage

Clone the repository

```bash
git clone https://github.com/inmanturbo/shell
```

Add to path

zsh

```zsh
echo 'export PATH=$PATH:/home/$USER/shell' | tee -a ~/.zshrc
```

bash
```bash
echo 'export PATH=$PATH:/home/$USER/shell' | tee -a ~/.bashrc
```
---

### Shell Programs (scripts)

- [valet-opcache](#valet-opcache)

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
