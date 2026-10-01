# NX TV

Live TV on your Nintendo Switch. Browse channels by category, search by name, flip through them with the shoulder buttons, and let the app recover on its own when a stream drops. Add as many TV servers as you like, each one just a file you copy to the SD card.

## Features

- **Channel guide** with logos, grouped into Sports, News, Bangla, Hindi and Entertainment
- **Search** for a channel by name with the on-screen keyboard
- **Quick channel switching** with L and R while watching
- **Automatic recovery**: if a channel freezes or goes offline, the app retries it, then tries a backup server, then skips to the next working channel
- **Your own servers**: add a playlist, an Xtream Codes login or a JSON feed, with a form in the app or by copying a file made by the companion PC tool
- **Server controls**: switch each server on or off and rename it
- **Light on your SD card**: video is buffered in RAM, nothing is recorded or cached to the card while you watch
- **Hardware accelerated** playback powered by mpv
- **Update from inside the app**

## Install

1. Download `NXTV.nro` from the [latest release](https://github.com/zhtipu/nx-tv/releases/latest).
2. Copy it to `/switch/NXTV/` on your SD card.
3. Open the Homebrew Menu or Install "NX TV [01ed051fb86f0000].nsp"
4. launch **NX TV**.

You need a homebrew-enabled Switch and an internet connection. For the best performance, open the Homebrew Menu in full memory mode by holding **R** on a game's icon (title takeover) instead of using the album applet.

## Controls

**Channel list**

| Button | Action |
|---|---|
| D-pad / left stick | Move around |
| A | Open the selected tab or play the selected channel |
| B | Back |
| + | Search channels |
| - | Refresh the channel list |

**While watching**

| Button | Action |
|---|---|
| L / R | Previous / next channel (wraps around) |
| Y | Show or hide the on-screen display |
| X | Player settings |
| A | Pause or resume |
| B | Back to the channel list |

The on-screen display also has a **Channels** button that opens a full list to jump to any channel.

## Adding your own servers

A server is a source of channels. NX TV comes with a few built in, and you can add as many of your own as you want. There are three ways, from easiest to most hands-on.

### 1. Server files from the NX TV Server Tool (easiest)

The [NX TV Server Tool](https://github.com/zhtipu/NXTV-Server-Tool/releases/latest) is a free Windows program that reads a TV server for you and saves it as a single file. See its own guide for the steps. In short:

1. On your PC, open the tool, paste the server's website address and press **Analyze**.
2. Press **Write to SD card** and pick your SD card. The tool saves one file, for example `My_Server.nxtv`, into `/switch/NXTV/servers/`.
3. Put the card back in the Switch and open NX TV. The server appears under **Settings → Your servers**. Press **Reload channels** if its channels are not in the list yet.

What to know:

- **One file per server.** Copy in as many as you have. Nothing is overwritten, and each file is its own server.
- **Plain playlists work too.** Any `.m3u` or `.m3u8` playlist you drop into `/switch/NXTV/servers/` becomes a server named after the file.
- **Removing a server** that came from this folder also deletes its file, so it does not come back.
- **Refreshing a server.** Some servers hand out streams that expire after a few hours. When one stops working, run the tool again and replace the file with the same name.

### 2. Link a file by hand

If a file is somewhere else on the card, open **Settings** and choose **Import a server file**. A small file browser opens. Go into folders with A, go back with the **.. (up)** entry, and pick a `.nxtv`, `.m3u` or `.m3u8` file. The server is added right away. A file linked this way stays where it is.

### 3. Type it in

Under **Your servers**, choose **Add a server** and fill in the form. Three kinds of server are supported:

| Type | What you need |
|---|---|
| **M3U playlist** | The playlist address, an `.m3u` or `.m3u8` link. Optional login, user agent and extra headers. |
| **Xtream Codes** | The server address (for example `http://host:port`), your username and your password. |
| **JSON API** | The API address, the path to the channel list in the response, and the names of the fields that hold each channel's name, stream address, category and logo. |

Use **Test server** to check that it works and see how many channels were found, then **Save**. Typing long addresses with the Switch keyboard is slow, which is why the PC tool above is usually the better choice.

### Managing servers

Open **Settings**. Highlight a server and press **A** to switch it on or off. Press **X** to rename a built-in server, or to edit or delete one of your own. At least one server always stays on. If two servers carry the same channel, the extra copy is used as a backup when the first one fails.

Channels are sorted into the five tabs by keyword (for example anything with "sport" in its category goes to Sports). Categories the app does not recognise go to Entertainment.

## Updates

NX TV checks GitHub for a newer release when it starts. If one is found, choose OK to download it. A progress bar shows the percentage and size, and when it finishes the app restarts on the new version. Cancel stops the download and leaves your current version untouched. You can also check manually from the **About** tab, which tells you if you are already up to date.

## Troubleshooting

**The channel list is empty or a channel will not play.**
Channel availability depends on the servers and on your network. Make sure your Switch is online, then try **Reload channels** in Settings. Some servers may only be reachable from certain networks.

**A server file I copied does not show up.**
Check that it is directly inside `/switch/NXTV/servers/` (not in a subfolder) and ends in `.nxtv`, `.m3u` or `.m3u8`. Restart the app or press **Reload channels**. If it still does not appear, use **Import a server file** in Settings, which tells you why a file cannot be used.

**A channel freezes.**
The app notices after about 15 seconds, reopens the stream, and after three failed tries moves on to the next channel. Picking the channel you are already watching from the list also forces a fresh reopen.

**Streams from one server stopped working after a few hours.**
Some servers use streams that expire. Run the PC tool again and replace that server's file.

**Video is choppy.**
Launch through title takeover (see Install) so the app gets the full amount of memory.

**Send a log with a bug report.**
Launch with the arguments `-d -o nxtv.log` and attach the file.

## Credits

- Based on [Switchfin](https://github.com/dragonflylee/switchfin) by dragonflylee, licensed under Apache-2.0

## Disclaimer

NX TV is a player. It does not host, store or provide any video content. You are responsible for making sure you have the right to watch what you stream. This project is not affiliated with or endorsed by Nintendo or any channel or server operator.
