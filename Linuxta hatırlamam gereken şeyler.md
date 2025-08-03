2>/dev/null -> error mesajlarını göstermiyor.


uniq -> filtreleyip lineları gösteriyor. -u ile kullanılınca unique olan lineları gösteriyor


sort -> kriterlere göre sortluyor

The `strings` command finds human-readable strings in files. Specifically, it prints sequences of printable characters. Its main use is for non-printable files like hex dumps or executables.

Linux has a command called `base64` that allows for encoding and decoding in Base64. For decoding, we need to use the flag `-d`.

The Linux `tr` command, which stands for ’translate’, allows replacing characters with others. The base command syntax looks like the following `tr <old_chars> <new_chars>`.

tr 'A-Za-z' 'N-ZA-Mn-za-m'


