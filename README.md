# Deadstart

A dead simple & minimalistic start page for your browser, inspired by a terminal experience.

![Image](https://github.com/user-attachments/assets/a07e5a0c-3fa5-4236-8c91-fc6ebbbb6fad)

## Features

- **Custom bangs** - prefix searches with `:`, `/`, or `>` followed by a bang and a search term
- **Bang suggestions** - ghost text shows completions as you type
- **Bang autocomplete** - press `Tab` or `Ctrl+F` to complete a bang
- **Bang validation** - bangs are colored green if valid, red if not

## Usage

Use like a regular search box by typing to serach with DuckDuckGo, or use a bang by starting with a command key (`:` `/` `>`), followed by a bang, a space, then your search term:

```
weather
/wiki linux
:yt one piece op1
>gmaps kyrgyzstan
```

If you forgot the command key, you can also put it after a valid bang and it will convert it to the correct format:

```
duck: -> :duck
yt: one piece --> :yt one piece
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

## Customisation

To add your own bangs, edit the `commands` object in `index.html` and add a new entry with the desired bang and URL template. For example:

```javascript
const commands = {
  // existing commands...
  gh: "https://github.com/search?q=",
};
```

Colors can be customised by editing the CSS variables in the `<style>` tag. For example:

```css
:root {
  --color-base: #1e1e2e;
  --color-text: #cdd6f4;
  --color-accent: #cba6f7;
  --color-subtext: #585b70;
  --color-success: #a6e3a1;
  --color-fail: #eba0ac;
}
```

## Todo

- [ ] Add option to open search results in a new tab
- [ ] Different URL if no search term is provided (e.g. `:g` goes to google.com instead of searching for an empty string)
- [ ] Fix overlay text not scrolling correctly on overflow
- [x] Fix URLs searching instead of going to the URL if the search term looks like a URL (e.g. `example.com` goes to `https://www.duckduckgo.com/search?q=example.com` instead of `https://example.com`)
- [x] Add support for forgetful bangs, where the command key is after the bang (e.g. `g:search term` or `search term:g` instead of `:g search term`)
