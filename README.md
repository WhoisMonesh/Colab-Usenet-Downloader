# Usenet Downloader

Download files from Usenet (.nzb files) to Google Drive.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/WhoisMonesh/Colab-Usenet-Downloader/blob/main/Colab-Usenet-Downloader.ipynb)

---

## Quick Start

1. **Open in Colab** (click badge above)
2. **Mount Drive** when prompted
3. **Set server credentials** in section 3 (SERVER_HOST, USERNAME, PASSWORD)
4. **Run the download cell** — you will be prompted to upload an `.nzb` file
5. Files appear in your Google Drive under `UsenetDownloader/`

---

## Features

| Feature | Description |
|---|---|
| **.nzb Upload** | Upload any `.nzb` file directly (no XML pasting) |
| **yEnc Decoding** | Automatically decodes yEnc-encoded binary articles |
| **SSL Connection** | Connects via NNTP_SSL on port 563 |
| **Per-file Progress** | Shows file index (3/15), name, and decoded file size |
| **Sync-safe** | Downloads locally first, then moves to Drive |
| **Keep-Alive** | JavaScript prevents Colab timeout during large downloads |
| **Auto-Zip** | Multiple files are zipped with progress + download link |

---

## Where to Put Your .nzb and Credentials

### Server Config (section 3)

```python
SERVER_HOST = 'news.yourprovider.com'  # your Usenet provider
SERVER_PORT = 563                       # 563 = SSL, 119 = plain
USERNAME = 'your_username'
PASSWORD = 'your_password'
```

### Upload .nzb (section 4)

When you run section 4, a file upload dialog appears. Select your `.nzb` file and the tool parses it automatically.

---

## All Configuration Options

| Variable | Default | Description |
|---|---|---|
| `SAVE_PATH` | `/content/downloads/UsenetDownloader/` | Local temp directory |
| `DRIVE_PATH` | `/content/drive/My Drive/UsenetDownloader/` | Final Drive destination |
| `SERVER_HOST` | `''` | Usenet server address |
| `SERVER_PORT` | `563` | Server port (563 = SSL, 119 = plain) |
| `USERNAME` | `''` | Usenet account username |
| `PASSWORD` | `''` | Usenet account password |
| `KEEP_ALIVE` | `True` | Prevent Colab timeout |

---

## Technical Details

- Uses Python's built-in `nntplib` for NNTP/SSL connections
- Parses NZB XML (namespace `http://www.newzbin.com/DTD/2003/nzb`)
- Custom yEnc decoder — handles `=ybegin`/`=yend` markers and `=` escape sequences
- Downloads to `/content/downloads/` first, then `shutil.move` to Drive (avoids FUSE sync conflicts)
- Per-file progress via `IPython.display` HTML with `display_id`
- JavaScript keep-alive prevents Colab session timeout
- Automatic ZIP when multiple files are downloaded

---

## Fair Use & Legal Notice

This tool downloads files from Usenet for **personal, non-commercial use only**.

**You agree to:**
- Only download content you have the legal right to access
- Comply with your Usenet provider's terms of service and acceptable use policy
- Respect copyright laws and applicable regulations
- Use downloaded content for personal offline access only

**You may NOT use this tool to:**
- Download copyrighted material without authorization
- Violate your Usenet provider's terms of service
- Distribute, re-upload, or monetize downloaded content
- Bypass any access controls or restrictions

**Disclaimer:** The authors are not responsible for how you use this software. You assume all legal responsibility for the content you download. This tool is provided for educational purposes only.

---

## License

MIT
