# wg-keychain-export

Export WireGuard tunnel configurations from the macOS Keychain to wg-quick compatible `.conf` files.

## Requirements

- macOS
- WireGuard for macOS installed (configs stored in Keychain)
- `/usr/bin/security` (included with macOS)

## Installation

```bash
chmod +x wg-keychain-export
```

Optionally copy to a directory on your `PATH`:

```bash
cp wg-keychain-export /usr/local/bin/
```

## Usage

```bash
wg-keychain-export [OPTIONS]
```

### Options

| Option | Description |
|--------|-------------|
| `--keychain PATH` | Keychain database file (default: `~/Library/Keychains/login.keychain-db`) |
| `--output DIR` | Output directory (default: `./wg-quick`) |
| `--tunnel NAME` | Export only the named tunnel |
| `--list` | List available tunnels without exporting |
| `-h, --help` | Show help |

### Examples

Export all tunnels to `./wg-quick/`:

```bash
./wg-keychain-export
```

List tunnels without exporting:

```bash
./wg-keychain-export --list
```

Export a single tunnel:

```bash
./wg-keychain-export --tunnel myvpn
```

Use a custom keychain and output directory:

```bash
./wg-keychain-export --keychain ~/other.keychain-db --output ~/wg-quick
```

## Output

Each tunnel is written as `{tunnel-name}.conf` in the output directory with file permissions `0600`.

Keychain entries are identified by:

- Service: `com.wireguard.macos`
- Label prefix: `WireGuard Tunnel: `

For example, a keychain entry labeled `WireGuard Tunnel: myvpn` becomes `myvpn.conf`.

## Keychain access

WireGuard stores tunnel configs as generic passwords with ACLs restricted to the WireGuard app. The first time you export, macOS will prompt for Keychain access for each tunnel.

To avoid repeated prompts, open **Keychain Access**, find the WireGuard entries, and grant your terminal or script permanent access.

## Limitations

- **Keychain ACLs**: You must approve access to each tunnel's secret.
- **`dump-keychain` parsing**: Listing tunnels relies on parsing undocumented `security dump-keychain` output; this may need updates after macOS changes.
- **No code signing**: Unlike a signed app, a shell script cannot inherit WireGuard's Keychain trust; expect authorization dialogs.

## License

MIT — see [LICENSE](LICENSE).
