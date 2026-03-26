docker
===

Containerization technology that packages an application and its dependencies into a portable container.

## Description

Docker containers can be quickly deployed, are portable, scalable, and can run on different platforms. Docker helps developers and operations personnel build, publish, and manage applications more easily.

## Installation

Install Docker on Linux using the following commands.

```bash
# CentOS    Reference: https://blog.csdn.net/zhaoyuanh/article/details/126610347
# If the system has an old version of Docker, remove it first:
sudo yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine

# Set up the repository:
yum install -y yum-utils

# Add the Docker repository:
yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo

# Install Docker Engine (default is latest):
yum install docker-ce docker-ce-cli containerd.io docker-compose-plugin

# Start Docker:
sudo systemctl start docker

```

```bash
# Rapid installation script provided by Docker official: https://github.com/docker/docker-install 
# Not recommended for production environments
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh ./get-docker.sh --dry-run

# Use systemctl to set auto-start at boot
sudo systemctl enable docker.service
sudo systemctl enable containerd.service
```

## Syntax

```shell
docker create [options] IMAGE
```

## Options

```shell
attach	Attach local standard input, output, and error streams to a running container
build	Build an image from a Dockerfile
commit	Create a new image from a container's changes
cp	Copy files/folders between a container and the local filesystem
create	Create a new container
diff	Inspect changes to files or directories on a container's filesystem
events	Get real-time events from the server
exec	Run a command in a running container
export	Export a container's filesystem as a tar archive
history	Show the history of an image
images	List images
import	Import the contents from a tarball to create a filesystem image
info	Display system-wide information
inspect	Return low-level information on Docker objects
kill	Kill one or more running containers
load	Load an image from a tar archive or STDIN
login	Log in to a Docker registry
logout	Log out from a Docker registry
logs	Fetch the logs of a container
pause	Pause all processes within one or more containers
port	List port mappings or a specific mapping for the container
ps	List containers
pull	Pull an image or a repository from a registry
push	Push an image or a repository to a registry
rename	Rename a container
restart	Restart one or more containers
rm	Remove one or more containers
rmi	Remove one or more images
run	Run a command in a new container
save	Save one or more images to a tar archive (streamed to STDOUT by default)
search	Search for images in Docker Hub
start	Start one or more stopped containers
stats	Display a live stream of container(s) resource usage statistics
stop	Stop one or more running containers
tag	Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE
top	Display the running processes of a container
unpause	Unpause all processes within one or more containers
update	Update configuration of one or more containers
version	Show the Docker version information
wait	Block until one or more containers stop, then print their exit codes

<Environment Parameters>
    --add-host list            # Add a custom host-to-IP mapping (host:ip)
-a, --attach list              # Attach to STDIN, STDOUT or STDERR
    --blkio-weight uint16      # Block IO (relative weight), between 10 and 1000, or 0 to disable (default 0)
    --blkio-weight-device list # Block IO weight (relative device weight) (default [])
    --cap-add list             # Add Linux capabilities
    --cap-drop list            # Drop Linux capabilities
    --cgroup-parent string     # Optional parent cgroup for the container
    --cgroupns string   # Cgroup namespace to use (host|private)
                        #  'host':    Run the container in the Docker host's cgroup namespace
                        #  'private': Run the container in its own private cgroup namespace
                        #  '':        Use the cgroup namespace configured by the 
                        #        default-cgroupns-mode option on the daemon (default)
    --cidfile string           # Write the container ID to a file
    --cpu-period int           # Limit CPU CFS (Completely Fair Scheduler) period
    --cpu-quota int            # Limit CPU CFS (Completely Fair Scheduler) quota
    --cpu-rt-period int        # Limit CPU real-time period in microseconds
    --cpu-rt-runtime int       # Limit CPU real-time runtime in microseconds
-c, --cpu-shares int           # CPU shares (relative weight)
    --cpus decimal             # Number of CPUs
    --cpuset-cpus string       # CPUs in which to allow execution (0-3, 0,1)
    --cpuset-mems string       # MEMs in which to allow execution (0-3, 0,1)
    --device list              # Add a host device to the container
    --device-cgroup-rule list  # Add a rule to the cgroup allowed devices list
    --device-read-bps list     # Limit read rate (bytes per second) from a device (default [])
    --device-read-iops list    # Limit read rate (IO per second) from a device (default [])
    --device-write-bps list    # Limit write rate (bytes per second) to a device (default [])
    --device-write-iops list   # Limit write rate (IO per second) to a device (default [])
    --disable-content-trust    # Skip image verification (default true)
    --dns list                 # Set custom DNS servers
    --dns-option list          # Set DNS options
    --dns-search list          # Set custom DNS search domains
    --domainname string        # Container NIS domain name
    --entrypoint string        # Override the default ENTRYPOINT of the image
-e, --env list                 # Set environment variables
    --env-file list            # Read in a file of environment variables
    --expose list              # Expose a port or a range of ports
    --gpus gpu-request         # GPU devices to add to the container ('all' to pass all GPUs)
    --group-add list           # Add additional groups to join
    --health-cmd string        # Command to run to check health
    --health-interval duration # Time between running the check (ms|s|m|h) (default 0s)
    --health-retries int           # Consecutive failures needed to report unhealthy
    --health-start-period duration # Start period for the container to initialize before starting health-retries countdown (ms|s|m|h) (default 0s)
    --health-timeout duration      # Maximum time to allow one check to run (ms|s|m|h) (default 0s)
    --help                     # Print usage
-h, --hostname string          # Container hostname
    --init                     # Run an init inside the container that forwards signals and reaps processes
-i, --interactive              # Keep STDIN open even if not attached
    --ip string                # IPv4 address (e.g., 172.30.100.104)
    --ip6 string               # IPv6 address (e.g., 2001:db8::33)
    --ipc string               # IPC mode to use
    --isolation string         # Container isolation technology
    --kernel-memory bytes      # Kernel memory limit
-l, --label list               # Set meta data on a container
    --label-file list          # Read in a line-delimited file of labels
    --link list                # Add link to another container
    --link-local-ip list       # Container IPv4/IPv6 link-local addresses
    --log-driver string        # Logging driver for the container
    --log-opt list             # Log driver options
    --mac-address string       # Container MAC address (e.g., 92:d0:c6:0a:29:33)
-m, --memory bytes             # Memory limit
    --memory-reservation bytes # Memory soft limit
    --memory-swap bytes        # Swap limit equal to memory plus swap: '-1' to enable unlimited swap
    --memory-swappiness int    # Tune container memory swappiness (0 to 100) (default -1)
    --mount mount              # Attach a filesystem mount to the container
    --name string              # Assign a name to the container
    --network network          # Connect a container to a network
    --network-alias list       # Add network-scoped alias for the container
    --no-healthcheck           # Disable any container-specified HEALTHCHECK
    --oom-kill-disable         # Disable OOM Killer
    --oom-score-adj int        # Tune host's OOM preferences (-1000 to 1000)
    --pid string               # PID namespace to use
    --pids-limit int           # Tune container pids limit (set -1 for unlimited)
    --platform string          # Set platform if server is multi-platform capable
    --privileged               # Give extended privileges to this container
-p, --publish list             # Publish a container's port(s) to the host
-P, --publish-all              # Publish all exposed ports to random ports
    --pull string              # Pull image before creating ("always"|"missing"|"never") (default "missing")
    --read-only                # Mount the container's root filesystem as read-only
    --restart string           # Restart policy to apply when a container exits (default "no")
    --rm                       # Automatically remove the container when it exits
    --runtime string           # Runtime to use for this container
    --security-opt list        # Security Options
    --shm-size bytes           # Size of /dev/shm
    --stop-signal string       # Signal to stop a container (default "SIGTERM")
    --stop-timeout int         # Timeout (in seconds) to stop a container
    --storage-opt list         # Storage driver options for the container
    --sysctl map               # Sysctl options (default map[])
    --tmpfs list               # Mount a tmpfs directory
-t, --tty                      # Allocate a pseudo-TTY
    --ulimit ulimit            # ulimit options (default [])
-u, --user string              # Username or UID (format: <name|uid>[:<group|gid>])
    --userns string            # User namespace to use
    --uts string               # UTS namespace to use
-v, --volume list              # Bind mount a volume
    --volume-driver string     # Optional volume driver for the container
    --volumes-from list        # Mount volumes from the specified container(s)
-w, --workdir string           # Working directory inside the container
```

