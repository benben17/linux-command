createrepo
===

Create a YUM repository

## Synopsis

```shell
createrepo [options] <directory>
```

## Description

`createrepo` is a program that creates RPM metadata from a set of RPMs, forming a RPM metadata repository (YUM repository).

## Options

```shell
-u --baseurl <url>
# Specify the base URL for the repository.

-o --outputdir <url>
# Specify the directory where the metadata should be generated.

-x --excludes <packages>
# Specify packages to exclude when generating metadata.

-i --pkglist <filename>
# Specify a file containing a list of packages to include in the metadata. Each package name should be on its own line. Wildcards and regular expressions are not supported.

-n --includepkg
# Specify packages to include via command line (URL or local path).

-q --quiet
# Quiet mode; suppress output.

-g --groupfile <groupfile>
# Specify a group file (e.g., comps.xml) for the repository. 
# Note: The group file should be in the same directory as the RPM packages.
# Example: createrepo -g comps.xml /path/to/rpms

-v --verbose
# Output detailed information.

-c --cachedir <path>
# Specify a directory for caching package checksums.
# This significantly improves performance when running createrepo repeatedly on the same repository with few changes.

--basedir
# The base directory path for directories in repodata. Defaults to the current working directory.

--update
# If metadata already exists and only some packages have changed, this option updates the existing metadata instead of re-analyzing everything. It is much faster.

--skip-stat
# Skip stat() calls when using --update. Assumes that if the filename hasn't changed, the file itself hasn't changed.

--update-md-path
# Use existing repodata from this path to perform an update.

-C --checkts
# Do not generate metadata if the existing metadata is newer than the RPMs. This reduces processing time for unmodified repositories but is incompatible with the --split option.

--split
# Run in split-media mode. Instead of a single directory, it processes a set of directories corresponding to different volumes in a media set.

-p --pretty
# Output formatted (pretty) XML files.

--version
# Output version information.

-h --help
# Display the help menu.

-d --database
# Generate SQLite databases for the metadata (default).

--no-database
# Do not generate SQLite databases.

-S --skip-symlinks
# Ignore symbolic links to packages.

-s --checksum
# Choose the checksum type (e.g., md5, sha1, sha256). The default is now "sha256" (if hashlib is available).

--profile
# Output time-based profiling information.

--changelog-limit CHANGELOG_LIMIT
# Include only the last N changelog entries from each RPM.

--unique-md-filenames
# Include a checksum in the metadata filenames to help with HTTP caching (default).

--simple-md-filenames
# Do not include checksums in metadata filenames.

--retain-old-md
# Keep the N most recent versions of the metadata (so clients with old repomd.xml files can still access it). Default is 0.

--distro
# Specify distribution tags. Can be specified multiple times.

--content
# Specify keywords/tags regarding the repository's content.

--repo
# Specify keywords/tags regarding the repository itself.

--revision
# An arbitrary string for the repository revision.

--deltas
# Generate delta RPMs and delta metadata.

--oldpackagedirs PATH
# Path to look for older packages for delta generation.

--num-deltas int
# The number of old versions to process for deltas. Default is 1.

--read-pkgs-list READ_PKGS_LIST
# Useful with --update to output paths to packages that were actually read.

--max-delta-rpm-size MAX_DELTA_RPM_SIZE
# Maximum size in bytes for RPMs to be processed for deltas.

--workers WORKERS
# Number of worker threads to spawn for reading RPMs.

--compress-type
# Specify the compression method: compat (default), xz, gz, bz2.
```

## Return Value

Returns 0 on success, and non-zero on failure.

## Examples

```shell
# Generate a repository with a groups file. 
# Note that the groups file should be in the same directory as the RPMs.
createrepo -g comps.xml /path/to/rpms
```
观察
