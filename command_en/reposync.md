reposync
===

Synchronizes yum repositories to a local directory.

## Synopsis

```shell
reposync [options]
```

## Description

`reposync` is used to synchronize remote yum repositories to a local directory, using yum to retrieve packages.

## Options

```shell
-h, --help
# Display help information.

-c CONFIG, --config=CONFIG
# Specify configuration file (default is /etc/yum.conf).

-a ARCH, --arch=ARCH
# Specify architecture.

--source
# Download both src and rpm files.

-r REPOID, --repoid=REPOID
# Specify repo id to query; can be specified multiple times (default is all enabled).

-e CACHEDIR, --cachedir CACHEDIR
# Directory to store metadata.

-t, --tempcache
# Use temporary directory to store/access yum-cache.

-d, --delete
# Delete local packages no longer present in the repository.

-p DESTDIR, --download_path=DESTDIR
# Specify download path; default is current directory.

--norepopath
# Do not add repo names to the download path. Only usable when synchronizing a single repository (default is to add repo names).

-g, --gpgcheck
# Delete packages that fail GPG signature check after download. Exit status is "1" if at least one package is deleted.

-u, --urls
# Only list URLs of contents to be downloaded, do not download.

-l, --plugins
# Enable yum plugin support.

-m, --downloadcomps
# Also download comps.xml.

--download-metadata
# Download all non-default metadata.

-n, --newest-only
# Download only the newest packages for each repo.

-q, --quiet
# Output as little information as possible.

--allow-path-traversal
# Allow synchronization of packages stored outside the repo directory. These packages are referenced in the metadata using absolute paths or parent directory ".." and are normally skipped in reposync for security reasons.
# Note: Using this option has potential security implications, as an attacker could provide malicious repodata to cause reposync to write files to arbitrary locations accessible by the user running the command.
```

## Examples

```shell
# Synchronize all packages in the 'updates' repository to the current directory:
reposync --repoid=updates

# Synchronize only the newest packages from the 'updates' repository to the current directory:
reposync -n --repoid=updates

# Synchronize packages from the 'updates' and 'extras' repositories to the current directory:
reposync --repoid=updates --repoid=extras

# Synchronize all packages in the 'updates' repository to the 'repos' directory:
reposync -p repos --repoid=updates

# Synchronize all packages in the 'updates' repository to the 'repos' directory, excluding x86_64 architecture files. Edit /etc/yum.conf, add the option `exclude=*.x86_64`, then execute:
reposync -p repos --repoid=updates
```

## Files

`reposync` uses the yum library to retrieve information and packages. If no configuration file is specified, the default yum configuration will be used.

*   /etc/yum.conf
*   /etc/yum/repos.d/