## Examples

Common scenarios: Docker Hub search and repository commands.

1. Download an image from Docker Hub.

```bash
docker pull user/image
```

2. Search for images in Docker Hub.

```bash
docker search search_word
```

3. Authenticate with Docker Hub.

```bash
docker login
```

4. Upload an image to Docker Hub.

```bash
docker push user/image
```


## docker network
## Syntax

```
docker network [COMMAND]
```

## COMMAND

### docker network connect
Connect a container to a network. You can connect by name or ID. Once connected, the container can communicate with other containers in the same network.

```shell
docker network connect [OPTIONS] NETWORK CONTAINER
```

#### Options

```shell
--alias	Add network-scoped alias for the container
--driver-opt	Driver options for the network
--ip	IPv4 address (e.g., 172.30.100.104)
--ip6	IPv6 address (e.g., 2001:db8::33)
--link	Add link to another container (Not recommended, may be removed in the future)
--link-local-ip	Add a link-local address for the container
```

### docker network disconnect
Disconnect a container from a network.

```shell
docker network disconnect [OPTIONS] NETWORK CONTAINER
```

#### Options

```shell
-f, --force	Force the container to disconnect from a network
```

### docker network create
Create a new network.

```shell
docker network create [OPTIONS] NETWORK
```

#### Options

