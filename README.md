# HTTrack — Website Copier

## What is HTTrack?

HTTrack is a free, open-source offline browser utility that allows you to download an entire website from the Internet to a local directory. It recursively builds all directories, fetching HTML pages, images, and other files from the server to your computer so you can browse the site offline exactly as it was online.

## Key Features

- **Offline browsing** — Download a full website for local, offline access.
- **Recursive downloading** — Follows links and rebuilds the site's directory structure locally.
- **Resume support** — Can resume an interrupted download and update an existing mirror.
- **Filter rules** — Include or exclude files by type, size, domain, or path pattern.
- **Multi-platform** — Available on Windows, Linux, macOS, and other Unix-like systems.
- **Open source** — Released under the GNU General Public License (GPL).

## How It Works

1. HTTrack connects to the specified URL.
2. It parses each HTML page for links and references to other resources.
3. All linked pages, images, CSS, JavaScript, and other assets are downloaded.
4. Internal links in downloaded HTML files are rewritten to point to the local copies.
5. The result is a fully navigable, self-contained copy of the website on your disk.

## Common Use Cases

- Archiving websites for offline reference or preservation.
- Creating local mirrors of documentation sites.
- Analyzing the structure and content of a website.
- Backing up a personal or organizational website.

## Basic Usage

```bash
# Install on Debian/Ubuntu
sudo apt-get install httrack

# Mirror a website
httrack "https://example.com" -O "/path/to/output"

# Mirror with a depth limit (e.g., 3 levels deep)
httrack "https://example.com" -O "/path/to/output" -r3

# Mirror only pages within the same domain
httrack "https://example.com" -O "/path/to/output" -%e0
```

## Official Resources

- Website: [https://www.httrack.com](https://www.httrack.com)
- Source code: [https://github.com/xroche/httrack](https://github.com/xroche/httrack)
