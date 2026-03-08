# Deadstart

A dead simple & minimalistic start page for your browser, inspired by a terminal experience.

![Image](https://github.com/user-attachments/assets/a07e5a0c-3fa5-4236-8c91-fc6ebbbb6fad)

## Features

- **Custom bangs** - prefix searches with `:`, `/`, or `>` followed by a bang and a search term
- **Bang suggestions** - ghost text shows completions as you type
- **Bang autocomplete** - press `Tab` or `Ctrl+F` to complete a bang
- **Bang validation** - bangs are colored green if valid, red if not

## Usage

Start typing with a command key (`:` `/` `>`), followed by a bang, a space, then your search term:

```
/wiki linux
:yt one piece op1
>gmaps kyrgyzstan
```

## Built in Bangs

| Bang                           | Destination                                  |
| ------------------------------ | -------------------------------------------- |
| `g`, `google`                  | [Google](https://www.google.com)             |
| `d`, `duck`                    | [DuckDuckGo](https://duckduckgo.com/)        |
| `y`, `yt`, `youtube`           | [YouTube](https://www.youtube.com/)          |
| `r`, `reddit`                  | [Reddit](https://www.reddit.com/)            |
| `gh`, `github`                 | [GitHub](https://github.com/)                |
| `gu`                           | [GitHub User](https://github.com/)           |
| `w`, `wiki`                    | [Wikipedia](https://www.wikipedia.org/)      |
| `map`, `maps`, `gmaps`, `gmap` | [Google Maps](https://www.google.co.uk/maps) |
| `nix`                          | [MyNixOS](https://mynixos.com/)              |
| `mal`                          | [MyAnimeList](https://myanimelist.net/)      |
| `miruro`                       | [Miruro](https://www.miruro.to/)             |
| `cs`, `codestats`              | [Code::Stats](https://codestats.net/)        |

## Installation

### Start page

Download the `index.html` file and set it as your browser's start page. For example, in Firefox, go to `about:preferences#home` and set "Homepage and new windows" to "Custom URLs..." and enter the file path (e.g. `file:///home/user/path/to/index.html`).

### New tab page

If using as a new tab page, you may need to use an extension to override the default new tab behavior. For example, in Firefox, you can use the "New Tab Override" extension. The extension may not function properly if the file is not served over HTTP, so you may need to run a local web server to serve the file. For example, you can use Python's built-in HTTP server:

```bash
cd /path/to/directory
python3 -m http.server 8000
```

or use busybox's httpd:

```bash
busybox httpd -f -p 8000 -h /path/to/directory
```

Add this to your startup config (e.g. `.bashrc`, `.zshrc`, `autostart` file) to start the server on login:

```bash
# Start local web server for new tab page
cd /path/to/directory && python3 -m http.server 8000 &
```

or start as a systemd service (check for your distro).
