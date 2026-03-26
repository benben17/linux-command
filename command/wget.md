wget
===

The non-interactive network downloader

## Description

The **wget command** is used to download files from URLs using the HTTP, HTTPS, and FTP protocols. It is designed for robustness over slow or unstable network connections; if a download fails due to a network problem, `wget` will keep retrying until the whole file has been retrieved. If the server supports regetting, it will instruct the server to continue the download from where it left off.

`wget` is non-interactive, meaning it can work in the background, after a user has logged off. This allows you to start a retrieval and disconnect from the system, letting `wget` finish the work.

Key features:
1.  **Resuming interrupted downloads**: Supports `REST` in FTP and `Range` in HTTP.
2.  **Support for HTTP/HTTPS and FTP**: Handles both protocols for broad compatibility.
3.  **Proxy support**: Can operate through HTTP proxies.
4.  **Simplicity**: Easy to use from the command line.
5.  **Free and Lightweight**: Open-source and has a small footprint.

### Syntax

```shell
wget [options] [URL]
```

### Options

**Startup options:**
- `-V, --version`: Display the version of Wget and exit.
- `-h, --help`: Print a help message.
- `-b, --background`: Go to the background immediately after startup.
- `-e, --execute=COMMAND`: Execute a `.wgetrc`-style command.

**Logging and input file options:**
- `-o, --output-file=FILE`: Log all messages to FILE.
- `-a, --append-output=FILE`: Append messages to FILE.
- `-d, --debug`: Print lots of debug information.
- `-q, --quiet`: Quiet mode (no output).
- `-v, --verbose`: Verbose mode (default).
- `-nv, --no-verbose`: Turn off verbosity without being completely quiet.
- `-i, --input-file=FILE`: Read URLs from FILE.
- `-F, --force-html`: Treat input file as HTML.
- `-B, --base=URL`: Prepend URL to relative links in -F -i file.

**Download options:**
- `--bind-address=ADDRESS`: Bind to ADDRESS (hostname or IP) on local machine.
- `-t, --tries=NUMBER`: Set number of retries to NUMBER (0 for unlimited).
- `-O, --output-document=FILE`: Write documents to FILE.
- `-nc, --no-clobber`: Skip downloads that would download to existing files.
- `-c, --continue`: Resume getting a partially-downloaded file.
- `--progress=TYPE`: Select progress gauge type.
- `-N, --timestamping`: Don't re-retrieve files unless newer than local.
- `-S, --server-response`: Print server response.
- `--spider`: Don't download anything; just check for file existence.
- `-T, --timeout=SECONDS`: Set all timeout values to SECONDS.
- `-w, --wait=SECONDS`: Wait SECONDS between retrievals.
- `--limit-rate=RATE`: Limit download rate to RATE.

**Directory options:**
- `-nd, --no-directories`: Don't create directories.
- `-x, --force-directories`: Force creation of directories.
- `-nH, --no-host-directories`: Don't create host directories.
- `-P, --directory-prefix=PREFIX`: Save files to PREFIX/...

**HTTP options:**
- `--http-user=USER`: Set http user to USER.
- `--http-password=PASS`: Set http password to PASS.
- `-C, --cache=on/off`: Allow/disallow server-side caching (default is on).
- `-E, --html-extension`: Save HTML documents with `.html` extension.
- `--header=STRING`: Insert STRING among the headers.
- `--user-agent=AGENT`: Identify as AGENT instead of Wget/VERSION.
- `--referer=URL`: Include `Referer: URL` header in HTTP request.
- `--load-cookies=FILE`: Load cookies from FILE before session.
- `--save-cookies=FILE`: Save cookies to FILE after session.

**FTP options:**
- `--passive-ftp`: Use the passive transfer mode (default).
- `--active-ftp`: Use the active transfer mode.

**Recursive download options:**
- `-r, --recursive`: Specify recursive download.
- `-l, --level=NUMBER`: Maximum recursion depth (inf or 0 for infinite).
- `-k, --convert-links`: Make links in downloaded HTML point to local files.
- `-m, --mirror`: Shortcut for -r -N -l inf --no-remove-listing.
- `-p, --page-requisites`: Get all images, etc. needed to display HTML page.

### Parameters

URL: The address of the file or directory to download.

### Examples

**Download a single file:**

```shell
wget http://www.example.com/testfile.zip
```

**Download and save with a different name:**

```shell
wget -O wordpress.zip http://www.example.com/download.aspx?id=1080
```

**Limit download speed:**

```shell
wget --limit-rate=300k http://www.example.com/testfile.zip
```

**Resume an interrupted download:**

```shell
wget -c http://www.example.com/testfile.zip
```

**Download in the background:**

```shell
wget -b http://www.example.com/testfile.zip
# Check progress with:
tail -f wget-log
```

**Masquerade User-Agent:**

```shell
wget --user-agent="Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/58.0.3029.110 Safari/537.3" http://www.example.com/testfile.zip
```

**Test if a link is valid (Spider mode):**

```shell
wget --spider URL
```

**Download multiple files from a list:**

```shell
wget -i filelist.txt
```

**Mirror a whole website:**

```shell
wget --mirror -p --convert-links -P ./LOCAL_DIR URL
```

**Download specific file types (e.g., PDFs):**

```shell
wget -r -A.pdf URL
```

**FTP download with authentication:**

```shell
wget --ftp-user=USERNAME --ftp-password=PASSWORD ftp://example.com/file.zip
```
