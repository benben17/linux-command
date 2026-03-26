pip
===

The package manager for the Python programming language, used to install and manage third-party modules.

## Syntax

```bash
pip <command> [options]
```

## Commands

```text
install                     Install packages.
download                    Download packages.
uninstall                   Uninstall packages.
freeze                      Output installed packages in requirements format.
inspect                     Inspect the Python environment.
list                        List installed packages.
show                        Show information about installed packages.
check                       Verify installed packages have compatible dependencies.
config                      Manage local and global configuration.
search                      Search PyPI for packages.
cache                       Inspect and manage pip's wheel cache.
index                       Inspect information available from package indexes.
wheel                       Build wheels from your requirements.
hash                        Compute hashes of package archives.
completion                  A helper command for command completion.
debug                       Show information useful for debugging.
help                        Show help for commands.
```

## General Options

```text
-h, --help                  Show help.
--debug                     Let unhandled exceptions propagate rather than logging them.
--isolated                  Run pip in isolated mode, ignoring environment variables and user configuration.
--require-virtualenv        Allow pip to only run in a virtual environment.
--python <python>           Run pip using the specified Python interpreter.
-v, --verbose               Give more output. Can be used up to 3 times.
-V, --version               Show version and exit.
-q, --quiet                 Give less output. Can be used up to 3 times.
--log <path>                Path to a verbose appending log.
--no-input                  Disable input prompts.
--proxy <proxy>             Specify a proxy in the form scheme://[user:passwd@]proxy.server:port.
--retries <retries>         Maximum number of retries each connection should attempt (default 5 times).
--timeout <sec>             Set the socket timeout (default 15 seconds).
--exists-action <action>    Default action when a path already exists: (s)witch, (i)gnore, (w)ipe, (b)ackup, (a)bort.
--trusted-host <hostname>   Mark this host or host:port pair as trusted, even if it does not have valid HTTPS.
--cert <path>               Path to alternate CA bundle.
--client-cert <path>        Path to SSL client certificate, a single file containing the private key and the certificate in PEM format.
--cache-dir <dir>           Store the cache data in <dir>.
--no-cache-dir              Disable the cache.
--disable-pip-version-check
                            Don't periodically check PyPI for a new version of pip.
--no-color                  Suppress colored output.
```

### Installation

Pip is usually installed along with Python. Ensure you are using Python 3.4 or higher.

**Ubuntu:**
```bash
sudo apt install python3-pip
```

**CentOS:**
```bash
sudo yum install python3-pip
```

**Upgrade Pip:**
```bash
python -m pip install --upgrade pip
```

## Package Operations

### Install a package
```bash
pip install <package_name>
```

### Uninstall a package
```bash
pip uninstall <package_name>
```

### List installed packages
```bash
pip list
```

### Export and Import Dependencies
Save current environment to a file:
```bash
pip freeze > requirements.txt
```

Install from a requirements file:
```bash
pip install -r requirements.txt
```

### Install a specific version
```bash
pip install package_name==1.2.3
```

### Install from a Git repository
```bash
pip install git+https://github.com/user/repo.git
```

## Official Website
For more information, visit: [https://pypi.org/project/pip/](https://pypi.org/project/pip/)
