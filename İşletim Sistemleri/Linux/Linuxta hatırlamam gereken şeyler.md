2>/dev/null -> error mesajlarını göstermiyor.


uniq -> filtreleyip lineları gösteriyor. -u ile kullanılınca unique olan lineları gösteriyor


sort -> kriterlere göre sortluyor

The `strings` command finds human-readable strings in files. Specifically, it prints sequences of printable characters. Its main use is for non-printable files like hex dumps or executables.

Linux has a command called `base64` that allows for encoding and decoding in Base64. For decoding, we need to use the flag `-d`.

The Linux `tr` command, which stands for ’translate’, allows replacing characters with others. The base command syntax looks like the following `tr <old_chars> <new_chars>`.

tr 'A-Za-z' 'N-ZA-Mn-za-m'


The final networking command we will cover in this room is `netstat`. This command displays current network connections and listening ports. A basic `netstat` command with no arguments will show you established connections, as shown below. In this case, we only have one SSH connection; we figured out it is SSH because it is bound to port 22.
If you are curious about the other options, you can run `netstat -h`, where `-h` displays the help page. We opted for the following options:

- `-a` displays all established connections and listening ports
- `-b` shows the program associated with each listening port and established connection
- `-o` reveals the process ID (PID) associated with the connection
- `-n` uses a numerical form for addresses and port numbers