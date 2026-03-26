ufw
===

Ubuntu firewall management tool

## Synopsis

```shell
sudo ufw [options] [rule/command]
```

## Purpose

- Manage Ubuntu system firewall rules and simplify `iptables` operations.
- Enable or disable the firewall and view the current firewall status.
- Quickly configure access for allowing/denying ports, services, or specific IPs.

## Parameters

### Common Operation Commands

- `enable`: Enable the firewall and set it to start at boot.
- `disable`: Disable the firewall.
- `reload`: Reload firewall rules (without interrupting existing connections).
- `reset`: Reset all rules to the initial state.
- `allow <rule>`: Allow a specified rule (e.g., port, service).
- `deny <rule>`: Deny a specified rule.
- `status`: Show the firewall status and list of rules.

### Rule Formats

- `<port>`: Port number (e.g., `22`, `80/tcp`).
- `<protocol>`: Protocol type (`tcp` or `udp`).
- `comment <text>`: Add a comment to a rule (must be used with `allow`/`deny`).

### Options

- `--dry-run`: Show rule changes only, without actually applying them.

------

## Return Value

- Returns `0` on successful execution.
- Returns a non-zero value for errors or invalid parameters.

------

## Examples

### Basic Operations

```
# Enable firewall
sudo ufw enable

# Disable firewall
sudo ufw disable

# View firewall status
sudo ufw status
```

### Rule Configuration

```
# Allow default SSH port (22/tcp)
sudo ufw allow ssh

# Allow port 8080 for TCP and add a comment
sudo ufw allow 8080/tcp comment "Web Server"

# Deny access from 192.168.1.5
sudo ufw deny from 192.168.1.5

# Deny port 53 for UDP
sudo ufw deny 53/udp
```

### Advanced Operations

```
# Show numbered rule list (useful for deletion)
sudo ufw status numbered

# Delete the 3rd rule
sudo ufw delete 3

# Reset all rules
sudo ufw reset
```

------

## Notes

1. **Privilege Requirement**: Commands must be executed using `sudo`.
2. **Default Policy**: When first enabled, it defaults to blocking all incoming traffic and allowing all outgoing traffic.
3. **Rule Priority**:
   Rules are matched in order; denying before allowing may cause conflicts.
4. **Logging**:
   Enable logging with `sudo ufw logging on`; logs are located at `/var/log/ufw.log`.
5. **Service Name Support**:
   Supports service names defined in `/etc/services` (e.g., `http`, `ssh`).
