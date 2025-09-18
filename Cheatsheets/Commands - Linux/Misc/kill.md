`kill` command is use to kill TCP connections on Linux machines.

```bash
# Use ss to list sockets (-l listening, -p show processes)
# Filter connections with destination port 60388, source IP 192.168.151.105
# Extract process IDs (pid=...) using grep with Perl regex
# Sort and deduplicate PIDs
# Kill each matching process
ss -lp '( dport = :60388 )' src 192.168.151.105 | grep -Po "(?<=pid=).*(?=,)" | sort | uniq | xargs kill

# Same as above, but for destination port 1000 and source IP 10.10.14.39
ss -lp '( dport = :1000 )' src 10.10.14.39 | grep -Po "(?<=pid=).*(?=,)" | sort | uniq | xargs kill

# Forcefully kill a process by its PID (-9 sends SIGKILL, cannot be trapped/ignored)
kill -9 <process ID>

```