```shell
--attachable		API 1.25+ Enable manual container attachment
--aux-address		Auxiliary IPv4 or IPv6 addresses used by Network driver
--config-from		API 1.30+ The network from which to copy the configuration
--config-only		API 1.30+ Create a configuration-only network
-d, --driver bridge	Driver to manage the Network
--gateway		IPv4 or IPv6 gateway for the master subnet
--ingress		API 1.29+ Create swarm routing-mesh network
--internal		Restrict external access to the network
--ip-range		Allocate container ip from a sub-range
--ipam-driver		IP Address Management Driver
--ipam-opt		Set IPAM driver specific options
--ipv6		Enable IPv6 networking
--label		Set metadata on a network
-o, --opt		Set driver specific options
--scope		API 1.30+ Control the network's scope
--subnet		Subnet in CIDR format that represents a network segment
```

### docker network inspect
Return information about one or more networks. By default, this command renders all results in a JSON object.

```shell
docker network inspect [OPTIONS] NETWORK [NETWORK...]
```

#### Options

```shell
-f, --format	Format the output using the given Go template
-v, --verbose	Verbose output for diagnostics
```

### docker network ls
List all networks the Engine daemon knows about. This includes networks across multiple hosts in a cluster.

```shell
docker network ls [OPTIONS]
```

#### Options

```shell
-f, --filter	Provide filter values (e.g., "driver=bridge")
--format	Pretty-print networks using a Go template
--no-trunc	Do not truncate the output
-q, --quiet	Only display network IDs
```

### docker network prune
Remove all unused networks. An unused network is one that is not referenced by any containers currently in use.

```shell
docker network prune [OPTIONS]
```

#### Options

```shell
--filter	Provide filter values (e.g., 'until=')
-f, --force	Do not prompt for confirmation
```
### docker network rm
Remove one or more networks by name or identifier. To remove a network, you must first disconnect all containers connected to it.

```shell
docker network rm NETWORKID [NETWORKID...]
```

## Official Website

For more installation and usage methods, visit: https://wangchujiang.com/reference/docs/docker.html
Written by Tu Tianyu, Shanghai.
